+++
title = "Paint Tests"
tags = ["study", "houdini", "dynamics"]
date = 2018-02-18T20:29:07-08:00
tools = ["Houdini", "Octane Render", "After Effects", "Filter Forge"]
active = false
peak = false
sections = ["Dynamics", "Textures"]
+++

This was a test I did of spilling paint on something. I originally planned for it to be distinct layers of colors on top of one another, but it naturally developed into the smoothly evolving change of one paint color to another.

{{< vimeo 255840349 540>}}

# Dynamics
This was one of my first serious forrays into FLIP simulations, and I learned a lot about fluid meshing, reseeding, and FLIP sources. This amount of simulation was probably overkill looking back, as the fluid mesh was much denser than the surface tension allowed detail for, and I could have gotten a similar blobby look from subdividing during render for a lighter alembic file.

Most of the fluid's behavior comes from it's fairly moderate viscosity, surface tension, and particle separation. The particle separation provided the necessary outward force for the fluid to go out and spread across the cube instead of piling up in a heap at the nozzle.

If you look at the invisible nozzle at the top of the video, you notice it moving around a bit. I gave it a simple noise-based motion but it really helped to break up the sim and give a natural and non-uniform pattern to the colors, even though the main body of the fluid seems to be unaffected by it. I also added a more subtle noise to the source volume that breaks up the stream a bit to give a varying flow.

## Final Particle Count: 21,724,899
## Final Mesh Vertices: 597,716
{{< video 1 "Here's a playblast showing the particle age as a gradient from black to white" >}}

I think what's personally interesting is to see where the early particles end up going throughout time. In real life you can never really visualize or track those kinds of things.

# Textures
Colors are actually done post-sim using the birth-time as an attribute and using that as a UV coordinate to look up a painted color spectrum texture to get realistic paint colors.

{{< image 2 "The paint spectrum photograph used to sample colors from.">}}

There's no particular reason for the tiles the way they are, I just thought they'd look nice as something for the paint to spill onto.
{{< image 1 "Various texture maps for the tiles, generated procedurally in Filter Forge.">}}
