+++
title = "Aircover Spot"
tags = ["houdini", "fx", "buck"]
date = 2022-11-14T10:43:06-07:00
client = "AirBnB @ Buck"
tools = ["Houdini"]
sections = ["Rain System"]
active = false
peak = false
draft = false
reel = true
+++
Buck was tasked with creating spots for AirBnB's Aircover, an insurance program for their hosts.
{{< youtube "HU-wFN42sMs" 540>}}

# Rain System
Similar to the [Amazon Halo Spot](/work/amazon-halo), we needed rain for this moody animation. In fact, I brought over the same system and tweaked it for our needs and added some additional controls.

There were many iterations on the look and feel of the rain drops, their splashes, and their puddles. Knowing this is always the case, the tool was designed for ultimate flexibility in mind, so it was easy to adjust. This is one of the many reasons I enjoy building and working with procedural systems instead of waiting and twiddling my thumbs for simulations to finish.

The biggest challenge was when the ground opens up in the middle of the spot. In a standard dynamics system this wouldn't be an issue, but with a procedural one, that animated data is more complicated to deal with since raindrops need to know where they'll be landing when they are created, but shouldn't be splashing in empty air by the time they get there so they need to look ahead in time.