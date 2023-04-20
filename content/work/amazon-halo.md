+++
title = "Amazon Halo"
tags = ["houdini", "fx", "buck"]
date = 2021-02-26T00:25:03-07:00
client = "Amazon @ BUCK"
tools = ["Houdini", "VEX"]
sections = ["Rain", "Ripples"]
active = false
peak = false
draft = false
reel = true
+++
In this project, I was tasked with doing some rain effects for the Amazon Halo commercial.
{{< youtube VRmBd51hfdI 540>}}

# Rain
One of the asks was for a particular droplet splash that hits the product. It needed to be able to be timed precisely and generate physically accurate secondary droplets. Because I hate simulating things, I decided I would design a procedural system for this that was seamless with the background rain.

The tool I made for this created two distinct pathways, one before the impact point, and one after for each of the secondary droplets, which needed to be parabolic instead of linear. 

{{< video 1 >}}

A similar rain system was made for the wider angle scene rain, just with less control over impact timing. Because it was procedural, a big obstacle I faced was needing to be able to have the rain stop on command. Simply reducing the raindrops of the system would result in raindrops disappearing mid-fall, so I had to come up with a way to have the rain drops complete their animation after the setting had been changed.

{{< video 2 >}}

# Ripples
The ripples were a separate but similar system that allowed for a number of ripples to be animating at once across a surface. These ripples too needed to be choked without cutting off ripples mid-animation.

To avoid close-but-separate puddles from sharing ripples that wouldn't have been able to propagate in real life, I temporarily shifted each puddle to a distant location in space where the ripples took place, then moved them back to their original locations before export.

{{< video 3 >}}