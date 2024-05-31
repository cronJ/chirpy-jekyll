---
layout: post
title:  "Robot platform for future development"
date:   2017-05-29 21:02:00 +0200
categories: electronics
---
Over the last weeks I was building a moving platform. The platform should serve as a base for future development with the Raspberry Pi and openCV.

For the platform I was using OpenBeam aluminum profiles. Therefor I got a nice kit with different pre-cut lengths. For the fixture I'm using the metal brackets from the kit and also self designed parts which I printed in PLA and PHA/PLA.

Currently the platform drives forward until an obstacles is in an 20cm range of the three Sharp distance sensors facing to the front. Then it backs up a little bit and turns to the right. If all three sensors are clear it continues driving forward. Two sensors are mounted with an angle so they can detect obstacles in front of the wheels. This results in two gaps between the sensors where no detection is possible. So the next step is to print an bumper with flexible material. This bumper then closes an contact when it is pressed against an obstacle. So in the end the platform can stop on direct contact.

And here a little video with the platform in motion: [[YouTube] Robot platform with OpenBeam](https://www.youtube.com/watch?v=Lk9jld7Yk3Y)
