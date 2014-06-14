---
layout: post
title: "Basic HUD Info Program using Python and Clutter"
description: ""
category: "PiHUD"
tags: [Raspberry Pi]
---
{% include JB/setup %}

![Clock Screenshot]({{ BASE_PATH }}/images/PiHUD/clock-screenshot.png)

I made a simple program in Python to show the date, time, and the next upcoming calendar event from my Google Calendar. This will be the program which runs on my Raspberry Pi HUD. The GUI was built using Clutter. I generated the Python bindings for Clutter using [GObject Introspection](https://live.gnome.org/GObjectIntrospection).

To read the calendar event data, I used the private XML data feed for my calendar (which can be found in the calendar settings), and parsed it with elementtree. To get the XML feed to show recurring events and dates, I had to change the “basic” parameter at the end of the HTML request to “full?futureevents=true”.

The next version of the program will most likely use Google Apps API and the corresponding Python client library to let me hook into other Google services, such as tasks and Gmail.

The code can be found on the [GitHub repo](https://github.com/Hylian/PiHUD).
