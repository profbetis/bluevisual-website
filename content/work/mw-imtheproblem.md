+++
title = "Morgan Wallen Tour"
tags = ["houdini", "projection mapping", "music", "rendering", "procedural"]
date = 2025-05-27T17:17:25-07:00
client = "Morgan Wallen @ Raw Cereal"
tools = ["Houdini", "Karma", "Copernicus"]
sections = ["Overview", "Bubble Simulation", "Glass Material"]
active = false
draft = false
+++
# Overview
[Raw Cereal](https://www.rawcereal.com) is a event design studio that creates larger-than-life productions employing new technology for fully immersive experiences. They hired me to help them with their event for Morgan Wallen.
{{< video_filename "HOUSTON_DAY_1_thisbar_front.webm" >}}

Each artist had their own song to fully own for graphics. We were given 3D and 2D templates for the stage screens and built our effects using them. My song was "This Bar", and it was designed to create the effect of turning the stage surfaces into frosted beer glass with live bubbles.

# Bubble Simulation
The bubble simulation was actually finished somewhat early on into the process. I used a particle simulation with a bit of POP fluids for collision behavior, and flocking microsolvers to create breaking and flowing clusters and strands of bubbles as they ascended.
{{< video_filename "mwt_fx_thisbar_v002_sim_web.mp4" >}}

In addition to this, we made it a 30 second loop to cut down on required simulation and rendering time. Looping the simulation was doable, but required a bit of creativity. The birth of the bubbles had to cut off before the simulation ended to allow the start of the looped sim to fill in the space behind it to create a seamless effect.
{{< video_filename "mwt_fx_thisbar_v016.floor_preview_web.mp4" >}}
<!-- {{< image_filename "mwt_fx_thisbar_v021_floorscreen.jpg" >}} -->

# Glass Material
Surprisingly, the majority of the effort spent on this project was actually the look development, lighting, and material of the glass.
{{< image_filename "mwt_fx_thisbar_v025_upperscreen.jpg" >}}

I developed the material in Houdini's Karma renderer. It takes a raw bumpmap for displacement, which it then blurs a bit to give it a softer glass feeling. Also, there is a procedural condensation layer with maps generated via the new Copernicus. It took the condensation droplet geo, trailed it upwards, distorted it, and tapered off the trail to give it a realistic mask on the frost effect.