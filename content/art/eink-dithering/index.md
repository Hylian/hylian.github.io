+++
title="Dithering for Inky Frame 7-color E-Ink Displays"
date=2025-06-03
transparent=true
+++

Let's dither this -

{{ resized(img="original.png") }}

\- into this

{{ resized(img="dithered.jpg") }}

but first, let's take a look at the display itself.

{{ resized(img="macro1.jpg") }}

* 7.3" EPD display (800 x 480 pixels)
* E Ink Gallery Palette ePaper
* ACeP (Advanced Color ePaper) 7-color with black, white, red, green, blue, yellow, orange.
* Ultra wide viewing angles
* Ultra low power consumption
* Dot pitch – 0.2 x 0.2mm

{{ resized(img="macro2.jpg") }}

* note how the square pixels cross the boundaries of the hexagonal e-ink cells

{{ resized(img="macro3.jpg") }}

* looks like a CMYG-type setup

{{ resized(img="macro4.jpg") }}

* orange pixels are softer and lower contrast than other pixels. hexagonal cells that are fully contained by the pixel appear darker. this effectively gives orange pixels antialiasing. note how adjacent orange pixels blend together.

with that tangent aside, let's experiment with dithering for this display in GIMP!

create an 800x480 canvas.

import this palette: [epaper-muted.gpl](./epaper-muted.gpl)

{{ resized(img="palette.png") }}

this is a 7-color palette of all the colors the display can show. 
I've manually muted the brightness of each color, lowering the gamma. by doing so, we are shoving the color space mapping around to get more effective color resolution out of our low contrast display.

now, select `Image > Mode > Indexed`

{{ resized(img="indexed.png") }}

use the custom color palette

{{ resized(img="indexed_menu.png") }}

hmm, it's close, but it looks a little odd

{{ resized(img="nijika_example1.png") }}

...WIP...
