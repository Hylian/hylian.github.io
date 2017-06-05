---
title: "arducard"
description: ""
date: "2014-03-13"
---
{% include JB/setup %}

arducard
========

![Arducard Prototype]({{ BASE_PATH }}/images/arducard1.jpg)

![Arducard Front]({{ BASE_PATH }}/images/arducard2.jpg)

An open-source e-paper development device.

[GitHub](https://github.com/Hylian/arducard)

Features
-----

* ATmega32U4 (Same as in the Arduino Leonardo)
* USB transceiver
* DS1343 Real-Time Clock
* 128KB FRAM
* LiR2016 Coin-cell Li-Ion battery
* Battery charging over USB
* 2.7" e-Paper display
* 5 edge-mounted interrupt-triggered tactile buttons
* Size: 80 mm x 45 mm x 5 mm

Applications
------------

* Google Auth Time-OTP
* Store barcodes for rewards cards, etc.
* Store QR codes
* USB text terminal for Raspberry Pi

Posts
-----
{% assign posts_list = site.categories.arducard %}
<html>
{% include JB/posts_list %}
</html>


