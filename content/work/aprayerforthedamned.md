+++
title = "A Prayer for the Damned"
tags = ["vfx", "houdini", "film"]
date = 2018-03-11T21:18:47-07:00
client = "San Rafael Productions"
tools = ["Houdini", "Adobe After Effects", "Mantra", "Octane Render"]
sections = ["Smoke & Debris", "Blood Splatters"]
active = false
peak = false
draft = true
+++

While most of [A Prayer for the Damned](https://www.imdb.com/title/tt7141520/) doesn't have VFX, there were a few shots that needed a little more _oomph_.

{{< video 1 >}}

# Smoke & Debris
## Dynamics
{{< video 3 >}}

I roughly remade the chest and boot geometry and motion just enough to affect the smoke motion, but not for any rendering purposes. I attached the smoke's fuel volume to the chest so that when kicked open, the emitter got dragged with it. The fuel source decays and shrinks over time in order to match the temperature diffusion of the metal.

For the lock debris, I originally tried scattering some pieces of distorted junk randomly near where it would have been shattered. This was okay but the pieces felt too random and unrelated to one another, along with not really matching the shape of anything too well. After trying out the procedural way, I quickly modeled a lock and shattered it with voronoi using points concentrated to where the bullet struck, giving a dense clump of small pieces at the impact, with larger cracked pieces further way.

I could have simulated a bullet impacting this geometry, but since you never see it explode, I went with simply applying an initial downward force with some angular velocity so that it scattered the pieces pretty well in the area. I used a simple heightfield terrain to mimic the uneven sand beneath. I then gave the ground plane a shadow catcher material and shifted them downwards into it a bit as if the pieces were stuck in the sand. The pieces didn't need to be animated for the shot, so I just rendered a still EXR with Mantra and matched it with the minimal camera motion in post.

## Compositing
{{< video 2 >}}

The shadows moving across the debris needed to be accounted for as well. I really didn't want to try to match the shadows in 3D and render a sequence, so instead I rendered one version with the sun in the render, and one without as if it was in shadow. I was able to create a difference matte against an unshadowed frame and use it to blend the two renders together without needing to do any keyframing. The smoke also needed to be shaded when appropriate, but I wasn't able to get clever with the footage, so I manually keyframed its lightening and darkening based on nearby objects.

There is a powder blast right under the smoke that also needed correct shading that I had no patience to do in 3D or manually, so I was able to use some extreme levels wrangling to turn the footage into a posterized shadow map which was at three luminance levels: full sun, shadow, and dark shadow. I applied this map on top to give the soot lighting derived from the footage while leaving the textures and details from the footage behind.

# Blood Splatters
{{< video 4 >}}

## Dynamics
I tried a few different methods for generating the splatter, but eventually settled on a hitting a small sphere of fluid with a bullet-like object with other geometry to break up the collision. With high reseeding values, this was enough to make an impressive upwards splash.

Looking back, I realize now that having too much reseeding is not volume-preserving, especially for particles in open-air. The output was usable anyway, but for future simulations that need more stablility, I'll find a better solution.

## Compositing
{{< video 5 >}}

Even though I had simulated at a real-time speed, it looked very slow when put onto the footage, so it had to be sped up a bit to match a physically probable speed. This may have been due to the high reseeding I mentioned earlier.

There was a lot of smoke coming from the gun. I needed to take this into account when compisiting it, so I blended the blood with a solid smoke color using an evolving turbulence noise in post. While it seems like a cheap hack, the results look fine due to the speed of the shots, and it made adjustments extremely fast.

Standard roto work for the hat, arms, and body, and there was also a bit of relighting and color correction to help it match the scene better.
