---
date: '2012-09-25 01:25:50'
layout: post
slug: using-mutt-with-offlineimap-and-vim
title: Using mutt with offlineimap and vim
categories:
- tech
tags:
- mutt
- vim
- google
- productivity
- unix
- offlineimap
---

My [brother][caleb] and I can be pretty geeky. We like trying out new unix tools and informing each other on them. I'm proud to say I've helped him take the plunge into [vim][], my tool of choice. He was an early adopter of [mutt][] in his command line walk, and he helped persuade me of its benefits. I was pretty reluctant at first. I had installed it previously and tried to configure it a bit, but it's fairly difficult to pick up at first. The configuration takes some time and it isn't a seemless integration for a former vim user. I was also pretty fast and comfortable with web-based gmail. Ever since they added the keyboard shortcuts (press ? to view them) my productivity workflow became much more efficient in gmail, so I didn't have much reason to switch to mutt. I also discovered [QuickCursor][], which allowed me to use graphical vim to edit my emails.

However, as my trip down the command line rabbit hole progresses I have found it useful to have more than one way of doing things. Similarly, once you get used to unlimited customization you become spoiled and want it everywhere. It irks me now when I use web-based or proprietary desktop software and I am unable to tweak it to my liking. Although the gmail keyboard shortcuts are an upgrade, they don't all make sense to me. You can change them with a lab add-on, but I don't think you can use key modifiers or add custom commands. I'm also a believer in having control of my information. A big reason I moved away from iTunes to [mpd and vimpc][music] was because I wanted to own what I purchased. Similarly, I wanted the assurance of having control over my email. If my account ever got hacked and they deleted all my emails I'd lose a lot of valuable information and memories.

All that being said, mutt still takes quite a bit of customization and learning. I thought this post might be useful for a vim user who is considering making the switch to mutt, since I have tried to make mutt look and act as much like vim and gmail as possible. I've also picked up a lot of useful tools along the way that I will discuss.

## offlineimap

One of the big draws to mutt was [offlineimap][], which allows you to sync an IMAP account with the [MailDir][] email format that mutt reads. You can set it to update whenever new mail is detected by IMAP so that you always have the most current mail. Not only is this awesome because it saves a local copy of your email, but it also saves a lot of time in checking your email. Since it syncs in the background and the email is local, when you open mutt it reads your email instantaneously. There is no waiting for gmail to load or for mutt to connect to the IMAP server. It's just there. That is one of my favorite things about checking my email with mutt.

