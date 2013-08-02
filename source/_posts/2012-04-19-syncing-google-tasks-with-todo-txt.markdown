---
date: '2012-04-19 20:01:37'
layout: post
slug: syncing-google-tasks-with-todo-txt
status: publish
title: Syncing Google tasks with Todo.txt
wordpress_id: '1380'
categories:
- tech
tags:
- bash
- google
- productivity
- todotxt
- unix
---

I use the [Gmail](https://accounts.google.com/SignUp?service=mail&continue=http%3A%2F%2Fmail.google.com%2Fmail%2Fe-11-b2c8e95d0c9cadf4d73c30ebee555-0902a9504a36824ab8103148af536a314bb03002) web-based email client to manage my mail because of its extensive features, HTML display, and helpful shortcuts. One day, as I was going through said shortcuts to see if there were any that I might profit from, I noticed the `T` command, which adds the current email to your [Google Tasks](https://mail.google.com/mail/help/tasks/*). I thought that was a pretty spiffy idea since so many times I have an email that needs my action but I can't act on it at the moment. I also archive everything to keep a clean inbox, so I'd rather have emails I need to devote a significant amount of time to on my todo list. The `T` command makes that very convenient, but the problem was that I use [Todo.txt](http://todotxt.com/), not Google Tasks.
Todo.txt is extremely quick and simple. It stores all of your todos in one text file and works all its magic with just one shell script. There are also iPhone and Android mobile apps that will allow you to access these todos on the go through syncing with [Dropbox](https://www.dropbox.com/). I use [Dterm](http://decimus.net/DTerm) for quick and easy shell access to modify my todos. I also use [GeekTool](http://projects.tynsoe.org/en/geektool/) to display available todos right on my desktop so I won't forget them. My GeekTool configuration looks something like this:

```
if [ `cat /Users/connermcd/Dropbox/Todo/todo.txt | wc -l` -gt 0 ]; then
   echo "Todo:"
   cat -n /Users/connermcd/Dropbox/Todo/todo.txt
fi
```

This checks to see if there's anything in the file, and if there is it prints it onto the Desktop. I set this to refresh every 10s since it takes up little to none of my processor's time. I then stumbled upon [Todo.txt plugins](https://github.com/ginatrapani/todo.txt-cli/wiki/Todo.sh-Add-on-Directory) which included a Google Tasks add-on. You will need to get an API key and follow the simple setup instructions provided on the project page. I additionally changed a few things to get it working a little smoother which can be found [here](https://github.com/connermcd/todo.txt-cli/blob/master/.todo.actions.d/google). This will allow you to push and pull changes from your todos. You might want to check and make sure this works before proceeding. Then I simply made a script and set up a crontab to do this automatically. First, make the script look like this:

```
#!/bin/bash
/usr/local/bin/t google push && /usr/local/bin/t google pull
```

Then edit the crontab by typing `crontab -e` and make it look like this:    

```
MAILTO=""
*/5 * * * * /path/to/google_sync.sh
```

The `*/5` means every five minutes but you can change that to your liking. Now your tasks and todos should be syncing automatically and you can use Gmail's `T` command to add to your todos!
