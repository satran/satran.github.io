---
layout: post
title: And God said "Let there be text, and there was text".
summary: 
---

And God said "Let there be text, and there was text". This would be the start of the bible if the historians of UNIX wrote one. `/etc/passwd`, `/var/log/messages`, `~/.bashrc` etc. All these wonderful ways of storing information in a very simple and importantly easily accessible format of file. It was all text. 

In this age we are so concerned about speed and scalability that we forget a lot of what is essential. Sometimes storing my personal finances, a list of my contacts or my task, all it needs is a text file. I can always use `grep` `sed` and `awk` to manipulate them. I can fire up my favourite editor[1] and modify it. I can store my files in my local harddisk, sync it with Dropbox or put them in some remote server that I can access. If one of these services die I always have my text files and not have to worry if I can open them. 

A while back I wanted to create a simple application for my iPhone. All I wanted was to store information as plain text, write small scripts that would generate reports. It turned out to be quite a task. This got me thinking about how we do things in the UNIX world. User details are stored in `/etc/passwd`. Logs, configurations, startup scripts[2] all of them are stored as plain text and I could use any language to manipulate them. And thus started my process of developing [Saola](https://saola.in). 

Saola is something that has come out of a need in the mobile platform. It is a place to store your text. But it does something important where the likes of Evernote or Simplenote fail. It provides a scriptable environment[3]. Your content is stored as plain text[4] with plans to provide a very easy sync to your systems. With JavaScript you can write tools to manipulate your text. You can integrate with external tools by `POST`ing to the script that you have written. 

Even though a lot of work has gone on developing it is still in a very early stage. There are features that we haven't implemented yet, there are things that would definitely break. But this is the beginning of a new era. It is like one said on [HN](https://news.ycombinator.com/item?id=10830587): A note platform for the web 3.0. Give it a shot and let me know what you think. Register at [https://saola.in/#register](https://saola.in/#register).

Here are a few plans that we have in mind:
- Provide a nice sync feature. I really would like to use existing tools like `rsync` or `scp`
- Be able to render various text formats like csv, org, rst etc.
- Make it more like the UNIX filesystem
- More language support, may be a lisp?


[1] Emacs for me and vi for the evil ones ;) 
[2] Sadly systemd is taking it away from me
[3] Currenly JavaScript, as much as I complain about it, it was something that was easy to integrate
[4] UTF-8
 
