---
layout: post
title: Atom - A hackable text editor for the 21st Century. WTF Github?
summary: Why are people desperately trying to make editors that behave the same way. Glorifying it is built using web technologies does not mean its different or better than the hundreds of editor available.
---

Why are people desperately trying to make editors that behave the same way. Glorifying it is built using web technologies does not mean its different or better than the hundreds of editors available. There are over 100 editors mentioned in Wikipedia's [List of Text Editors](http://en.wikipedia.org/wiki/List_of_text_editors). All provide some basic text editing facilities. Of course there are the likes of Emacs and Vim which go beyond "basic usage". 

What is so appalling is that there is a huge hype about Atom. Is it just because the whole editor is made using Web technologies? Or is it the node.js integration? JavaScript is a terrible language. A quick search on its quirks gives you its nature. The sad part is that it is the only language that is available on the web browser. Now here comes a bunch of blokes who want to bring it into the editor too? Haven't we had enough of JavaScript yet?

Lets talk about plugins. Plugins are ways in which the editor interacts with the OS. It is not a way you replicate the features the OS provides. It gives you the ability to adjust the editor to your needs. It provides ways to interact with API's in the open web. The dream would be to write a plugin for one editor and be able to use it many others.

Various editors either created new languages or used existing to provide a system of plugins. Vim went into creating a language that at the least makes you want to take the keyboard and bang it a hundred times on your head. Emacs provided beauty with LISP. Sublime Text got away with using Python. Now we have Atom which tries to do this using JavaScript. Let the Lord of the Editors condemn the key developer to eternity in JS land. 

Editors generally get the concept of plugins wrong. The only one that I know of that gets it right is Acme. You extend the editor's capability using the commands around you. The OS, at least UNIX variants, provides a brilliant set of tools to do almost everything. You should not be recreating those excellent tools using a pathetic language provided by your editor(such as VimL). `git diff` is quite sufficient. If you want a little more flair use `git diff --color`. Trying to make a plugin which does that does is an overkill. You might as well use an IDE. Providing a catchy "Choose from over 50 thousand in Node's package repository" is pure horse shit. How many of the 50 thousand node.js modules are you like to use in an editor?

Their website claims to have these features out of the box: 

- File system browser
- Fuzzy finder for quickly opening files
- Fast project-wide search and replace
- Multiple cursors and selections
- Multiple panes
- Snippets
- Code folding
- A clean preferences UI
- Import TextMate grammars and themes

Of these what does it provide which others do not have? A clean preferences UI? Thankfully they use TextMate's grammars which would be one rule less to write for a new language.

You might ask me why such a hatred towards Atom. GitHub is quite an influential company and soon we will be having several of its minions running around creating thousands of meaningless plugins. They have not innovated a bit. The time that could have been spend on creating an editor that would have ground breaking ideas like Acme or Light Table they did it in fornicating JavaScript with the desktop.

An editor is a developer's religion, almost. One has endless flame wars and pointless arguments that have lasted over decades. It is the tool that we stare sometimes more than twelve hours a day. It is a personal choice. If you are out there making an editor put some real effort into it. Think what can it provide that other age old Titans cannot. Think about what ecosystem would you create or enhance by creating the editor.


[Havoc Pennington wrote](http://www106.pair.com/rhp/hacking.html):

> Don't start by launching your own project. Lots of people want to write free software, so the first thing they do is scribble some code, slap on the GPL, and release version 0.0.1 alpha. While fun and possibly educational, this is totally unproductive.

There are several editors that are begging for contribution. Put your resources on the ones that are changing the way we code.
