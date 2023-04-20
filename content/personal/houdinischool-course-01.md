+++
title = "Problem Space Course"
tags = ["houdini", "teaching"]
date = 2022-01-14T13:01:11-07:00
tools = ["Houdini", "Houdini.School", "OBS"]
active = false
peak = false
draft = false
+++
When it first opened, [Houdini.School](http://www.houdini.school/)'s founder Deborah reached out to me to have me make a class. I was very busy at the time for many months but eventually in 2022 I was able to set aside some time to create a small syllabus and a cohesive theme enough to create a course for.

{{< image 1 >}}

{{< video 1 "Teaser for the course">}}

[Problem Space](https://www.houdini.school/courses/hs-219-problem-space) is an atypical course more about concepts and thinking strategies rather than focused on a particular tutorial for an effect. I call this approach solving things in "problem space" since you fundamentally change the logic of the problem in order to more easily solve it.

In the first part of the course, I introduce the idea of swapping vector attributes temporarily with the position attribute in order visualize certain things such as UVs or color in world space.

We also use this concept to use the Clip SOP to clip in attribute-space smoothly instead of the originally planar style it operates in.

{{< image 2 >}}

The second part of the course talks about how to manipulate vectors using intuitive controls, especially since vectors can be difficult or arduous to create manually or to reason about to control in a reliable and consistent manner.

One of the example uses for this that I gave was to direct a particle stream source towards a transformed version of itself so that you could manipulate the tranform in the viewport and see a visual guide of where the particles will go, as well as employing intuitive and geometric concepts as controls such as translation, rotation, and scaling.

{{< image 3 >}}

The third part of the course refers back to the first course, and heavily employs the effects of transforming or distorting worldspace by saving the original position into a rest attribute, distorting the geometry, applying a usually more rigid effect like Fuse or Connect Adjacent Pieces, and transforming the positions back to their original position with the effect now applied to them.

{{< image 4 >}}

The course idea came from a talk I gave back in 2019 for a Houdini User Group meetup at the SideFX office. The talk was called Thinking Outside the Box SOP, and it talked about how to use data and attributes in a more powerful and abstract way.

I plan to do create some more courses in the future as well, such as an OpenCL course and a Procedural Animation course.