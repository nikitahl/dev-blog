---
layout: post
permalink: basic-terminal-commands
title: Basic terminal commands and tips for beginner developers daily use
date: 2020-11-13T07:24:08.316Z
description: Basic terminal commands and tips. Easy to remember and understand
  for beginner developers, use it daily and improve your terminal skills.
tags:
  - development
---
Knowing how to use a terminal is a good skill to have as a developer. You can use to run various tools or running [git commands](/basic-git-commands).

It can be intimidating at first, especially if you are a beginner. But once you understand the principles behind it, it is not so complicated.

The terminal commands listed below are the founding stones for your further work. They are easy to understand and remember.

1. [`pwd`](#1-pwd)
2. [`ls`](#2-ls)
3. [`cd`](#3-cd)
4. [`mkdir`](#4-mkdir)
5. [`rmdir`](#5-rmdir)
6. [`rm`](#6-rm)
7. [`!!`](#7-)
8. [`clear`](#8-clear)
9. [`sudo`](#9-sudo)
10. [Tips](#tips)

## 1. `pwd`

`pwd` - stands for **print working directory**. Running this command will output the path to the directory your currently in.

```shell
Nikitas-MBP:~ nikitahlopovs$ pwd
/Users/nikitahlopovs
```

## 2. `ls`

`ls` - stands for **list**. This command will output a list of all directories and files inside the current directory.

```shell
Nikitas-MBP:~ nikitahlopovs$ ls
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Library             
              
```

## 3. `cd`

`cd` - stands for **change directory**. This command is used to change directory and move around your system.

```shell
Nikitas-MBP:~ nikitahlopovs$ cd Documents/Sites
Nikitas-MBP:~ nikitahlopovs$ pwd
/Users/nikitahlopovs/Documents/Sites
```

Some additional **change directory** commands are quite useful.

* To go to the parent directory use: `cd ..`
* To go to the root directory from any location use: `cd /`
* To go to the home directory from any location use: `cd ~`

## 4. `mkdir`

`mkdir` - stands for **make directory**. This command is used to create a directory. 

```shell
Nikitas-MBP:~ nikitahlopovs$ mkdir helloWorld
Nikitas-MBP:~ nikitahlopovs$ ls
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Library				helloWorld
```

## 5. `rmdir`

`rmdir` - stands for **remove directory**. This command is used to remove a directory. 

```shell
Nikitas-MBP:~ nikitahlopovs$ rmdir helloWorld
Nikitas-MBP:~ nikitahlopovs$ ls
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Library
```

## 6. `rm`

`rm` - stands for **remove**. This command is used to remove the specified directory or file. 

```shell
Nikitas-MBP:~ nikitahlopovs$ rm index.php
```

## 7. `!!`

`!!` - execute the last command typed.

```shell
Nikitas-MBP:~ nikitahlopovs$ ls
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Library
Nikitas-MBP:~ nikitahlopovs$ !!
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Library
```

## 8. clear

`clear` - will clear the terminal screen of all the text.

```shell
Nikitas-MBP:~ nikitahlopovs$ clear
```

## 9. `sudo`

`sudo` - stands for **super user do**. This command will execute any command with the security privileges of the super user. The example below will execute the last typed command with the security privileges of the super user.

```shell
Nikitas-MBP:~ nikitahlopovs$ sudo !!
```

## Tips

Below are some useful key combinations that will help you be more productive and handle terminal with ease.

* <kbd>fn</kbd> + <kbd>shift(⇧)</kbd> + <kbd>←</kbd> - Jump to the start of the line
* <kbd>fn</kbd> + <kbd>shift(⇧)</kbd> + <kbd>→</kbd> - Jump to the end of the line
* <kbd>alt(⌥)</kbd> + <kbd>←</kbd> - Jump to the previous word
* <kbd>alt(⌥)</kbd> + <kbd>→</kbd> - Jump to the next word
* <kbd>ctrl(⌃)</kbd> + <kbd>u</kbd> - Remove all text in the current line
* Double-clicking on the <kbd>Tab</kbd> button acts as an autocomplete and will offer you suggestions. This is useful when typing in a path.

## Additional resources

There are a lot more than these basic terminal commands. You can learn a lot more and become very productive and efficient if you know more commands. Below just a few useful resources for you to extend your knowledge:

* [MAC terminal cheat sheet](https://www.makeuseof.com/tag/mac-terminal-commands-cheat-sheet/)
* [Basic terminal commands list](https://medium.com/@manujarvinen/learning-some-basic-terminal-commands-d478e7b8ffe4)