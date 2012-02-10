---
layout: post
title: Creating Abstract Base Class in Mongoengine
---
I guess some how they missed it in the documentation or I have overlooked it. We had a situation where we needed to create an abstract base class. It is quite a simple process. Create the base class with meta, abstract: true. 

    class BaseAbstractClass(Document):
        meta = {
            'abstract': True
        }
        pass
        
Thus if I create another class inheriting from `BaseAbstractClass` say Child:

    class Child(BaseAbstractClass):
        pass

Child would be created as a collection called `child` and not `baseabstractclass.child`.
