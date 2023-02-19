+++
title="USB to SATA Adapter From a Shucked EasyStore"
date=2019-06-25
transparent=true
+++

After shucking the HDD out of a WD EasyStore, I was left with the USB to SATA PCB. SATA hard drives take both 5V and 12V to drive the motor inside, and the PCB takes a 12V barrel jack input that it then steps down 5V. I wanted to use these adapters with SSDs, which don’t need the 12V rail, but since the 5V rail is derived from the barrel jack input, I still needed to plug in the power supply to use it.

By jumping the 5V from the USB input to the SATA 5V pin, I was able to bypass the power circuitry and use SSDs without the power supply plugged in.

{{ resized(img="pcb.png") }}
