+++
title = "Essentia Spot"
tags = ["houdini", "fx", "dynamics", "buck"]
date = 2023-03-14T10:46:10-07:00
client = "Essentia @ Buck"
tools = ["Houdini", "FLIP"]
sections = ["Splash", "Air Bubble"]
active = false
peak = false
draft = true
reel = true
+++
FLIP simulations for a short Essentia spot we were tasked with at Buck.
{{< video 1 >}}

# Splash
{{< image 1 >}}

I used a custom SOP microsolver to improve and give more elegant surface-tension dynamics.

{{< video 2 "A visualization for an alternate splash. The colors represent particle travel distance." >}}

# Air Bubble
I also did procedural dynamics for the air bubble inside the bottle which turned into a trickier process than I originally anticipated.

When I first approached the simulation, I had a decent smooth bubble geo, and a decently smooth bottle mesh, however booleaning them always resulted in chunky terrible geo no matter how much I futzed with it.

{{< image 2 "The result of a regular boolean of the bubble and the bottle.">}}

I had an idea to smooth the intersecting edges, project them back onto the bottle, and then snap the edge points back to the smoothed reprojected points.

{{< image 3 "The smoothed and reprojected intersecting edge loop.">}}
{{< image 4 "The resulting boolean after moving the intersecting edge points to the smoothed edge.">}}

As you can see in the final video, the boolean edges are smooth and very stable!