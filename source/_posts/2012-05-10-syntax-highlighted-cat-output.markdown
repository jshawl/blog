---
date: '2012-05-10 10:32:50'
layout: post
slug: syntax-highlighted-cat-output
status: publish
title: Syntax highlighted cat output
wordpress_id: '1424'
categories:
- tech
tags:
- bash
- python
- unix
---

If you want your cat output to be colorized it's relatively simple. If you already have [python](http://www.python.org/getit/) and [pip](http://www.pip-installer.org/en/latest/installing.html) installed then you're in luck, but if you don't then you'll need them. Then just use `pip install pygments` and you can use `pygmentize script.sh` to get syntax highlighted cat output. I've set an alias in my rc file as `alias pat = 'pygmentize -g'` since I think replacing cat systemically could potentially cause some problems. On my system it looks like this:

![Pygments](/images/colorized_cat_output.png)
