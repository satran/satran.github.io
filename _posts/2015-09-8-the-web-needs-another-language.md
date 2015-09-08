---
layout: post
title: The web needs another language.
summary: I recently had a conversation with a colleague about JavaScript (I cannot bother to call it ECMAScript). He was praising the language and how nodejs is brilliant with the whole Isomorphic pattern. This got me thinking why I despise JavaScript. Was it prejudice? Was it the "Java" in the name? There was something about it that irked the programmer in me. I needed an answer. To this I decided to take Hofstadter's approach...
---

I recently had a conversation with a colleague about JavaScript (I cannot bother to call it ECMAScript). He was praising the language and how nodejs is brilliant with the whole Isomorphic pattern. This got me thinking why I despise JavaScript. Was it prejudice? Was it the "Java" in the name? There was something about it that irked the programmer in me. I needed an answer. To this I decided to take [Hofstadter's approach][1].

---
*Achilles visits his friend the Tortoise*

**Achilles**: My, your screen looks quite drab. Are you still using Emacs?

**Tortoise**: Yes my dear friend. It has been around since the 1970s. It may be not as old as you but it is definitely a joy to use.

**Achilles**: Well I am using this new editor called Atom.

**Tortoise**: That's new. What is so special about it? How is it different from Emacs or (may the hard shell protect me from the flames) vi?

**Achilles**: It is written in JavaScript. The whole thing is actually built on web technologies. It is a built on top of chromium so that the entire editor is built with JavaScript. And you can write plugins using JavaScript.

**Tortoise**: *Interesting!*
(author's note: sarcasm emphasized)

**Achilles**: I know you do not like JavaScript. But the editor is fantastic. It has everything and it has got a fantastic user interface.

**Tortoise**: Well it is not that I hate JavaScript. One can argue that it is not the language to blame but the programmer. There have been wonderful projects created in languages which many thought were un-programmable. Yet Facebook was created with Php, Hadoop was written in Java, Firefox and Chrome were written in C++. If I may quote Bjarne Stroustrup:

> There are only two kinds of languages: the ones people complain about and the ones nobody uses.

JavaScript has its [good parts][2] even though it was [created in 10 days][3]. 

**Achilles**: So why do I hear you complain about it all the time. Just imagine what has happened in the past few years. I can program in an editor that was created using JavaScript with which I use to create wonderful single page client side applications which in turn communicates with a server written completely in JavaScript which communicates with the database server again with JavaScript. It is all JavaScript. The only thing I feel sad is that we have not created an operating system with JavaScript yet.

**Tortoise**: You have summarized my whole problem with JavaScript. Every one looks at it like a hammer. And when you look at it like a hammer every thing looks like a nail. It is bad enough that we are forced to write in JavaScript for the web but now there are people trying to evangelize the need to use it in for server side works as well. 

*The conversation between the two continue for hours as Achilles tries to convince that is a good thing. Finally the Tortoise having had enough opens up Emacs and types: M-x destroy-world-mode*

---

I have no problem with people looking at JavaScript as a hammer. I do not care as long as you don't force me to see it that way. But the Tortoise mentioned an important point - you can program the web with just one language - JavaScript. That is my biggest problem. Its not the language itself but how the web has evolved. It is surprising that no one complains about it more often(*).

The web ought to be more open, providing options where one can create code with the parenthesis of Lisp or cryptic Perl or the beautiful Pythonic spaces or may be even obfuscated C. I want to have the freedom to write in any language of choice. But we are not there, yet.

I don't have an answer. Maybe WebAssembly is the answer. But for now I will try to hate JavaScript with a vengeance :)

---

[*] Yes there is clojurescript and a few others which are still in the nascent stage - sadly they compile to JavaScript!

[1]: https://en.wikipedia.org/wiki/G%C3%B6del,_Escher,_Bach

[2]: http://www.amazon.com/gp/product/0596517742/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0596517742&linkCode=as2&tag=satyaranje-20&linkId=32DY54ZOMHGLAA2P

[3]: https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript

