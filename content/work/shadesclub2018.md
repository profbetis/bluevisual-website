+++
title = "ShadesClub 2018"
tags = ["modeling", "rendering", "houdini"]
date = 2018-10-23T17:22:53-08:00
client = "ShadesClub"
tools = ["Houdini", "Octane Render", "Affinity Designer"]
sections = ["Scene Setup", "Modeling"]
draft = false
+++
### Older ShadesClub work can be found [here](/work/shadesclub2016).

Every so often [ShadesClub](http://www.shadesclub.com/) upgrades its wares, packaging, and branding, and needs new visualizations of their products for their digital storefront.

{{< image 1 "Various layouts of various products" >}}

{{< video 1 "Lens layer animation" >}}

# Scene Setup
Before this project, I hadn't had the chance to do a multiple-product rendering project in Houdini before, so I learned lots. The challenge was to have the same products in different layouts to have the client pick his favorite, sometimes with different rig parameters and different cameras.

{{< image 2 "Object Network" >}}

My solution was to create each product as a separate HDA, and load the various arrangements of them for each shot into subnetworks within the `/obj/` graph. In order to render each layout for each shot, I created a separate output ROP for each layout, and merged them to create a meta shot node that would re-render all of them if I changed anything about the product.

{{< image 3 "Output Network" >}}

While designing and creating the system took more time than I wanted it to, it's a great framework I can use on future projects and easily spit out new things for the client when there are more renders in the future.


# Modeling
In order to accurately portray the products, I requested manufacturing files from the client in order to build the products with, instead of guessing measurements and folds. This let me essentially recreate the manufacturing process, and rig the objects realistically. UVs and texturing happened naturally since I re-used the files he sent to the factories for production.
