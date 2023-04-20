+++
title = "7up Spots"
tags = ["houdini", "dynamics", "particles", "fluids", "buck"]
date = 2023-02-11T00:19:31-07:00
client = "Pepsi Co. @ Buck"
tools = ["Houdini", "POPs"]
sections = ["Overview", "Fizz Simulations", "Carbonation Simulations"]
active = false
peak = false
draft = true
reel = true
+++
# Overview
Buck was hired to create new 7up spots for TV. I was tasked with a majority of the bubble and fizz dynamics for the spots.

# Fizz Simulations
The exterior fizz simulations were done by advecting a POPs simulation with a smoke solver simulation to generate fluid forces which helped give the fizz a sense of underlying flow and cohesion.

I also lightly used POP Fluids to ensure particles didn't interpenetrate and were able to bunch up in areas of high concentrations. Had the spot been much more focused on the details of the fizz, I might have merged bubbles to form larger ones, but it wasn't necessary for this.

{{< video 1 >}}

{{< video 2 >}}

{{< video 3 >}}

# Carbonation Simulations
The carbonation simulations were a bit different and didn't require a driving sister simulation for advection. They were driven using an upwards gravity/buoyancy force, a POP Wind node for some turblence, POP Fluids to allow the bubbles to bunch up at the surface, and bounded by an inverted SDF of the bottle geometry.

To improve interactivity of working, the bottle SDF was calculated high res at a static rest frame and then transformed with the animation to be able to give fast and accurate subframe collision data to the sim.

{{< video 4 >}}

{{< video 5 >}}

{{< video 6 >}}

{{< video 7 >}}

{{< video 8 >}}