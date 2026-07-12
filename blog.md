---
layout: default
title: Blog
hero_description: Technical writing on Red Team, malware, threat intelligence, security reviews, risk, and adversarial thinking.
---

# Blog

Latest posts:

{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url }})**  
  <small>{{ post.date | date: "%Y-%m-%d" }}</small>
{% endfor %}
