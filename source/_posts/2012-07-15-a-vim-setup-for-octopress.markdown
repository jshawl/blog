---
date: 2012-07-15 17:01:20
layout: post
slug: a-vim-setup-for-octopress
title: A vim setup for octopress
categories:
- tech
tags:
- wordpress
- vim
- ruby
- octopress
---

There's been plenty of posts out there discussing the pros and cons of [octopress][] and other static site generators, so I'm not going to add to the list. I will say that from my personal experience the transition was relatively smooth and that octopress happened to have the necessary features, plugins, and community I needed to get the website I wanted. This certainly may not be the case for everyone, but I am pleased with the overall result so far. Octopress probably does require a bit of web development experience, which I'm fortunate to have. For users without that knowledge base, wordpress is very friendly. However, my needs in a personal webpage are simplistic, and [wordpress][] is just a little too much overkill. It has also become rather mainstream and uses a lot of PHP, which makes it a potential security threat -- especially with a lot of (often shady) plugins. I enjoyed working with [vimrepress][], but since I'm moving away from wordpress, I won't be [developing on it][wpdev] anymore. I did learn something about python-based vim plugins from the experience though.

I wanted a similar vim setup for my new octopress blog. I read [another post][post] belaboring this as a lacking feature that ultimately moved them back to wordpress. I was confused by that, since making a decent workflow in octopress is not all that difficult. Here's the steps I took:

```
nnoremap 'bn :NewPost 
command! -nargs=1 NewPost call NewPost("<args>")
fun! NewPost(args)
   let file = "/web/octopress/source/_posts/" . strftime("%Y-%m-%d") . "-" . tolower(substitute(a:args, " ", "-", "g")) . ".markdown"
   exe "e!" . file
   let g:post_title = a:args
endfun

nnoremap 'bs :SavePost 
command! -nargs=1 SavePost call SavePost("<args>")
fun! SavePost(args)
   let file = "/web/octopress/source/_posts/" . strftime("%Y-%m-%d") . "-" . tolower(substitute(a:args, " ", "-", "g")) . ".markdown"
   exe "w!" . file
   let g:post_title = a:args
endfun
```

The `:NewPost` command will allow you to quickly make a new file in the appropriate directory with the appropriate name. The `:SavePost` command does essentially the same thing except that it uses the buffer you're currently working with instead of making a new one. There might be a better approach than this, but this is just my first go at a solution. Both of the functions set a variable, `g:post_title`, which I then use in a [snipmate][] snippet file like this:

```
snippet b
	---
	date: `strftime("%Y-%m-%d %T")`
	layout: post
	slug: `tolower(substitute(g:post_title, " ", "-", "g"))`
	title: `g:post_title`
	categories:
	- ${1}
	---
	
	${2}
```

That way I can press `ib<Tab>` in the new file to get the appropriate front matter. The next thing I wanted was tag and category completion like vimrepress had, so I solved that using these in my ~/.vimrc:

```
au BufNewFile,BufRead /web/octopress/source/_posts/*.markdown setl completefunc=TagComplete | cd /web/octopress/source
fun! TagComplete(findstart, base)
  if a:findstart
    " locate the start of the word
    let line = getline('.')
    let start = col('.') - 1
    while start > 0 && line[start - 1] =~ '\a'
      let start -= 1
    endwhile
    return start
  else
    let tags = split(system("ls /web/octopress/public/blog/tags"), "\n")
    let cats = split(system("ls /web/octopress/public/blog/categories"), "\n")
    return tags + cats
  endif
endfun
```

You'll have to change the appropriate directories of course. This allows you to use `<C-x><C-u>` for tag and category completion and changes the directory automatically when you use the `:NewPost` command. I might modify these some in the future and update this post, but for now this solution is working for me.

   [post]: http://www.kevindangoor.com/2012/03/wordpress-to-octopress-and-back/
   [octopress]: http://octopress.org/
   [wordpress]: http://wordpress.org/download/
   [vimrepress]: https://github.com/connermcd/VimRepress
   [wpdev]: http://connermcd.com/blog/2011/05/04/blogging-with-wordpress-vim-and-markdown/
   [snipmate]: https://github.com/msanders/snipmate.vim
