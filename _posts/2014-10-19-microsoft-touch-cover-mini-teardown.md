---
layout: post
title: "Microsoft Touch Cover Mini Teardown"
description: ""
category: "cover"
tags: []
---
{% include JB/setup %}

In preparation for creating my own Thinkpad keyboard cover for my Surface Pro 2, I decided to take apart a Touch Cover to get a better look at how they worked. I bought a non-working Touch Cover off eBay for $10 and went at it.

![Intact Cover]({{ BASE_PATH }}/images/touchcover/cover1.jpg) 

I used a knife to rip open the skin of the cover. Looks like it's made of some sort of tough plastic cloth; it took some work to rip through it all.

![Ripped Open Seam]({{ BASE_PATH }}/images/touchcover/cover2.jpg) 

Front of the cover exposed!

![Ripped Open Cover]({{ BASE_PATH }}/images/touchcover/cover3.jpg) 

A first look at the capacitive touchpad.

![Touchpad]({{ BASE_PATH }}/images/touchcover/cover4.jpg) 

Individual keys were glued to the fabric of the cover to make sure they connected well. 

![Connector]({{ BASE_PATH }}/images/touchcover/cover5.jpg) 

The Touch Cover is a silicone membrane keyboard, not a purely capacitive one as I had initially thought. Here, the top membrane layer is removed. As pressure is applied to the pads, they touch the capacitive traces underneath, triggering a keypress.

![Membrane]({{ BASE_PATH }}/images/touchcover/cover6.jpg) 

Looks like the space bar is split into two pads.

![Split Spacebar]({{ BASE_PATH }}/images/touchcover/cover7.jpg) 

A look at the arrow keys.

![Arrow Keys]({{ BASE_PATH }}/images/touchcover/cover8.jpg) 

Now, for the second layer. This contains all the circuitry, and is backed by some sort of laminate board on the other side.

![Bare Board]({{ BASE_PATH }}/images/touchcover/cover9.jpg) 

![Bare Board Top ViewCover]({{ BASE_PATH }}/images/touchcover/cover10.jpg) 

A better look at the touchpad. 

![Bare Board Touchpad]({{ BASE_PATH }}/images/touchcover/cover11.jpg) 

There are several test points on the board. Some JTAG test points for programming/debugging the main MCU, as well as some I2C test points for the accelerometer. I was able to confirm with a multimeter that the two left-most connectors on the cover are +5V and Ground, but unfortunately, the two I2C pins and interrupt pin weren't broken out onto any test points. It should be fairly easy to determine by poking around the signals on a working cover, though.

![Test Points]({{ BASE_PATH }}/images/touchcover/cover14.jpg) 

![Capacitive Key Closeup]({{ BASE_PATH }}/images/touchcover/cover12.jpg) 

There is also a metal insert on the bottom left of the board.

![Mysterious Magnet]({{ BASE_PATH }}/images/touchcover/cover13.jpg) 

It's magnetic! Maybe it's for detecting the open/closed positions?

![Magnetic Closeup]({{ BASE_PATH }}/images/touchcover/cover25.jpg) 

Laminate backing on the other side of the board.

![Board Back]({{ BASE_PATH }}/images/touchcover/cover16.jpg) 

All the goodies are glued up in the bottom.

![Board Back Closeup]({{ BASE_PATH }}/images/touchcover/cover17.jpg) 

The skin is mostly just held in place by the force of the connector, with the exception of a few anchors.

![Skin Attachment]({{ BASE_PATH }}/images/touchcover/cover18.jpg) 

![Removed Skin]({{ BASE_PATH }}/images/touchcover/cover19.jpg) 

Backside of the connector.

![Removed Connector]({{ BASE_PATH }}/images/touchcover/cover20.jpg) 

I cut out the capacitive sensing layer. You can see that it's a big matrix of sensors all feeding into the main board.

![Removed Capacitive Layer]({{ BASE_PATH }}/images/touchcover/cover23.jpg) 

![Capacitive Layer Closeup]({{ BASE_PATH }}/images/touchcover/cover24.jpg) 

With some force, I managed to pry the PCB free. Unfortunately, it was glued in pretty tightly, and the board suffered some casualties.

I was able to identify a few of the big ICs inside.

First up is the [Atmel maXTouch mXT112E](http://www.atmel.com/microsite/maxtouch_eseries/mxt112e.aspx). This is a capacitive touchscreen controller that's likely used for the touch pad.

The markings on this chip were:

ATMEL
MXT112E
MASH1R0
2U29S0B

The main MCU is a [Freescale MK10DN512Z](http://www.freescale.com/webapp/sps/site/prod_summary.jsp?code=K10_100&lang_cd=). This is one of Freescale's Kinetis MCUs based on ARM Cortex-M4 cores.

The markings on this chip were:

MK10DN512Z
AB10 4N30D
UYDM1233A

There was a third IC marked:

2233
C3H
GKXCQ

I am not quite sure what it is, but I suspect it may be a [Texas Instruments MSP430 G2233](http://www.ti.com/product/msp430g2233), which comes in QFN packages. 

![Removed PCB]({{ BASE_PATH }}/images/touchcover/cover26.jpg) 

![Removed PCB Different Angle]({{ BASE_PATH }}/images/touchcover/cover27.jpg) 

![Removed PCB Different Angle 2]({{ BASE_PATH }}/images/touchcover/cover28.jpg) 

I removed the connector and FPC. Should be useful to use in my own cover.

![Removed Connector]({{ BASE_PATH }}/images/touchcover/cover29.jpg) 