My `~/.offlineimaprc` looks like [this](http://connermcd.com/paste/213158091912.html). You'll notice the `idlefolders` option, which is what allows offlineimap to check for new mail detected by IMAP. You'll also see the `autorefresh = 10`, which means that offlineimap does a full sync every 10 minutes. It syncs to a folder called `~/.mail` which is set to be read in my mutt configuration. Make sure you download the newest source code and compile it yourself to get all the latest features and bugfixes.

Occasionally I want to run a full offlineimap update without waiting the whole ten minutes. To accomplish this I wrote a little [mailrun script][mailrun] that will suspend the current waiting offlineimap process, run a single full update, and restart the process. I bind this to a key in my mutt configuration like this:

```
macro index,pager,attach gra "!sh ~/.mutt/mailrun.sh<enter>" "Refresh offlineimap"
```

## goobook

Another lifesaving utility for gmail integration into mutt is [goobook][]. I would not be still be using mutt if it weren't for goobook. I love google contacts and rely heavily on it. I'm an android user, so I loved the ability of being able to edit a contact and add an email address on the go. Then when I get home and want to gmail that person it just magically appears in the `To:` field when I start typing their name. I wasn't about to switch to a new email client that didn't have this feature, which is why goobook saves the day. It lets you query your google contacts and groups and autocomplete them. It has a very simple setup and integrates with mutt nicely. If there are more than one possibilities for autocompletion then it creates a pleasant selection menu with the options. If you want to add someone who sent you an email to your contacts, you can accomplish this with an easy goobook binding. Just use it; it's awesome. I use these two lines in my mutt configuration for goobook:

```
set query_command = "goobook query '%s'"
macro index,pager gb "<pipe-message>goobook add<enter><pipe-message>goobook reload<enter>" "add address to Google contacts"
```

## notmuch

If I was going to move away from gmail's web interface completely, I quickly realized how much I would miss it's powerful search functionality. I needed a way to search through my email and to do it well. I haven't explored all the dark crevices of [notmuch][] yet, but for now it meets my basic search function requirements. It allows filtering for attachments, to, from, etc. It has been a little slower than gmail's search bar, but it's not too painful. There are also [some things][notspeed] you can do to speed it up that I haven't tried yet. I have two bindings for notmuch in my mutt configuration:

```
# performs a notmuch query, showing only the results
macro index Z "<enter-command>unset wait_key<enter><shell-escape>read -p 'notmuch query: ' x; echo \$x >~/.cache/mutt_terms<enter><limit>~i \"\`notmuch search --output=messages \$(cat ~/.cache/mutt_terms) | head -n 600 | perl -le '@a=<>;chomp@a;s/\^id:// for@a;$,=\"|\";print@a'\`\"<enter>" "show only messages matching a notmuch pattern"
# 'A' shows all messages again (supersedes default <alias> binding)
macro index A "<limit>all\n" "show all messages (undo limit)"
```

## urlview

It becomes necessary to be able to quickly access links in emails you're reading. There's more than one way to accomplish this, and I'm not sure if I'm satisfied with the one I've adopted. However, it seems to work for now. Just install urlview with your package manager and then put this in your mutt configuration.

```
macro index,pager,attach,compose go "\
<enter-command> set my_pipe_decode=~4~pipe_decode pipe_decode<Enter>\
<pipe-message> urlview<Enter>\
<enter-command> set pipe_decode=~4~my_pipe_decode; unset my_pipe_decode<Enter>" \
"call urlview to extract URLs out of a message"
```

## gmail folders

Gmail uses separate IMAP folders for archiving mail, starred mail, sent mail, trash, and the inbox, so you need to set up mutt to behave this way. These folders are synced down by my offlineimap configuration that was previously discussed, but you need to set up a way to move between them in mutt. I do this with bindings based off of gmail's shortcuts:

```
macro index,pager,attach gi "<change-folder>=INBOX<enter>" "Go to inbox"
macro index,pager,attach ga "<change-folder>=[Gmail].All Mail<enter>" "Go to all mail"
macro index,pager,attach gs "<change-folder>=[Gmail].Sent Mail<enter>" "Go to sent mail"
macro index,pager,attach gd "<change-folder>=[Gmail].Drafts<enter>" "Go to drafts"
macro index,pager,attach g* "<change-folder>=[Gmail].Starred<enter>" "Go to starred"
macro index,pager,attach gt "<change-folder>=[Gmail].Trash<enter>" "Go to trash"
```

You also need a way to move mail from one folder to the other. Mutt handles some of these options automatically if you set your mbox, and postpone folders. I set these bindings for archiving, deleting, and starring messages:

```
macro index,pager a "<save-message>=[Gmail].All Mail<enter><enter><sync-mailbox>" "Archive"
macro index,pager d "<save-message>=[Gmail].Trash<enter><enter><sync-mailbox>" "Trash"
macro index,pager * "<save-message>=[Gmail].Starred<enter><enter><sync-mailbox>" "Star"
```

## multiple accounts

Adding to the complexity of moving away from gmail is the fact that I have more than one email account. Using gmail makes this a lot easier since the mail from my other accounts comes into my gmail with a label anyway. The only thing I really need to change for other accounts is what account I use to send the mail (the SMTP settings). To do this I made a `~/.mutt/accounts` directory with a file for each of my accounts. I use mutt keybindings to source that file when I want to change my account. For example:

```
macro index,pager,attach,compose gfs "<enter-command> source ~/.mutt/accounts/school<Enter><enter-command> my_hdr From: Conner McDaniel <email@school.edu><Enter><change-folder>=INBOX<Enter>" "School"
macro compose gfs "<esc>f\CuConner McDaniel <email@school.edu><enter>"
```

There's probably a way to do this automatically with hooks instead of using a keybinding, but I haven't taken the time to figure it out yet.

## other settings

To make mutt behave more like vim I use a host of [keybindings](http://connermcd.com/paste/005650092512.html) and [options](http://connermcd.com/paste/012839092512.html
). You'll notice in that second file that I reference a mailcap file on line 26. The mailcap file is extremely useful. You can use it to view HTML emails using lynx or pandoc.

```
# HTML
# text/html; lynx -stdin -dump -force_html ; copiousoutput
text/html; pandoc -f html -t markdown; copiousoutput
```

I use this in my personal mailcap file to read HTML emails. For every other mimetype I reference a [script][], which I modified a little to convert certain filetypes into a PDF with my [any2pdf][] script. This way if someone sends me a .docx and I just want to browse it without downloading it I can hit enter on the attachment to open it as a PDF without ever downloading it -- another very useful feature.

You can set up your `~/.vimrc` with some autocommands for mail filetypes to make mutt specifications. I turn certain paragraph formatting options on and put spell checking on. I usually write with my paragraphs wrapping which makes for long lines, so I also set my `synmaxcol` to unlimited.

```
au FileType mail setl spell fo=wantq1 smc=0
```

I'm still getting the hang of mutt and have more to learn. I'm sure I'll have updates to add at a later date, but this setup has been working pretty well for me. Let me know in a comment or email if you need clarification on something because it can be somewhat convoluted getting yourself set up.

   [caleb]: http://wcm1.web.rice.edu/
   [vim]: http://www.vim.org/
   [mutt]: http://www.mutt.org/
   [QuickCursor]: http://connermcd.com/blog/2011/11/03/using-vim-anywhere-with-quickcursor/
   [music]: http://connermcd.com/blog/2012/09/07/the-virtues-of-vimpc/
   [offlineimap]: http://offlineimap.org/
   [Maildir]: http://en.wikipedia.org/wiki/Maildir
   [mailrun]: http://connermcd.com/paste/083800092512.html
   [goobook]: http://pypi.python.org/pypi/goobook/1.4alpha4
   [notmuch]: http://notmuchmail.org/
   [notspeed]: http://notmuchmail.org/performance/
   [script]: https://gist.github.com/2942855
   [any2pdf]: http://connermcd.com/blog/2011/11/03/using-vim-anywhere-with-quickcursor/
