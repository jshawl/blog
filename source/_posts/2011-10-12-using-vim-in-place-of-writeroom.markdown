---
date: '2011-10-12 20:42:35'
layout: post
slug: using-vim-in-place-of-writeroom
status: publish
title: Using vim in place of WriteRoom
wordpress_id: '947'
categories:
- tech
tags:
- vim
---

Fullscreen editors, also called distraction-free editors, have become popular lately. It's appealing to have nothing but the words you're editing before you. However, these editors are often lacking some of the most elemental of features and sometimes cost money. Fortunately, it's pretty easy to make MacVim into an exact replica of WriteRoom (or gVim into DarkRoom on Windows).
Put the following into your .vimrc:

```
let g:writeroom = 0
let g:transparency = &transparency
function! WriteRoom()
   if has("gui_running")
      if g:writeroom == 0
         let g:writeroom = 1
         set columns=80
         set fullscreen
         set linebreak
         set nocursorline
         set nolist
         set nonumber
         set noshowmode
         set rulerformat=%{strftime('%b %e %I:%M %p')}
         set transparency=0
         hi NonText guifg=bg
      else
         let g:writeroom = 0
         set cursorline
         set list
         set nofullscreen
         set nolinebreak
         set number
         set rulerformat=
         set showmode
         let &transparency=g:transparency
         hi clear
      endif
   endif
endfunction
```

This creates a function that you can execute to put MacVim into WriteRoom mode. If you don't want the clock display then you can comment out the lines about rulerformat. Personally, I like to keep track of time when I'm in fullscreen mode. You can also change the lines and columns to best fit your screen size. Then, you can map a shortcut to execute the function. I use `gw` for normal mode and `\w` for insert mode.

```
nmap gw :exe WriteRoom()<cr>
imap <leader>w <esc>:exe WriteRoom()<cr>i
```

It's pretty easy to make vim look however you want. If you happened to have some secret passion for notepad then it wouldn't be difficult to make vim look that way either.
