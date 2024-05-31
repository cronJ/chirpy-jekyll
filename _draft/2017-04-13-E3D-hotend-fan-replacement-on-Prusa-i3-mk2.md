---
layout: post
title:  "E3D hotend fan replacement on Prusa i3 mk2"
date:   2017-04-13 18:29:00 +0200
categories: 3d-printing
---
So my Prusa i3 MK2 is printing just fine and I get awesome results with PLA and nGen. But two things are missing to be an perfect printer which is living room compatible.

The y-axis in comparison to the x- and z-axis is really loud. A few days ago I read on the Prusa website about an upgrade kit which includes new rods and bearings to eliminate this issue. So I will keep this in mind until the lead time is acceptable.

Second thing is the fan from the E3D hotend. It is an 30x30 fan which runs in full turbine mode. After reading in the forum I stumbled about a post with other users which had the same problem. One critical point was getting the same airflow as the small fan, so the hotend doesn't clog during print. I found an nice 40x40x10 Noctua fan which fits my needs. It runs on 12V, creating an airflow of 8.2m³/h with an acoustical noise of 17.9dB(A).

For the adapter my co-worker printed an nice adapter in orange ABS ([http://www.thingiverse.com/thing:1827477](http://www.thingiverse.com/thing:1827477)).

# Upgrade
{% include image.html path="/images/2017/04/" img="removing_old_fan" type="jpg" desc="Removing the old fan" %}

{% include image.html path="/images/2017/04/" img="mounting_adapter" type="jpg" desc="Mounting the adapter" %}

The old fan was unscrewed and removed. With three M3x18 screws I mounted the new fan adapter.

{% include image.html path="/images/2017/04/" img="mounting_fan" type="jpg" desc="Mounting the new fan" %}

Now I attached the new fan to the adapter. Be careful with the length of your screws. If your screws are to long they will damage the other fan.

{% include image.html path="/images/2017/04/" img="connecting_fan" type="jpg" desc="Connecting the fan" %}

With my new fan came a short cable with a three pin connector. I removed the spiral wrap on the cables until I could get the fan cable plus the connector cable in there. The old fan wires where cut. Then I soldered the connector cable on the old wires and isolated the two wires from another.

{% include image.html path="/images/2017/04/" img="spiral_wrap" type="jpg" desc="Spiral wrap attached again" %}

For the last step I reattached the spiral wrap on all the cables. Check that the cable doesn't touch the heated bed.

# Noise level
Now that the fan noise is vanished the printer is really quiet. Only on the bed leveling procedure the y-axis makes noises. But now that the printer is so quiet I located a rattling noise which seems to come from the extruder. It only occurs some times during print and I couldn't locate it further. I reassembled all the screws on the extruder, because it sounds like a loose nut. But this doesn't help. I fastened the screws which mount the new fan which seems to fix it. But some times it occurs again.

But aside from that the printer now is quiet enough during print.
