---
date: '2011-11-03 20:13:57'
layout: post
slug: using-vim-anywhere-with-quickcursor
status: publish
title: Using vim anywhere with QuickCursor
wordpress_id: '1119'
categories:
- tech
tags:
- vim
- mac
---

Once you get addicted to vim it's really a struggle to type with anything else. I gave [vmail](http://danielchoi.com/software/vmail.html) a chance, but it would be extremely difficult for any plugin developer to keep up with the advances of Google. It seems they are constantly coming out with new and wonderful updates that I certainly don't want to miss. Plus, I enjoy the smooth graphical interface that Gmail allows for, and I like to see images when they appear in my e-mails. I mean -- there's a reason I still use a browser, and a lot of e-mails come in HTML format. The issue is that e-mail is one of the main places that I edit text, and that was just a tragedy.

Then I found [QuickCursor](http://www.hogbaysoftware.com/products/quickcursor) from the creators of WriteRoom. [QuickCursor](http://www.hogbaysoftware.com/products/quickcursor) lets you edit any text anywhere with your favorite text editor. So be it Gmail, a textarea, or any area that takes text input and with a quick shortcut you can be using vim to edit it. Once you save and quit it puts your edited text into position and you're done! The idea sounded great to me on first listen until I realized that [QuickCursor](http://www.hogbaysoftware.com/products/quickcursor) costs money and unfortunately it puts an unoptional icon in your menubar. However, there is a way to kill two birds with one stone.

The source code for [QuickCursor](http://www.hogbaysoftware.com/products/quickcursor) is hosted [here](https://github.com/jessegrosjean/quickcursor), and you can download the project for free. This also allows you to modify the source code a bit. Needless menubar icons are a pet peeve of mine, so I set out to solve this problem. If you open up the Xcode project and edit the QCAppDelegate.m file then search for "Status" you'll find a code block about quickCursorStatusItem. Comment out that block of code and search for the last instance of "Status" in the file and comment out that line too. Save and build the project with Command-S and Command-B. You can find the compiled .app file in the ./build/Debug folder of your project. Copy that to your /Applications folder and you're done!

Of course, not having the menubar icon means you can't visually get to the preference pane for [QuickCursor](http://www.hogbaysoftware.com/products/quickcursor); however, if you click on the .app icon in your Applications folder and then press Command-, (with the comma) then the preference pane will appear. This will allow you to change the shortcut key, startup options, and text editor of choice! If you find that you love it then you may want to give the developer some credit by buying him a cup of coffee. 
