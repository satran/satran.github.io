---
layout: post
title: Python repr and str - the difference
---
# [{{ page.title }}]({{ page.url }})

This is usually a question asked in many Python interviews: What is the difference between the `__str__` and `__repr__` methods of a Python object. The same question was asked by one of my colleagues, which got me researching.

In short `__repr__` goal is to be unambigous and `__str__` is to be readable. 

The official Python documentation says `__repr__` is used to [compute the "official" string representation of an object][1] and `__str__` is used to [compute the “informal” string representation of an object][2]. The `print` statement and `str()` built-in function uses `__str__` to display the string representation of the object while the `repr()` built-in function uses `__repr__` to display the object. Using this definition let us take an example to understand what the two methods actually do.

Lets create a datetime object:

    >>> import datetime
    >>> today = datetime.datetime.now()

When I use the built-in function `str()` to display today:

    >>> str(today)
    '2012-03-14 09:21:58.130922'

You can see that the date was displayed as a string in a way that the user can understand the date and time. Now lets see when I use the built-in function `repr()`:

    >>> repr(today)
    'datetime.datetime(2012, 3, 14, 9, 21, 58, 130922)'

You can see that this also returned a string but the string was the "official" representation of a datetime object. What does official mean? Using the "official" string representation I can reconstruct the object:

    >>> eval('datetime.datetime(2012, 3, 14, 9, 21, 58, 130922)')
    datetime.datetime(2012, 3, 14, 9, 21, 58, 130922)

The `eval()` built-in function accepts a string and converts it to a datetime object. 

Most functions while trying to get the string representation use the `__str__` function, if missing uses `__repr__`. Thus in a general every class you code must have a `__repr__` and if you think it would be useful to have a string version of the object, as in the case of `datetime` create a `__str__` function.

A few references:

[Stackoverflow: http://stackoverflow.com/a/2626364/504262](http://stackoverflow.com/a/2626364/504262)

[Python reference for `__repr__`][1]

[Python reference for `__str__`][2]

[1]: http://docs.python.org/reference/datamodel.html#object.__repr__
[2]: http://docs.python.org/reference/datamodel.html#object.__str__


