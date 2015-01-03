---
layout: post
title: "Adventures in Sourcing and Building an ErgoDox"
description: ""
category: "ergodox"
tags: [keyboard]
---
{% include JB/setup %}

I spent this semester pulling together the parts to build an ErgoDox, and recently completed my build over winter break. The ErgoDox is an open-source, split key, mechanical keyboard. I chose to build an ErgoDox because it uses Cherry MX keys, has multiple thumb keys, and made for a nice DIY project. ErgoDox kits occasionally go on sale on Massdrop, but I tried to save some cash by sourcing all the components individually.

Electronics
===========

I purchased the ErgoDox PCBs for $30 through a group buy by ATX Hackerspace. The Teensy 2.0 was purchased off SparkFun for free using a coupon. The Cherry MX brown switches were purchased off [MechanicalKeyboards.com](http://mechanicalkeyboards.com/shop/index.php?l=product_detail&p=1034) at $50 for 100. The type that you want is the PCB mount, not the plate mount model. All the remaining passive components were purchased off DigiKey for $14.

For assembly, I followed Massdrop's assembly instructions found [here](http://www.massdrop.com/ext/ergodox).

I initially used through-hole diodes, and soldered an entire board before realizing that the leads sticking out on the other side blocked the switch plate of the enclosure. I ended up having to desolder all the diodes and solder in surface-mount ones instead.

![Through-Hole Diodes]({{ BASE_PATH }}/images/ergodox/03.jpg)

![Surface-Mount Diodes 2]({{ BASE_PATH }}/images/ergodox/05.jpg)

![Plate]({{ BASE_PATH }}/images/ergodox/06.jpg)

![Teensy]({{ BASE_PATH }}/images/ergodox/07.jpg)

![Completed Plates 1]({{ BASE_PATH }}/images/ergodox/08.jpg)

![Completed Plates 2]({{ BASE_PATH }}/images/ergodox/09.jpg)

![Completed Plates 3]({{ BASE_PATH }}/images/ergodox/10.jpg)

Enclosure
=========

For the enclosure, I used Litster's acrylic case design, which uses slices of laser-cut acrylic. The original design calls for three 5mm slices in the middle and two 3mm slices on the top and bottom. However, metric thickness acrylic isn't very popular, so it's a bit difficult to source. Instead, I used 3/16" and 1/8" sheets, which are almost the same thickness. I purchased the acrylic online in 12x12" sheets from Delvie's Plastics for $36.

![Enclosure 1]({{ BASE_PATH }}/images/ergodox/01.jpg) 

I opened up the design files in Inkscape and managed to fit two slices onto each 12x12" acrylic sheet, and laser cut the sheets using the laser cutter in my school's machine shop. Interestingly, CorelDRAW seemed to have some scaling issues with the right hand side design files, where they were scaled larger than their actual size. The holes in the case are made for 3mm diameter screws, but I wasn't able to find 3mm screws that were long enough (20mm screws were barely not enough). Instead, I used 1" long #4-40 screws. It's a bit of a loose fit, but seems to work just fine.

![Enclosure 2]({{ BASE_PATH }}/images/ergodox/02.jpg)

Because the slices I used were thinner than the design was intended for, the TRRS jack on the board was taller than the height of the slice. I ended up having to snap off parts of the spacer plate to make room for the jack.

![Cut Plates]({{ BASE_PATH }}/images/ergodox/11.jpg)

![Completed Build 1]({{ BASE_PATH }}/images/ergodox/12.jpg)

![Completed Build 2]({{ BASE_PATH }}/images/ergodox/13.jpg)

Although the screws seem to work decently as feet, I went and bought some adhesive rubber laptop feet to give it some grip. The specific model I purchased was 3M C6835; there are 16-packs you can purchase on eBay for a few dollars.

Keycaps
=======

The keycaps were purchased from [Signature Plastics](http://keyshop.pimpmykeyboard.com/products/full-keysets/dsa-blank-sets-1). The caps are PBT plastic, so they should last a while. They sell sets specifically for the ErgoDox; the ErgoDox Modifier set and ErgoDox Core set contain enough keycaps for both halves of the keyboard.

![Completed Build 3]({{ BASE_PATH }}/images/ergodox/14.jpg)

Cost
====

Sourcing everything myself took considerably more effort than just ordering a kit off Massdrop. Was it worth it?

* PCB: $30
* Teensy: $0
* Switches: $50
* Passive Components: $14
* Acrylic: $36
* Keycaps: $52
* **Total**: $182

Considering that the Massdrop group buy costs $200 without keycaps, it seems like sourcing parts yourself will save you a good amount of money.
