---
date: '2012-09-07 18:08:53'
layout: post
slug: the-virtues-of-vimpc
title: The virtues of vimpc
categories:
- tech
tags:
- mpd
- unix
- productivity
---

Not too long ago I made a post about [managing music with mpd](/blog/2012/07/15/managing-music-with-mpd-and-mpc/), but I didn't get the chance to really sell [vimpc][] all that much. That's regrettable because vimpc is one of those tools that I use literally on a daily basis. It vastly increases my productivity and ability to listen to and manage my music effectively. When I first got started with [mpd][] I looked into several other [alternatives][clients], but I found that vimpc was the best fit for me. I'm glad to say that it's only gotten better since then. It has an active [developer][boysetsfrog] and [maintainer][richo] that are very responsive to feature requests and bug reports. It's a good enough product on its own, but the localized friendly community has made me a die hard vimpc user. I'll attempt to explain why I like it so much.

Many of its virtues as opposed to iTunes, Songbird, Banshee, or another music player are due to its inseparable relationship with mpd. Using mpd in and of itself will probably be a huge boost in inner peace and effectiveness, but vimpc is the perfect tool to accompany mpd's simplicity, especially if you're a [vim][] user. For example, you can easily use [mpc][] and the command line to execute simple tasks or script it with other programs if you don't need a graphical editor. When you do need a graphical editor you can very quickly load vimpc so that you can see and edit your playlist or save it and load a different one. You can also use it to browse your library or move songs around in the playlist. One of the virtues of mpd is that you can close vimpc when you're done with it and the music will keep on playing. You don't have to have the client open to be playing the music like in iTunes, Songbird, or Banshee. Maybe it's easiest to just show you a video:

{% youtube RRFAqqPKiPs %}

It may be difficult to see what keys I'm pressing in the video, but in general vimpc behaves like vim. You can take a look at the `:help` documentation for an explanation of all of its features. I use a `~/.vimpcrc` file with the following lines:

{% raw %}
```
set window playlist
set autoscroll
set colour
set hlsearch
set searchwrap
set ignorecase
set sortignorethe
set sortignorecase
set mouse
set add next
set songformat {%a - %b - %t}|{%f}$E$R $H[$H%l$H]$H

map Q ZQ
map <C-N> gt
map <C-P> gT
map gs :shuffle<C-M>
map ga :!mpc listall | mpc add<C-M>:shuffle<C-M>
map gl :load 
map <BS> p
```
{% endraw %}

You can read the `:help` to find out how they work and what they do. Development is still active, so new features are still being added! I especially like the `gs` and `gl` mappings in my rc file above. It makes loading and shuffling playlists very quick and seamless. The `:load` command has tab completion so you can just hit `glch<Tab><Enter>gs` to load and shuffle the playlist "chill". The colorscheme also matches nicely with [irssi][] and my [mutt][] color scheme options.

   [vimpc]: https://github.com/richo/vimpc
   [mpd]: http://en.wikipedia.org/wiki/Music_Player_Daemon
   [clients]: http://mpd.wikia.com/wiki/Clients
   [boysetsfrog]: http://sourceforge.net/users/boysetsfrog
   [richo]: https://github.com/richo
   [vim]: http://www.vim.org/
   [mpc]: http://mpd.wikia.com/wiki/Client:Mpc
   [irssi]: http://www.irssi.org/
   [mutt]: http://www.mutt.org/
