---
date: '2011-05-15 20:56:42'
layout: post
slug: using-pandoc-on-mac-osx
status: publish
title: Using pandoc on Mac OSX
wordpress_id: '793'
categories:
- tech
tags:
- mac
- markdown
- pandoc
---

## EDIT:

This post is now for the most part obsolete since there is a [package installer](http://code.google.com/p/pandoc/downloads/list) for pandoc available. However, you may still find the LaTeX information useful.

Sometimes it's useful to convert your Markdown files into other formats. Particularly, PDF is a universal, printable format that's useful to convert to. However, since Markdown has had some struggles becoming standardized, converting it to more common formats isn't always easy. Luckily, [pandoc](http://johnmacfarlane.net/pandoc/index.html) remedies this solution and isn't all that hard to install. However, it does require some dependencies. The easiest way to install pandoc is probably through using Macports, which requires Xcode. You'll also need a basic install of MacTeX to convert to LaTeX and PDF formats.

## Installing Xcode and MacPorts

First, you'll need to install Xcode. If you're not sure whether or not Xcode is already installed you can look in your main HD where OSX is installed and look for a folder named Developer. From the command line you could just type `ls /` and look to see if the word Developer shows. If it's present then Xcode is installed. Xcode comes included on your Mac OSX installation disc distributed with your computer. Just pop in the disc and find the Xcode installation package. Alternatively you can download Xcode from [Apple's website](http://developer.apple.com/technologies/tools/whats-new.html) but you'll have to register as a developer. Be aware, however, that it's large download. Once installed, download the .dmg file for Macports from [their website](http://www.macports.org/install.php) and install the .pkg file within. Now macports should be installed. Open your terminal and run the command `sudo port -v selfupdate` to update the manager. You can now install Macports packages using `sudo port install name-of-package` In our case we'll be installing pandoc, so execute `sudo port install pandoc`

## Installing MacTeX

Now you'll need to install [MacTeX](http://www.tug.org/mactex/2010/), but don't rush ahead just yet. You'll soon notice that the generic MacTeX is approximately a 1.6GB download! That's pretty hefty. Frankly, I didn't feel like waiting around for such a huge package to download for such a small purpose. Instead, you can install the lighter package called [BasicTeX](http://www.tug.org/mactex/2010/morepackages.html), which is only 92MB (that's more like it). Download and install the BasicTeX .pkg file. Finally, for pandoc's markdown2pdf command to work you'll need one additional package. Luckily, BasicTeX includes TeXLive which is a package manager for TeX packages (similar to Macports, which is also a package manager). First, update the package manager with `sudo tlmgr update --self` and then install the required package with `sudo tlmgr install ucs` Now you should be able to use the markdown2pdf command! You may need additional TeX packages for other commands. If so, just use the `sudo tlmgr install name-of-package` command.
