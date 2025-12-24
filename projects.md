---
layout: default
title: Projects
permalink: /projects/
---

This page contains all my quantitative research and trading-related write-ups.

{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url }})**  
  <small>{{ post.date | date: "%Y-%m-%d" }}</small>
{% endfor %}
