+++
title = "Brawlidays 2021"
tags = ["houdini", "dynamics", "particles", "volumetrics", "buck"]
date = 2021-12-08T13:20:51-07:00
client = "Supercell @ Buck"
tools = ["Houdini", "POPs", "DOPs", "VEX"]
sections = ["Overview", "Snow Explosion", "Other Snow"]
active = false
peak = false
draft = false
reel = true
+++
# Overview
Supercell hired Buck to create an entirely 3D animation to advertise their new holiday skins for the winter holidays. I was tasked with creating various snow effects for the animation.

{{< video 1 "An exciting moment that releases the snow into the scene.">}}

{{< youtube GVWLG1Z9B1Y 540 >}}

# Snow Explosion
{{< video 2 "Snow explosion fx in viewport.">}}

For the snow explosion, I employed a few different experimental techniques to assemble it. The base of the simulation actually starts as procedurally generated ballistic paths. I was able to shape and distort these ballistic paths to better match notes about shape and size of the explosion without needing to worry about the physics of creating such shapes.

I then used the ballistic paths to instance and move chunks along them in a semi-physical but mostly controlled manner. This animation was then used to advect and generate the snow volume smoke simulation.

Because this effect worked best as combination of volumes and particles/geometry, I then used the snow simulation to advect the particles of various masses to achieve a unified motion and look.

# Other Snow
{{< video 3 "Procedural snow used as an asset for various scenes after the snow explosion.">}}

{{< video 4 "In the final rebuilding scene, fire extinguishers blow the snow around in flurries.">}}

{{< video 7 "The fabric pieces of Tick's scarf were eventually replaced with chunks of snow.">}}

{{< video 6 "The snow in this shot was eventually cut due to plot inconsistencies (he hasn't exploded to generate the snow yet)">}}

You can find Buck's project page for this project [here](https://buck.co/work/brawl-stars-brawlidays).