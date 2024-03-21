---
layout: archive
permalink: /projects
title: "Projects"
---

# Projects

## Web Development Projects

<ul class="link-grid">
  {% for link in site.data.projects %}
    <li><a href="{{ link.url }}" target="_blank">{{ link.name }}</a></li>
  {% endfor %}
</ul>

<style>
.link-grid {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 10px;
}

.link-grid li {
  text-align: center;
}

.link-grid li a {
  display: block;
  padding: 10px;
  background-color: #f0f0f0;
  text-decoration: none;
  color: #333;
  border-radius: 5px;
}

.link-grid li a:hover {
  background-color: #ccc;
}
</style>
