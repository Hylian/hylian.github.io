---
layout: post
title: "SLAMbot Lives!"
description: ""
category: "slambot"
tags: []
---
{% include JB/setup %}

The SLAMbot PCBs have arrived! I soldered one up and mounted the LIDAR and it seems to be working well so far.

I had some concerns as to whether the Evalbot's onboard voltage regulators could power the LIDAR motor and onboard processor, but I tested it out and it doesn't seem to be an issue.

Next step is to code the MSP430 to handle passing off the LIDAR data to the Stellaris ARM microcontroller on the Evalbot and control the LIDAR motor speed via PID.

![PCB]({{ BASE_PATH }}/images/slambotpcb.png)

![Assembled SLAMbot]({{ BASE_PATH }}/images/slambot1.jpg)

