+++
title = "Can't Live There"
tags = ["houdini", "fluids", "procedural", "framestore"]
date = 2026-01-27T17:18:00-07:00
client = "Homes.com @ Framestore"
tools = ["Houdini", "Redshift", "VEX"]
sections = ["Overview", "Space Station", "Mt Everest"]
active = false
draft = false
+++
# Overview
I was hired by [Framestore](https://www.framestore.com) to help them out with a Superbowl spot for [Homes.com](https://www.homes.com). I did the ketchup and sparks for the space station shot, and snow for a Mt. Everest shot which I believe ended up getting cut from the final spot, sadly.
{{< video_filename "homescom_cant_live_there_full.mp4" >}}
# Space Station
The ketchup simulation part came from a tracked ketchup bottle and emitted flip particles throughout the shot that blobbed up together. It connects the rest of the ketchup stream that is exists before the shot starts. One could pre-roll the sim if they needed to, but since we never see it emitted, I figured I would generate it procedurally with a spline and some realistic scattering of particles onto it. This allowed it to be easily art-directable and require no sim times. Over the duration of the shot, the particles stretch apart to simulate drifting in microgravity. Luckily, the drift is slow enough to also not require a simulation to solve.
{{< video_filename "homescom_cantlivethere_web.mp4" >}}

The sparks were done with a custom procedural actor-based VEX animation solution, which allows for particle-like behavior without any simulation, instead defining their animations as a function of time and space. I go over this in detail in my Houdini School course [HS241 Procedural Animation](/personal/hs241_procedural_animation/).

# Mt Everest
While I wasn't able to find a final clip of this anywhere online or in my files, a second shot I did involved the two actors stationed on Mt. Everest. They needed snow drifts coming off the mountain in a realistic fashion.

One of the main challenges of this was scene scale. Normally you can separate things into foreground and background elements, but because there was a continuous scene depth to very far away, using traditional volumes, particle scales, and other things was not easy. I had to break up the mesh and sims into smaller chunks, but it did let me focus on main areas to art direct them better instead of trying to wrangle all the physics in one network.

{{< image_filename "snow-halfrender.png" >}}

The other was realistic snow drift physics. The snow particles follow the wind, but traditional particle wind doesn't usually account for eddies, curling motion, and wind shadows. Luckily, a more recent version of Houdini did include wind shadows, which was interesting to experiment with. For the eddies and curls that come with that, I added some custom vortex forces along the mountain ridge line so that they got swept into a little wave-like shape following the mountain side.
