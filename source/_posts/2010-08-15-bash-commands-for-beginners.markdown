---
date: '2010-08-15 00:04:03'
layout: post
slug: bash-commands-for-beginners
status: publish
title: Bash commands for beginners
wordpress_id: '323'
categories:
- tech
tags:
- bash
- unix
---

So you want to know how to use bash commands. Well why shouldn't you? Bash commands are a necessary part of navigating modern day terminals for web servers, linux operating systems, Mac OS X, and even jailbroken iPhones. Of course it's not necessary for the every day user, but for those who want to develop on the web or become comfortable with linux, bash commands are a must have. The [average bash guides](http://tldp.org/LDP/Bash-Beginners-Guide/html/) you'll find are anything but easy to follow. You don't want to know every command there is! You just want to be able to get the basics down and accomplish simple tasks. Well, that's why I wanted to create a short, quick and easy tutorial for the essentials.

A lot of guides will give you way too much information about the different commands and options available in bash, which is an intimidating array of preferences even for more experienced users. My intention is to give you the bare bones of what you'll need on a day to day basis using the terminal. I've split this guide up into two sections: how to see stuff and how to do stuff.## How to see stuff

### ls

First off, ls, which stands for list. This command will show you the contents of a directory. The ls command is your eyes in the terminal; there is no command more basic or necessary than seeing. It's also the most simple command in that it's just two letters and enter. There are several options for ls, but the only two you'll ever really need are -l and -a. If you're not ready for options then just move on to the next command.

### ls -l

The -l option stands for long and will display a lot more information about the files in the directory. It will show you timestamps for when they were last edited, the size of the file, the owner of the file, the group that can edit it, the file's permissions, and another column of numeric data that's not really important.

### ls -a

The -a options stands for all and will display hidden files in the directory. Keep in mind that bash options can be combined for a command, so instead of trying to remember all of these one letter options you might just want to remember ls -al (which you can remember as a mnemonic if you think of "list all." Or, you can even type `ls -all` if you want to). To see the next command, move on to page two.

### cd

The second most important command is cd, which is your legs in the terminal. The cd command stands for change directory and does just that. Unlike the ls command, the cd command takes a parameter. If the word parameter scares you, think of it this way. If you tell someone taking orders to jump, they will jump, but if you tell someone to go, they will ask "Where?" Some commands require information. The cd command needs to know what directory you want to change to. It's really simple. You just type `cd /where/you/want/to/go/to`. That's it.### A short discourse on directories

Directories in Windows are separated by backslashes, whereas in Unix based systems(Linux, Mac OS X, etc) they are separated by forward slashes. For example, in Windows file path may look like `C:\\Documents and Settings\Owner\My Documents`, but in a Unix system it might look like `/home/owner/Documents`. In the interest of keeping things short and sweet, Unix directories also employ a couple of symbols to help you navigate.

### cd /

The `/` stands for the root directory, which just means it is the very top directory. There is nothing above that directory. Whenever a file path begins with /, such as the example above, the path is beginning at the root directory and then moving downward from there. If there is no slash at the beginning then it is beginning in the directory you are currently in. For example, if I am currently in the owner directory there are at least two ways to get the the Documents directory. The easiest is `cd Documents`, but I could also begin at the root directory and type `cd /home/owner/Documents`.

### cd ~

The `~` stands for your user directory. If your username is owner then `cd ~` would take you to the owner directory too. If you were in some other directory and wanted to quickly get to Documents you could type `cd ~/Documents`.

### cd ..

A period(.) is the symbol for the directory you're currently in, and a double period(..) is the symbol for the directory one level above you. If I was in the owner directory I could type `cd ./Documents`, but it would be redundant since I can just type `cd Documents`. The reason for having a period symbol at all will become apparent once you work in the terminal more. However, the double period is obviously very useful since you can type `cd ..` to move from /home/owner to /home. You can also move up more than one directory by typing `cd ../../..` for as many directories as you want.

That's the absolute basics. To see more commands, move on to the second section on page three.## How to do stuffNow we'll move into the basics of how to do things inside the bash shell. The things I consider important are moving files, renaming files, copying files, pasting files, deleting files, and editing files. I won't cover how to edit files in this tutorial because editing files on the command line will take more time to explain. Perhaps I will write a future post about editing. For now, let's begin with the others.### A short discourse on permissions

Now, you don't want just anyone moving, renaming, and deleting files on your computer, so bash requires some authentication to do these actions to files that don't belong to you. So before you start doing them you'll want to authenticate by typing `su` and hitting enter. The terminal will then ask you for the root password. Alternatively you can type `sudo` just before a command to authenticate it individually.

### Moving and renaming

Both moving and renaming files are accomplished by one command, `mv`, which stands for move. This command takes two parameters, what and where. So let's say I'm in a directory that has a file called file.txt and I want to move it to my home folder. I can do so by typing `mv file.txt ~`. That's it. If I want to rename the file I just specify a name at the end of where I want to move it. So I could do `mv file.txt newname.txt` if I didn't want to move it or `mv file.txt ~/newname.txt` if I did. It's really simple. Keep in mind if the files don't belong to your username you'll need to log in using `su` or type `sudo` before. Reread the section above for more information.

### Copying and pasting

Copying and pasting are also accomplished in one command, which is very similar to mv. The command is `cp`, which stands for copy. It also takes two parameters, what and where. To copy the file without moving it I would type `cp file.txt ~`. Yup, it's really that easy.

### Removing

Removing a file uses the `rm` command and takes one parameter, what. So to remove the file just type `rm file.txt`. If you want to remove a directory and everything in it, add -rf as an option (i.e. `rm -rf Documents`). Now keep in mind that this will completely delete a file or directory forever. There's no going back afterwards, so it might require some authentication using `su` or `sudo`.

There you are! Some basic bash commands.
