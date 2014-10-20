---
layout: post
title: "Capacitive Touch Business Cards and DirtyPCBs Review"
description: "Designing a unique PCB business card"
category: "card"
tags: []
---

In preparation for the job fair here at school, I decided to make a cool PCB business card to differentiate myself from the crowd. There were already several examples on [Hack-A-Day](http://hackaday.com/?s=PCB+business+card) that I used as inspiration. 

The card needed an unique feature while keeping the parts count down, to minimize assembly overhead and cost. Meanwhile, cutouts, silkscreen, and drill hits are all free, so it's possible to get creative with those. The most popular features from the ones I saw online were LEDs, capacitive touch, and USB. I decided to use capacitive touch, as it didn't require any assembly and kept the profile of the board low. I also used USB, as it removes the need for a battery, and lets the board be a bit more useful.

The design I ended up with was a gamepad with capacitive buttons, styled after the Nintendo Entertainment System. I used an ATtiny44 running the [V-USB library](http://www.obdev.at/products/vusb/index.html) for USB. The card has all the buttons of an NES controller: a D-pad, A, B, select, and start.

To keep the profile of the board down, I decided to try out a trick that I saw used in the [Arduboy](http://www.arduboy.com/); I mirrored the footprint of the ATtiny and drew a cut out so that the IC could be mounted upside-down, with the packaging going through the board.

For the capacitive buttons, I used the method described by Tuomas Nylund [here](http://tuomasnylund.fi/drupal6/content/capacitive-touch-sensing-avr-and-single-adc-pin). It implements a single pin capacitive button by taking advantage of the ADC sample-and-hold capacitor being in parallel with the capacitive pad.

I designed the board in KiCad, and decided to try out Dangerous Prototype's "new" DirtyPCBs service for fabrication. They offered the most variety in colors at no extra cost, and the pricing was better than Seeed Studio's FusionPCB service, as it used the actual dimensions of the board to quote pricing instead of tiering by size. The cost came out to be $28 for 10 boards and $15 for DHL shipping, which is a very nice price.

Overall, I'm impressed with the quality of the boards. The blue boards look really nice.

![Full View of Boards]({{ BASE_PATH }}/images/card/card1.jpg)

![Top View of Boards]({{ BASE_PATH }}/images/card/card2.jpg)

There were a couple blemishes in the silk screen that appeared on all the boards, however. Likely a problem with the stencil. I did use a ton of silk to get the "negative" effect on the cards, so I don't really blame them.

![Silkscreen Blemish 1]({{ BASE_PATH }}/images/card/card3.jpg)

![Silkscreen Blemish 2]({{ BASE_PATH }}/images/card/card4.jpg)

Looks like the order number was printed in reverse on the bottom of the board, as the top was fully covered in silk.

![Order Number]({{ BASE_PATH }}/images/card/card5.jpg)

Unfortunately, the fab missed the cutout I specified for the reverse-mounted ATtiny, so I wasn't able to move forward with assembling the board quite yet. They did a fine job with the slot cutouts for the micro USB, though, so I'm not sure what went wrong.

![Missed Cutout]({{ BASE_PATH }}/images/card/card6.jpg)

Minus the missed cutout, I was very satisfied with how the boards came out. With more options and flexible pricing in comparison to FusionPCB, DirtyPCBs will likely be me go-to fab service in the future.

As for the business cards, I will have to figure out what went wrong and order another batch. The full project source can be found on my GitHub [here](https://github.com/hylian/card).

{% include JB/setup %}
