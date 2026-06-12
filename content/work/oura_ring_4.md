+++
title = "Oura Ring 4"
tags = ["projection mapping", "houdini", "framestore"]
date = 2024-11-11T00:19:31-07:00
client = "Oura @ Framestore"
tools = ["Houdini"]
sections = ["Overview", "Aurora", "Custom Preview Tool", "Render Wrangling"]
active = false
peak = false
draft = false
reel = false
+++
# Overview
Framestore approached me to do some procedural volumetric aurora for their latest project for [Oura Ring](https://ouraring.com) on the [Sphere](https://www.thesphere.com) in Vegas.

{{< video_filename "framestore_ouraring4_aerial.mp4" >}}

I have known about projection mapping for some time but had only done one previous project involving it, which didn't present too many technical challenges apart from a cyclindrical-perspective camera. In contrast, this project helped me understand and face a deeper set of challenges for 360 mapping onto a sphere.

# Aurora
The aurora was fully procedural and involved intuitive art-directable controls, like a single simple spline for location and shape, and then had layers of duplication and noise for a more realistic and dynamic feeling. 

{{< video_filename "sphere_oura_auroratests_5up_v015.mp4" >}}

In addition to the volumetric aurora, there was also a digital dot matrix effect that accompanied it. While not shown in this next viewport preview, the final effect did have a subtle motion and flow to the grid. I rendered it as a separate pass with different attributes applied to the Red, Green, and Blue channels so that compositing could do interesting things with it that they saw fit.

{{< video_filename "oura_Aurora_v011_kw.mp4" >}}


# Custom Preview Tool
One of the unique challenges of this project was getting a clear idea of how the auroras I was creating would look on the final sphere. What most other people were doing was doing preview renders out of the spherical rendering camera and then importing it into an After Effects comp to see different views of it (pictured above). The problem was, this was way too slow for me to iterate and hit notes with.

My solution was to create a custom visualizer inside Houdini itself. I just created a sphere with a decent number of points (80k or so) and raytrace along outwards to essentially "render" the volumetric aurora to the points, and apply a simple color ramp to it to approximate the final render colors. This let me and the art directors see things quickly and give informed notes.

{{< image_filename "oura_ring_4_viewport_01.png" >}}

# Render Wrangling
After the aurora effects were done and my contract was closed, I was brought back on for a bit of time to help deal with render wrangling for various materials and states of the ring in different scenes and ensure efficiency.

I set up a simple but effective HDA to allow animation of a few key controls that allowed us to work at a higher abstract level instead of worrying about the details of tiny things like checkboxes deep in material networks, object render flags, file paths, etc.  