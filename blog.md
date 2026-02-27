---
layout: default
title: Blog
---

# Blog

Latest posts:

{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url }})**  
  <small>{{ post.date | date: "%Y-%m-%d" }}</small>
{% endfor %}
