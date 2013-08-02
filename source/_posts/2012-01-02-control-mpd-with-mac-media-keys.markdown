---
date: '2012-01-02 18:38:09'
layout: post
slug: control-mpd-with-mac-media-keys
status: publish
title: Control mpd with mac media keys
wordpress_id: '1267'
categories:
- tech
tags:
- bash
- mac
- mpd
---

I've recently bought into using [Music Player Daemon (mpd)](http://en.wikipedia.org/wiki/Music_Player_Daemon) to manage my music. I've never liked [iTunes](http://en.wikipedia.org/wiki/ITunes), and I couldn't find an alternative that well suited my needs. I tried [VLC](http://en.wikipedia.org/wiki/VLC_media_player) for a while, but it's better suited for videos than music management. I tried [Songbird](http://en.wikipedia.org/wiki/Songbird_(software)) for a while, but it has several bugs and none of the plugins I want work after they updated to the newest version. As you know, I'm a command line sort of guy, so I looked for a way to manage my music on the shell. As it turns out, mpd is the best and most widely used means of doing this. There are many various clients to control the daemon, but the standard command line option is [Music Player Client (mpc)](http://mpd.wikia.com/wiki/Clients). It has a rich set of features, but doesn't attempt to facilitate visual management. There are several clients that remedy this, and the nice thing about mpd is that you can have multiple clients running (or not) at the same time. Opening and closing a client doesn't affect the music playing server. I may write a post later on which client I settled on.

Before I could be convinced to switch to solely using mpd there was one thing that I had to resolve. I enjoy using the media keys on my mac (e.g. previous, pause/play, and next), but remapping them can be something of a hassle. I already use [BetterTouchTool](http://blog.boastr.net/) to help manage key mapping and trackpad mapping on my mac, so I was really looking for a way to accomplish this with it. However, there are two problems to overcome.

There's no way to directly map to a bash command in BetterTouchTool. You can map a key to run a script, but a terminal window will have to temporarily open. That temporary terminal window can cause some issues if you have other terminal plugins running. However, if you open Utilities > AppleScript Editor you can use `do shell script "/usr/local/bin/mpc prev"` then save that AppleScript somewhere convenient (I put mine in ~/.mpd), and map a BetterTouchTool key to trigger it. Now you can trigger the command flawlessly without opening that pesky terminal window.

I wasn't satisfied though. I wanted to use my media keys to control this action and BetterTouchTool doesn't allow mapping of media keys. If you go to System Preferences > Keyboard you will find an option to "Use all F1, F2, etc. keys as standard function keys" which will swap your F# keys with your media keys. This is not the effect I was looking for. I don't want to have to hit Fn+F10 to mute - I just want the previous, play/pause, and next media keys to be swapped. The solution I found was [KeyboardRemap4MacBook](http://pqrs.org/macosx/keyremap4macbook/) which allows just that (and a lot more). Install the dmg then go to System Preferences > KeyboardRemap4MacBook and activate both "Music Controls to F7,F8,F9" and "Fn+F7,F8,F9 to Music Controls". Now you can map F7, F8, and F9 to your AppleScripts so you can control mpc. At the same time, if you have a video running in VLC you can pause/play it with Fn+F8.

Perhaps it's not the cleanest solution in the world, but I'm satisfied!
