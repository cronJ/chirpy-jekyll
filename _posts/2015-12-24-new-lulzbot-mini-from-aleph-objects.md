---
title: New Lulzbot Mini from Aleph Objects
date: 2015-12-24 11:46:00 +0200
categories: [3D-Printing]
tags: [3d-printing, lulzbot]
---

After printing a good amount of filament with the GRR Neo, I’m really happy with a 3D printer as another tool in my drawer.
So the investment was worth it.
From time to time I’m printing a part from Thingiverse, but mainly I print parts I created by myself.
Creating your own part is most of the time easier than searching for a part on Thingiverse, which serves your needs.
As a bonus you can consider quirks of your printer into the part design, to prevent print failures.
All my parts I create currently with the help of OpenSCAD or Autodesk Fusion 360.

But as good as the GRR Neo is, there are a few downsides to it.
To receive a successful print, you have to take care of the bed leveling.
How it works I wrote in this article.
Most of the time, I had to adjust the first layer height during the print.
One minor annoyance was the filament holder, which is located on the backside.
So it was not easy for me to switch the filament.
And when you had switched the filament roll, you had to fiddle the filament in the Bowden tube, which also was mounted on the back.

These are the only two things I don’t like.
One was simply because of the place where the printer was located.
I was mainly happy with the printer.
Also, when a hot end blockage occurred, it was easy to correct.

## New requirements

After some time in a new hobby, the requirements for the tools are changing.
Test prints of PLA smartphone cases were ripped apart when trying to mount it on a phone.
Flexible filament is available but can’t be used with my printer because of the Bowden tube.
Other materials like ABS, HIPS, Nylon or filament with wood, copper or bronze properties are also available.
A new printer should be able to print all this new materials.

One printer I had already in mind, was the Lulzbot Mini from Aleph Objects.
This one features an automatic bed leveling system.
Therefor, each corner of the print bed has a little metal disc.
The hot end is used as an electrical probe to touch the metal discs and closes the electrical circuit.
With the height data from these four points, the software calculates where the print bed is located.
During the print, the z-axis is corrected on-the-fly.
The bed leveling process is done before each print without human intervention.

With this printer, the bed leveling will be no issue anymore.
But what about the other properties and features of the printer?
The print area is 152 x 152 x 158 (L x W x H), which is roughly the same as on my GRR Neo.
This print area was enough for everything I print.
Until now, there were only two parts I printed, with a length of 150 mm.
The filament holder is mounted on the top and easy reachable.

The Lulzbot Mini features a full metal hot end which can reach 300 °C.
With this temperature it can handle most of the newer materials (e.g. Nylon 225 °C – 270 °C).
But all the materials require a heated print bed.
The Lulzbot Mini has one which can reach a temperature of 120 °C.
It has a direct drive extruder sitting over the hot end, so a filament change is easy.

For the print, it requires a USB connection to the software.
But with the help of [OctoPi](https://github.com/guysoft/OctoPi) it can be used without a PC.
The Lulzbot Mini requires 3 mm filament, so I can’t use my old 1.75 mm filament.

So, after weighing the pros and cons, I decided to buy one.

## The new one

The new one has replaced my GRR Neo.

![Lulzbot Mini - Printer](/assets/img/2015-12-24-lulzbot-mini/2015-12-24-lulzbot-mini-printer.jpg)

Currently, printing a holder for my trunk.
The material used is black HIPS.
Opposite to PLA it has a matted surface.

![Lulzbot Mini - Printing](/assets/img/2015-12-24-lulzbot-mini/2015-12-24-lulzbot-mini-printing.jpg)

After the print, the print bed drives to the back and waits until it is cooled down to 60 °C.
Then it drives forward, so you can remove the print.

![Lulzbot Mini - Octopus](/assets/img/2015-12-24-lulzbot-mini/2015-12-24-lulzbot-mini-octopus.jpg)

This octopus comes with the printer and was used as a calibration print by the manufacturer.

![Lulzbot Mini - Rocktopus](/assets/img/2015-12-24-lulzbot-mini/2015-12-24-lulzbot-mini-rocktopus.jpg)

The `rocktopus` is located on the USB stick which comes with the printer.
It is used as a test print.
For the print there is one meter of yellow HIPS in the delivery.
It is printed with half speed.
