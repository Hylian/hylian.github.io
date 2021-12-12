---
layout: page
title: edwardsh.in
tagline: electronics and other things
---
{% include JB/setup %}

Projects
========

<ul class="posts">
  {% assign sorted_projects = site.projects | sort: 'date' | reverse %}
  {% for project in sorted_projects %}
    <li><span>{{ project.date | date: "%b %Y" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ project.url }}">{{ project.title }}</a></li>
  {% endfor %}
</ul>

Posts
=====

<ul class="posts">
  {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
