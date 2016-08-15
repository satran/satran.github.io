---
layout: default
title: Satyajit Ranjeev
---
Hi! I am **Satyajit Ranjeev**. I am a computer programmer who loves to solve problems. I currently work at [OptioPay](http://optiopay.com).

{% for post in site.posts limit:6 %}
  {{post.date | date_to_string}} [{{post.title}}]({{post.url}}) 
{% endfor %}

*Older posts can be found at [/articles](/articles)*
