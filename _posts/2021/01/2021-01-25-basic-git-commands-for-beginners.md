---
layout: post
permalink: basic-git-commands
title: A list of basic Git commands for beginners for everyday use
date: 2021-01-29T09:34:39.657Z
description: Get familiar with the most basic git commands for beginners. This
  is a complete list divided into groups for better comprehension.
tags:
  - git
  - development
---

Knowing how to use Git is a must-have skill for any kind of developer these days. [Git](https://git-scm.com/) is a [version control system](https://en.wikipedia.org/wiki/Version_control) for tracking file changes.

Ideally, you should start learning Git right after you started to learn coding fundamentals. Git will be your tool to handle projects whether they're your personal or you work in a team.

Git commands are executed in a terminal, so before we begin you should have a basic understanding of how to work in a [terminal](/basic-terminal-commands).

1. [Configuration](#1-configuration)
2. [Initialization](#2-initialization)
3. [Cloning](#3-cloning)
4. [Adding/removing files](#4-addingremoving-files)
5. [Checking status](#5-checking-status-and-changes)
6. [Committing](#6-committing)
7. [Undoing/reverting commits](#7-undoingreverting-commits)
8. [Pushing](#8-pushing)
9. [Branching](#9-branching)
10. [Remote repos](#10-remote-repos)

## 1. Configuration

Use `git config` command to configure your user name and email for Git. It's a good idea to set these from the beginning, so that your name will be displayed in the contribution history.

```shell
git config --global user.name "Name Surname"
git config --global user.email yourname@example.com
```

## 2. Initialization

To initialize a Git repository run following command in your project directory:

```shell
git init
```

You may notice that a new *.git* directory is created inside your project directory. NOTE: *.git* is a hidden directory so you may want to enable hidden files and folders view on your system.

## 3. Cloning

To clone an existing remote repository use:

```shell
git clone https://github.com/username/reponame.git
```

This command creates a copy of a remote repository by downloading all the files.

To clone a local repository use:

```shell
git clone path/to/the/local/repository
```

## 4. Adding/removing files

After you've made changes to your project you can add changed files to a temporary staging with `git add` command.

```shell
git add file1 file2 file3
```

To add all files use dot:

```shell
git add .
```

To remove a file from a temporary staging use `git reset` command:

```shell
git reset file1 file2 file3
```

To remove all files use:

```shell
git reset .
```

## 5. Checking status and changes

These commands can help you overview the status of your changes before adding or committing.

After changes are done or the file gets added or removed from temporary staging, you can check the current status of the situation.

```shell
git status
```

This command will show you new, deleted, or modified files as well as if the file is added to the temporary staging.

To see the changes you've made use:

```shell
git diff
```

### 5.1. Stashing

If for some reason you need to save changes and apply them later Git allows you to temporarily stash your changes:

```shell
git stash
```

List all stash changes:

```shell
git stash list
```

Apply changes from latest stash:

```shell
git stash apply
```

Apply specific stash from index:

```shell
git stash apply stash@{0}
```

## 6. Committing

Once you've added your files and ready to commit them use the command:

```shell
git commit
```

NOTE: this command will prompt you with a commit message screen, where you have to input your commit message, save it and close the screen. Many beginners [struggle with this screen](https://stackoverflow.com/questions/13239368/git-how-to-close-commit-editor). To make it easier you can write it in one line by adding `-m` option:

```shell
git commit -m "Your commit message"
```

## 7. Undoing/reverting commits

Before you pushed any commits there's a possibility to revert or undo them. The `git reset` command will allow you to roll back to a given commit. Suppose you've made several commits already.

To undo/revert the last commit use:

```shell
git reset HEAD~
```

To revert to a specific commit, you'll need to specify the [commit SHA](https://blog.thoughtram.io/git/2014/11/18/the-anatomy-of-a-git-commit.html) key. To do that you'll need to view your history of changes with:

```shell
git log
```

It will output a list of your commits, each containing a unique SHA key. Copy that key and run:

```shell
git reset 0447816744595c69968bb517b93bc4f5b42df20f
```

## 8. Pushing

Once you've satisfied with your changes and have committed all of them you're ready to push them to your repo.

### 8.1. Syncing

Before the actual push, you'll need to synchronize your local project instance with the remote repository changes. To do that you'll need to fetch and merge the latest changes from the remote repo.

```shell
git pull
```

If you only want to see the changes without merging then use fetch command:

```shell
git fetch
```

To finally push changes run:

```shell
git push
```

## 9. Branching

Branches allow you to work safely and independently on different features. Git allows to have multiple branches. A few commands that will help you quickly get into the issue.

See the list of all local branches and the current active one:

```shell
git branch
```

Create a new branch:

```shell
git branch feature-x
```

Change the branch:

```shell
git checkout feature-x
```

Delete the branch:

```shell
git branch -d feature-x
```

A few useful commands to be more productive.

Checkout to the previous branch:

```shell
git checkout -
```

Create a new branch and immediately checkout to it:

```shell
git checkout -b feature-y
```

Rename current branch:

```shell
git branch -m feature-z
```

## 10. Remote repos

If you're going to collaborate on project with multiple people, you'll need to know few commands to set up your local project just for that.

To check all of your [remote repositories](https://docs.github.com/en/github/using-git/managing-remote-repositories):

```shell
git remote -v
```

 To connet your local project to a remote repository:

```shell
git remote add origin https://path.to/remote/repository.git
```

## Conclusion

The above commands should cover the basics and will give you the foundation with Git. Make sure to practice them regularly and consider checking other resources for more in depth knowledge.

* [Pro Git book, by Scott Chacon and Ben Straub](https://git-scm.com/book/en/v2)
* [Most visual and interactive way to learn Git](https://learngitbranching.js.org/)