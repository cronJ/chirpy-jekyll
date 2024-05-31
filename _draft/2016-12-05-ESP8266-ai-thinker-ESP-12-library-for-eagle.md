---
layout: post
title: "ESP8266 Ai-Thinker ESP-12 library for Eagle"
date: 2016-12-05 19:35:00 +0200
categories: electronics
---
Started working on an little ESP8266 project again. This time with an ESP-12 module from Ai-Thinker. Therefor I created an new part in Eagle after the specifications from Ai-Thinker ([Technical Specifications](http://wiki.ai-thinker.com/lib/exe/fetch.php/modules/esp-12_wifi.pdf)).

My purchased module has an slightly different silkscreen as shown in the document. On my module GPIO4 and GPIO5 are swapped and pin EN is labeled CH_PD. That should be checked before using the part.

Library: [https://github.com/cronJ/EagleLibrary](https://github.com/cronJ/EagleLibrary)

{% include image.html path="/images/2016/12/" img="esp_fits" type="jpg" desc="ESP fits on footprint" %}
{% include image.html path="/images/2016/12/" img="esp_side" type="jpg" desc="ESP and footprint" %}
{% include image.html path="/images/2016/12/" img="esp_pinout" type="jpg" desc="ESP pinout" %}
