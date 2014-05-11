---
layout: post
title: My thoughts on Go
summary:Though the designers keep emphasising that it is quite different, it reminds me of C in many ways.  It is simple and succinct. The whole language specification fits in a single page html - that says something. I felt comfortable learning the language.
---

I have been programming in Go for a few weeks now and these are my thoughts on it. 

Though the designers keep emphasising that it is quite different, it reminds me of C in many ways.  It is simple and succinct. The whole language specification fits in a [single page html](http://golang.org/ref/spec) - that says something. I felt comfortable learning the language. It was a stark contrast to what happened when I decide to re-learn C++. I say re-learn as many years ago I was taught using Turbo C++. I must say it was quite a challenge: finding the right book to start off with and having to deal with numerous ways just to initialise an object. A quick summary of the language was provided in ["A Tour of Go"](http://tour.golang.org/#1) and [Effective Go](http://golang.org/doc/effective_go.html) to help me get the idiomatic way to start coding. Some say it takes [ten years to learn programming](http://norvig.com/21-days.html) and with a language that doesn't lend itself to doing the same thing in many ways I'm sure in that time I would have achieved something.

I know that there will be lesser arguments of the right style to write a function in Go with the language designers deciding to provide `gofmt`. That ends the discussion of GNU style vs the Linux kernel style. The tools that surround the language are fantastic. With documentation support built in I can happily kick off RST and sphinx (even though there will be folks arguing of its features) out into the closet. Though I cannot call it a test suite but `go test` just works. All these tools including race detector, package installation, profiling and benchmarks are tools that help you concentrate on building your application. Tools that **just work**.

I feel packages and namespaces are done right. Attributes, functions, variables that start with an uppercase letter are exposed publicly. All others are private. Names are simple and should be accessed using the package name. Thus creating a new Tree structure from the tree package is just `tree.New`. Writing packages are also simple. Files start with defining what package they belong to. While creating complex programs very long files can be easily broken down into several files using the same package. Each file can define multiple `init` functions to initialise the package.`init` is called after all the variable declarations in the package have evaluated their initialisers, and those are evaluated only after all the imported packages have been initialised. Which makes init quite powerful.

I believe anyone who has been following Go would agree that it solves most problems of concurrency. Again here it does is with utmost ease with goroutines: call a function concurrently with just `go <function_name>`. Rob Pike gave a wonderful presentation about [concurrency](http://www.youtube.com/watch?v=f6kdp27TYZs). Being one of the designers he does more justice in explaining concurrency.

The standard library is quite sufficient. With the focus on web technologies in the past few years the `http` and `template` packages come in standard. Handling JSON, connecting with databases, basic 2d image manipulation, to name a few, are provided right in the standard library. With UTF-8 built right into the language handling unicode is much simpler.

There are many other features that I feel are worth looking at:


- error handling (yes I do like the error handling. I just can't count the numerous time I have seen `raise` being called in Python code without any custom exception, or even built-in exceptions. It is better to handle exceptions right where the call is made.)
- interface declaration - no explicit declaration that my custom type is an interface, define the methods and it satisfies the interface.
- channels (I'm not talking too much about concurrency and channels as many have done enough justice about them.)
- slices
- `select`ing channels and types
- multiple return values

More than beauty and theoretical soundness Go went for practicality. The face that `range` acts differently for different types just shows that. Having an empty select to construct complex if statements is another example. The fact that they chose to go with practicality will pay off. Even though many are complaining now I believe the language will stand time. 

What ever the designers say not having generics is a bit of a pain. I'm writing more code. I do like the duck-typing I get through interfaces. But at times I just want a better option to `interface{}`. I do lose the advantages of static typing. That being said I would advice my fellow programmers who lament about the fact that there is no generics and have a huge blog post on why Go sucks etc., not to jump into it. Deal with it right in the beginning. You are not going to get generics for a while. Period. Either quit complaining about the lack of features or use another which suits your needs. 

So far I have enjoyed programming in Go. The simplicity made me even adopt Acme as my default editor. As with Acme from the outside people frown at the minimalism but fail to see the completeness it provides with simplicity.
