---
layout: post
title: Django Managers
summary: I have been working with Django for more than a two years now and the more I learn about it the more it gets better. I do have a few hiccups but there are solutions for them, mostly. Any ways one thing I find very interesting is the model’s manager. Objects  of a model, or a few objects, can be retrieved using these methods.
---

I have been working with Django for more than a two years now and the more I learn about it the more it gets better. I do have a few hiccups but there are solutions for them, mostly. Any ways one thing I find very interesting is the model’s manager. Objects  of a model, or a few objects, can be retrieved using these methods: 

    Model.objects.get()
    Model.objects.filter()

Manager allows you to create such methods for your own Models. Let me give you an example. I have been working on a calendar app for a while and I have a model which looks like this:

    class EventCalendar(models.Model):
        """Create calendar for every year use this for different levels or departments"""
        name = models.CharField(max_length=50)
        academic_year = models.ForeignKey(AcademicYear)
        is_closed = models.BooleanField(default=False)
        is_default = models.BooleanField(default=False)
 
The is_closed boolean value tells me that the calendar is closed for adding events. Thus when I want to create a new event I should get just the list of calendars that is open. Thus I created a manager class:

    class EventCalendarManager(models.Manager):
        def list_open(self):
            '''Lists all active or calendars on which events can be added.'''
            return self.filter(is_closed=False)
  
and added a line to my EventCalendar model objects = EventCalendarManager(). Thus the entire code would look like this:

The manager:

    class EventCalendarManager(models.Manager):
        def list_open(self):
            '''Lists all active or calendars on which events can be added.'''
            return self.filter(is_closed=False)
  
The model:

    class EventCalendar(models.Model):
        """Create calendar for every year use this for different levels or departments"""
        name = models.CharField(max_length=50)
        academic_year = models.ForeignKey(AcademicYear)
        is_closed = models.BooleanField(default=False)
        is_default = models.BooleanField(default=False)
        objects = EventCalendarManager()
 
And now if I want to list down the calendars open for adding events all I need to do is:

    cals = EventCalendar.objects.list_open() 

I can similarly add a function to the manager class to return the default calendar and various other things. This has helped the way I implement my code. Hope you find this useful. Cheers!
