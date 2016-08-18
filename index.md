---
layout: page
title: hyliantech
tagline: electronics and other things
---
{% include JB/setup %}

I'm an Electrical and Computer Engineering student at Carnegie Mellon University.

My main interests are Embedded Systems, Digital Design, and IC Design.

Projects
========

<ul>
    {% assign pages_list = site.pages %}
    {% assign group = 'projects' %}
    {% include JB/pages_list %}
</ul>

Posts
=====

<ul class="posts">
  {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
        </ul>
