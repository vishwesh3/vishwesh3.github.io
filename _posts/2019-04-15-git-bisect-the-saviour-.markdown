---
title: "git bisect - the saviour"
layout: post
date: 2019-04-15 02:04
image: /assets/images/git-bisect-fig1.png
headerImage: true
tag:
  - git
  - find bug
  - find fix
  - binary search
category: blog
star: true
author: vishwesh
description: Find any culprit commit within no time
---

Hey! today I am going to talk about one of my favorite git command i.e `git bisect`.

_At present, [Git](https://git-scm.com/) is the most widely used distributed version control system. With the help of `git`, one can easily collaborate his work easily with others. Read more about `git` in my [another post](https://jainkuniya.github.io/i-introduction-to-git/)_

So let's start with the problem:

Let's say you are working in a large code base with tons of people working on the same project, lots of commits per day. Imagine you went for a week long vacations. After coming back, you find that the product has some issues which was working totally fine when you left. It's a huge codebase and you aren't aware of which module is responsible for this wrong behavior. What will you do in that case??

- **Option - 1**
Call a meeting of all the contributors and ask who introduced this?
There can be cases where this behavior is caused by two changes of multiple commits from different people (whose individually change was working fine).
Also calling out a meeting is time-consuming and might waste the time of whole team.

- **Option - 2**
You already are managing commit history, then why don't you check each and every commit and find the root cause.
But what if there are hundreds of commits in between, checking each and every commit will be really hard, boring and again time-consuming.

- **Option - 3**
Use the binary search on commits _(Yup! the same searching algorithm which you studied at high school 😅)_
Here `git bisect` comes into the picture. Yes! it can help you to find a specific commit which introduced this behavior by iterating commits in binary search manner. So now you only have to check only `Log(N)` commits instead of `N` commits (as described in option - 2).

So your next question will be how to use it:

- Keep ready the commit `SHA` on which
  -  it was fine, let's call it `good`
  -  it is not behaving correctly, let's call it as `bad`
  (in the worst case they can be `start` and `end` commits of the whole project, respectively)

Just remember 3 things:
- `git bisect start GOOD BAD`, where `GOOD`, `BAD` are the reference to the `good` and `bad` commit respectively (or just `git bisect`)
- Check behavior, if it is `good`
  - Enter `git bisect good`
  - else, Enter `git bisect bad`

  repeat the above command till you find `SHA` of first `bad` commit in the terminal like this
  ```
  < ... sha ... > is the first bad commit
  ```
- Use `git bisect reset` to reset and get back to the original state from where you started via `git bisect start`.

In the meantime, you can also get the logs of the binary search you are performing with the help of:
```
git bisect log
```

And yay! without making many efforts you have found out the commit which caused this behavior. It can also be used to find an issue of the bug or to find the fix of bug.

Read more it at https://git-scm.com/docs/git-bisect

I love fixing the bugs and found `git bisect` really helpful to find the commit which introduced the bug.

Hoping you will also like it 👍

Thanks 

_Keep Building & Debugging_