---
layout: page
title: "SLAMbot"
description: "SLAM with the TI Stellaris Evalbot and a LIDAR"
group: projects
---
{% include JB/setup %}

SLAMbot: SLAM with a TI Stellaris Evalbot and XV-11 LIDAR
=========================================================

Description
-----------
The TI Evalbot is a cute little robotic dev board from Texas Instruments that uses their Stellaris ARM processor as a core. The Neato XV-11 is a robotic vacuum cleaner that has an inexpensive laser distance sensor which can be removed. This project combines the two to perform Simultaneous Localization and Mapping (SLAM) and autonomous navigation.

This project is funded by the CMU Robotics Club.

[GitHub](https://github.com/Hylian/SLAMbot)

Posts
-----
{% assign posts_collate = site.categories.evalbot %}
<html>
{% include JB/posts_collate %}
</html>

