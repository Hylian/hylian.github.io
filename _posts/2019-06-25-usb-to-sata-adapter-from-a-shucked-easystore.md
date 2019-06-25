---
layout: post
title: "USB to SATA Adapter From a Shucked EasyStore"
description: ""
category: ""
tags: []
---
{% include JB/setup %}

Shucking is where you pull hard drives out of consumer USB hard drives, like the WD [EasyStore](https://www.bestbuy.com/site/wd-easystore-8tb-external-usb-3-0-hard-drive-black/5792401.p?skuId=5792401). You can usually get drives significantly cheaper than the sticker price this way, albeit without any warranty.

After shucking an EasyStore, I was left with the PCB that does the USB to SATA conversion. SATA hard drives take both 5V and 12V to drive the motor inside, and the PCB takes a 12V barrel jack input that it then steps down 5V. I wanted to use these adapters with SSDs, which don't need the 12V rail, but since the 5V rail is derived from the barrel jack input, I still needed to plug in the power supply to use it.

By jumping the 5V from the USB input to the SATA 5V pin, I was able to bypass the power circuitry and use SSDs without the power supply plugged in.

![PCB with wire jumping USB power to SATA power]({{ BASE_PATH }}/images/sataconverter.png)
