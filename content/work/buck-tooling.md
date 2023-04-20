+++
title = "BUCK Houdini Pipeline"
tags = ["tool", "python", "buck", "houdini"]
date = 2023-04-10T00:25:45-07:00
client = "Buck Design"
tools = ["Houdini", "Python"]
sections = ["Pipeline", "HDA Library", "Zhora"]
active = false
peak = false
draft = false
+++
# Pipeline
When I was first hired at Buck in 2019, one of the things I expressed interest in and that they wanted was tools to make using Houdini easier. Before I started my work, Buck had no Houdini pipeline. I established a global HSITE and turned it into a git-based respository which allowed me to make changes which propagated across all the studios around the globe.

I converted any the local 'houdini.env' files that artists had in their documents folder into a robust global package system. Switching to the package system also let me debug any pipeline issues easily, as well as work from a local development branch of the pipeline, and switch to the live version easily to verify my changes worked.

In addition to making various HDAs and packages, I also upgraded and customized existing nodes with automatically applied presets, pre-filled file paths for ROPs and file reading nodes upon creation, and hooked into the Buck's core pipeline library to access system environment variables and database querying via Python.

# HDA Library
Buck's entire HDA library has been developed by me as well and includes numerous tools in different categories, some of which are extremely versatile and can be used for every project, others which are very niche and were developed for a particular project, and everything in-between.

## Tool List

{{< image 1 "A non-exhaustive list of tools I created and maintained at Buck.">}}

**Attribute Layer** - Takes incoming attributes and volumes, and layers them with various blend modes, masks, and remapping curves.

**Attribute Blend** - Takes two geometry streams and blends the attributes between the two with a remappable mask attribute.

**Attribute Shape** - Generates analytic SDF values and gradients of certain mathematical primtives like a plane, ellipse, box, and line.

**Generate Magnetic Fields** - Takes standard 3D geometry with a charge attribute, and generates a magnetic force field with it using OpenCL.

**Point Orientation Tools** - Generates, manipulates, and provides an intuitive toolset for working with orient attributes.

**Point Vector Tools** - Manipulates vector attributes to be able to do things like rotating around a normal, normalizing them, or scaling them.

**Generate Triangular Grid** - Generates a grid of tiling equilateral triangles.

**VDB Deactivate by Visibility** - Deactivates VDB voxels hidden from a camera by geometry.

**Sequence Analytics** - When given a file sequence path, creates a chart with to plot various variables like disk space, or time.

## Documentation
Inside each of the nodes in the documentation file, I built out a few example use-cases for each tool as well as describing how to use it.
{{< image 2>}}

## Interfaces
I put time into making quality tool interfaces that attempt to match or exceed SideFX's own quality for their tools. I know how to add viewport handles, use python to manipulate interfaces, and follow design guidelines to keep interfaces inuitive and simple (where possible) while remaining powerful.

Some interfaces are very lightweight, like the Attribute Blend SOP below, which takes two topologically identical inputs and blends between any float, vector, and quaternion attributes using an optional mask attribute and remap curve.
{{< image 3 >}}

Others are much more advanced, yet allow a huge range of possibility, such as the Attribute Layer SOP interface below. Attribute Layer allows you to combine, mask, stack, and remap various attributes together. When time allows, I even add tooltips to potentially ambiguous or confusing controls. When possible, I make use of Python to fill attribute menus for intuitive selection and cohesion with the rest of the application.

{{< image 4 >}}

# Zhora
Zhora is an asset management project that I founded using Python 3. It is split into two main systems. Zhora Core is the DCC-agnostic backend that handles the database tree, file manipulation, and logging. Each DCC has its own frontend for interacting with Zhora Core.

The system is a tree structure to parallel the natural file systems in computers. Each node can have content (like a model file) as well as child nodes (such as variants).

## Zhora Houdini
Because it's easiest to develop tools and plugins for, Houdini was a natural first choice for developing a frontend for.

The tool featured a way to save Houdini material networks into a file on disk and then load them into an isolated material network to apply as different material variations.