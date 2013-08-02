---
date: '2012-09-28 21:39:06'
layout: post
slug: chatting-with-bitlbee-and-irssi
title: Chatting with bitlbee and irssi
categories:
- tech
tags:
- irssi
- google
---

I've been using [bitlbee][] for a while now, and it's worth promoting. I understand that not everyone uses or needs an IRC client, but you don't have to use IRC or be on an IRC network to use bitlbee. You can treat it as if its only purpose is a command line chat agent. I mainly only chat using [google talk][talk]. This is supported in bitlbee through XMPP/jabber, a chat protocol that google supports. Facebook chat also supports XMPP, so you can facebook chat with bitlbee too if you want. On top of that bitlbee supports MSN messenger, Yahoo! messenger, AIM, ICQ, and twitter. In other words, it supports pretty much everything worth supporting.

So it supports stuff, but why should you use it? The obvious part has already been said -- it allows you to move your chat client to the command line. If you are already using a command line IRC client then moving to bitlbee is very easy. I use one of the [public servers][public] that bitlbee provides to connect. Of course, bitlbee is open source and you're welcome to compile and run your own server if you like control, but using a public server is hassle free. Once you have a server chosen (or up and running) just open up your IRC client and connect to it. It will automatically connect you to a channel with instructions on setting up your various accounts. Setup is a one time thing, and if you set your IRC client to automatically connect to the server then everything happens automatically on start.

I use [irssi][] for my IRC client. There's plenty of guides out there about irssi and how to use it, so I won't go too far into that for this post. I don't use IRC that much, but I do occassionally hang out in the `#vim` room on freenode. You can learn a lot from those guys! Any IRC client will do for bitlbee, but I like irssi since it's very customizable and I can theme it to fit with my [vimpc][] and [mutt][]. You can set your away status easily just like you would in IRC with `/away Gone fishing...`. Messaging a buddy is as easy as `/msg dan<Tab>` and it autocompletes their name. That will start a private window with them, so you only have to type it once and then you can chat as per normal. You can also facilitate group chats and modify other settings quite easily -- it just works! There are also some [irssi scripts][scripts] to add other functionality like a notification that the other person is typing.

   [bitlbee]: http://www.bitlbee.org/main.php/news.r.html
   [talk]: http://www.google.com/talk/
   [public]: http://www.bitlbee.org/main.php/servers.html
   [irssi]: http://www.irssi.org/
   [vimpc]: http://connermcd.com/blog/2012/09/07/the-virtues-of-vimpc/
   [mutt]: http://connermcd.com/blog/2012/09/25/using-mutt-with-offlineimap-and-vim/
   [scripts]: http://the-timing.nl/stuff/irssi-bitlbee/
