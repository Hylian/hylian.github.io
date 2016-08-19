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

[Build18 Wiki](http://build18.org/wiki/index.php/FPGA_on_the_Web!)

Winner, Faculty Choice Award, Build18 Hackathon 2015

FPGA on the Web allows students to program and interact with Altera DE2-115 FPGA boards over the web. Students can upload SystemVerilog files to be compiled on the server and programmed onto a real development board. Students can then virtually view and control the peripherals of the board to interact with it, allowing them to complete their FPGA labs from home.

Posts
-----
{% assign posts_list = site.categories.boosterbot %}
<html>
{% include JB/posts_list %}
</html>


