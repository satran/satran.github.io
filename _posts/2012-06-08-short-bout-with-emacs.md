---
layout: post
title: My short bout with Emacs and why I chose to stick with Vim.
summary: Ever since I came across Linux and UNIX I had been told about two great editors- Emacs and vi. Toying around Linux I came across vi more frequently. Many articles had me typing commands in bash like 
---

This is not to kindle the flame wars of Emacs and Vim. This is just my experience with Emacs.

Ever since I came across Linux and UNIX I had been told about two great editors: Emacs and vi(I'm going to use vi for Vim throughout the article.) Toying around Linux I came across vi more frequently. Many articles had me typing commands in bash like 

    vi /etc/sysconfig/network-scripts/ifcfg-eth0

I had to press `i` to start typing and then `Esc` and a `:wq` to save and quit! From the Windows' world of notepad it all seemed weird in the beginning. But it now seems to be the right way to edit files (I even have my zsh configured with vi bindings.) I have been using vi for more than 6 years now, and in the past few years became a lot more productive with it. I have my configurations hosted on [git](https://github.com/satyajitranjeev/Dotvim) so I can easily clone my setup in various machines. I have my favourite [plugins](https://github.com/satyajitranjeev/Dotvim/tree/master/bundle) and key bindings to make editing very comfortable. Why, I have even written my own plugin. So why did I want to try Emacs? 

My experience with creating a plugin for vi had me toying around with VimScript <sup>1</sup> . Looking on the "greener" Emacs side I saw Lisp. I had just started learning Lisp and the idea of tweaking Emacs with Lisp drew me to Emacs like a wasp to a flame.

The "greener" side:
- Emacs uses Lisp (rather elisp)
- Some times modal editing could get uncomfortable (which I will explain later)
- Executing programs with C-c C-c
- M-x shell
- M-x python-shell
- I wanted something new to toy around with

With these benefits I dug into Emacs. I personalized it: got my key bindings, plugins, color-theme (boy did I have a tough time getting this one work) and a few init.el customizations. I tried my best not to use vi.

I loved the fact I could use C-c C-c and test my Python programs right away. With the pony-mode for Django projects I could run the server with a few keystrokes and run `manage.py` commands too. And moving into a shell was as simple as M-x shell and typing a few commands. One annoying thing with vi was that I had to leave home position to reach for the arrow keys or go to command mode to move one character to the right or left in the insert mode. C-f was just brilliant. Dired, scratch buffer, debugger, to name a few were the good things.

But as I constantly edited I stumbled across things I missed in vi: 
- A plugin, [Command-T](https://github.com/wincent/Command-T), very similar to that of Textmate's find in project was something I missed the most. Even though dired was good finding files using the Command-T plugin was extremely convenient. I tried to find similar plugins in Emacs but nothing was close enough.
- `df(` moves the character to the first `(` in the line. I just could not find an alternative for this in Emacs. `M-z (` deletes till the first `(` but does not with navigation.
- Jumping to a line is just `Esc:20`.
- Repeating commands just needs a prefix of the number unlike `C-x <number> <other-commands>`.
- Starting vi is extremely fast, Emacs took 7 seconds longer. And in the terminal vi is just blazing fast.
- Using rope for python takes more time to jump to a definition in Emacs.
- Even though M-x shell sounded cool I just could not get the completion work for M-x shell or ipython work. And I realized I am breaking away from the UNIX principle of grouping small programs to do tasks. I can always `Ctrl-z` from vi perform tasks in my shell and return with `fg`.


I believe the main reason was I had started to grok vi and any other thing seemed alien. Had I started with Emacs before vi I probably would have titled this "my short bout with vi and why I chose to stick with Emacs". Emacs is a great piece of software and kudos to all the great hackers using it. 
  
  
Just a screenshot.
![Screenshot Emacs](/images/others/emacs.png "Just a screenshot.")
  
   
<sub>1. Eventually I wrote the plugin with Python.</sub>
