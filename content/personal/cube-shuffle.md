+++
title = "Cube Shuffle"
tags = ["houdini", "procedural", "animation", "art"]
date = 2017-03-22T13:38:17-08:00
tools = ["Houdini", "Octane Render", "Filter Forge"]
# active = true
# peak = false
sections = ["Orthographic Pathing", "Edge Walking", "Textures"]
+++

This was one of my first forrays into Houdini and VEX, as the whole concept of open manipulatable data was so exciting (spoiler: it still is). I wanted to sort of "atomize" an object, and the reassemble it in a different order.

{{< vimeo 257441986 540 >}}

{{< image 5 >}}

# Orthographic Pathing
I'm always attracted to cubes, so that was the first shape I decided to try it with, and it grew from there. The geometry of cubes led me to want to make paths that only took cardinal axes one at a time. It does this by joining every vertex and its next neighbor by two intermediate points that lie on each axis independently.

{{< image 1 >}}
{{< image 2 >}}

It turns out there are multiple orders to do this in, so I added the order parameter to include every axis order, as well as a "Min/Max" order that chose the shortest/longest axis first.

# Edge Walking
Once the paths are generated, I needed a way to traverse them. Any Houdini-user should be shouting  "Carve SOP!!" by now. Normally I would too, but Carve disregards actual path length, so short paths take just as much time as longer paths. This led me to create yet another tool that walks along paths and creates a "position" point at that relative or absolute distance along that path.

You can also enable a velocity based motion which keeps objects animating in parallel moving at the same speed regardless of their path length. The only problem is that it's a simple functional solution and doesn't account for changing velocities. I may add that in the future.

{{< image 3 >}}
{{< image 4 >}}

# Textures
The tile texture was generated -mostly- procedurally in Filter Forge. Rather than making a complex parametric and randomizable tile generator, I sort of had ideas of what I wanted for this particular ornate pattern, and just accomplished it with procedural tools. I was working at a lower level to adjust settings instead of exposing every parameter to a more organized system.

{{< image 6 >}}

This is the only texture I used in the whole project. I was able to use transforms and image processing to get the most out of it.
