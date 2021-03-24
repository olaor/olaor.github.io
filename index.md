---
title: What to do or have done
---


## Some writeups on stuff I have bothered with in the past and present.

Some of it may be relevant, most is not.

{% assign cutoff = "2021-03-20" %}

{% for post in site.posts %}

{% capture postdate %}{{ post.date | date: "%Y-%m%d" }}{% endcapture %}
{% if postdate < cutoff %}
{% continue %}
{% endif %}

### {{ post.date | date: "%Y-%m-%d" }} [{{ post.title }}]({{ post.url }}) by {{ post.author }} 

{% endfor %}

***

## Older historical records from previous blogging attempts  

Lots of these are 1) Crap. 2) In norwegian. Don't bother.

{% for post in site.posts %}

{% capture postdate %}{{ post.date | date: "%Y-%m%d" }}{% endcapture %}
{% if postdate > cutoff %}
{% continue %}
{% endif %}

### {{ post.date | date: "%Y-%m-%d" }} [{{ post.title }}]({{ post.url }}) by {{ post.author }} 

{% endfor %}

***

_Last update: {{ "now" | date: "%Y-%m-%d %H:%M:%S"}} Europe/Oslo_

