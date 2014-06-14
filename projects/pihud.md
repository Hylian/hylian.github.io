---
layout: page
title: "PiHUD"
description: ""
group: projects
---
{% include JB/setup %}

PiHUD
========

![Display]({{ BASE_PATH }}/images/PiHUD/display.png)
![Enclosure Open]({{ BASE_PATH }}/images/PiHUD/enclosure-open.png)
![Enclosure Closed]({{ BASE_PATH }}/images/PiHUD/enclosure-closed.png)
![Clock Screenshot]({{ BASE_PATH }}/images/PiHUD/clock-screenshot.png)

A Google Glass-style Heads Up Display. Display is taken off an old iPod HMD and connected to a Raspberry Pi with a battery and enclosure.

[GitHub](https://github.com/Hylian/PiHUD)

Posts
-----
{% assign posts_list = site.categories.pihud %}
<html>
{% include JB/posts_list %}
</html>


