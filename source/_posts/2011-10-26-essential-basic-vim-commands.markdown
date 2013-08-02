---
date: '2011-10-26 01:13:41'
layout: post
slug: essential-basic-vim-commands
status: publish
title: Essential, basic vim commands
wordpress_id: '1052'
categories:
- tech
tags:
- bash
- mac
- ubuntu
- vim
---

Learning vim can be a daunting task. When you first open up the editor and start typing it becomes evident that things aren't working the way you're used to. You quickly read a few introductory tutorials that distinguish insert, normal, and command line mode, but the only one that makes any sense to you is insert. So, you use insert mode for a bit but realize there's really nothing about insert mode that's more useful than any other editor you've used. The endless lists of commands and tutorials for the other modes may soon overwhelm you. This tutorial aims to introduce 20 commands that will immediately improve your vim experience. However, I am cheating a little bit. Truthfully there are 29 commands, but the capital letter counterparts to single letter commands generally have similar functions.
## Insertion
### i and I - "insert"
You probably already know that 'i' stands for insert and it puts you into insert mode when you're in normal mode, but you might not know that a capital 'I' will put you into insert mode at the beginning of the line.
### a and A - "append"
The 'a' command stands for append. It also puts you into insert mode except it places the cursor after the character you were on top of in normal mode. 'A' is the opposite of 'I" in that it places the cursor at the end of the line.
### o and O - "open" new line
The 'o' and 'O' commands also put you into insert mode. Lowercase 'o' starts a new line after the one you're on while 'O' creates a new line above the one you're on.
## Movement
I assume that you've already learned that the arrow keys or 'h', 'j', 'k', and 'l' can be used to move around. Here are some other useful movement commands that are essential. All of these commands can be prepended with a number to repeat the motion. So, for example, you could type '5j' to move down 5 lines.
### ^ - start of line
Moves cursor to the beginning of the line. This may not seem intuitive, but the reason this character was chosen is because '^' means beginning of the line in regex. Alternatively you can use '0' so that you don't have to press shift.
### $ - end of line
Moves cursor to the end of the line. Also named for regex. If you have a keyboard with an 'End' key you can use that as an alternative or create your own alternative.
### w - "word"
Moves forward one word including white space.
### b - "beginning"
Moves backwards one word or to the beginning of the current word.
### e - "end"
Moves to the end of the current word.
### t and T - "to"
These move "to" the character you type after them. So if I typed 'tf' while at the beginning of this sentence my cursor would land on the 'i' of 'if'. The opposite of this motion is 'T' which moves backwards "to" the character.
### f and F - "find"
This is similar to 't' but it lands on the character instead of just before it. In general, 'f' is more useful than 't' because it can be repeated.
### ; - find next
Semi-colon is the character that repeats the last 't/T/f/F' command. This works much better with 'f' since 't' will get stuck on the character after using it once. However, if you move past or delete that character you can use semi-colon to repeat the last 't' command.
### , - find previous
Same as semi-colon but in reverse.
### G - line number or end of file
Without a prepended number, 'G' will take you to the end of the file. If you prepend a number, like '12G', then it will take you to line 12.
### gg - beginning of file
Puts cursor at the beginning of the file.
## Commands
### c and C - "change"
The 'c' command takes a motion. This means that after you type 'c' you must then type one of the motion commands. It will delete everything between the cursor and the end of the motion and then put you into insert mode. A common use for this is 'cw' to change the current word. A capital 'C' will delete everything until the end of the line and put you into insert mode.
### d and D - "delete"
The 'd' command takes a motion like the 'c' command but does not put you into insert mode. It also copies whatever you deleted to the main register, so it is very similar to the traditional "cut" command except that what is cut is not put on your system clipboard. A capital 'D' will delete to the end of the line.
### y and Y - "yank"
The 'y' command also takes a motion and will copy the area instead of deleting it. A capital 'Y' or 'yy' alternatively will copy the current line.
### p and P - "paste"
The 'p' command will paste the main register contents collected by 'd' or 'y' after the cursor position. If the register contains whole lines then 'p' will paste those lines after the current line. 'P' does the opposite in that it either pastes before the cursor position or before the current line.
### ZQ - quit
Shortcut to quit the document without saving.
### ZZ - save and quit
Shortcut to save and quit the document.
With some practice you'll find that these commands almost immediately make vim faster than your standard GUI editors like notepad or TextEdit. For example, I can get to a specific location in the file quickly by typing something like '54G3ft' to get to the third occurence of 't' on line 54. These commands can also be used at the terminal. Put `set -o vi` in your ~/.bashrc or ~/.profile, type `source ~/.profile` and then when you press _<Esc>_ on the bash line you can use these commands to quickly edit your bash command!
