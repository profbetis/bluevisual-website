+++
title = "Moxy Hotel Billboard"
tags = ["houdini", "dynamics", "fluids", "buck"]
date = 2022-12-11T00:21:45-07:00
client = "Moxy Hotel @ Buck"
tools = ["Houdini", "FLIP"]
sections = ["Overview", "Simulation", "Procedural Extension"]
active = false
peak = false
draft = true
reel = true
+++
# Overview
The ask for this project was to create two animations for a wrapped building-mounted billboard. One of these videos was to be a forced-perspective empty room that fills up with a beverage.

{{< video 1 >}}

# Simulation
All animation of interior objects and ice cubes was done manually by another artist and converted into a pair of surface and velocity VDBs in order to influence and advect the simulation.

Due to the physically dubious methods of filling up the tank by using divergence fields, there was some unexpectedly high energies in the fluid that made it look a bit too wild while filling up. To combat this, I built some custom VEX microsolvers to curtail vertical motion  in certain areas of the tank.

{{< video 2 >}}

# Procedural Extension
Even though the animation is for 15 seconds, after the initial splash and tank filling, I realized further simulation was unnecessary, and could be faded into procedural motion. I used Houdini's ocean spectrum tools to create a realistic yet efficient animated surface that carried the motion for as long as necessary.