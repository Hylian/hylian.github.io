---
layout: post
title: "PCB Business Card: Round 2"
description: "Ordering from DirtyPCBs the second time around"
category: "card"
tags: []
---
{% include JB/setup %}

![Front]({{ BASE_PATH }}/images/card2/front.jpg)

![Back]({{ BASE_PATH }}/images/card2/back.jpg)

My last order of my capacitive touch PCB business cards had some unfortunate bugs, like a missed
cutout for the reverse-mounted ATtiny and a short from power to ground.

I fixed the bugs and re-ordered from DirtyPCBs. It seems what caused the
missed cutout in the last order was the "CUTOUT" text in the middle of the cutout in the edge cuts
layer, which is the format OSHPark uses. After removing it, the fab correctly processed the cutout.

I used the DirtyPCB's "protopack" quantity option this time, which can yield more or less than 10
PCBs, depending on what the manufacturer needs to fill out a panel. I lucked out this time and
received 12 boards.

However, the fab accidentally exposed the capacitive pads this time, which was interesting, 
as I didn't indicate anything on the soldermask layer. Perhaps they thought I had made a mistake?

The silkscreen on the board seems to be lower quality this time. The print isn't as bold, and
there are small spots where the silkscreen didn't transfer. There is also some distortion because
the silkscreen gerber wasn't perfectly aligned with the print, so there are some small artifacts 
with straight lines that don't look too great.

![Stack of Boards with Blemishes]({{ BASE_PATH }}/images/card2/stack.jpg)
