---
date: '2012-05-20 23:57:15'
layout: post
slug: updating-vim-pathogen-plugins
status: publish
title: Updating vim pathogen plugins
wordpress_id: '1440'
categories:
- tech
tags:
- bash
- productivity
- unix
- vim
---

I love [pathogen](https://github.com/tpope/vim-pathogen) for managing my vim plugins. It allows me to put plugins in my ~/.vim/bundle directory and have the confidence of being able to simply uninstall them by deleting the plugin directory. Since nowadays almost every vim plugin has a github repository, it's very simple to do a `git clone <paste>` in the ~/.vim/bundle and then later update it with a `git pull`. Since a `git pull` will do nothing to a directory that either isn't a repository or has changes, you can safely execute it on all the directories in your bundle without worrying. I made a simple command to put in my .vimrc that will do just that.

```
command! -nargs=0 Update :!find ~/.vim/bundle -type d -d 1 |\
while read line; do\
   echo `basename "$line"`;\
   cd "$line" && git pull; cd -;\
done
```
