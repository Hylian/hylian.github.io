+++
title="Therapy Light"
date=2019-07-22
transparent=true
+++

{{ resized(img="therapylight.jpg") }}

## Background
I suffer from Delayed Phase Sleep Disorder (DPSD), which basically means a day in my body’s circadian rhythm is significantly longer than 24 hours. This results in me going to sleep later and later until eventually it just cycles around and repeats all over again.

I started looking into therapy lights to try and help align my sleep schedule. Most therapy lights are typically designed for Seasonal Affective Disorder (SAD), a mood disorder caused by reduced sunlight in the winter months. The lights come in a few types:

* **Full Spectrum**: Designed to replace sunlight by using lights across many different wavelengths
* **Blue Light**: Targets specific blue wavelengths for SAD. Studies show that you need less total light output than a full spectrum light when treating SAD. Basically the opposite of f.lux.
* **Green Light**: Same idea as blue light, but potentially less harmful for your eyes. These only started appearing in the last 10 years or so.

Since I was trying to fix my sleep, I decided to go with green light. Blue light can eye damage, such as macular degeneration, and that seems a bit scary when you’re going for 10,000 lux in a therapy light.

I saw this paper in Nature that shows the melaopsin receptors in your eyes is highly receptive to 510 nm green light, while not being terrible for your eyes. Melanopsin are the photopigments in your eyes that suppress melatonin in your body, so that’s what you want to target for circadian rhythm.

Here are some graphs from the paper:

{{ resize(img="graph1.png", width=400) }} {{ resize(img="graph2.png", width=400) }}

I also saw this product, the Re:Timer, which seemed to match what I want. However, $200 seemed a little steep for some green lights, and you had to wear it on your face whenever you wanted to use it.

Instead, I decided to make my own light that would mount above my bed and wake me up every morning to get me out of bed and align my sleep cycles. I also wanted it to be compatible with my existing Philips Hue system, since I already use the Hue app to schedule lights to turn on in the morning.

## Electronics

{{ resized(img="breadboard.jpg") }}

To start with, I used the Mesh Bee from Seeed Studio. This uses an NXP chipset that supports the ZigBee Pro protocol, the same as Hue bulbs. I then flashed this binary from PeeVeeOne to have it act as a Hue bulb.

For the LED driver, I used this module from Aliexpress. These boards take a PWM control signal and drive a bunch of series LEDs in constant current mode. 100% duty cycle is actually fully off on this board, while the Mesh Bee firmware is configured the opposite way. I tried to modify the firmware source, but the NXP SDK had changed in the meantime and there was some weird GUI based configurator that I couldn’t figure out, so I ended up just sticking a hex inverter between the Mesh Bee and the driver.

For the LEDs themselves, I got these 510 nm bead LEDs from Aliexpress and wired them all up in series straight to the driver board. They’re rated at 3W each, with 10 LEDs, for a total of 30W.

Finally, for power, I cut the tip off an old HP 36V power brick and soldered that to the driver board. I then used the D24V5F3 3.3V buck converter from Pololu to power the Mesh Bee and the inverter.

## Enclosure

{{ resized(img="enclosure.jpg") }}

I designed the enclosure to mount above my bed in OpenSCAD and laser cut it in plywood. I also laser cut a diffuser for the lights with some frosted 3mm acrylic. The whole build is pretty hacked together right now, but it does the job. I was also a bit concerned about eye strain, so I covered it with kapton tape, as some online sources seemed to suggest that kapton tape will absorb blue light.

## Results

{{ resized(img="final.jpg") }}

Pretty good! I can’t look directly at the lights, or they’ll leave trails in my vision for minutes after. I was able to schedule the lights in the Hue app and they woke me up in the morning. I also felt more energetic after lying under them for several minutes.

I also bought a used Extech lux meter and measured the lux output at eye level. It was reading about 466 lux. Commercial therapy lights typically target a melanopic lux of 1500 lux or more, where melanopic lux is the light that will actually be absorbed by melanopsin. Melanopic lux is calculated as a multiple of the actual lux output, so outdoor light might have a M/P value of 0.5, while just green light is more like 2.0. For example, here are the measurements of the Re:Timer on f.luxometer (which is an awesome website, by the way!) Since my lights are also 510 nm, assuming a M/P value of 2.0, I’m getting 932 melanopic lux!


