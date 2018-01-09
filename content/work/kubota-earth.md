+++
title = "Kubota Earth Anim"
tags = ["animation"]
date = 2017-10-17T22:49:56-08:00
client = "Ambidextrous Productions"
tools = ["3DS Max", "Octane Render", "Affinity Photo"]
active = false
peak = false
draft = true
+++

[Ambidextrous Productions](http://www.ambidextrous.net/) came to me for rendering a realistic globe animation for a commercial spot they were working on. They were creating a spot for Kubota Tractors, which provide a wide range of farming vechicles across the globe. The animation was urgent, and important, but the project completed on-time and successfully.

{{< video 1 >}}

## Shaders
Earth's surface was created with NASA's blue dot textures (diffuse, specular, bump). When the camera zooms down into the surface, I needed closer maps, so I grabbed some from Google Earth at different zoom levels and positioned them so they lined up. Because the lighting at that time is fairly noon-like, I didn't need any other maps besides diffuse to get a nice look.

The atmosphere was a variable-density SSS material with blue scattering and a little bit of schlick phase to match our atmosphere. Octane made beautiful work of the SSS and created soft red hues at glancing angles that really sell the atmospheric visuals.

## Map
This actually ended up being a more complicated part of the project that I didn't anticipate. The problem is that while the earth textures are an equirectangular projection that map perfectly onto a sphere, the maps provided with locations are "regular" (unspecified projection) isolated maps of the United States. Trying to align these two types of projections was difficult, but ultimately doable.

Another thing I had to fudge was Hawai'i's distance from the continental states. In reality, it's much further out into the Pacific Ocean and is awkwardly far away for a nice presentation. I manipulated the maps to bring it closer together.
