---
date: '2013-05-14 13:45:32'
layout: post
slug: syncing-music-to-android-from-arch
title: Syncing music to Android from Arch
categories:
- tech
tags:
- arch
- android
- google
- unix
---

One of my main reasons for getting away from iPhone was iTunes. Some people seem to love and worship iTunes but I can't stand it, so when I had my macbook instead of using iTunes I would just use [mpd][] and sync my music to my android over a [samba][] share using [SyncMe wireless][syncme]. This solution works great. All you have to do is connect your device to the same wireless network as your computer, point, and shoot. It syncs up all the new music you've purchased on your computer to your devices so you can listen anywhere.

Unfortunately, when I moved to a very minimalistic system samba sharing gave me some trouble. I had never set up a samba server manually before and in some ways it's less than intuitive. For instance, who would have guessed you needed commands like `testparm` and `pdbedit` for samba? They don't start with smb or anything.

Luckily, arch has great documentation (as always) and provides some useful systemd service files to get you going once you install samba (`sudo pacman -S samba`). Once you've got it installed you'll need to `sudoedit /etc/samba/smb.conf` to set up your server. My setup looks like this:

```
[global]
   workgroup = CMCD
   server string = Conner's Share
   security = user
   log file = /var/log/samba/samba.log
   max log size = 50
   dns proxy = no 

[connermcd]
   comment = Conner
   path = /home/connermcd
   browsable = yes
   writable = yes
   valid users = connermcd
```

So, you might think that now you can just `sudo systemctl start smbd` and be merrily on your way, but you would be wrong. First you need to add your user to the samba database:

```
sudo pdbedit -a -u connermcd
```

Then, make sure that you have the appropriate ports open in iptables:

```
-A INPUT -p tcp --dport 139 -j ACCEPT
-A INPUT -p tcp --dport 445 -j ACCEPT
-A INPUT -p udp --sport 137 -j ACCEPT
-A INPUT -p udp --dport 137 -j ACCEPT
-A INPUT -p udp --dport 138 -j ACCEPT
```

Finally, start both NetBios and Sambda (and optionally enable them for automation):

```
sudo systemctl enable nmbd
sudo systemctl enable smbd
sudo systemctl start nmbd
sudo systemctl start smbd
```

Then you should be good to go. Set up the computer in [SyncMe wireless][syncme] and sync whatever you want!

   [mpd]: http://connermcd.com/blog/2012/07/15/managing-music-with-mpd-and-mpc/
   [samba]: http://www.samba.org/
   [syncme]: https://play.google.com/store/apps/details?id=com.bv.wifisync&hl=en
