---
title: What to do or have done
---


## Some writeups on stuff I have bothered with in the past and present.

Some of it may be relevant, most is not.

{% for post in site.posts %}
### {{post.date | date: "%Y-%m-%d"}} [{{ post.title }}]({{ post.url }}) by {{post.author}} 



{% endfor %}



_Last update: {{ "now" | date: "%Y-%m-%d %H:%M:%S"}} Europe/Oslo_

