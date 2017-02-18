---
layout: default
title: Satyajit Ranjeev
---
Hi! I am **Satyajit Ranjeev**. I am a computer programmer who loves to solve problems. I currently work at [OptioPay](http://optiopay.com).

### Articles

{% for post in site.posts limit:6 %}
  {{post.date | date_to_string}} [{{post.title}}]({{post.url}}) 
{% endfor %}

*Older posts can be found at [/articles](/articles)*

### Books Read
{% assign sortedbooks = (site.books | sort: 'date') | reverse %}
{% for book in sortedbooks limit:6 %}
  {{book.date | date_to_string}} [{{book.title}}]({{book.url}}) 
{% endfor %}


### Contact

I am satran on freenode, sat_ran on twitter and you can email me at s@ranjeev.in
