+++
title = "iPhone X Cases"
tags = ["product", "rendering"]
date = "2017-08-23T00:00:00-08:00"
client = "Caudabe"
tools = ["3DS Max", "Octane Render"]
active = false
peak = false
sections = ["Renders", "iPhone X Model"]
draft = false
+++

Phone case renders for [Caudabe's iPhone X Collection](https://www.caudabe.com/collections/iphone-x-accessories).

[Caudabe](https://www.caudabe.com/) is a phone case manufacturing company which specializes in sleek, precision products that offer beauty and protection. I work with them to visualize their products for online presentation.<!--more--> For this project, they had four new cases for their 'iPhone X Collection'. The client needed near-final products before the announcement of the iPhone X. This presented a challenge in that all looks and styles of the new phone were educated guesses and speculation.

{{< image 11 "Family lineup; art directed shot">}}

For most of the shots, the camera angle and object layout is decided by the client and then fine-tuned later on in the project. Some shots and image concepts are less solidified and require artistic direction, such as the family shot above.

# Renders
There were about 21 different shots for this project, all with their own camera angles, lighting setups, and object positions, as well as different variations on colors for each shot. I worked with external file references for all phones and cases in order to keep things as compartmentalized and organized as possible. This let me work in a very abstract manner and kept human error to a minimum when dealing with all the deliverables.

## Lucid
The Lucid is their crystal clear transparent case. This case can be difficult to work with due to the highly glossy reflective and refractive nature of the material. Extra attention must be paid to the intensity and shape of the highlights.
{{< image 2 "Lucid Silver">}}
{{< image 7 "Lucid Clear">}}

## Veil XT
The Veil XT is a texturized case that's usually opaque, but the Frost variation introduces some transluscency.
{{< image 1 "Veil XT Frost">}}
{{< image 9 "Art-directed Frost and Black shot">}}

## Synthesis
The Synthesis has a transluscent rough back. Here I implemented subsurface scattering to accurately capture the effect as the case tapers towards the rear camera element.
{{< image 4 "Clear Synthesis that shows the reflective iPhone X logo through the back">}}
{{< image 8 "Three Synthesis cases that show the subtle transluscent properties of the back acrylic">}}

## Sheath
The Sheath is a rougher shell with a large area of carbon fiber on the back. The carbon fiber was a fairly complex material with patterned anisotropic reflections. To accomplish the look, I used Filter Forge to create a procedural maps that I combined together in Octane Render to mask out different anisotropic directions. While the look is subtle, it makes the material feel rich and complex.
{{< image 3 "Black Sheath hero shot">}}
{{< image 10 "Stacked Sheath cases that show off the carbon fiber material">}}

# iPhone X Model
About a month before the iPhone X was announced, the client sent me manufacturing files for the new Apple product. While this is typically intended for accessory manufacturers like Caudabe to design their products to fit and adjust their products for the new device, I used it to create an accurate 3D model of the product intended for direct rendering.

It's not as easy as slapping some materials onto it though, as lots of intricate features aren't present, like lenses, screens, ports, and any other detail like that. To help with this, I brought over assets from our [previous project with the iPhone 7].

That being said, things like the glossiness of the back, the color of the metals, and the antenna lines were all unconfirmed until the announcement, which made matching the product quite difficult.

{{< image 12 >}}
