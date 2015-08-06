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

A BoosterPack that turns your TI LaunchPad into a fully functional robot!
-------------------------------------------------------------------------

2nd Place Winner of the 2014 Texas Instruments Intern Design Contest

BoosterBot attaches underneath any 40-pin LaunchPad to give it batteries, wheels, and access to
distance and line tracking sensors; perfect for anyone who wants to get started with the MSP430 and
robotics, or just wants an easy-to-use robotics platform to build off of.

[Purchase on Tindie](https://www.tindie.com/products/HylianSavior/boosterbot/)

[Bill of Materials](https://docs.google.com/spreadsheets/d/1mRRuciIq44UwTY0NZKw7sUpmjOIC4nQgimvoF12DIwo/pubhtml)

[Website](http://boosterbot.in)

[GitHub](https://github.com/Hylian/BoosterBot)

[Hackaday](https://hackaday.io/project/1845-BoosterBot)

Features
--------

* Distance sensing with a Sharp IR distance sensor
* Line tracking with five QRE1113 reflectance sensors
* Differential steering with Micro Metal Gearmotors
* Built-in Power with a 3xAAA battery holder
* FuelTank BoosterPack support for a larger capacity battery with USB charging
* Servo Header supports one servo motor

Compatibility
-------------

BoosterBot adheres to the 40-pin BoosterPack standard, meaning it should be compatible with most 40-pin LaunchPads.

However, it has only been tested with the MSP430F5529 LaunchPad.

Software Support
----------------

BoosterBot supports Arduino code using the Energia library. There are code examples for line tracking, distance tracking, and wireless communication using Bluetooth and the AIR BoosterPack to get you started.

Posts
-----
{% assign posts_list = site.categories.boosterbot %}
<html>
{% include JB/posts_list %}
</html>


