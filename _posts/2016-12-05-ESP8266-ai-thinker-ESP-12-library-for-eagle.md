---
title: ESP8266 Ai-Thinker ESP-12 library for Eagle
date: 2016-12-05 19:35:00 +0200
categories: [Electronics]
tags: [electronics, eagle, library]
---

## Introduction

Started working on a little ESP8266 project again.
This time with an ESP-12 module from Ai-Thinker.
For that I created a new part in Eagle after the specifications from Ai-Thinker ([Technical Specifications](http://wiki.ai-thinker.com/lib/exe/fetch.php/modules/esp-12_wifi.pdf)).

My purchased module has a slightly different silkscreen as shown in the document.
On my module GPIO4 and GPIO5 are swapped, and pin EN is labelled CH_PD.
That should be checked before using the part.

## Library

Library: [https://github.com/cronJ/EagleLibrary](https://github.com/cronJ/EagleLibrary)

![ESP fits on footprint](/assets/img/2016/12/esp_fits.jpg)
![ESP and footprint](/assets/img/2016/12/esp_side.jpg)
![ESP pinout](/assets/img/2016/12/esp_pinout.jpg)
