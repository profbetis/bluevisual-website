+++
title = "Organic Bracelet"
tags = ["procedural", "modeling", "houdini"]
date = 2018-12-20T13:37:18-08:00
client = "ARYSE"
tools = ["Houdini 17"]
sections = ["Voronoi Wrangling", "SDF Meshing", "Miscellaneous"]
+++

As an introductory project for working with [ARYSE](https://aryse.com/), they wanted to create a bracelet using less material, and an interesting design that showcased their identity as a company. They are looking into experimental and generative design techniques for their products.

For this first project, they just wanted a bracelet for promotional material. This let me explore what the pipeline would be like with them and to start building some techniques and tools that would work well for future projects.

I also was able to get a sense of the company's visual style that they were seeking. They wanted something webby, organic, and somewhat irregular.

{{< image 1 >}}

# Voronoi Wrangling
I scattered points along the base bracelet shape, and used those ase points for voronoi cells to break up the mesh. The voronoi algorithm separates a space into cells that are the closest areas to the center of that point using euclidian distance. I biased cell locations to be nearer to the edges and also in clumps to give a more natural appearance.

{{< image 2 >}}

I next selected points within the logo areas, and grew the selection until it covered the whole cell, and finally deleted them. This let the edges be more broken up and less stiff.

{{< image 3 >}}

# SDF Meshing
After the cell shapes are generated, I extruded them and converted them into a Signed Distance Field (SDF) which is a voxel-grid with values of the distance to the closest surface at that point. While that sounds abstract, it allows certain methods of volumetric modeling to be much faster and naturally controlled.

Here you can see the extruded cells that will later be cut out of the classic bracelet shape. At this stage, I've already applied a smoothing filter to help round out many edges and corners, giving a more organic feeling to the structure.

{{< image 4 >}}

Booleans with SDFs are relatively fast, and give water-tight and well-distributed geometry when converted back into polygons. This is important for real-world applications such as 3D printing or injection mold processes.

Lastly, I took the supplied vector logos and gave them the same treatment as the voronoi cells in order to cut them out of the bracelet.

{{< image 5 >}}

# Miscellaneous
This is the node network for the entire process.
{{< image 6 >}}

This is the very first node in the tree. It uses some custom parameters (Circumference) and formulas to stay mathematically precise and fit the specification from the client. The radius is determined by inversing the `C = 2πr` equation into `r = C/2π`. I'd rather use Tau here, but don't get me started on that.
{{< image 7 >}}
