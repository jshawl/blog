---
date: '2011-11-27 15:40:07'
layout: post
slug: syncing-bashrc-and-vimrc-with-dropbox
status: publish
title: Syncing bashrc and vimrc with Dropbox
wordpress_id: '1148'
categories:
- tech
tags:
- bash
- dropbox
- vim
---

### The problem...
If you're like me then you are probably constantly making various changes to your computer. Often I make changes to my .vimrc, .profile, .vim folder, and other various system files multiple times a day. Then, paranoia sets in. What if your computer suddenly crashes one day and all your beautiful settings are destroyed? You've made backups for your videos and music, but who pays mind to those pesky hidden configuration files? Furthermore, what if you want to use those same configuration settings on another computer or operating system? You would constantly be having to copy and transfer these files to stay up to date.
### The solution...
Enter Dropbox. You're probably already syncing other various documents and files with Dropbox, but you hadn't thought to try syncing your configuration files. The reason is probably because they have to be in a particular location and they are often hidden files that are difficult to view in finder. Well, with some symbolic link magic you can easily get these files synced so you never have to worry about losing them.

```
cd ~
mv .vim Dropbox/vim
mv .vimrc Dropbox/vimrc
mv .profile Dropbox/profile
ln -s Dropbox/vim .vim
ln -s Dropbox/vimrc .vimrc
ln -s Dropbox/profile .profile
```

This also provides the added benefit of being able to actually see these files in Finder. That means you when find a new cool plugin that you want to download into your .vim folder you can download it directly into the plugin directory. Then, if you use other computers or operating systems you can add symbolic links that access your Dropbox folder there as well so that your plugins are universally available. It also makes it really easy to share your [.vimrc](https://www.dropbox.com/s/rsx0su1cravnjip/vimrc) with your friends.
