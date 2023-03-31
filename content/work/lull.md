+++
active = false
client = "Lull"
date = "2017-02-10T10:43:41-08:00"
peak = false
tags = ["product", "modeling", "rendering"]
title = "Lull"
tools = ["3DS Max", "Octane Render", "Affinity Photo", "Filter Forge"]
sections = ["Composites", "Mattress Renders", "Box Construction"]
draft = true
+++

[Lull](http://www.lull.com/) is an online mattress supplier that needed original as well as updated graphics for their Jungle Box promotional event.<!--more--> They were originally looking to hire a photographer and send the product directly to them, but were open to a 3D approach that would be more cost-effective and provide more flexibility and control over the style and outcome. In the time it would have taken to ship the mattress, test renders were already being sent and refinements were being made.

# Composites
Some scenes required the box to be updated with their current branding. An extremely rough reconstruction of the bedroom was made in order to match the lighting of the photograph, and then the camera was matched, and finall y placing the box model into the scene.

## Bedroom Box Composite
This was a photograph they already had but the box needed to be updated with their promotional graphics.

{{< image 1 "Final Composite" >}}

{{< sbs >}}
  {{< image 2 "The rendered box alone">}}
  {{< image 3 "The original photograph taken by Lull">}}
{{< /sbs >}}

## Outdoor Box Composite
In this scene there was no real box for reference, unlike the Bedroom Box Composite.

{{< image 4 "Final Composite" >}}

{{< sbs >}}
  {{< image 5 "The rendered box alone">}}
  {{< image 6 "The stock photograph provided by Lull">}}
{{< /sbs >}}

## Bedframe Composite
{{< image 7 "Final Composite" >}}

{{< sbs >}}
  {{< image 8 "The rendered mattress alone">}}
  {{< image 9 "The stock photograph provided by Lull">}}
{{< /sbs >}}


# Mattress Renders

To begin the modeling process, a simple cube shape with proportions the same as a queen-sized mattress was created. Next, a wide chamfer to the edges to give a rounded appearance, and then lots of relaxation was applied in order to give it a much more natural shape. Finally, a subtle 3D noise to introduce some imperfection and natural warping.

{{< image 11 >}}

Seamless textures for the top and bottom were generated and applied procedurally in Filter Forge, so that they maintained their real-world-scale even when the mattress was resized.

The graphics were rendered with an alpha channel in order to be placed on any background.

## Frontal Angle
The standard angle for displaying the mattress on the website.
{{< image 10 >}}

## Cutaways
For these graphics, the mattress model was procedurally sliced to show the various foam layers the mattress is comprised of.
{{< image 12 >}}
{{< image 13 >}}
{{< image 14 "The final cutaway graphic live on the website" >}}

# Box Construction
The box is modeled with real-world manufacturing in mind by taking the raw box graphics and dimensions, and folding them along the same lines that the machines do.

First, the box is cut out from the graphic template and the template is applied to help guide during the process. The cutout is then extruded for thickness and given textures for the inside, outside, and even the edges. Next, the top and bottom flaps are folded. After that, the sides fold in to complete the box

{{< image 15 "The box at various construction stages" >}}
