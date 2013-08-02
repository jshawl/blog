---
date: '2012-01-07 11:13:21'
layout: post
slug: tasky-txt-a-google-tasks-cli
status: publish
title: Tasky.txt, a Google Tasks CLI
wordpress_id: '1277'
categories:
- tech
tags:
- bash
- google
- productivity
---

Ever since I started using vim my fingers have been glued to the keyboard. I've adapted to methods that allow me to open programs, surf the web, listen to music, and be productive without moving my hands to the trackpad. The command line is a great asset in accomplishing this since it facilitates file management and other products that share the no-mouse mentality. Several months ago I started using [vimium](http://vimium.github.com/), a chrome extension that allows web surfing with keyboard shortcuts. It works great on most sites; however, it was causing issues with Gmail. I had looked at [mutt](http://www.mutt.org/) and other email clients, but I really appreciated the rich features, images, and HTML content that Gmail allowed for. Fortunately, Google has glimpsed at the beauty of the no-mouse mindset and created customizable keyboard shortcuts for Gmail.

One of the cool features I noted when I was exploring these shortcuts is that you can press 'T' on a message to automatically add a email-associated task to your Google Tasks with a link to the email. That seemed really nifty to manage those emails that I never quite got around to answering; however, I had been using [Todo.txt](http://todotxt.com/) to manage my todo list due to its simplicity. To my chagrin, there wasn't a comparable option for the Google Tasks API on the command line. The product I did find was [tasky](https://github.com/jrupac/tasky) by [Ajay Roopakalu](http://jrupac.wordpress.com/) which allows Google Tasks management using python. While [tasky](https://github.com/jrupac/tasky) is a great product, compared to [Todo.txt](http://todotxt.com/) it seems very clunky and unhelpful. It lacks minimalism and simplicity and is often very verbose. I [forked the project](https://github.com/connermcd/tasky) in an attempt to make it more user friendly for task management.

It's still a work in progress, has a few bugs, and completely disregards error catching, but the basic necessities are there if you use it correctly. Sometimes the task list display after executing a command is incorrect and you have to list again. I'll fix that when I'm able based on perceived interest in the project. You can read more about the project in the documentation on [the github page](https://github.com/connermcd/tasky).
