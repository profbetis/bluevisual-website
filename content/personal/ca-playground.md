+++
title = "Cellular Automata Playground"
tags = ["houdini", "math", "tool"]
date = 2020-02-16T20:21:53-07:00
tools = ["Houdini", "OpenCL", "VEX"]
sections = ["Overview", "Internals", "UI", "Artworks"]
active = false
peak = false
draft = false
reel = true
+++
# Overview
Cellular Automata has always fascinated me, and as a teenager I even programmed some recreations of [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life). After getting into Houdini and seeing some beautiful rules or patterns, I wanted a way to play around with rules and create my own artworks.

In particular, I was inspired by the concept of multiple rules on a singular canvas. I had seen someone implement this concept poorly, and I wanted to do it better. The inspiration took me down many deep rabbit-holes and late nights bleary eyed wondering how to fix something or implementing a new feature.

After getting the basics down, I was once again inspired by next-nearest-neighbor cellular automata, which instead of only having 256 rules, has over four billion (2³² = 4,294,967,296). Implementing the feature to be able to do this generalized some of my systems to be able to do n-nearest-neighbor (although anything past 3 is pretty much nonsense).

While my VEX-based setup was arguably efficient, it was running into a computational bottleneck. Realizing these systems are extremely iterative and parallelizable, OpenCL came to the rescue. This was a great crash course into understanding OpenCL code, being able to translate my VEX code into it, and ensuring parity between them. The OpenCL code can run over 100x faster than the VEX code, letting you design your canvases in virtually real-time, granted your trajectory bounds and grid resolution aren't too high.

You can find a more in-depth dive of Elementary Cellular Automata on [Wikipedia](https://en.wikipedia.org/wiki/Elementary_cellular_automaton).

# Internals
The internal node network is quite large, though organized by function pretty well.

{{< image 1 >}}

The blue area at the start is the grid data prep, ensuring the grid points have the proper groups, postioning, and attributes to feed into the kernel.

The large purple area on the top-right is the layer map creation. It can either use a noise, another cellular automata kernel, or an image to determine which cells will follow which rules.

The yellow and green boxes are where the main kernels are located. The VEX kernel is inside a compiled for-loop block for maximum efficiency, and the OpenCL kernel is in the green box. A simple switch flips between them based on user preference, though the default of using OpenCL is strongly recommended.

After the kernel runs, it's just a bit of cleanup and post-processing to remove cells that aren't within the canvas, color the points appropriately, and apply a sprite texture for nice viewport visualization. You can see here how each cell with a 1px sprite image with color can look great for the viewport very efficiently. Converting lots of points to quads was very slow, even with instancing.

{{< image 2 >}}
{{< image 3 >}}
{{< image 4 >}}

# UI
## Canvas
The canvas tab is where you set up the output and grid that you wish to run the kernel over. They're not generally relevant to the behavior of the system, just how it is output.

Internally, there is a COP2 Network that reads the grid point color attributes and converts them into pixels in order to output to an image file.
{{< image 11 >}}

## Rule
This is where most of the fun is. Here you can specify the kernel radius, the rule, and the layering system to build up as many rules as you want, each with their own independent noise pattern.

The 'Rule Base' parameter specifies how the rule string is to be interpreted. Because there are a finite number of rules, each rule has a single index, and in binary actually represents the rule logic itself. Rules for a nearest-neighbor kernel are 8 binary digits in length, while rules for a next-nearest-neighbor kernel are 32 binary digits in length. These can be quite unwieldy, so they can be set to decimal or hexadecimal formats for easier grokking. When the rule base is changed, a python script runs that converts all rule parameters to the new base automatically.

{{< image 12 "A simpler UI when not dealing with layers." >}}
{{< image 13 "Once layers are part of the equation, the UI reveals more controls to the user." >}}

## Kernel Parameters
The kernel parameters tab is not touched very often, but is there to control how the kernel runs. Here you can toggle using the OpenCL kernel.

{{< image 14 >}}

The Canvas Padding Cells and Border Style parameters are interesting. Essentially, when a cell wants to know the value of a neighbor outside of the canvas area, that data needs to be generated somehow. Usually if you just fill it in with zeroes, you'll start to get artifacts or strange patterns from it. One solution is to simulate a little bit outside the canvas area so that those artifacts get mitigated by more real cell calculations.

If aesthetics are your only goal, this is usually sufficient, however another interesting concept starts to come into play. Those extra padding cells also need data for their inputs, and those inputs needs data for their inputs. If you only have 4 generations, you only need 4 extra cells of padding on each side for a nearest-neighbor kernel, since nothing outside of that will be able to affect your canvas. If you raise your kernel radius higher though, you need to account for that as more and more cells will be able to affect the final row of the canvas.

## Visualization
This tab is for helping you understand what's going on under the hood. You can visualize the cell padding extents (trajectory bounds), the rulset map (useful when dealing with layers and trying to grok which cells are part of each layer), and the UV bounds (for when using an image map to control your layers instead of a noise function).

{{< image 15 >}}

Here you can see the effect of 'View Trajectory Bounds' looks like. These cells are necessary to compute the result within the canvas, but are deleted for output once they're used.
{{< image 16 >}}

# Artworks
{{< image 21 >}}
{{< image 22 >}}
{{< image 23 >}}
{{< image 24 >}}
{{< image 25 >}}
