---
date: '2012-01-07 21:21:01'
layout: post
slug: drag-items-from-snow-leopard-list-stacks
status: publish
title: Drag items from Snow Leopard list stacks
wordpress_id: '1287'
categories:
- tech
tags:
- bash
- mac
---

In Snow Leopard the Dock has various stack options for folders. You can view folders as a fan, list, grid, or let the Dock decide. I use a mixture of these options for different folders on my Dock. For example, I like having my Dropbox folder in a grid mode that's similar to Finder, but for my Applications folder, which has quite a few items, I use the list mode. The downside to the list mode is that you can't drag and drop items from it. So when I want to delete an application I end up having to right click, open in Finder, sift through all of my applications to find the right one, and then delete it. Today I [stumbled across](http://www.macosxtips.co.uk/index_files/terminal-commands-for-hidden-settings-in-snow-leopard.php]) a hidden Snow Leopard feature that allows you to make list mode work more like grid mode. This allows you to drag and drop items directly out of the list and into the trash. Sub-folders, unfortunately, do not expand, but you can click on them to open a list view of that directory. Simply open up Applications > Utilities > Terminal.app and type

```
defaults write com.apple.dock use-new-list-stack -bool YES
killall Dock
```

then your list stacks will have drag and drop enabled!
