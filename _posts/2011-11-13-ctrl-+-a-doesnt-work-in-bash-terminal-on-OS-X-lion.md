---
layout: post
title: Ctrl + a doesn't work in Bash Terminal on OS X Lion
---
# [{{ page.title }}]({{ page.url }})

I had this problem for a while and just ignored it for a while till it was unbearable. Well after googling a bit I came across stackoverflows answer. `^A` and `^E` are commands of bash's “emacs mode”. All I had to do was in the terminal type  

    r2d2:~ satyajit$ set -o 

and found out vi was set to on and emacs to off. I edited ~/.bashrc to add:

    set -o emacs

And yes got the key bindings back to `^A` & `^E`.

This got me wondering on the `set - o` to vi mode. I am a HUGE fan of vi. I love the modal editing so why not just use it. In fact it seems better than `^A` and `^E`. Love the vi key bindings.
