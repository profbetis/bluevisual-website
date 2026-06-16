+++
title = "Space Dock"
tags = ["houdini", "procedural", "karma", "study"]
date = 2025-05-04T15:13:17-07:00
tools = ["Houdini", "VEX", "Karma", "Copernicus"]
sections = ["Overview", "Structure", "Stars", "Miscellaneous"]
active = false
+++
# Overview
This is a project I started to explore the concept of fractal cuboid animation. At first it just started abstract and exact, with no space between the units, and the math started out extremely simple. However, I realized I wanted something a bit more grounded, and kind of saw them as shipping containers in space, so I went with that concept. This concept added a lot of interesting but challenging complexity to everything due to the math of the padding and structures while keeping the locomotion systems plausible and realistic.

This project is still in progress when I have time to get around to it. I'd like to add a few more structures, objects to sell the scale of the structure, and a bit of a story arc for a full animation that follows different parts of the structure to take you on a journey that lets you appreciate the complexity and focus on intersting vignettes.
{{< video_filename "fcs_v020_cam05_720p.mp4" "Test animation showing most of the systems and animations in place" >}}
{{< image_filename "fcs_v030_001.jpg" "A more recent render showing different, non-extant logos, and an additional iteration of the structure." >}}
{{< image_filename "fcs_v018_002.jpg" "A version with a much more minimal and uniform crate material. I am a bit partial to this version due to it letting you focus on the structure instead of focusing on the colors and logos." >}}
{{< image_filename "fcs_v017_001.webp" "A random artsy shot focusing on the look of the frame" >}}
# Structure
The structure is based on those slide-puzzles that have all grid points filled up except for one, and the way that you move stuff around is by moving one point into the space, and then moving another one into the space that it left.
{{< video_filename "unit_anim.mp4" >}}

For the eight points of a cube, I removed one and specified a hard-coded order to move the points around. A unit cube is copied to each of the moving points, then you treat the set of eight cubes as a larger cube and iterate. Each iteration moves exponentially slower than the previous, to help give the animations a sense of realistic weight and scale. In most of the renders, there are 6-7 iterations, but I did experiment with 8. It gets quite heavy at that level though.
{{< video_filename "fcs_v025_enteringexiting_shaded.mp4" "Test with entering and exiting cubes to the structure." >}}
{{< video_filename "fcs_v025_enteringexiting.mp4" "A very similar test showing the parental skeleton" >}}

Keep in mind that all of these animations are 100% procedural/analytical and are therefore scrubbable at any frame. In fact, all the heavy lifting happens way before any animation occurs, resulting in a mostly static, cacheable tree, and a very performant animation step at the very end.
<!-- {{< video_filename "random_shuffle_04_hierarchy.mp4" "Test" >}} -->
{{< video_filename "random_shuffle_05_hierarchy8.mp4" "Non-frame animation test" >}}

Adding the frame structure significantly added to the complexity of the positioning of everything, but allowed for some really satisfying and precise structures. Instead of each iteration just being twice the size of the previous, now it has to account for padding and frame width accumulated for all of the previous layers in order to have a final accurate position.
{{< image_filename "solve_2d_002.webp" "2D view of the frame structure" >}}
# Stars
I made a small network to layer some subnets that function like an HDA and have some linked parameters. Each of these layers acts as a different "shell" further out into space, making each layer have smaller stars, higher redshift values, and their own density zones.
{{< image_filename "fcs_stars_001.png" "Material X / Karma material network at a high level" >}}
{{< image_filename "fcs_stars_002.png" "UI for the star layer subnet" >}}

The basis of the stars is a 3D voronoi noise based on ray direction, which makes it invariant to the surface of the object it rests on, similar to a background HDRI but without needing large distant geometry like a sky dome. I can use these voronoi cells to act as an ID per star for randomization and sampling for things such as star color, or to sample a noise field for larger structure noise.
{{< image_filename "fcs_stars_003.png" "Voronoi cell ID visualization" >}}
{{< image_filename "fcs_stars_004.png" "Cell distance visualization" >}}
{{< image_filename "fcs_stars_005.png" "Final star shader" >}}
# Miscellaneous
<!-- {{< image_filename "fcs_v017_002.webp" "caption 5!" >}} -->
{{< video_filename "nonrandom_shuffle.mp4" "A very early test with no randomness" >}}