---
layout: page
title: "FPGA on the Web"
description: ""
group: projects
---
{% include JB/setup %}

FPGA on the Web
================

![Website Screenshot]({{ BASE_PATH }}/images/fpgaweb/fpgascreenshot.png)

[GitHub](https://github.com/build18-fpga-on-the-web)

[Build18 Wiki](http://build18.org/wiki/index.php/FPGA_on_the_Web!)

Winner, Faculty Choice Award, Build18 2015

FPGA on the Web allows students to program and interact with Altera DE2-115 FPGA boards over the web. Users can upload SystemVerilog files, which are then compiled on the server and programmed onto a real development board. The user can then virtually view and control the peripherals of the board to interact with it, allowing them to do their FPGA labs.

Posts
-----
{% assign posts_list = site.categories.boosterbot %}
<html>
{% include JB/posts_list %}
</html>


