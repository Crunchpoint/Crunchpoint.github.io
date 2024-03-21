---
layout: archive
permalink: /projects
title: "Projects"
---

# Projects

## Web Development Projects

<ul class="project-grid">
  {% for project in site.data.projects %}
    <li>
      <a href="{{ project.url }}" target="_blank">
        <img src="{{ project.image }}" alt="{{ project.name }}">
        <p>{{ project.name }}</p>
        <p><{{ project.stack }}></p>
      </a>
    </li>
  {% endfor %}
</ul>

<style>
.project-grid {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 한 행에 3개의 아이템 */
  grid-gap: 10px;
}

.project-grid li {
  text-align: center;
}

.project-grid li a {
  display: block;
  padding: 5px;
  background-color: #fafafa;
  text-decoration: none;
  border: 1px solid #ddd;
  /* color: #333; */
  border-radius: 5px;
}

.project-grid li a:hover {
  background-color: #ccc;
}

.project-grid li a img {
  border-radius: 5px;
  border: 1px solid #ddd;
}

.project-grid li a p {
  font-size: 0.85em;
  font-weight: bold;
  margin: 5px 0 0 0;
}

.project-grid li a p:last-child {
  font-weight: normal;
  font-size: 0.6em;
}
</style>
