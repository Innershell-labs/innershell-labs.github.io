---
layout: default
title: InnerShell Labs
---

## InnerShell Labs

**InnerShell Labs** is an independent security research space focused on:

- Ransomware & incident analysis  
- Adversary tradecraft & CTI  
- Offensive & defensive security fundamentals  
- Lessons learned from real-world incidents  

We believe **strong fundamentals beat hype-driven security**.

---

### Latest Research & Blog Posts

{% for post in site.posts limit:5 %}
- **[{{ post.title }}]({{ post.url }})**  
  <small>{{ post.date | date: "%d %B %Y" }}</small>
{% endfor %}

---

### About

This space exists to document:
- real incidents
- technical analysis
- critical thinking in cybersecurity

No vendor hype. No magic AI. Just security.
