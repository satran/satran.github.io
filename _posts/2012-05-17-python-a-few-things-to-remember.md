---
layout: post
title: A few things to remember while coding in Python.
---
# [{{ page.title }}]({{ page.url }})

UPDATE: There has been much discussion in [Hacker News](http://news.ycombinator.com/item?id=3996708) about this article. A few corrections from it.

- **Zen of Python**
  
    Learning the culture that surrounds a language brings you one step closer to being a better programmer. If you haven't read the Zen of Python yet open a Python prompt and type `import this`. For each of the item on the list you can find examples here  [http://artifex.org/~hblanks/talks/2011/pep20_by_example.html](http://artifex.org/~hblanks/talks/2011/pep20_by_example.html)

    One caught my attention:  

    **Beautiful is better than ugly**  

    Give me a function that takes a list of numbers and returns only the
        even ones, divided by two.
        
        #-----------------------------------------------------------------------
        
        halve_evens_only = lambda nums: map(lambda i: i/2, filter(lambda i: not i%2, nums))
        
        #-----------------------------------------------------------------------
        
        def halve_evens_only(nums):
            return [i/2 for i in nums if not i % 2]
      
  
  
- **Remember the very simple things in Python**
  
    - Swaping two variables:

            a, b = b, a

    - The step argument in slice operators. For example:

            a = [1,2,3,4,5]
            >>> a[::2]  # iterate over the whole list in 2-increments
            [1,3,5]
            
        The special case `x[::-1]` is a useful idiom for 'x reversed'.

            >>> a[::-1]
            [5,4,3,2,1]

    UPDATE: Do keep in mind `x.reverse()` reverses the list in place and slices gives you the ability to do this:

            >>> x[::-1]
            [5, 4, 3, 2, 1]

            >>> x[::-2]
            [5, 3, 1]

- **Don't use mutables as defaults**
  
      
        def function(x, l=[]):          # Don't do this

        def function(x, l=None):        # Way better
            if l is None:
                l = []

    UPDATE: I realise I haven't explained why. I would recommend reading the [article by Fredrik Lundh](http://effbot.org/zone/default-values.htm).
    In short it is by design that this happens. "Default parameter values are always evaluated when, and only when, the “def” statement they belong to is executed;"

- **Use `iteritems` rather than `items`**
  

    `iteritems` uses `generators` and thus are better while iterating through very large lists.

        d = {1: "1", 2: "2", 3: "3"}

        for key, val in d.items()       # builds complete list when called.

        for key, val in d.iteritems()   # calls values only when requested.

    This is similar with `range` and `xrange` where `xrange` only calls values when requested.

    UPDATE: Do note that the `iteritems`, `iterkeys`, `itervalues` are removed from Python 3.x. The `dict.keys()`, `dict.items()` and `dict.values()` return views instead of `lists`. [http://docs.python.org/release/3.1.5/whatsnew/3.0.html#views-and-iterators-instead-of-lists](http://docs.python.org/release/3.1.5/whatsnew/3.0.html#views-and-iterators-instead-of-lists)


- **Use `isinstance` rather than `type`**

    Don't do 

        if type(s) == type(""): ...
        if type(seq) == list or \
           type(seq) == tuple: ...
        
    rather:

        if isinstance(s, basestring): ...
        if isinstance(seq, (list, tuple)): ...

    For why not to do so: [http://stackoverflow.com/a/1549854/504262](http://stackoverflow.com/a/1549854/504262)  

    Notice I used `basestring` and not `str` as you might be trying to check if a unicode object is a string. For example:

        >>> a=u'aaaa'
        >>> print isinstance(a, basestring)
        True
        >>> print isinstance(a, str)
        False

    This is because in Python versions below 3.0 there are two string types `str` and `unicode`:

              object
                 |
                 |
             basestring
                / \
               /   \
             str  unicode

- **Learn the various [`collections`](http://docs.python.org/library/collections.html)**

    Python has various container datatypes which are better alternative to the built-in containers like `list` and `dict` for specific cases. 

    <s>Generally most use this:</s>
    UPDATE: I'm sure most do not use this. Carelessness from my side. A few may consider writing it this way:

        freqs = {}
        for c in "abracadabra":
            try:
                freqs[c] += 1
            except:
                freqs[c] = 1

    Some may say a better solution would be:

        freqs = {}
        for c in "abracadabra":
            freqs[c] = freqs.get(c, 0) + 1


    Rather go for the `collection` type `defaultdict`

        from collections import defaultdict
        freqs = defaultdict(int)
        for c in "abracadabra":
            freqs[c] += 1

    **Other collections**
        
        namedtuple()	# factory function for creating tuple subclasses with named fields	
        deque	        # list-like container with fast appends and pops on either end	
        Counter	        # dict subclass for counting hashable objects	
        OrderedDict	    # dict subclass that remembers the order entries were added	
        defaultdict	    # dict subclass that calls a factory function to supply missing values	

    UPDATE: As noted by a few in Hacker News I could have used `Counter` instead of `defaultdict`.

        >>> from collections import Counter
        >>> c = Counter("abracadabra")
        >>> c['a']
        5
        

- **When creating classes Python's [magic methods](http://www.rafekettler.com/magicmethods.html)**

        __eq__(self, other)      # Defines behavior for the equality operator, ==.
        __ne__(self, other)      # Defines behavior for the inequality operator, !=.
        __lt__(self, other)      # Defines behavior for the less-than operator, <.
        __gt__(self, other)      # Defines behavior for the greater-than operator, >.
        __le__(self, other)      # Defines behavior for the less-than-or-equal-to operator, <=.
        __ge__(self, other)      # Defines behavior for the greater-than-or-equal-to operator, >=.

    There are several others.

- **Conditional Assignments**

        x = 3 if (y == 1) else 2
    It does exactly what it sounds like: "assign 3 to x if y is 1, otherwise assign 2 to x". You can also chain it if you have something more complicated:

        x = 3 if (y == 1) else 2 if (y == -1) else 1

    Though at a certain point, it goes a little too far.

    Note that you can use if ... else in any expression. For example:

        (func1 if y == 1 else func2)(arg1, arg2) 

    Here `func1` will be called if y is 1 and `func2`, otherwise. In both cases the corresponding function will be called with arguments arg1 and arg2.

    Analogously, the following is also valid:

        x = (class1 if y == 1 else class2)(arg1, arg2)

    where `class1` and `class2` are two classes.

- **Use the `Ellipsis` when necessary.**

    UPDATE: As one commenter mentioned in Hacker News "Using Ellipsis for getting all items is a violation of the Only One Way To Do It principle. The standard notation is `[:]`." I do agree with him. A better example is given using numpy in [stackoverflow](http://stackoverflow.com/a/118508/504262):

    The ellipsis is used to slice higher-dimensional data structures.

    It's designed to mean at this point, insert as many full slices (:) to extend the multi-dimensional slice to all dimensions.

    Example:

        >>> from numpy import arange
        >>> a = arange(16).reshape(2,2,2,2)

    Now, you have a 4-dimensional matrix of order 2x2x2x2. To select all first elements in the 4th dimension, you can use the ellipsis notation

        >>> a[..., 0].flatten()
        array([ 0,  2,  4,  6,  8, 10, 12, 14])

    which is equivalent to

        >>> a[:,:,:,0].flatten()
        array([ 0,  2,  4,  6,  8, 10, 12, 14])


    **Previous suggestion.**

    When creating a class you can use `__getitem__` to make you class' object work like a dictionary. Take this class as an example:


        class MyClass(object):
            def __init__(self, a, b, c, d):
                self.a, self.b, self.c, self.d = a, b, c, d

            def __getitem__(self, item):
                return getattr(self, item)

        x = MyClass(10, 12, 22, 14)

    Because of `__getitem__` you will be able to get the value of `a` in the object `x` by `x['a']`. This is probably a known fact. 

    This object is used to extend the Python slicing.([http://docs.python.org/library/stdtypes.html#bltin-ellipsis-object](http://docs.python.org/library/stdtypes.html#bltin-ellipsis-object)). Thus if we add a clause:

        def __getitem__(self, item):
            if item is Ellipsis:
                return [self.a, self.b, self.c, self.d]
            else:
                return getattr(self, item)

    We can use `x[...]` to get a list containing all the items.

        >>> x = MyClass(11, 34, 23, 12)
        >>> x[...]
        [11, 34, 23, 12]

