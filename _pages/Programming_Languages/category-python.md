---
title: "Python"
layout: archive
permalink: categories/python
entries_layout: grid
---

{% assign posts = site.categories.python %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
