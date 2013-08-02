---
date: '2012-05-20 23:28:13'
layout: post
slug: pandoc-table-editing-in-vim
status: publish
title: Pandoc table editing in vim
wordpress_id: '1434'
categories:
- tech
tags:
- bash
- markdown
- pandoc
- productivity
- unix
- vim
---

I've been itching for a way to get more efficient at creating pandoc tables ever since I started writing my notes in pandoc. Perhaps the only thing I've ever been jealous of [emacs](http://www.gnu.org/software/emacs/) about is a [video I saw](http://youtu.be/EQAd41VAXWo) using it's [orgtable](http://www.gnu.org/software/emacs/manual/html_node/org/Built_002din-table-editor.html) mode. I haven't quite adapted vim to work as emacs shows in this video. I'm convinced that it's possible but also believe that the spreadsheet functionality shown is overkill. I don't need my tables to do any math anyway; I just need them to be fast and seamless. To accomplish this, I turned to [tabular](https://github.com/godlygeek/tabular).
I originally got the idea while watching [a vimcast](http://vimcasts.org/episodes/aligning-text-with-tabular-vim/) on tabular that seemed to be behaving similarly to the emacs video. It uses [a gist](https://gist.github.com/287147) written by [Tim Pope](https://github.com/tpope) that executes :Tabularize every time you enter a pipe symbol. The code is provided in the show notes of the video, so you can easily copy that to your .vimrc. You can use this create a basic table structure dynamically, which ends up looking something like this:

```
| Fruit  | Amount | Price | Total |
| Apple  | 2      | $2.00 | $4.00 |
| Banana | 3      | $1.00 | $3.00 |
| Kiwi   | 5      | $0.50 | $2.50 |
```

Well, that's nice and all, but this is not a pandoc table. I wrote a simple (probably imperfect) function to convert this into a standard pandoc table:

```
Fruit   Amount  Price  Total
------  ------  -----  -----
Apple   2       $2.00  $4.00
Banana  3       $1.00  $3.00
Kiwi    5       $0.50  $2.50
```

It works by visually selecting the lines and executing :Tabularize one last time in case there is any remaining misalignment.

```
vnoremap <leader>t :call <SID>table()<cr>
function! s:table() range
   exe "'<,'>Tab /|"
   let hsepline= substitute(getline("."),'[^|]','-','g')
   exe "norm! o" .  hsepline
   exe "'<,'>s/-|/ |/g"
   exe "'<,'>s/|-/| /g"
   exe "'<,'>s/^| \\|\\s*|$\\||//g"
endfunction
```

There is another type of pandoc table, called a grid table. You can easily convert the markdown table into a grid table using pandoc itself like this:

```
command! -range=% Rst :'<,'>!pandoc -f markdown -t rst
```

Just select the pandoc table and run :Rst to convert it into a grid table like this:

```
+----------+----------+---------+---------+
| Fruit    | Amount   | Price   | Total   |
+==========+==========+=========+=========+
| Apple    | 2        | $2.00   | $4.00   |
+----------+----------+---------+---------+
| Banana   | 3        | $1.00   | $3.00   |
+----------+----------+---------+---------+
| Kiwi     | 5        | $0.50   | $2.50   |
+----------+----------+---------+---------+
```
