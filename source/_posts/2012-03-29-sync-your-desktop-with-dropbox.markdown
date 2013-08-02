---
date: '2012-03-29 11:11:49'
layout: post
slug: sync-your-desktop-with-dropbox
status: publish
title: Sync your desktop with Dropbox
wordpress_id: '1351'
categories:
- tech
tags:
- dropbox
- unix
---

I generally have two locations where I put things requiring action from me: my email inbox and my computer's desktop. Once I've dealt with emails I archive them so my inbox is always kept clean except for things requiring my action. Likewise I either delete or organize documents that have been on my desktop once I'm done with them. It's always bothered me however, that once I turn my computer off I can't get to those files on my phone or other computers. If you try to make an alias of your Desktop and put it into Dropbox it won't work. Thankfully, there is a way using symlinks. Open up Applications→Utilities→Terminal and type in:

```
cd ~/Dropbox
ln -s ~/Desktop Desktop
```

Now you'll have a folder in your Dropbox folder that is kept in sync with your desktop. You can do this on other computers as well to keep your desktop synced across multiple computers!
