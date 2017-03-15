+++
client = "Space360"
date = "2016-10-12T00:53:46-05:00"
tags = ["animation", "logo", "4k"]
title = "Choice"
tools = ["3DS Max", "Octane Render", "Neat Video Denoiser"]

+++

[Space360](http://www.space3sixty.com/) asked me to create a logo animation for a new logo they designed for their client [Choice](http://www.choicetool.com/) as part of their marketing package.<!--more-->

{{< video 1 "The full logo animation">}}

Choice is a tool and mold company, so an important aspect of their branding is machines and lasers. To communicate this, Space360 decided to go with an almost completely steel environment, except for a deep red lake that matches Choice's identity primary color.

{{< image 1 "The camera starts low and at the bottom of their logo" >}}

{{< image 2 "As the camera follows the arc of their logo, the letters emerge from the floor after a laser slices them out" >}}

{{< image 3 "Traveling further, more letters are being created" >}}

{{< image 4 "Finishing the arc, the camera begins to lift into the sky" >}}

The logo was imported into 3DS Max as splines, which were then extruded and used to carve out from the metal ground plane.

{{< image 5 "As the camera lifts, you see the laser finish its last letter" >}}

I created a procedural brushed-metal material for the ground, which let the camera be very close and also very far without needing to worry about texture resolution or detail. This put Octane Render's bump mapping to the test, as the anisotropic nature of brushed steel is mimicked perfectly.

{{< image 6 "As the camera settles, a bright reflection passes overhead, transforming the letters from steel into their final less literal state" >}}

{{< image 7 "the materials in the scene transform into the final branding colors" >}}

Because of the highly reflective metal and large resolution, rendering was trickier than usual to optimize and make look clean. One technique I employed is called supersampling, where you render at a larger size than you intend to use and shrink it down to the final size later. This eliminates fireflies and hotspots that can be problematic for clean renders.

In addition to supersampling, I also processed the frames with [Neat Video](https://www.neatvideo.com/) which can use temporal sampling and also a very effective YCrCb colorspace for accurately separating content from the noise. This helps keep the real look of the reflections and surface of the metal while eliminating lots of the scattered rays from the render.
