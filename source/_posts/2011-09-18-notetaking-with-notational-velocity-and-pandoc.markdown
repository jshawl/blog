---
date: '2011-09-18 23:41:26'
layout: post
slug: notetaking-with-notational-velocity-and-pandoc
status: publish
title: Notetaking with Notational Velocity and pandoc
wordpress_id: '879'
categories:
- tech
tags:
- dropbox
- mac
- markdown
- notational velocity
- pandoc
- snippets
- vim
---

Being a medical student, taking notes is a large part of my life right now.  I developed a way to take, organize, and share my notes with others in an easily readable format. I am addicted to [vim](http://www.vim.org/), so for a long time I searched for a way to conveniently take notes with it. Many people get by with taking notes solely with vim. I tried this for a while, but it had a few pitfalls. The files were generally disorganized, so it was hard to locate a particular term or topic that needed to be reviewed (EDIT: I have since switched to using solely vim. You can read about it [here](http://connermcd.com/blog/2011/10/21/notetaking-with-vim/)). Since I take notes in [markdown](http://daringfireball.net/projects/markdown/), they are reasonably readable straight from the text file; however, when I shared these text files with others they often got jumbled and ugly in a different text editor. Equations and images were also ugly and absent, respectively.

My eldest brother is a professor and has a similar need to take down notes. He persuaded me to try [Notational Velocity](http://notational.net/), a notetaking application for Macs, and despite my initial hesistance I have come to really enjoy it. It doesn't do anything that couldn't be done from the command line, but it organizes and searches through notes cleanly and _quickly_. It's a fast way to find a particular term or topic in a large folder of notes. It has a built in text editor, but I simply use it as an organizer and use its hotkeys to use my editor of choice (vim). Of course, the organization could be done solely through vim or the command line if you don't have a Mac.

Taking notes in [markdown](http://daringfireball.net/projects/markdown/) makes it pretty easy to convert them to other file formats. The best program for doing this is [pandoc](http://johnmacfarlane.net/pandoc/) which includes a wrapper that allows for conversion to PDF. I wrote a post on how I got pandoc to [install on Snow Leopard](http://connermcd.com/blog/2011/05/15/using-pandoc-on-mac-osx/). The nice thing about pandoc is its extended markdown features and quick file conversion. Also included is the ability to use LaTeX math equations and images. Exporting your notes into a PDF with nice looking equations and images makes reviewing and studying them much more enjoyable. It also creates a table of contents based on your headers that makes the PDF easy to navigate.  Mapping a hotkey to export your notes as a PDF in vim is quick and easy.

All of my notes and my conglomerate PDF get saved within a folder in my [Dropbox](https://www.dropbox.com/), which automatically syncs everything for easy access on my phone.  The Dropbox app for Android allows me to edit the text files as well as view the PDF with images. This also allows me to easily share the folder with other students, and since the file format is PDF, everybody can use it. I use a public link to share my notes so that others cannot edit the file, but if you wanted to let others edit the documents, Dropbox has folder sharing options.
