+++
title = "Shogun"
date = 2023-08-01T17:16:48-07:00
client = "FX Network"
tags = ["houdini", "dynamics", "ue5", "python", "vellum"]
tools = ["Houdini", "UE5", "Python"]
sections = ["Overview", "Maps", "Ocean Sims", "Armor Sims", "Asset Ingestion"]
active = false
draft = false
+++
# Overview
Like [Alien: Earth](/work/alien-earth), FX Network does the promotional materials for their shows, separate from the effects crew for the shows. So while I didn't do any work on the show itself, I did some things for the marketing materials, including simulations, renders, and tool development.
{{< youtube "dz9Ijf_PXlI" 540 >}}

# Maps
A live map at FX Network can be found [here](https://www.fxnetworks.com/shogun-japan-map).

The clouds started as an asset pack, that needed to be scattered and placed strategically, roughed up with other volumetric procedurals, and then given life through procedural volumetric animation, and to explore the appropriate material development and lighting for the context.
{{< video_filename "shogun-maps.mp4" >}}

# Ocean Sims
{{< video_filename "shogun-water.mp4" >}}

I made procedural ocean rocks for the waves to crash against. These waves then were used to source the whitewater sim. Because of the long and panning shot used, the whitewater sim was quite large in size and took a lot of optimization and little tricks to get as much out of as little as possible.
{{< video_filename "SHO1_wav000_fx_v017.mp4" >}}

# Armor Sims
Armor Sims were done using Vellum, attaching rigid pieces together with stiff but not too-stiff welds, to match the apparent strapped bindings that the armor had in order to match how it would actually fall.
{{< video_filename "shogun-armor.mp4" >}}
{{< video_filename "SHO1_hel300_fxArmor_v011b.mp4" >}}
{{< video_filename "SHO1_hel1100_fxArmor_v011.mp4" >}}

# Asset Ingestion
Layout of this and other shots like this were done in Unreal Engine 5. Out team inherited some sort of scene setup, but was unoptmized, and needed some things to be solved for real-time effects issues like Ambient Occlusion.
{{< video_filename "shogun-city.mp4" >}}

For the above shot, we had different artists working on assets for it that were scanned but needed to be constructed and then laid out.

We needed to keep server and local asset files synchronized and be able to push and pull them. For this, I built a custom Python GUI tool for UE5 to be able to do these things.