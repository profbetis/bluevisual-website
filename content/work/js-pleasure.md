+++
title = "Jolin Tsai Tour FX"
tags = ["projection mapping", "dynamics", "music", "houdini"]
date = 2025-12-26T17:17:38-07:00
client = "Jolin Tsai @ See You Later"
tools = ["Houdini", "Redshift", "Deadline", "Linux/Bash"]
sections = ["Overview", "Simulations", "Procedural Animations", "Rendering", "Farm Management"]
active = false
draft = false
+++

# Overview
[See You Later](https://seeyoulater.la) took on a massive project for [Jolin Tsai](https://en.wikipedia.org/wiki/Jolin_Tsai) to fully 3D animate and render content for a 200 foot wide by 45 foot tall 4-section screen for her [Pleasure Tour](https://en.wikipedia.org/wiki/Pleasure_World_Tour) shows, which first debuted at the Taipei Dome in Taiwan.

The album centers on the concept of the seven deadly sins, exploring multiple dimensions of desire, portraying it as both an inherent human instinct and a driving force toward transcendence through pleasure.

{{< video_filename "jtpt_highlights_official.webm" >}}

Our animation team was quite small of the scale of the project, but we managed to pull through. Each artist had their own chapter to work on and do everything for, from modeling, animation, simulation, lighting/materials, and rendering. We had about 2.5 months to finish everything.

Mine was the second chapter, "Pleasure Echoes Pain", which was set in a volcanic-rocky space filled with embers, fire, and crumbling rocks, so I had a lot of simulation to do! I handled everything in this chapter apart from the crow animations.
{{< video_filename "jtpt_full_clipped_song2.mp4" "Pyro fx, embers, crow transition">}}
{{< video_filename "jtpt_full_clipped_song3.mp4" "Pyro bursts, materials, lighting">}}
{{< video_filename "jtpt_full_clipped_song4.mp4" "Crumbling wall, pyro bursts, embers">}}
# Simulations
For this job, I decided to try to do all pyro simulations in the new Copernicus toolset. Since COPs Pyro is fully 3D, I thought it would be a good chance to explore its benefits for speed and other potential boons.

What I learned is that while it is fast and has some interesting concepts, the toolset was still in its immaturity, and a lot of the more realistic systems usually provided were up to the artist to create and manage within the new COPs context. Sourcing, dissipation, and other fundamental concepts needed to be solved entirely new.
{{< video_filename "jtpt_rnd_tectonic_v029_firebursts_web.mp4" "Fire burst assets and other misc elements" >}}

Something we learned was that because there was simply so much simulation and effects to do, we tried to create re-usable assets as much as possible.
{{< video_filename "jtpt_rnd_a_v003_web.mp4" "Early RnD for COPs Pyro" >}}

# Procedural Animations

For the "musical" rocks, I set up a procedural beat/keyframe system completely controllable via parameters so that I could easily create various animations for parts of the stone wall without needing to deal with a bunch of manual keyframing and errors.

The same procedural animation system that animated the rocks also animated the falling debris that comes off of them. As a function of time, I remapped the debris to a ballistic trajectory based on some random initial random and calculated attributes.

{{< video_filename "jtpt_rnd_tectonic_v030_coreographed_rocks_web.mp4" >}}

Particles are another thing you can somewhat simply animate procedurally by defining a hero curve and then cloning/distorting that curve for every particle, then slicing along each curve at the position you want the particle to appear. Done naively, this can look fairly unnatural, but giving subtle offsets and noise to each particle can really make it look nice.

{{< video_filename "jtpt_ch2a_v037_embers_swirling_web.mp4" >}}

I am someone who absolutely loves not using simulations when possible. I find procedural animations completely fascinating, efficient, intuitive to control and iterate on, and can be very clever. I know they have their limitations, but you'd be surprised how little they are with some ingenuity!

# Rendering
Rendering for this project presented many unique challenges due to many factors.

First, there were 4 large screens that had various projections to consider. Because we wanted the lighting of the physical screens to be represented in the scene, we had to make sure some screens casted shadows and lighting on other screens, but also to reduce render time, remove some screens from the render. This may seem simple on the surface, but gets hairy when you start adding more layers, and those layers need to cast shadows on their wall only, but not walls behind, etc.

Second, we had many lighting groups in order for post-production to change and vary the lights in time with music and make last-second changes without the need to re-render everything. 

Thirdly, there were just a lot of frames to render out, and getting something wrong in one section could mean a lot of re-rendering, which generates many more times the number of files than there are frames, for each screen, element, and AOV passes / lighting groups.

# Farm Management
Due to the immense amount of rendering and frames coming from each of the artists, we had to rent many computers for a farm, but even that got bogged down at certain pain points. For this, we had to oursource some rendering to external farms.

While some of this worked okay, downloading the frames turned out to be a huge challenge on its own. Not only that, but keeping new and old versions separate without accidentally writing over sequences we did not have any more time to re-render. For instance, downloading one particular song sequence took about 10 hours, and if something interrupted the transfer, there was no way to resume the transfer or check for which frames have already been downloaded (hint: it wasn't sequential)

During a particularly crunchy time where we had about 93% of the files downloaded and no time to restart the whole download, I broke out some coding to analyze the sequences and spit out Deadline-compatible strings of frame file patterns so that we could re-render the necessary frames and merge them into the ones downloaded. Fingers crossed that there were no rendering inconsistencies between the external render farm frames and ours (which would be a flickering nightmare) and... it worked! I didn't get much sleep that day.