+++
client = "Space360"
date = "2016-10-12T00:53:46-05:00"
tags = ["animation", "logo", "4k"]
title = "Choice"
tools = ["3DS Max", "Octane Render", "Neat Video Denoiser"]

+++

[Space360](http://www.space3sixty.com/) asked me to create a logo animation for a new logo they designed for their client [Choice](http://www.choicetool.com/) as part of their marketing package.

Choice is a tool and mold company, so an important aspect of their branding is machines and lasers. To communicate this, Space360 decided to go with an almost completely steel environment, except for a deep red lake that matches their identity's primary color.

{{< image 1 "Camera starts out low and at the bottom of their logo" >}}
{{< image 2 "As the camera follows the arc of their logo, the letters emerge from the floor after a laser slices them out" >}}
{{< image 3 "Traveling further, more letters are being created" >}}
{{< image 4 "Finishing the arc, the camera begins to lift into the sky" >}}
{{< image 5 "As the camera lifts, you see the laser finish its last letter" >}}
{{< image 6 "As the camera settles, a bright reflection passes overhead, transforming the letters from steel into their final less literal state" >}}
{{< image 7 "the materials in the scene transform into the final branding colors" >}}

Because of the highly reflective metal and large resolution, rendering was trickier than usual to optimize and make look clean. One technique I employed is called supersampling, where you render at a larger size than you intend to use and shrink it down to the final size later. This eliminates fireflies and hotspots that can be problematic for clean renders.

On top of 150% supersampling, I also processed the frames with [Neat Video](https://www.neatvideo.com/) which can use temporal sampling and also processes images using a very effective YCrCb colorspace for accurately separating content from noise. This helps keep the real look of the reflections and surface of the metal while eliminating lots of the scattered rays from the render.
