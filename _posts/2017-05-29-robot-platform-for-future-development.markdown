---
title: Robot platform for future development
date: 2017-05-29 21:02:00 +0200
categories: [Electronics]
tags: [electronic, robot, 3d-print, openbeam]
---

## Introduction

Over the last weeks I was building a moving platform.
The platform should serve as a base for future development with the Raspberry Pi and openCV.

## The platform

The platform uses aluminium profiles from OpenBeam.
I got a nice kit with different pre-cut lengths.
For the fixture I'm using the metal brackets from the kit and also self designed parts which I printed in PLA and PHA/PLA.

## In motion

Currently, the platform drives forward until an obstacle is in a 20cm range of the three Sharp distance sensors facing to the front.
Then it backs up a little bit and turns to the right.
If all three sensors are clear it continues driving forward.
Two sensors are mounted with an angle so they can detect obstacles in front of the wheels.
This results in two gaps between the sensors where no detection is possible.
So the next step is to print a bumper with flexible material.
This bumper then closes a contact when it is pressed against an obstacle.
So in the end the platform can stop on direct contact.

## Video

And here is a little video with the platform in motion:

{% include embed/youtube.html id='Lk9jld7Yk3Y' %}
