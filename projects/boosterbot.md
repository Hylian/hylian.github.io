---
layout: page
title: "BoosterBot"
description: ""
group: projects
--- 
{% include JB/setup %}

BoosterBot
========

![BoosterBot Photo]({{ BASE_PATH }}/images/boosterbot/boosterbot-robot.jpg)

<iframe width="705" height="400" src="https://www.youtube.com/embed/C60c98HO0_U" frameborder="0" allowfullscreen> </iframe>

A BoosterPack that turns your TI Launchpad into a fully functional robot!

The BoosterBot attaches underneath any 40-pin Launchpad to give it batteries, wheels, and access to a bunch of sensors; perfect for anyone who wants to get started with MSP430 and robotics, or just wants an easy to use robotics platform to build off of.

It comes with line sensors and an IR distance sensor to support lots of cool demos out of the box!

[Purchase on Tindie](https://www.tindie.com/products/HylianSavior/boosterbot/)

[Website](http://boosterbot.in)

[GitHub](https://github.com/Hylian/BoosterBot)

[Hackaday](https://hackaday.io/project/1845-BoosterBot)

Features
--------

* Micro Metal Gearmotors from Pololu
* Powered by 3xAAA batteries
* Five QRE1113 Reflectance sensors for line following and maze solving
* Header for a Sharp IR distance sensor
* Header for a servo
* Compatible with other BoosterPacks, including the FuelTank battery BoosterPack and AIR module BoosterPack

Posts
-----
{% assign posts_list = site.categories.boosterbot %}
<html>
{% include JB/posts_list %}
</html>


