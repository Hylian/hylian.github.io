---
layout: page
title: "Quadrotor"
description: "Quadrotor created from scratch"
group: projects
---
{% include JB/setup %}

Quadrotor: UAV made from scratch
================================

Description
-----------
Quadrotor that I'm building from scratch, including a custom PCB. Frame is made from carbon fiber rods and the PCB has an Atmel XMEGA MCU and an accelerometer, gyroscope, and magnetometer.

[GitHub](https://github.com/Hylian/quadrotor)

Posts
-----
{% assign posts_list = site.categories.quadrotor %}
<html>
{% include JB/posts_list %}
</html>

