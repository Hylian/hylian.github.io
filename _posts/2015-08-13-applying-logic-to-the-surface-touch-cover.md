---
layout: post
title: "Applying Logic to the Surface Touch Cover"
description: "Using the Saleae Logic to analyze a Surface Touch Cover"
category: "keyboard cover"
tags: [microsoft, keyboard]
---
{% include JB/setup %}

![Probing Setup]({{ BASE_PATH }}/images/logic/touchcoversetup.jpg)

Thanks to Saleae's generous student discount, I was finally able to purchase a Logic 4 logic
analyzer and start probing at the Surface Touch Cover. I hooked it up to my previous breakout board
and recorded the signals on the pins at power-on and while pressing various keys.

After some analysis, it turns out my hypothesis about the protocol in my previous post was completely wrong! 
Instead of HID over I2C, the keyboard uses duplex serial communication, and thankfully so, as serial is much easier to
analyze and implement than the HID over I2C spec.

The serial configuration used is a bit strange:

* 1000000 bits/sec bitrate
* 9 bits per transfer
* 1 Stop bit (Standard)
* No parity bit (Standard)
* Least significant bit sent first (Standard)
* Non inverted (Standard)

I took a capture of the board at power-on and parsed some of the data into a spreadsheet. You can find it
[here](https://docs.google.com/spreadsheets/d/12D0grXNK70KVoA9GRbzztGao7zjCuJUPEbxAdMz5sp0/edit?usp=sharing)
or embedded down below. The cells are color-coded to make some of the patterns more apparent. 

Some observations:

* All packets share a common header format that describes the type of information being sent.
* Both the Surface and the Keyboard count the number of packets sent and transmit the index of the current packet.
* Both the Surface and the Keyboard have two different "types" of packets, with separate counter
values: one begins at `0`, and the other begins at `0x1E4`. These correspond to different header values, 
and are color-coded as yellow/orange or green/navy based on channel.
* The size of the payload in bytes is transmitted in the header. There is an overhead of +10 bytes
for the total transmission size including header and prologue. (1 byte = 9-bit transmission)
* Every packet ends with a two byte prologue that does some sort of validity checking. Every 10 byte
transmission has the same prologue of `0x1FF, 0x1FF`, so it's not likely to be something fancy like
a CRC. Rows 7 and 13 have the same header and prologue, so it may be that identical headers implies
identical prologues.

I'm hoping to boil this information down to the minimum required to communicate with the Surface and
replay enough packets to press a key.

Feel free to drop me a line if you discover something interesting or want the original capture data.

<iframe src="https://docs.google.com/spreadsheets/d/12D0grXNK70KVoA9GRbzztGao7zjCuJUPEbxAdMz5sp0/pubhtml?widget=true&amp;headers=false" width="705" height="850"></iframe>
