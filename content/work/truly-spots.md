+++
title = "Truly Spots"
tags = ["houdini", "dynamics", "particles", "buck"]
date = 2020-12-14T00:16:39-07:00
client = "Truly @ Buck"
tools = ["Houdini", "POPs", "VEX"]
sections = ["Overview", "Droplet Simulation", "Lemon Spiral"]
active = false
peak = false
draft = false
reel = true
+++
# Overview
Buck was hired to do some mind-bendingly fun spots for Truly's new flavors. I was brought on in the middle of production to handle the dynamics for certain shots.

{{< video 1 >}}

{{< video 2 >}}

# Droplet Simulation
In this shot, the droplets were needed to splash away from the can and be gone where the fruits had touched the can.

{{< video 3 >}}

One of the difficulties in this ask was that the droplets on the can were already baked in as a static mesh. When simulating, I used a POP network for the physics, but had to transfer that motion to a mesh. The flattened droplet shapes once moved away from the can surface naturally had to morph into spherical shapes, so I calculated the volume per droplet and morphed it into a spherical shape of the same volume, to preserve mass.

In order to optimize render times and file sizes, I was able to detect which droplets would remain on the can versus the ones that would be affected by the simulation. I split the export into two parts, one static one with all the preserved droplets, and another animated one with the simulated droplets. This was a big help to the lighting team as it made my exports much lighter weight.

# Lemon Spiral
For this shot, I needed to take a cluster of strawberries and collapse them into a twisting unspiralizing lemon. While this shot appears simple and effortless on the surface, there were a few interesting things I had to solve for it to feel right.

{{< video 4 >}}

For the strawberries, they were turned into proxies and instanced as packed RBD objects and needed to shrink down towards the bottom of the lemon, as well as experience an axial force. I used an invisible cone collider to help shape the simulation and keep them from escaping the lemon. After the sim, I was able to instance the original high-resolution geometry back onto the physics proxies I used for efficient simulation.

The lemon spiral was a challenge on its own. I was given the solid basic lemon model and needed to procedurally spiralize and thicken it to give it its peeled appearance. The way I solved this was to create a generally spherical spiral spline in the shape I needed and then ray it onto the surface. I extruded this spline into a hollowed version of the lemon model, and used it to boolean. This disconnected the lemon surface and allowed me to use a Distance Along Geometry solve to get a spiraling mask which let me stretch and warp the lemon as a spiral.

The spiralization on its own was not enough to complete the effect. The physics of the strawberries did not fit the original lemon model's size, and too much spacing looked awkward. I used a smoothed SDF of the convex hull of the strawberry simulation to push out the lemon rind so that they smoothly wrapped the strawberries without penetrating into them. 