---
date: '2012-05-01 23:55:01'
layout: post
slug: file-encryption-and-password-management
status: publish
title: File encryption and password management
wordpress_id: '1392'
categories:
- tech
tags:
- android
- bash
- gpg
- mac
- security
- unix
- vim
---

I've been meaning to make my setup more secure for sometime. In general, I have held to the logic that I'm not someone important enough to be worried about security threats. I still believe that to be true, but I am in the process of gaining a medical license which will quickly make me a target for various frauds, identity thefts, or general treachery. I'm also doing some HIPAA-compliant research this summer which qualifies as a bona fide excuse to get myself secure instead of studying. I started out by finally getting around to tackling [Gnu Privacy Guard (gpg)](http://www.gnupg.org/), which I've been putting off for some time. Honestly, it's not as complicated as I thought it would be. Start by making a private key for yourself:

```
gpg --gen-key
```

It will ask you a bunch of questions to which you can just hit enter for the defaults mostly. You should enter your real name and email address. It confused me at first, but you actually want people to be able to find your public key. It isn't a security threat. Also, make sure you set a password that you'll remember later because if you lose it whatever you encrypt is gone forever, and it's probably important stuff. You can always change your password later with `gpg --edit-key 'Your Name'`. After all that you're pretty much set to start encrypting or decrypting files, which is pretty shweet.

```
# This encrypts (.pdf → .pdf.gpg)
gpg -e tax_info.pdf

# This decrypts (.pdf.gpg → .pdf)
gpg -o tax_info.pdf -d tax_info.pdf.gpg
```

You can also get someone elses public key and encrypt it so that only they can open it. This is a secure way of emailing important documents around. Vice versa you can export your own key and let other people encrypt stuff under your key. There's also a spiffy [Android app (apg)](http://thialfihar.org/projects/apg/) that allows you to do encryption and decryption on your phone. Now, this is spiffy and all but you'll probably soon see how tedious it can be to encrypt and decrypt things. I generally just make a folder into a tarball and then encrypt that. There's also an awesome [vim plugin](https://github.com/vim-scripts/gnupg) called vim-gnupg that allows you to pop in and out of encrypted files seemlessly with a password. Using this plugin the passwords are only stored in RAM and are not written to swap files or viminfo files.
This got me thinking about other ways I could use this. I have always used strong passwords, and I change them often. However, there's generally a lot of overlap between the web services I use to where one password is used in several places so I can keep my sanity. It would be great if I could keep all my passwords in one place in an encrypted file, but what a hassle to constantly be opening it up and copy/pasting! So, having recently read up a little on [awk](http://en.wikipedia.org/wiki/AWK) and feeling a bit adventurous, I set out to create a nifty password wallet. Basically this allows me to do something like `pass google` on the command line, enter my master password, and get Google's password copied to my clipboard. For extra security, it removes it from the clipboard 10 seconds later so that I don't accidentally paste it somewhere. I set up my configuration like this:

{% raw %}
```
# Google {{{
google password1
}}}
# Facebook {{{
facebook password2
}}}
# Twitter {{{
twitter password3
}}}
```
{% endraw %}

Notice the vim folding markers using `set foldmethod=marker` to help hide the passwords from prying eyes when you open the file. This file is then encrypted and synced using [Dropbox](https://www.dropbox.com/). I installed a nifty tool called [pwgen](http://sourceforge.net/projects/pwgen/) to help me make a bunch of new strong passwords. Once you've opened the password wallet with [vim-gnupg](https://github.com/vim-scripts/gnupg) you can do `:r !pwgen -cn 8` to read a standard 8-character strong password into the file or customize it according to that application's specifications for more security. I did this for all my passwords and changed them using the various services. Then I created a tool to quickly access the wallet as previously stated using this code in my shell's rc file:

```
pass() {
   gpg -q -d ~/wallet.gpg | awk "/^$*/ { printf \$2 }" | pbcopy
   (sleep 10 && echo -n '' | pbcopy) &!
}
```

This decrypts the wallet and pipes it to awk, which finds the specified application and then pipes the password to the clipboard. Then simply paste the password where it needs to go. The last part starts a process separate from the shell that will wait 10 seconds and then empty the clipboard. Now I can update one master password regularly with hefty security while all of my applications have strong passwords! I suppose you could convert this into more of an actual wallet and put keys to credit card numbers or other sensitive information in here. I'm not exactly a security guru, but as I understand it the password will only be stored in the RAM and would be pretty dang difficult to get at. If you do happen to be a security guru and notice something lacking here, please leave a comment or otherwise let me know.
> 

> 
> P.S. This is one of those moments I love vim so much. I stupidly accidentally closed my terminal window without saving this entire post, and a simple :restore saved the day!
> 
> 

