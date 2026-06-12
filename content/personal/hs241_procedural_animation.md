+++
title = "HS241 Procedural Animation"
tags = ["houdini", "teaching"]
date = 2025-10-07T13:01:11-07:00
tools = ["Houdini", "Houdini.School", "OBS"]
active = false
draft = false
sections = ["Course Overview", "Session 1", "Session 2", "Session 3", "Promotional Materials"]
+++


[HS-241: Procedural Animation](https://www.houdini.school/courses/hs-241-procedural-animation) is my second Houdini course (the first being [Problem Space](/personal/houdinischool-course-01)), this time focusing on procedural animation. While Houdini is known most for its strengths as a dynamics and simulation engine, much can be done with math, expressions, and attributes to efficiently define parametic and procedural animations to geometry.

A lot of concepts I find particularly fascinating and use regularly in professional environments are built live, discussed, and come together to bring a unified understanding of the concepts of time and data.

# Course Overview
{{< image_filename "hspa_course_cover_v001.jpg" "Main course graphic" >}}

**Class Description:** This course delves into various levels of procedural animation, from keyframe basics, to attribute-based animation and the concept of “geometric keyframes”, to more experimental point-based animation systems to offer an alternative method of efficiency and control over traditional simulation-based approaches, pushing the boundaries of what a procedural system can accomplish.

**Learning Outcomes:** Students will gain a deeper understanding of animation as a whole, and how to better leverage the existing animation system to create smarter animations with less keyframes, or without keyframes entirely. They will also explore ways to use attributes to directly drive art-directable animations, and learn about some more advanced systems to explore some further reaches of what procedural systems can do.

# Session 1
### Leveling Up Keyframes
Learning more advanced keyframe settings to make them work smarter and harder, allowing for less keyframes but more animation. Get into channel expressions to get procedurally defined or referential values.

**Sections:** Course Intro, Keyframe overview, Smarter Animation Curves, Time Shifting and Remapping, Animating with Ramps, Channel Expressions, Layering and Composing Expressions, Transformation Noise Example

{{< image_filename "hspa_session01_cover_v001.png" "Graphic for Session 1" >}}

# Session 2
### Attribute-Driven Animation
By taking some of the same concepts from the first session, we can treat points as individual animation curves, allowing geometric attributes to influence our animation on a per-point basis. We also discuss the concept of “Geometric Keyframes”.

**Sections:** Per-Point Noise Animation, Offset Attribute, Time Attribute for Noises, Transition Attribute, Geometric Keyframes

{{< image_filename "hspa_session02_cover_v002.png" "Graphic for session 2" >}}

# Session 3
### Actor-Based Animation
Taking attribute animation further, we explore some procedural point-based animation systems that let us explore the procedural side of what would normally require simulation or particle systems to achieve.

**Sections:** Base Actor System, Rain System, Puddle System, Fireworks System

{{< image_filename "hspa_session03_cover_v002.png" "Graphic for Session 3" >}}

# Promotional Materials
A few videos were made using the concepts employed from this course for promotional material.
{{< video_filename "HS_procedural_animation_cubes_001.mp4" "Actor-based cube animations" >}}
{{< video_filename "HS_procedural_animation_ripples_002.mp4" "Actor-based rain and puddle system" >}}
{{< video_filename "HS_procedural_animation_fireworks_003.mp4" "Actor-based firework system" >}}