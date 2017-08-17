---
title: "Introdution to GIT"
layout: post
date: 2017-03-01 20:19
image: /assets/images/Git-Logo.png
headerImage: true
tag:
- git
- vcs
category: blog
star: true
author: vishwesh
description: Some basic commands of git to get statred.
---

Let's start with a simple question.

**What is GIT?**


Git is **version control system**. There are many VCS other than git eg: - CVS, SVN etc. Git
serve as the foundation of many services like Github, Gitlab etc, but it can also be used without any other services.

If you have ever collaborated on any project with others, then you know how it becomes hard to copy paste both the copies(one of your's and other of your partner). You have added a new feature to project and deployed it and distributed source code to your team, one team member enhanced that one, in the meanwhile you fixed some bugs, now it becomes difficult to combine both the works.

Git is an amazing tool to handle such situations;

It can be used via different interfaces:-

- GUI

- CLI (command line interfaces)

- third party software like source tree etc

Here are some commands to get started with git. (I am using Github as a GIT service)

**How to fork a repo?**

A fork is a copy of a repository. Forking a repository allows you to freely experiment with changes without affecting the original project.

Just click on **Fork** button on the repo and a copy will be created to your account.

**How to clone repo?**


You can clone a repo in order to make it available offline on your local machine.

Get the `URL` of the repo from repo page by clicking on **Clone and download**.

and then in your terminal run command

`git clone URL`

`URL` consists of username of the account which have hosted repo and repo name

eg:- `git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY`

**How to make your first commit?**

`commit` is done so that your changes are recorded in the repo. It stores the current content with a log message.

You can add content (or new file) in the commit by

`git add path/to/file`

`git add -A` can be used to add all.

then commit by

`git commit -a -m "message."`

`-a` stands for automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

If you don't want to commit all content

`git commit path/of/files -m "message"` can be used.  

`-m` stands for message. If multiple `-m` options are given, their values are concatenated as separate paragraphs.

**How to get logs?**

Shows the commit logs.

command:- `git log`

it will show the list of last commits with their author details, date, message etc.

**How to create new branch?**


Branching is generally done when we want to try different approach.

command:- `git checkout -b branch-name`

Above command will create(from your current point) and checkout to the new branch.


**How to checkout to a branch?**


command:- `git checkout branch-name`


**How to push your commits?**

command:- `git push origin branch-name`

**How to update your local branch and forked repo?**

You can get list of tracked repositories by

`git remote`

add a new repo in remote by

`git remote add upstream https://github.com/url`

here `https://github.com/url` is the URL of the repo from which we have forked (from which we want to update our repo).

Now get the updates

`git fetch upstream`

Now finally merge our local repo and fetched one.

`git rebase upstream/branch-name`

If there are merge conflicts then solve then and run

`git add path/of/file/in/which/changes/are/done`

Now complete rebase

`git rebase --continue`

Now forcefully push commits (as head is changed)

`git push -f origin branch-name`

**How to change git default editor?**

`git config --global core.editor "vim"`.

I generally prefer `vim`.

**How to squash your commits?**

First get the hashcode of the previous commit, after which you want to squash

run `git log`

copy the hashcode.

Interactive rebase off of a point earlier in the history than the commit you need to modify

Now run `git rebase -i copied-hash-code`

`git` default editor will be opened(assuming `vim`)

you can see the list of all the commits committed after entered hashcode.

replace `pick` with `squash` for all those commits which you want to squash. Save and close the file (`:wq` for `vim`). After closing new file will be opened containing the list of all commit messages(which you want to squash), now enter your message for single commit and save it.

You can use `git log` to verify that commit are squashed.

**How to edit your commits messages?**

If you want to change message of the last commit then run

`git commit --amend -m "New commit message"`

Another way is to replace `pick` with `edit` in the file opened above.

Use `git commit --amend` to enter the new commit message and `git rebase --continue` to continue to rebase.

**How to drop commits?**

Replace `pick` with `drop` in the file opened above.

**How to change author details?**

- Replace `pick` with `edit` in the above file.
- Run `git commit --amend --author="Author Name <email@address.com>"`
- and `git rebase --continue` to continue rebase  

**How to rearrange your commits?**

Rearrange the commit lines in the file, which was opened by `git rebase -i copied-hash-code`.

That's it, you can easily start `git` in your project with this commands. Get more info from [here](https://git-scm.com/).

Have a nice day!
