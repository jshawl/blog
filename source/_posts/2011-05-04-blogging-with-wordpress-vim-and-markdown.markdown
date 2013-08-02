---
date: '2011-05-04 21:18:49'
layout: post
slug: blogging-with-wordpress-vim-and-markdown
status: publish
title: Blogging with Wordpress, vim and markdown
wordpress_id: '679'
categories:
- tech
tags:
- markdown
- vim
- wordpress
---

Recently I made a post on converting your Wordpress posts into markdown files. You may be wondering, "What now?" Now that all your posts are on your file system, how do you continue to make Wordpress posts in markdown? Well, you could write your new posts in markdown in a text editor on your local filesystem and then copy paste them into Wordpress using one of the Wordpress markdown plugins ([1](http://wordpress.org/extend/plugins/markdown-on-save/),[2](http://wordpress.org/extend/plugins/markdown-for-wordpress-and-bbpress/)). Personally, I would rather not have to copy and paste and there is no text editor I would rather use than VIM. So, I looked into several options to determine what the best way to go about this would be.

I tried several plugins, but the simplest I found was vimpress. It's features are to the point and effective,and there are also several adaptations of it with different features. One of these adaptations is [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) which adds the features of colorizing the vimpress display, allowing for the upload of files, and supporting the markdown syntax. [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) does require vim-python, so if you're on a mac you'll have to compile MacVim from source.

### Compiling MacVim with Python & Ruby

Compiling can be tricky sometimes, especially since things seem to almost always break with some unforeseen error. I will show you how I accomplished this using OSX 10.6.7 Snow Leopard with Xcode installed. There's a guide for compiling MacVim [here](https://github.com/b4winckler/macvim/wiki/Building). First, download or use git to acquire the source then navigate to the 'src' folder within it. The guide then lists several configuration options that are available for compiling the code, however, you don't need them all and I personally had trouble with _--enable-perlinterp_. Ruby is a useful language that you may want to use for a different plugin later, so I'd go ahead and throw that option in too. I simply used `./configure --enable-rubyinterp --enable-pythoninterp` followed by a `make` This should compile the software and create the .app file. You can then copy the .app file from files/src/MacVim/build/Release/MacVim.app into your /Applications folder and use it as normal.

### Installing VimRepress

Now you'll need to download the files from [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510). They need to be placed within a folder named .vim in your personal directory. To do this you can execute these commands.

```
mkdir ~/.vim
cd ~/.vim
mv ~/Downloads/vimpress* .
unzip vimpress*
```

You'll have to tell [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) the username, password, and URL of your blog, so the next step is to set those options. The easiest way to do this is in your ~/.vimrc file. If you don't already have one then make one and add the [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) configuration variable to it.

```
let VIMPRESS=[{'username':'user', 
               'password':'pass', 
               'blog_url':'http://your-first-blog.com/' 
               }, 
              {'username':'user', 
               'password':'pass', 
               'blog_url':'http://your-second-blog.com/' 
               }]
```

If you download [my fork](https://github.com/connermcd/VimRepress) of the project, you don't need to hardcode your passwords. As you can see, you can use multiple blogs with [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) if needed. If not, then just specify one without a comma after the closing curly brace. You will need to go to your Wordpress and make sure that Settings→Writing→XML-RPC is checked for this to work.

### Using VimRepress with markdown
Python comes pre-installed on Mac. You can check your version with `python --version` Download the [python-markdown](http://pypi.python.org/pypi/Markdown) package, extract it and install it using 

```
python /path/to/package/setup.py install
```

Half the point of this whole effort is to be able to code in the syntax simplicity of markdown. So, first things first, you are going to want some markdown syntax highlighting for VIM. You can download the files you need [here](https://github.com/plasticboy/vim-markdown) and then unzip them into your ~/.vim folder. Now, navigate to the folder that contains all your Wordpress posts in markdown format with VimRepress meta content and create a new, appropriately titled file. From here you can immediately begin writing your post in markdown. Once you're done and ready to preview or publish the post, type the command :MarkDownNewPost and you will enter the [VimRepress](http://www.vim.org/scripts/script.php?script_id=3510) management window. This command will convert the current file from markdown into HTML and add post metadata to the top. In the metadata you can assign categories, tags, and a title. This file does not need to be saved. It's just a way to allow you to edit this data and double check the HTML conversion if you're concerned about it. Once you're ready you can use `:BlogSave draft` or `:BlogSave publish` depending on whether you want to preview or publish. Pretty nifty, huh?

{% youtube nBHBwOns5bE %}
