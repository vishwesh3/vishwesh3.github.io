---
title: "Version Controlling System (VCS)"
layout: post
date: 2017-06-02 22:38
image: /assets/images/VCS.jpeg
headerImage: true
tag:
- git
- vcs
category: blog
star: true
author: vishwesh
description: Introduction to VCS.
---

What is VCS? What is the use of this? Why it is used so widely? How does it works? It’s past? It’s architecture?

Let’s start with a simple question,

## What is Version Controlling?
It is a simple system, which manages different versions and drafts of softwares (but not limited to only softwares). It is the mean of recording changes in files (softwares are nothing but systematic collections of files). Let’s take an example, books have different version (editions) then the collections of all this versions with difference (what changed in which version) can be referred to VCS.

## Why it is so important?
It is used to get previous state. Getting previous version of book in above example. You can easily trace history of files. With this system, you can easily restore to any previous state easily. For example you are working on an product to revamp it’s UI, but designs are not yet decided. So to impress your boss, you tried different UI’s and showed it to your boss. But unfortunately boss rejects all of them and gave you new designs. So in order start work, you have to restore to previous state for which either use continuous `ctrl+z` (which will only be useful for small changes) or use **VCS**. With VCS you can restore within few seconds.

There are mainly 3 models of VCS:-

### Local data model
In this model, all developer must use the same file system (file system varies with OS).

Limitations:- All developers have a bound to use same file system/OS while working on a single project.

e.g.:- Revision Control System (RCS) and Source Code Control System (SCCS). Both of them are open source.

### Client-server model
In this model, developers works on a single repo hosted on server.

Limitations:- developers can’t create there own local repo.

e.g.:- Open source – Concurrent Versions System (CVS), Subversion (SVN) etc

Proprietary – IBM Rational Synergy, Vault etc.

### Distributed model
In this, each developer works directly with his own local repo, changes are shared between repo as a separate step (merge commits).

It is most widely used model.

e.g.:- Open source – Git, ArX, SVK, GNU arch etc

Proprietary – Code Co-op, Plastic SCM etc

**Git** is most common along all of them. It is written in a collection of **Perl**, **C**, and **various shell scripts**.

## Why it is used so widely?
Some advantages of VCS:
- Easily understand who made a change & when it happened and then when it went to production (through releases).
- Feel free to try different approaches as it is very simple to revert back.
- No need of manually combining work of your teammates.

## Basic concepts
### Recording changes
It is the primary work of VCS. It generally records change, date of change, author. You can tell VCS which files/directories to track (some are OS generated and vary from one system to another). In Git,
Put files in `.gitignore` if you don't wish to track them.
Run `git add path/of/file` to make file/dir trackable.
As you make changes, it will track each of them. Run `git status` to get which file have been changed. It will only show those changes which are not committed. Once committed they will not be shown in the output of `git status`.

### Committing
As you make changes VCS will track them automatically. Changes can be of addition and deletion. Addition means adding content to file and same for deletions. Once you are in a state which is consistent you can commit.
**How to commit?**
In Git, run `git commit path/to/file -m ‘Commit message’`.
Tip:- commit message can be divided into two part title and message. Title consists of brief message, (eg:- fix: app crash on clicking more info button) and message which describes changes (eg:- make sure items array is not null. Added try catch)
It looks like
`fix: app crash on clicking more info button
make sure items array is not null.Added try catch.`

**How to get list of commits?**
In Git, run `git log`.

### Updating your codebase.
As your team members commit changes, it is very much important to get them (maintain latest codebase). Working on latest codebase reduces conflicts. Now question arises How to get updates? It is as simple as performing a pull (or fetch and then rebase) or update form another source (copy paste). While pulling (or fetching) only objects which are changed are downloaded.

**Conflicts**                                                                                                         
What are conflicts? How they arises?
While merging two code if system get’s confused which to take, then system takes help from you which code to consider. Let’s take an example:-We have a project in a consistent state, let’s say A. Both the person 1 and 2 have the copy which is at state A. Now person 1 commits a changes in file q at line number 3 and pushed it to the host (so that other one can get changes). On the other hand person 2 is also working on file q and done changes in line number 3. Now when person 2 updates his code (through pull or rebase), system will throw conflicts on line 3 of file q. System is confused which change to consider, changes of person 1 or person 2. So while updating, system will let us to decide what to do, which code should be final (taken).  It will look like this

_in file q_


```
..........
<<<<<<<HEAD
I am person 1, I have done changes in this line (line number 3).
=======
I am person 2, I have done changes in this line (line number 3).
>>>>>>>
..........
```

Now person 2 have to decide:

 1) either take changes of person 1. (for this edit file in below manner and save it.)
  ```
   ..........
   I am person 1, I have done changes in this line (line number 3).
   ..........
   ```
 2) or override it with his changes (for this edit file in below manner and save it.
  ```
   ..........
   I am person 2, I have done changes in this line (line number 3).
   ..........
   ```
 3) or take both changes or do something else. (for this edit file in below manner and save it.)
 ```
  ..........
  I am person 1, I have done changes in this line (line number 3).
  I am person 2, I have done changes in this line (line number 3).
  Combine this changes as you want.
  ..........
  ```

and finally run continue command to tell that you have removed conflicts, now system can proceed to merge. (run `git add path/of/files` and then `git rebase —continue` to continue rebasing in git).

### Branching

It is helpful when you want to do experiments.
 1) Let’s say you are in master branch and in order to impress your boss you want to experiment some new features. So in such cases you can checkout to new branch, experiment it, show it to your boss. If it is approved then merge it to the main master branch else drop it and continue work on master.
 2) Another use of branching, Use master branch for releases, means always this branch will contain code which is stable. So whenever someone wants to use your code, he can refer to to master. And in the mean time to can continue work on another branch (let’s say bug-fix). With the addition of new feature there are possibility of bugs, so add new feature in bug-fix branch and wait until you feels that it is now stable and then merge it to the master.
 3) Another common use is contributing in open source. You can works on different issues and create multiple PR by making branches.

### Revision
When changes are committed, a new commit is recorded in the system. Each commit is given a unique identity which varies on different systems. Git uses hashing, it gives a unique hash code to each commit. Hash code looks like `936d9ba5c3ad345831e5846eee7d92415cfd3f8a`. Each commit consists of
 1) changes make in files
 2) Changes made in which files
 3) changes are done by whom
 4) date of changes
Revision is mostly helpful when we are working in a team, to know changes done by other person. Different systems have different representation of showing diff.
In diff, addition are shown in green colour while deletion are in red.
Use `gitk` command to get history (and full revision)

[Click here](https://github.com/vishwesh3/central-medic-center/commit/bad16e13f2e313541b6b42d5baa9db20ff5b6329) to get an idea of how diff looks like.

## Concluding

I hope you will get an basic idea on What is VCS, how it makes development easy and other concepts of VCS. Find my another blog on [Introduction to GIT](https://vishwesh3.github.io/i-introduction-to-git/). If you find anything difficult, just ping me on catchvishwesh@gmail.com, I would love to help you.

Have a nice day!
