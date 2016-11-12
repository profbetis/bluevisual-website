+++
client = "AminoCat"
date = "2015-11-01T17:50:45-04:00"
tools = ["3DS Max", "Octane Render", "Adobe After Effects", "Adobe Photoshop"]
tags = ["logo", "animation", "3D"]
time = "2015 Nov"
title = "AminoCat Logo Animation"

+++

For this project, [AminoCat Entertainment](https://www.facebook.com/AminoCat-Entertainment-135792499865038/) needed a new and updated logo animation to put on their films. The studio wanted the output to be 4k, putting a foot forward in the UHD world.

{{< video 1 >}}

The client originally did not have a solid idea on what they were looking for, so together we worked to find an appealing idea. Being a film studio, we of course needed to incorporate a film strip into the animation.

{{< image 1 "Intro film strip">}}
{{< image 2 "Start of film burn">}}
{{< image 3 "The film melting, stretching, and tearing">}}

The film melting was a big challenge material-wise. I used a combination of bitmaps and procedural noise to drive a semi-physical heat/melting map. At the same time, I distorted the film strip's polygons to warp and stretch as it melted away. For the logo underneath, I used an occlusion/dirt map to darken the edges of the hot glowing logo to emulate how hot metal cools faster at edges exposed areas.

{{< image 4 "Logo text being created">}}
{{< image 5 "Logo cooling and lighting fading in">}}
{{< image 6 "Final logo settle">}}

Like most of my projects, I used 3DS Max to create the scene and <a href="https://home.otoy.com/" target="_blank">OTOY's Octane Render</a> for rendering. Because GPU rendering's main problem is noise, I use <a href="https://www.neatvideo.com/" target="_blank">Neat Video</a>, a great hardware accelerated denoising plugin that works on render noise and sensor noise alike. It's saved me lots of hours of render refinement. You can see a comparison video I made <a href="https://vimeo.com/139969530" target="_blank">here</a>.
