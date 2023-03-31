+++
title = "Highland Park Spots"
tags = ["houdini", "dynamics", "TD"]
date = 2021-11-29T23:11:07-07:00
client = "Highland Park Whiskey @ Buck"
tools = ["Houdini", "FLIP"]
sections = ["Overview", "Simulation", "Rendering"]
active = false
peak = false
draft = false
+++

# Overview
For this project, I worked with Buck's Amsterdam office to create a series of tantilizing spots to showcase their 10, 12, and 18-year whiskies.

I was brought on very early on the project to oversee the creation of the primary effect of the commercials. I had to make sure the simulated effect was efficient enough to work with in a reasonable fashion to be able to iterate on quickly, as well as be able to send to the render farm and get final render results in a reasonable time frame.

{{< video 1 "18-year Spot" >}}
{{< video 2 "12-year Spot" >}}
{{< video 3 "10-year Spot" >}}

# Simulation
The primary effect is achieved by a very thin (2-3 layers) of FLIP particles that have the original image remapped to different physical properties like density and viscosity at the artist's direction, and also take artist input for flow direction and intensity using velocity painting. This allowed for each shot and image to be dialed in in a directable fashion.

{{< video 4 >}}
{{< video 5 >}}

When the effect was complete I needed to hand it off to freelancers to set it up for each shot, so it had to be inuitive enough for them to open up and work with.

{{< video 6 >}}
{{< video 7 >}}


{{< video 8 >}}
{{< video 9 >}}

On its own, the flip simulation did not provide a satisfactory smearing of colors when certain eddies would carry particles far away, and produced a grainy/sand-like result instead of a more fluid one that we were looking for. For this, I had to develop a custom solution that involved calculating fluid shear forces and apply a blurring operation only in those areas.

{{< image 1 "Shear map visualization, where I applied a blur to the colors of the simulation">}}

# Rendering

In addition to making sure the fluid motion was nice, I needed to be sure it was going to render as we expected. There was lighting in the scene so I had to give the liquid some interesting height and respond to lighting, as well as making sure the particles did not leave gaps when there was too much space.

The particle gaps was an interesting and efficient solve. I was able to transfer the particle colors to an underlying mesh that was able to fill in any gaps when particles got too far from each other, and was indistinguishable from the particles in the render.
