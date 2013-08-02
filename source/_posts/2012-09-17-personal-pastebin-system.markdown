---
date: '2012-09-17 00:16:22'
layout: post
slug: personal-pastebin-system
title: Personal pastebin system
categories:
- tech
tags:
- productivity
- unix
- vim
- rsync
---

For people that talk code a lot, having a handy place to paste and share code is essential. There are tons of services available for this, and many of them have a wide following and various features. Likewise, there are also tons of tools available to integrate these services into various editors, IDEs, and who knows what else. It all becomes quite cluttered when my whole purpose was to make things simpler. I've tried a few different vim plugins and services over the years, but most recently I had been using [hastebin](http://hastebin.com/), which is a ruby gem that accepts `STDIN` then uploads it and syntax highlights it. I liked the simplicity of it since I could just select code and do something like `:'<,'>!haste | pbcopy` to copy a link of the paste to my clipboard.

However, the syntax highlighting they provide leaves something to be desired and you have to deal with their logo and options. I'm not sure how long the pastes last or if you can even specify the length. All of these critiques are being fairly picky, though. The reason I absolutely had to make a change was simply because their service is out of order way too often. I needed a better solution, and I wasn't keen on finding yet another service that would probably let me down.

Why do I need some other service to paste and store my code anyway? I can store all the code pastes I want indefinitely on my own website. I had already been using vim's `:TOhtml` command to generate local copies of my code. It's nice because it communicates exactly what I'm seeing in my vim session via HTML: syntax highlighting, line numbers, and all. With all this frustration it dawned on me how easy it would be to just use this to make my own pastebin alternative, so... I did. I used the following vimscript to do so:

```
com! -range=% HtmlPaste <line1>,<line2>call HtmlPaste()
noremap <silent> gH :HtmlPaste<cr>
fun! HtmlPaste() range
   exe a:firstline.",".a:lastline."TOhtml"
   let curTime = strftime("%H-%M-%S_%m-%d-%y")
   exe "sav! /web/octopress/source/paste/" . curTime . ".html"
   wincmd c
   exe "silent !rsync -a /web/octopress/source/paste connermcd@linode:/web"
   exe "silent !echo \"http://connermcd.com/paste/" . curTime . ".html\" | pbcopy"
   redraw!
endfun
```

As you can see, it creates a `:HtmlPaste` command that will create a pastebin out of the selected region. If no region is selected then it operates on the whole file. It then converts that region into HTML with vim's `:TOhtml` command then syncs that file to my server and copies the link to my clipboard. It ends up looking like [this][example].

   [example]: http://connermcd.com/paste/005108091712.html
