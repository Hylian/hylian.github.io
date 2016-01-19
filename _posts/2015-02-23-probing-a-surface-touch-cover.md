---
layout: post
title: "Probing a Surface Touch Cover"
description: ""
category: "keyboard cover"
tags: [microsoft, hid over i2c, keyboard]
---
{% include JB/setup %}

*THIS INFORMATION IS INCORRECT!*

Take a look at the more recent post for a correct description of the protocol

I created a breakout board for the keyboard connector of my Surface to probe for the pinout and logic levels of the interface.

The keyboard connector uses Microsoft's [HID over I2C interface](https://msdn.microsoft.com/en-us/library/windows/hardware/Dn642101.aspx). There is also a useful Texas Instruments appnote on it [here](http://www.ti.com/lit/an/slaa569/slaa569.pdf).

The interface is essentially the same as the USB HID spec, but implemented over an I2C transport and one interrupt pin. This means our keyboard needs to act as an I2C slave and assert an interrupt signal to the PC whenever data is available.

I took the connector from my [previous Touch Cover teardown]({{ BASE PATH }}/cover/2014/10/19/microsoft-touch-cover-mini-teardown/) and sanded down the flat cable until the copper was exposed. I then soldered this to a working Touch Cover with some pins to probe the lines.

![Breakout Cable]({{ BASE PATH }}/images/touchpinout/cable.jpg)

Here's what I found after hooking it up to an oscilloscope:

![Interrupt, (Unused), SDA, SCL, +5V, Ground]({{ BASE_PATH }}/images/touchpinout/cover_pinout.png)

The logic levels of the SDA and SCL lines were 1.8V. The interrupt pin is likely 1.8V as well, but I wasn't able to get a good capture of it on the oscilloscope.

Since the TrackPoint module on ThinkPad keyboards uses 5V logic, I'll have to do some level shifting on my microcontroller to interface with everything. For now, I will try and write a HID over I2C library for MSP430 from just the spec, and only hook up a logic analyzer to the keyboard as a last resort.
