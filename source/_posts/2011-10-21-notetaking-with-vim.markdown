---
date: '2011-10-21 22:43:38'
layout: post
slug: notetaking-with-vim
status: publish
title: Notetaking with vim
wordpress_id: '1033'
categories:
- tech
tags:
- mac
- markdown
- notational velocity
- snippets
- vim
---

Eventually I realized that Notational Velocity was just an extra keyboard shortcut and window on my desktop, so I ditched it for some better alternatives in vim. I'm especially fond of using [ack](http://betterthangrep.com/) and the [ack plugin for vim](https://github.com/mileszs/ack.vim). I'm using these mappings for my .vimrc

```
map n :e! /notes
map ] :Note
map [ :NoteTab
map 0 :Nls
imap ] :Note
imap [ :NoteTab
imap 0 :Nls
command -nargs=1 Note :exe "e! " . fnameescape("/notes/.txt")
command -nargs=1 NoteTab :exe "tabnew " . fnameescape("/notes/.txt")
command -nargs=1 Nls :Ack --text "" /notes
```

I've also made some snippets to help with notetaking in markdown.

```
snippet img
![${1}](/notes/img/${2})${3}
snippet t
# `expand("%:r")`
> Date: `strftime("%m-%d-%y")`
> Instructor: ${1} `

## ${2}
```

The video also references my post about [WriteRoom mode in vim](http://connermcd.com/blog/2011/10/12/using-vim-in-place-of-writeroom/).

{% youtube HJ93UYeaoww %}
