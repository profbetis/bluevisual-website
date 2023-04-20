+++
title = "Arcane Worlds 2021"
tags = ["volumetrics", "dynamics", "particles", "buck"]
date = 2021-10-01T00:25:24-07:00
client = "Riot @ BUCK"
tools = ["Houdini"]
sections = ["Overview", "Volumetrics", "Embers", "Particles"]
active = false
peak = false
draft = false
reel = true
+++
# Overview
BUCK was hired to assist with VFX and CGI for the Arcane Worlds 2021 Opening.

I worked closely with the lead on this project to provide all the volumetric and particle effects for the scene.

{{< video 1 "A trimmed version of the Arcane Worlds 2021 Opening.">}}

Watch the full video on YouTube [here](https://www.youtube.com/watch?v=1OzoFq4Q3_c).

# Volumetrics
The clouds are primarily procedural and time-independent, requiring no simulation, and a very simple and art-directable input.

I built the base shape with low res sculpted geometry that defines the main mass of the clouds. I then turn it into a VDB and apply a cloudy noise to it, along with an offset that matches the general wind speed and direction.

Because the volume is viewed straight-on, I was able to optimize the VDB by using non-square voxels, stretching them in the Z-plane by a factor of about 4 to optimize export size and speed.

# Embers
The embers are procedural and time-independent as well, requiring no simulation. Additionally, they have a static point count which makes motion blur vectors and exports simpler and easier to work with.

First, linear particle trajectories are created in the direction of the wind, for the distance that they will travel before resetting. Points are then loosely scattered along these pathways, and then a flowing and evolving noise field displaces them along their path. When points begin and near the ends of their paths, they shrink in size to zero so that they can reset their position seamlessly. In this way, particle trajectories could be manipulated intuitively without simulation.

Because this method involves no simulation, particles often clipped through objects. To solve this, I created a low-res SDF of the scene geometry which I used to scale down particles as they neared the geometry, as well as veering their flow around it when possible.

# Particles
The embers aren't the only particles in the scene. When Jynx picks up the broken object, the blue crystal has subtle particles drifting off of it, as well as in motion when the gem bounces around the ground.

After the gem bounces off the ground energetically, the ball explodes in a brilliant flash of power. I was also responsible for the particles here.