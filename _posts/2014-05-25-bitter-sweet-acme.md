---
layout: post
title: Bitter Sweet Acme
summary: The first time someone mentioned Acme, I immediately thought of The Road Runner show. Anvils, bombs, rockets all made by Acme. If I remember well anything Wile E. Coyote bought,it was from the Acme Corporation. Acme meaning the peak, zenith or prime. So when Rob Pike had to name his editor, which did "everything" Acme was the perfect choice.
---

The first time someone mentioned Acme, I immediately thought of The Road Runner show. Anvils, bombs, rockets all made by Acme. If I remember well anything Wile E. Coyote bought,it was from the Acme Corporation. Acme meaning the peak, zenith or prime. So when Rob Pike had to name his editor, which did "everything" Acme was the perfect choice.


> When I started working on Acme, I had a pretty strong idea about what it would be and what it would look like, but I didn't have a name yet. As I usually did at the time, on Friday night I went to Times Square for Movie Night. Penn Jillette was there, and I told him I needed a name for my new project.

> "What does it do?" he asked.

> "Umm... Everything." I said.

> "Acme," said Penn, and laughed.

> [Rob Pike](http://research.swtch.com/acme)

Acme has not gotten the popularity of Emacs or Vim. It is probably because it is counter to what people think an editor is capable of doing. These are a few features that I used to think an editor should be good at:

- have complex key-bindings to navigate to any part of the file, modify text 
- be able to completely use the keyboard, as every one knows that using the mouse is counter productive
- ability to extend it with some language, even if it means ripping your heart of while using it
- customize the look and feel to my needs
- have great syntax highlighting


Acme does none of it, though it allows you to **extend with any language of your choice**. It is absolutely minimal. I remember our company's designer almost instantly said it looks ugly. Well that's what I thought at first. But the colour choices in the editor are well thought. The colours are picked using the triad colour scheme of the base background colour. The background causes the least strain to the eye on prolonged usage. Whether it was intentionally or out of randomness the colours are almost perfect. There is no way to change the colours but by editing the code. 

The few key bindings it provides are:

- ctrl + f: tries to auto complete a path, something like tab would do in a bash shell.
- ctrl +w: deletes the previous word
- Esc: selects the last typed characters
- ctrl + u: deletes to the start of the line
- ctrl + a: moves the cursor to beginning of the line
- ctrl + e: moves the cursor to the end of the line
- ctrl + i: inserts a tab
- ctrl + h: deletes a character
- ctrl + j: break the line at the cursor

I have not tested these key-bindings in any other system so I'm not sure if it is the OS which is doing parts of it. 

It has no syntax highlighting nor does it have line numbers. It uses the mouse extensively. The fonts almost look terrible. You just **cannot** move between lines using the up and down arrow keys. So one might ask why did I leave the comfort of Vim to use this for the past one month? Because it could do, as Rob Pike put it, "Umm... Everything."

Using Acme as my primary editor for the past month has taught me that simplicity and minimalism is everything. The jarring colours of my colour scheme does not come in the way while I program. I do not spend time trying to change the green colour for keywords. It has no configuration files, so one less file to maintain. I do not spend hours on the :help page trying to figure out the right key combination to do x or y. I feel comfortable that I do not need to leave the editor to execute a command in the shell. Everything is right here in my editor. In fact it feels like an IDE built completely out of UNIX.

**It uses the mouse, and it is a good thing.**

Most of your work is done using the mouse. [Jesper L. Andersen](http://jlouisramblings.blogspot.in/2013/04/acme-as-editor_20.html) gave a wonderful description of the mouse usage:

> In a moded editor like vim, you are usually either in command mode for cursor movement or in insert mode for entering text. To understand acme, it is the same, either you have a hand on your mouse and are doing commands, or you are inserting text into the buffer at some place.

Copy, paste, cut is done using the mouse. Unlike the usual GUI tools where you right click to get a menu to cut+copy+paste Acme uses mouse chords. You select the text using the left button, while still pressing the button you press the middle button and that does a cut. Pressing the left button and the right button in succession pastes the text. Left+middle+right does a copy. It seems a bit weird to start of with but chords become amazing the more you use it.

The middle button executes selected text or the word under the cursor. Thus middle clicking `make` executes make and the output is pasted into a +Errors buffer. If the command spewed out errors right clicking on a `src/hello/hello.go:34` opens the hello.go file and moves the cursor to the 34th line. The right click instructs Acme to locate or acquire the file search for a string or even open a link in your web browser. You can also sweep using the appropriate button to avoid selecting and clicking. Right click on acme(1) and it opens the man page. All this is done through what the authors call plumbing (which comes from Plan9 OS). 

Instead of developing tools to search files in project folder the authors decided it would be best if existing tools served the purpose. Executing `grep -rn "func hello" *.go"` brings up a +Errors buffer with the output of grep which you can right click to open the required file. Acme allows you to extend it using any command in your shell PATH. With principles founded in the Plan9 OS Acme exports everything using a file system. So if you want to edit the first buffer's tag you can write into the /mnt/acme/1/tag. 

There are a few tricks I learnt over the past month which might be useful to a few. Here they are:

- To find which line number you are on execute Edit =
- Right clicking on :34 takes you to the 34th line of the buffer
- Middle+Left button on a command executes the previously selected text as an argument. I keep a separate buffer with commands that I use in several buffers. One such is gofmt. Selecting `,|gofmt $%` and executing Edit formats my go code. 
- `:/foobar` - searches backwards
- Executing Edit with arguments: 
    - `,` selects the whole file
    - `#0` takes you to the top of the file
    - `<range>d`  deletes text in range
    - `s/regex/text/[g]`  replaces regex with text 
    - `<range>m a1` moves range to after a1
    - `<range>t a1`  copies range to after a1
    
- Acme takes a few arguments:
    - `-a` does auto indent. Export variable `tabstop` to specify the width of a tab.
    - `-f` specifies the font. It can use the OS's fonts. To use Inconsolata you can pass -f /mnt/font/Inconsolata/12a/font. The a in 12a sets antialias.
    - with `-F` you can specify another fixed font. You can execute Font to switch between fonts

- You can pass a file name as an argument to Dump. Use it to store various sessions. 

Russ Cox has made a wonderful introductory [video](http://research.swtch.com/acme). That should be your start point.

Acme has taught me to leave all that is unnecessary and concentrate on the code that I write using the tools provided by the OS. It takes the "Everything is a file" to a whole new level. It is the Zen of all Editors.
