---
layout: page
title: "SLAMbot"
description: "SLAM with the TI Stellaris Evalbot and a LIDAR"
group: projects
---
{% include JB/setup %}

SLAMbot: SLAM with a TI Stellaris Evalbot and XV-11 LIDAR
=========================================================

![Assembled SLAMbot]({{ BASE_PATH }}/images/slambot1.JPG)

Description
-----------
The TI Evalbot is a robotic Stellaris ARM dev board from Texas Instruments designed for teaching RTOS concepts. The Neato XV-11 is a robotic vacuum cleaner with an inexpensive laser distance sensor. This project combines the two to perform Simultaneous Localization and Mapping (SLAM) and autonomous navigation.

This project is funded by the CMU Robotics Club.

[GitHub](https://github.com/Hylian/SLAMbot)

Posts
-----
{% assign posts_list = site.categories.slambot %}
<html>
{% include JB/posts_list %}
</html>

