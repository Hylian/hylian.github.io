---
layout: page
title: hyliantech
tagline: electronics and other things
---
{% include JB/setup %}

About Me
========


I'm an ECE and CS student at Carnegie Mellon University.

This site logs my various thoughts and projects.

Projects
========

<ul>
    {% assign pages_list = site.pages %}
    {% assign group = 'project' %}
    {% include JB/pages_list %}
</ul>

Posts
=====

<ul class="posts">
  {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
        </ul>
