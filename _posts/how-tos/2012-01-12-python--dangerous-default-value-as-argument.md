---
layout: post
title: Python - Dangerous default value as argument
---
# [{{ page.title }}]({{ page.url }})

Pylint in my vim constantly showed this error:

     warning| Dangerous default value [] as argument

This usually happened when I used an empty list `[ ]` or empty dict `{ }` as an argument in a function. I always wondered why this should raise a warning. I got my answer in [stackoverflow](http://stackoverflow.com/questions/101268/hidden-features-of-python#113198).

Take this code for example:
    
    >>> def foo(x=[]):
    ...     x.append(1)
    ...     print x
    ... 
    >>> foo()
    [1]
    >>> foo()
    [1, 1]
    >>> foo()
    [1, 1, 1]

As you can see the default value of x changes. A commenter [Jim Dennis](http://stackoverflow.com/users/149076/jim-dennis) explained it pretty well. To quote him:

> As the def statement is executed its arguments are evaluated by the interpreter. This creates (or rebinds) a name to a code object (the suite of the function). However, the default arguments are instantiated as objects at the time of definition. This is true of any time of defaulted object, but only significant (exposing visible semantics) when the object is mutable. There's no way of re-binding that default argument name in the function's closure although it can obviously be over-ridden for any call or the whole function can be re-defined).

The author [Jason Baker](http://stackoverflow.com/users/2147/jason-baker) suggested not using `[ ]` but rather:

    >>> def foo(x=None):
    ...     if x is None:
    ...         x = []
    ...     x.append(1)
    ...     print x
    >>> foo()
    [1]
    >>> foo()
    [1]

