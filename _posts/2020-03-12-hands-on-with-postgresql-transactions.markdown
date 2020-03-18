---
title: "Hands on with PostgreSQL transactions"
layout: post
date: 2020-03-12 01:07
image: /assets/postgresql/transactions/header.jpg
headerImage: true
tag:
  - postgresql
  - transactions
  - concurrency
category: blog
star: true
author: vishwesh
description: Playing with transactions in Postgresql
---

**Life would have been a lot easier without concurrency or parallelism**.

Everything working sequentially. Cars moving one by one on a single lane road, no overtaking, no accidents. Simple and straightforward.

But its a tradeoff:

- all cars need to run at a constant speed.
- if one fails in between, the road is chocked.
- a limited number of cars passing in/out at any given point of time.

In short, this is not feasible at present. Target is to increase the number of cars passing in/out (high throughput) and decrease travel time (low latency). It can be simply solved with the help of lanes.

Let's say your API takes 1s, then in 24hrs, you can only serve 86,400 (24 * 60 * 60) requests. So definitely sequential is not an option at this point, [with 640,000 daily active internet users](https://ourworldindata.org/internet).

So you need to handle requests concurrently/parallelism. At the server level, this can be easily achieved with the help of threads (or equivalent). But how will you handle it at the DB layer?

This boils down to a simple money transaction problem. Two API calls are initiated at the same time, to transfer 50 bucks from A to B. Both runs in different threads, both read the balance of A as 60 bucks and validates the request and performs it. Thus resulting in undesired output.

One simple way to solve this is to queue requests and execute one at a time. This will drastically impact your throughput. And why you want to block another person from transferring money when A and B are operating, at this same point C can transfer to D without causing any problem.

So you want to execute requests concurrently/parallelism but not for the same person.

Here come the database transactions in the picture.

_Note: The scope of this blog is only limited to PostgreSQL transactions._

### Postgresql transactions

Basically, there can be 4 situations: **dirty read**, **nonrepeatable read**, **phantom read** and **serialization anomaly**.

<img src="../assets/postgresql/transactions/transactions.png" />

And to handle all these 4 scenarios, there are four types of isolation level.

Thanks to PostgreSQL, that it automatically takes care of **Dirty Read**, i.e you won't be able to read any uncommitted change by another concurrent transaction.

Let's go through each transaction type one by one.

**Note: In this whole blog, will be taking examples of table whose schema looks like this:**
<br>
<img style="height:200px; display:block; margin:auto;" src="../assets/postgresql/transactions/sample_example_table_describe.png" />

### Serializable transaction

This is one of the simplest transaction types. Exactly similar to what we have discussed above, cars running in a single lane.

At a time only one transaction is allowed.

<img src="../assets/postgresql/transactions/serializable_postgresql_transaction.png" />

As you can see later (right side) transaction is waiting until the first (left side) transaction is either **committed** or **rollback**.

- If left-hand side transaction is committed, then right-hand one failed with error:

> ERROR: could not serialize access due to concurrent update

<img src="../assets/postgresql/transactions/serializable_postgresql_commit_transaction.png" />

- But if left-hand side transaction is rollbacked, then the right one will get committed.

<img src="../assets/postgresql/transactions/serializable_postgresql_rollback_transaction.png" />

In the above two cases, we were trying to update the same tuple. Now let's try to update different tuples in different **Serializable transactions**.

<img src="../assets/postgresql/transactions/serializable_postgresql_different_tuples_transaction.png" />

Although we were able to update different tuples in two different transactions but were not able to commit both the transactions.

**Conclusion: as the name implies, only one transaction at a time. The parallel transaction will not be able to commit**.

### Read committed transaction

**Read Committed** is the default isolation level in PostgreSQL. This gives assurance that you never be reading any uncommitted change from another transaction.

Let's take an example

<!-- <img src="../assets/postgresql/transactions/read_committed_postgresql_transaction.png" />

In this case, changes done in the first transaction is not visible to other transaction. Thus no chance of **dirty read**. -->

<img src="../assets/postgresql/transactions/read_committed_postgresql_transaction.png" />
<img src="../assets/postgresql/transactions/read_committed_postgresql_transaction.png" />

In both, the above cases, changes made in a transaction are only visible within the transaction until they are committed. Thus no chance of **dirty read**.

Now let's try to update the same tuple in two different transactions.

<img src="../assets/postgresql/transactions/read_committed_postgresql_update_same_tuple_transaction.png" />

See the later updates are waiting for the first one to complete, either **commit** or **rollback**.

- Let's say we committed the first transaction:

<img src="../assets/postgresql/transactions/read_committed_postgresql_update_same_tuple_transaction_committed.png" />

The second transaction failed with an error:

> ERROR: could not serialize access due to concurrent update

but the updated value id **3033** that means query without any transaction got excecuted and had overridden the first transaction update.

In such cases using delta update will help, just tweak your query to:

> update test set count = count + 3033 where id = 4;

So that changes are not overridden.

- Now let's see what happens if we rollback the first transaction:

<img src="../assets/postgresql/transactions/read_committed_postgresql_update_same_tuple_transaction_rollback.png" />

After rolling back the first transaction, the next one i.e second one got executed. Still, the 3rd one is pending. As it is without any transaction, after completion of the second transaction it will anyhow execute.

**Note: Here quires are executed in first-in, first-out (FIFO) fashion**

Not let's try to update different tuples in different transactions.

<img src="../assets/postgresql/transactions/read_committed_postgresql_update_different_tuple_transaction.png" />

Oh, all updates were successful.

**Conclusion:**
- **It takes a lock on a tuple and no other transaction will be able to update it.**
- **Changes done in a transaction are only visible within the transaction until committed.**

### Repeatable read transaction

It is more strict then **Read committed**. In addition to all that **Read committed** offers, **Repeatable read** also offers you guarantee what, whatever you have read once will not change for that transaction.

<img src="../assets/postgresql/transactions/repeatable_read_postgresql_transaction.png" />

As you can see in the above example, the output of `select` quires is constant even after data is changed from outside.

But when you try to update based on outdated data, then it throws an error
> ERROR:  could not serialize access due to concurrent update

<img src="../assets/postgresql/transactions/repeatable_read_update_postgresql_transaction.png" />

**Conclusion:**
- **Whatever is read, will be same within the transaction scope**
- **But update operations will not work if changes are made**

----------------------------------------------------------------------------------------------------------------------
This was all about **handling transactions in postgresql**. Thanks for reading. Hoping to write more blogs on **Hands on**.


_Note: In this blog concurrency and parallelism are used interchangeably, though both are different. The aim is just to differentiate it from sequential._


Thanks to [@ronakjc](https://twitter.com/ronakjc) for pairing me on this!