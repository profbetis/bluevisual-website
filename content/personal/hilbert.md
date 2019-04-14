+++
date = "2017-09-28T18:24:03-04:00"
tags = ["art", "concept", "study"]
tools = ["Houdini", "Octane Render", "Affinity Designer"]
title = "Hilbert Stairs"

+++
The [Hilbert Curve](https://en.wikipedia.org/wiki/Hilbert_curve) is a space-filling fractal curve. It has many computer science applications and I've run across its algorithm in the programs I use before.<!--more--> I took an interest to it and created it in various 2D forms until I wanted to try doing it in 3D. Houdini's loopable node-graph system made it very simple and natural to set up.

{{< image 1 >}}

{{< sbs >}}
  {{< video 1 "Iterate">}}
  {{< video 2 "Determine Length">}}
{{< /sbs >}}
{{< sbs >}}
  {{< video 3 "Height via Path Distance">}}
  {{< video 4 "Extrude">}}
{{< /sbs >}}

{{< image 2 "The network for the algorithm">}}
