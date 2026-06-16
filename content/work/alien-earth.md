+++
title = "Alien: Earth"
tags = ["houdini", "dynamics", "lookdev"]
date = 2024-03-27T17:09:35-07:00
client = "FX Network"
tools = ["Houdini", "Heightfields", "POP Fluids", "Redshift"]
sections = ["Overview", "Saliva", "Exploration"]
active = false
draft = false
+++
# Overview
Like [Shogun](/work/shogun), FX Network does the promotional materials for their shows, separate from the effects crew for the shows. So while I didn't do any work on the show itself, I did some things for the marketing materials, including simulations and visual exploration.
{{< video_filename "fx-alienearth-web.mp4" "FX Teaser trailer for Alien: Earth" >}}
# Saliva
It felt really cool to be able to do some saliva simulations for the famous xenomorph.

I created a custom saliva drip tool at first, before we wanted it to drip along the chin and interact with the teeth and lips. It allowed me to create and animate saliva drops individually with high artistic control. It wasn't a waste of time though because I ended up using it to guide the fluid sim via attractive forces and add defined end droplets to the sim.
{{< video_filename "ALI1_rfl010_fxDrool_v020_mesh.mp4" "Meshed simulation" >}}
{{< video_filename "ALI1_rfl010_fxDrool_v020_particles.mp4" "Particle simulation" >}}
# Exploration
For a few months, we were trying to do lookdev for various marketing things. While these particular ones didn't end up going anywhere, I feel they deserve to be seen.
{{< video_filename "ALI1_dev000_fxTerrainKW_v012.mp4" "Heightfield Erosion tests" >}}
{{< video_filename "ALI1_dev000_fxGigerEarthKW_v005_flip.mp4" "Heightfield Erosion tests on Earth with cinematics" >}}
{{< video_filename "ALI1_dev000_fxMoonSim_v005.mp4" "Moon impact test" >}}