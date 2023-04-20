+++
title = "Snap Summit 2020 Intro"
tags = ["houdini", "procedural"]
date = 2020-06-11T00:22:43-07:00
client = "Snapchat @ Buck"
tools = ["Houdini", "Nuke", "V-Ray"]
sections = []
active = false
peak = false
draft = false
reel = true
+++

Snapchat needed a tranquil intro for their Snap Summit 2020 before the event aired. The animation actually lasted for 15 minutes and was very slowly evolving.

The ask was for something seemingly holographic a la James Turrell's artwork. I created a system in Houdini that let me take a base shape and create a slew of faint distorted shells that covered the visual spectrum to build up an ethereal image.

The shape eventually needed to flatten and settle as a perfectly flat yellow circle, so all parameters needed to be able to be animated to zero with no effect on the final image. Additionally, the depth of the shape needed to be felt through its graphic and flat shape.

{{< video 1 >}}

Eventually, I rendered this in V-Ray and comped it in nuke to dial in subtle post-processing effects and extend the rendered frames into a 15 minute animation.

{{< youtube BfvubHha69k 540 >}}

BUCK's project page for this can be found [here](https://buck.co/work/snap-partner-summit).
