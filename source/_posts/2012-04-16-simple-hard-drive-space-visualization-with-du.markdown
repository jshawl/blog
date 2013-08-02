---
date: '2012-04-16 09:39:36'
layout: post
slug: simple-hard-drive-space-visualization-with-du
status: publish
title: Simple hard drive space visualization with du
wordpress_id: '1372'
categories:
- tech
tags:
- mac
- productivity
- ubuntu
- unix
---

One of the main problems I hear from people is that their hard drive is running out of space and they're not sure why. External hard drives are useful, but only if you really know what is taking up all the space and want to preserve it. Otherwise, you need to do some diagnostics to find out where these large, unknown files are. If you have Windows, there is a wonderful program called [WinDirStat](http://windirstat.info/) that can help visualize space allocation. Just install and run it then click on the plus signs to the left of various folders to see how much space they and their subdirectories are using. There are also some [mac applications](http://www.macworld.com/article/1050432/spaceutilities.html) that do similar things, but I prefer to use the command line.

The `du` (disk utility) command in unix can make this process very simple. If you simply run `du` by itself then it isn't very useful. It will begin cycling through all subdirectories and spit out byte information on their size. However, with a few simple flags it can become very user-accessable. That's why I've made an alias for my du command in my ~/.profile:

```
alias duh="du -h -d 0 [^.]*"
```

After updating and sourcing your .profile, `duh` will now display a simple, human-readable output of the directories in the current folder.

```
connermcd@~$ duh
  5.5M  Desktop
  119G  Documents
   60K  Downloads
  2.5G  Dropbox
  2.3G  Library
  128G  Movies
   28G  Music
  2.4G  Pictures
  8.0K  Public
```

If you want to see hidden directories too then remove the `[^.]*` part from the command and change `-d 0` to `-d 1`.
