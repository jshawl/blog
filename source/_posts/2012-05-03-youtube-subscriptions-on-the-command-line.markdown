---
date: '2012-05-03 01:11:58'
layout: post
slug: youtube-subscriptions-on-the-command-line
status: publish
title: YouTube subscriptions on the command line
wordpress_id: '1402'
categories:
- tech
tags:
- awk
- bash
- google
- mac
- unix
- vlc
- youtube
---

I'm a fan of [YouTube](http://www.youtube.com/), but I am not a browser. I only want to watch what I want to watch. Generally I'll go to their site, add the new subscription videos I haven't seen yet to a watch later playlist and then play the playlist. I can't believe how difficult this is. Why isn't there any easier way to see new videos I'm subscribed to? Even once you get the playlist going there isn't a good way to watch it. There's all this busyness on the screen and sometimes I have to scroll to get the picture in the right place. You can fullscreen it, but that renders the browser useless for other tasks. Well, despite my being peeved at the inconvenience I kept at this for some time until yesterday when I realized that the button to add to the watch later playlist was no longer working. How's that for making something bad terrible? So, I decided I'd look for a simpler solution.

What I found is not what I thought I'd find. The first thing I found was a simple command line utility to download YouTube videos. To my surprised, it worked without any trouble. It's unimaginatively called [youtube-dl](http://rg3.github.com/yohttp://rg3.github.com/youtube-dl/utube-dl/), and it does exactly what it says if you just point and shoot. That's great and all, but it's not at all what I'm looking for. I don't want to be downloading all my videos just to watch them. Then I found [this video](http://youtu.be/QCuq0_nY3Xk) on streaming YouTube to mplayer. There's actually now a much easier way with [VLC](http://www.videolan.org/). With VLC you can simply point and shoot at the video link:

```
vlc "http://youtu.be/QCuq0_nY3Xk"
```

Awesome. The quality is actually great, and this allows you to turn the volume up even higher. You can also fast forward and rewind without much difficulty. You can even speed up or slow down the video - no sweat! Now I was onto something. I just need a way to stream the videos I want. I looked into RSS feeds for new subscriptions and found that you can get one at `http://gdata.youtube.com/feeds/base/users/USERNAME/newsubscriptionvideos`.

as long as your user settings under sharing allow other people to see when you subscribe. Then you can RSS subscribe to see your videos. This is exactly what I was looking for. With a simple bash script I can parse this, check for new content, and play it with VLC. 

Get the script [here](https://www.dropbox.com/s/tt8srp45j9c26i4/youtube.sh). Just edit the username variable with yours and this should work provided you're on a mac and have VLC installed. If you're on a linux distro this could easily be adapted to work for you as well. It could probably use some work to make it more user friendly. As of now to proceed to the next video you have to close VLC, and if you want to stop playback you have to ^C during the sleep. I couldn't figure out a simple way to add the file to an existing VLC playlist and when I tried passing all new videos as arguments VLC crashed. It also grabs videos that are in the info area of the subscriptions. I may look into this more later, but if you figure something out about it let me know!
