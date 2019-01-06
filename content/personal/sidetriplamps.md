+++
title = "SideTrip Lamps"
tags = ["procedural", "houdini", "modeling", "art"]
date = 2018-10-30T21:50:42-08:00
tools = ["Houdini 17", "Octane Render"]
+++

"[SideTrip](https://skybase.xyz/sidetrip) is a series of paintings focused on two characters: Azure, a boy and Alex, the God of Hiding who travel in a lonely universe of everything and nothing. The two characters explore various worlds shaped by emotion, idea, and philosophy." — Project Director

It's a project directed by my friend [Yuya Takeda](http://skybase.xyz) where he frequently gets 3D artists to contribute to scenes. For this scene we were asked to contribute intricate designs in the style of turkish mosaic lamps.

We were provided reference material showing some real-life examples, appropriate level of modeling detail, and other constraints like size, making sure there was bulb geometry inside the lamp, etc. The constraints were important because the models were going to be collected from various modeling programs and imported into Modo for scene layout and final rendering in Octane Render.

{{< sbs >}}
  {{< image 1 >}}
  {{< image 2 >}}
{{< /sbs >}}

I knew from the beginning that I wanted to do a very procedural/parametric approach so that tweaking and adjusting parts of the lamp after its initial creation look. Naturally, Houdini was my weapon of choice. Sure enough, when a second, larger radius of the lamp crown was requested, it took no more than a minute to adjust, and most things are adjustable in the viewport so that it's artist-friendly.

The bulb texture was designed by Yuya Takeda (the director of the SideTrip project) and given to the 3D artists to work with and design their lamps with in mind.

{{< sbs >}}
  {{< image 3 >}}
  {{< image 4 >}}
{{< /sbs >}}

This was a fairly new modeling style for me that embraces a few concepts I've been trying to incorporate into my workflow: manual human-made decisions and elements, procedural elements that are best solved by a computer and not a human, and the synergy of the two to create something that doesn't feel randomly generated, but something that would have been impractical to be hand-crafted.

Along-side those concepts, I also thought about how these lamps were being created in reality, and modeled with that in mind. For instance, instead of starting with a cylinder and punching holes into it, I created a flat sheet of metal, did my edits to that, then rolled it up into a cylinder. In this way, some things that would have been more complex actually ended up being easier, just like in real life.

{{< image 6 >}}

For the first time in a while, I was having a lot of fun not being so caught up in code and the nuances of geometry like in some of my other fully procedural projects. In this, I was able to bring out a more care-free and artistic side of myself and keep adding more and trying to channel the real-life lamps but also create my own style.

This network is one of the lower nodes in the tree. My main workflow was to have skeleton geometry that represented lines and anchor points that things were generated from and instanced onto, and passed down the procedural tree. This let me easily manipulate this base skeleton geometry and generate my high-resolution details from that.

{{< image 5 >}}

[MOPs](https://github.com/toadstorm/MOPS) was a huge help for most of the instancing work. I used it to set up radial arrays of elements, and for the chains that needed to be rotated mostly orderly but also somewhat randomly.
