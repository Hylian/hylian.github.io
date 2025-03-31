+++
title="Leica M10 Battery Teardown and Reverse Engineering"
date=2025-03-31
transparent=true
+++

The Leica M10 family of cameras use the proprietary BP-SCL5 battery. Of course, Leica being Leica, these batteries cost an eyewatering $200 a pop. Even after many years, a third-party battery option has never materialized. These batteries are also often hard to find in-stock. Li-Ion batteries are consumables with a limited lifespan, and Leica is the only game in town, purely due to their own decision to DRM the battery. While there's a discussion to be had about "luxury" brand pricing, it remains that the BP-SCL5 is the only battery I have to baby around due to not having a big pile of ready-to-go spares. Let's take a peek at what kind of DRM is inside this thing.

```
Disclaimer: Lithium-Ion batteries are a fire hazard, and care should be taken when handling them. This post is for informational purposes only.
```

## Protocol Reversing
{{ resized(img="breakout_1.jpg") }}

The BP-SCL5 uses a single data pin between `+` and `-` to communicate with the camera body. When this pin is taped over, the camera refuses to boot.

Using some magnet wire to break this pin out, we observe that:
* The camera communicates with the battery approximately every second.
* When the pin is grounded, this battery check fails, and the camera powers off.
* The protocol appears to be Dallas 1-Wire.

{{ resized(img="breakout_2.jpg") }}

{{ resized(img="scope_1.jpg") }}

{{ resized(img="scope_2.jpg") }}

When hooking up to a Saleae, I had to use an instrumentation op-amp to boost the signal to an appropriate voltage. (Unfortunately, I've lost track of the actual capture. I'll update this post if I manage to find it.)

{{ resized(img="saleae.jpg") }}

## Teardown
Now, let's teardown an (already dead) M10 battery and see what's inside.

We see four programming pins hidden under a sticker. I haven't investigated these any further.
{{ resized(img="pogo_pins.jpg") }}

After some quality time with the snippers, I finally managed to get the shell off. It's certainly well-built. The plastic was ultrasonically welded shut and the negative space was filled with silicone.
{{ resized(img="teardown.jpg") }}

Some more scraping frees the PCB, giving us a look at the ICs.

{{ resized(img="macro.jpg") }}

{{ resized(img="microscope.jpg") }}

## Analysis
The battery uses a [DS2776 "2-Cell, Fuel Gauge with FuelPack, Protector, and SHA-1 Authentication"](ds2775-ds2778.pdf) from Maxim. The fuel gauge protects the bare battery cells and reports a bunch of useful measurements about the battery, such as discharge current, temperature, and estimated cell wear. The chip communicates with the host via Dallas 1-Wire.

This fuel gauge in particular has a SHA-1 authentication feature. Let's see what the datasheet has to say about it. 

{{ resized(img="ds-0.jpg") }}

{{ resized(img="ds-31.jpg") }}

{{ resized(img="ds-32.jpg") }}

Each chip is provisioned with a secret key at the factory. The host writes a 64-bit challenege to the chip, and the chip responds with a SHA-1 Message Authentication Code (MAC). The MAC can be computed using just the secret or with the chip's serial number included as a salt.

Given this, I believe all copies of the battery should have the same shared secret. If the serial number is used as a salt, it would prevent replay/rainbow table attacks, but there's no getting around the fact that every M10 needs to work with every battery.

Either way, we would need to read the secret from the chip to do anything. Of course, doing so is non-trivial, as the chip has readout protection. It'll need some sort of side-channel attack. I found this paper by David Oswald from the University of Birmingham: [Side-Channel Attacks on SHA-1-based Product Authentication ICs](cardis_2015_sha1_paper.pdf). Oswald describes successful power analysis attacks on Maxim ICs with SHA-1 authentication over Dallas 1-Wire. I suspect the authentication IP used is very similar to the one in our DS2776. I could see a sufficiently motivated individual with a [ChipWhisperer](https://www.crowdsupply.com/newae/chipwhisperer-husky) managing to retrieve the key - I'm just not that individual. Remember, key material is not copyrightable. :)

