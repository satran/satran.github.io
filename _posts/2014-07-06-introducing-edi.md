---
layout: post
title: Introducing EDI
summary: 
---

![Screenshot EDI](/images/others/edi.png "Introducing EDI")

I've had this thought from the time I tried to settle down on one editor. There was always something that did not quite work for me. Vim worked most of the times and when it didn't I tried to jump ships to Emacs. I gave Sublime Text, Textmate, and a number of others a fair chance. Last I came across Acme. It was brilliant in many ways and terrible in others. I wanted the plumbing and ability to execute commands on the go and have better keybindings and editor features. So I decided to write my own. So here is EDI (pronounced as Eddy).

<iframe width="640" height="480" src="//www.youtube.com/embed/bDlXj4hW0JI" frameborder="0" allowfullscreen></iframe>

It is a web application which runs on port 8312. Written in Go it can be cross compiled on platforms that it supports(not tested on Windows thought). It is in its nascent stage and does not provide features you would see in other editors. 

It has two panes: the **command** and the **editor**. The command pane aspires to be a replacement for your terminal. It cannot currently handle scripts/programs that depend on ncurses or require an input. There is no concept of running jobs in the background, you can run multiple commands at the same time. EDI itself has a few commands: 

- E <file_name> opens a file in the editor pane.
- W saves the edited buffer
- L lists the current buffers open

The plumbing in Acme inspired me to do something similar in EDI. Currently right-clicking on the text in the command pane opens up valid files.


EDI does very little now. But here are a few things that will be added in the next few releases:

- A way to extend the editor in any language of your choice
- Ability to add plumbing rules (or the right-click context rules)
- A better command pane with tab completion
- Multiple connections and peer coding
- A standalone application probably based on XUL/CEF

EDI will always strive to be minimal and lean on the tools that the OS provides or the ones created by its users. I believe Editors and IDEs should always be open sourced. Thus you can find its source here [https://github.com/satran/edi](https://github.com/satran/edi).

I would love to hear your feedback. Comments are disabled on the site now so start a discussion on Hacker News or Reddit.
