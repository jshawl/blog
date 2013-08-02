---
date: 2012-07-15 15:38:10
layout: post
slug: managing-music-with-mpd-and-mpc
title: Managing music with mpd
categories:
- tech
tags:
- mac
- mpd
- unix
- android
---

I've been using the Music Player Daemon ([mpd][]) to manage my music for about a year now, and I couldn't be more pleased with it. I was itching for a way to move away from iTunes because of the inability to truly own the music you buy and the unruly (and often unstable) software. Being a simplistic, command-line-kind-of-guy, I didn't want my music player to take 10 seconds to load, have 50 menus, steal my right to purchase music and crash every now and then. Music Player Daemon ([mpd][]) provides a simple way to play your music. A daemon is a program that runs persistently in the background and waits for other programs or users to interact with it. For example, apache and the ruby on rails server are daemons. This means that mpd is not a GUI like iTunes or [Songbird][]. By itself, mpd does not have the commands needed to manage itself. It simply sets up the possibility of a persistently active playlist that can be managed by other [clients][]. This is nice because you don't have to have any particular client open all the time. When you're playing music with iTunes or [Songbird][], you must have the program running.

Music Player Client ([mpc][]) is a basic command-line client for mpd. With it you can control mpd's behavior by pausing, skipping to the next or previous track, making and managing playlists, searching for songs, changing the volume, seeking, shuffling, and a host of other options. However, there are some advantages to having some graphical control over mpd, and that's where vi music player client ([vimpc][]) comes in. I tried several other clients such as [ncmpc][], [ncmpcpp][], [vimmp][], and [pms][], but [vimpc][] is the one I settled on. The reason is because it has the most [vim][]-like characteristics and customization. It could use some additional features, but it excels in the essentials. It has a very rudimentary configuration file (.vimpcrc) that allows some startup customization. There are also plenty of graphical [clients][] available if you're not a command line person.

## But... why?

Sure, it seems like a lot of hassle to move everything from iTunes to a command line solution. That's because it is. Managing music libraries is a huge pain, but in the year I've been doing this since I got it set up, it has been anything but painful. On the other hand, iTunes is not a one-time frustration. It's a frustration every time you want to sync a new device, move your library to a new computer, or share a song with a friend. With my setup now, all my music is organized with properly tagged metadata and unrestrictive file types. I can simply turn on my computer, hit play, and it will start shuffling all my music. Moving to a new system would be a breeze and syncing to my android is easy and wireless with [SyncMe][]. I can access my music graphically or via the command line with almost zero CPU usage overhead. It's easily scriptable so that you can integrate your music with all kinds of things. I also managed [Growl][] notifications by tweaking [mpd-hiss][] and [mpd-albumart][]. There are mpd remotes for android and I'm sure there are iPhone apps as well. I also got my mac media keys to work, which I discuss in [this post](http://connermcd.com/blog/2012/01/02/control-mpd-with-mac-media-keys/). I love having all my music in simply named directories under `~/Music`. When I download music from amazon it automatically puts the new album in the correct spot. It just makes sense.

Unfortunately, transitioning can be more difficult if you have already purchased a lot of music from the iTunes Store. The only way to get encrypted iTunes songs out of iTunes is by burning them to a CD and then re-ripping them. If you have a big library this could take forever. Some programs to hack this have come and gone -- there may still be some available, but when I looked they weren't any good solutions. Luckily, I hadn't purchased all that much from the iTunes Store. I used [MusicBrainz][] to help appropriately tag all my music and organize it. It took a while to get the handle of and get everything organized, but I'm so glad I did. I feel that the hoardes of iTunes Store users will be upset when one day iTunes goes the way of the dodo and they can't get their music. The only real downside is that I can't use iTunes gift cards when people buy them for me. They make great re-gifts though.

## Usability scripts

To get my mpd setup to run on system startup, I execute a script that looks like this:

```
#!/bin/sh

/usr/local/bin/mpd
/usr/local/bin/mpc listall | /usr/local/bin/mpc add
/usr/local/bin/mpc shuffle
/Users/connermcd/.mpd/mpd-albumart.py
/Users/connermcd/.mpd/mpd-hiss/mpd-hiss.py &>/dev/null
```

The first line starts the daemon. The second adds all of my music in my library to my playlist and the third shuffles it. This way, I can party shuffle by just pressing play once I log in. Then, I run my tweaked versions of [mpd-albumart][] and [mpd-hiss][]. I may edit this post later and share them if there's interest. From that point, I can run [vimpc][] or just do [mpc][] commands. I made a short script based on [mpd-hiss][] to growl the currently playing song too. That way I can run it on a keypress and see what's currently playing. Everything runs smoothly without slowly down my system's performance at all. In my eyes, it's worth it.

   [mpd]: http://mpd.wikia.com/wiki/Install
   [clients]: http://mpd.wikia.com/wiki/Clients
   [Songbird]: http://getsongbird.com/
   [mpc]: http://sourceforge.net/projects/musicpd/files/mpc/0.22/mpc-0.22.tar.bz2/download
   [vimpc]: https://github.com/richo/vimpc
   [ncmpc]: http://sourceforge.net/projects/musicpd/files/ncmpc/0.20/ncmpc-0.20.tar.bz2/download
   [ncmpcpp]: http://unkart.ovh.org/ncmpcpp/
   [vimmp]: http://www.vim.org/scripts/script.php?script_id=2369
   [pms]: http://pms.sourceforge.net/
   [vim]: http://www.vim.org/index.php
   [SyncMe]: https://play.google.com/store/apps/details?id=com.bv.wifisync&hl=en
   [Growl]: http://growl.info/
   [mpd-hiss]: https://github.com/ahihi/mpd-hiss
   [mpd-albumart]: http://crunchbanglinux.org/forums/topic/4686/howto-mpd/
   [MusicBrainz]: http://musicbrainz.org/
