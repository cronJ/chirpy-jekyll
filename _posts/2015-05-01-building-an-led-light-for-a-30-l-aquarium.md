---
title: Building an LED light for a 30 l aquarium
date: 2015-05-01 15:30:09 +0200
categories: [Electronics]
tags: [electronics, 3d-printing]
---

I wasn’t really happy with the light which comes with my 30 l aquarium.
But I have a lot of white 3 W LED lying around.
So we will build a new LED light for the aquarium.

## Bill of Materials

- 3x [Aluminum heat sink for 4 x 3 W LEDs](http://www.amazon.de/gp/product/B00L11IFBS?psc=1&redirect=true&ref_=oh_aui_detailpage_o08_s00)
- 1x [Constant current source 11-20W 350mA](http://www.amazon.de/gp/product/B00E5YVFNS?psc=1&redirect=true&ref_=oh_aui_detailpage_o07_s00)
- 12x 3 W LED on a star PCB
- 2x [`nano_cube_led_heatsink_clamp_part1_v2.stl`](/assets/files/2015-05-01-nano-cube-led/nano_cube_led_heatsink_clamp_part1_v2.stl)
- 6x [`nano_cube_led_heatsink_clamp_part2_v1.stl`](/assets/files/2015-05-01-nano-cube-led/nano_cube_led_heatsink_clamp_part2_v1.stl)
- 12x [`nano_cube_led_reflector_v1.stl`](/assets/files/2015-05-01-nano-cube-led/nano_cube_led_reflector_v1.stl)
- Thermal paste or thermal glue

## Building the new LED light

First, we place the heat sinks into the clamp and fix it with the second part.
So we have it easier to work with the heat sinks and the cables.

Second, we add the thermal paste to the LEDs and place them on the heat sink.
Try to orient the polarity of the LED in an alternating pattern.
Then we can solder the cables easily to the LEDs later.

![Nano Cube LED - heat sink](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-heatsink.jpg)

If we use thermal paste instead of thermal glue, we can fix the LEDs with two drops of superglue to the heat sink.

![Nano Cube LED - glued](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-glued.jpg)

Now we can solder the cables to the LEDs.
We solder all 12 LEDs in series.

The last step is to place the reflectors on each LED.
They should just clip on the heat sink.

## Comparison of both lights

So, here is the old `Dennerle Nano Cube 11 W` light, which comes with the aquarium:

![Nano Cube LED - old light](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-old-light.jpg)

And here with the new light:

![Nano Cube LED - new light](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-new-light.jpg)

And here are some pictures from different angles of the finished light:

![Nano Cube LED - top](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-top.jpg)

![Nano Cube LED - right](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-right.jpg)

![Nano Cube LED - left](/assets/img/2015-05-01-nano-cube-led/2015-05-01-nano-cube-led-left.jpg)
