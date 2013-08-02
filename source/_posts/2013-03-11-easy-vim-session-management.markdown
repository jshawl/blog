---
date: '2013-03-11 10:48:08'
layout: post
slug: easy-vim-session-management
title: Easy vim session management
categories:
- tech
tags:
- vim
- productivity
---

Until recently I haven't really harnessed the power of vim's session management capabilities. It can be a hassle somewhat to always use `:mksession` and `:source`, so I usually just neglect to do it; however, if you're commonly working with large projects then it can be very useful to drop a session file into the root directory and make use of it. To aid me in utilizing this feature I added some customizations to my `~/.vimrc`:

```
command! Mks let g:session = getcwd() <bar> call Mks(g:session)

augroup vimrc
  au!
  au BufRead *.session let g:session = expand('%:p:h') | so % | bd #
  au VimLeave * if exists('g:session') | call Mks(g:session) | endif
augroup end

fun! Mks(path)
    exe "mksession! ".a:path."/".fnamemodify(a:path, ':t').".session"
endfun
```

First, this sets a new custom user command called `:Mks` which will make a session file based on the current working directory. For instance, if `:pwd` is `/home/connermcd/.bin/project/` then this will make a file inside that folder called `project.session`. It also sets a global variable (`g:session`) to the current working directory so that it can save the session here later. In the `augroup` a couple of autocommands are set. The first one (`BufRead`) executes when you open a file with the `.session` extension. This will set the `g:session` variable, source the session file, and delete it from the buffer list. The second one (`VimLeave`) executes when you close vim. If a `g:session` variable is found then it will override the session file with the new information. That's pretty much it!

This works best if you aren't using the `autochdir` option. I find that with it turned off it makes project navigation much more simple. Now when you create a new project just run the `:Mks` command to start session tracking, and when you want to access it later just open the `.session` file with vim.
