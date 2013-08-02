---
date: '2012-09-19 22:21:17'
layout: post
slug: personal-screenshot-system
title: Personal screenshot system
categories:
- tech
tags:
- mac
- bash
- unix
- rsync
---

A couple of days ago I made [a post][pastebin] describing how I made a personal pastebin system. Since this was fresh on my mind, today when I needed to share a screenshot with someone I naturally thought there must be a simpler way to do this. I'm sure there are a hundred different proprietary programs I could download that would provide me a similar service, but I have all the tools I need right here and I want full control of my system without installing extra applications. This is one of those few occasions when [Automator.app][automator] comes in very handy. It's very easy and enjoyable to use; I just don't have a lot of need for it. But when I do, it is awesome.

I created a new workflow with just two jobs: take a screenshot interactively (allowing me to select the region) and run a script. This way I can use the script area to rename and sync the screenshot, like this:

```
curTime=`date +%H%M%S%m%d%y`
mv /screenshots/tmp.png "/screenshots/$curTime.png"
rsync -a /Users/connermcd/Dropbox/Tech/web/octopress/source/screenshots connermcd@linode:/web
echo "http://connermcd.com/screenshots/$curTime.png" | pbcopy
```

Once I run it it automatically syncs to my website and copies the link to my clipboard. The result looks like [this][example]. I then saved the workflow as an application and I trigger it with a keyboard shortcut using [BetterTouchTool][BTT]. I also changed my [lighttpd][lighttpd] settings so that my `/paste` and `/screenshots` folders are password protected. That way I can look at my pastes and screenshots en masse without opening them to the whole world.

   [pastebin]: http://connermcd.com/blog/2012/09/17/personal-pastebin-system/
   [automator]: http://www.automatorapp.com/
   [example]: http://connermcd.com/screenshots/223821091912.png
   [BTT]: http://blog.boastr.net/
   [lighttpd]: http://www.lighttpd.net/
