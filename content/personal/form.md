+++
title = "Form"
tags = ["houdini", "procedural", "python", "rendering"]
date = 2018-02-07T20:27:25-08:00
tools = ["Houdini", "Octane Render", "Cura 3D"]
active = true
# peak = false
draft = true
sections = ["Custom Slicer", "G-Code Parsing"]
+++

Having recently got a 3D printer, I became really interested in creating one virtually in Houdini. There are a few different approaches, just like there are in real life. What's great is being able to break the constraints of technology and do any made-up method you want.

### Video goes here

# Custom Slicer
The first thing I did is try to slice up a 3D model into lots of layers, as 3D printers do. I also know they typically use a nozzle to extrude from, and follow a path across the object until the layer is complete.

I learned that they handle walls and infills separately, so I traced the outline of each slice, and then needed a way to fill in that layer. Printers don't just randomly fill in a layer, they usually have a certain pattern that they follow that maximizes structural stability as well as minimizing print time. This is usually accomplished by a layer-alternating diagonal pattern. There's no functional solution to this, so I had to connect each line by walking the points and using the best next point to move to. If it wasn't directly reachable, I recorded the position as "moving" as opposed to extruding.

After learning more and more about the system I realized how overwhelming it would be to add all these options while keeping things consistent and stable. I realized that what I was doing was exactly the job of professional slicing programs that take STL files and convert them into G-Code as instructions for the printer.

# G-Code Parsing
Thankfully, unlike most file formats, G-Code is actually very simple and readable.

{{< image 3 "Example G-Code" >}}

I realized that essentially, each instruction was a coordinate. If I could load this into Houdini, I could rebuild the model using actual machine instructions! To do this, I used Houdini's built-in Python SOP to open the G-Code file and create a point for each line in the file, with the line as a string attribute.

While I may have been able to do a lot of parsing in Python and encode certain attributes directly, I was attracted to the parallelism and personal comfort level I have with VEX. Parallelism is especially important with large data sets such as some of these G-Code files which can have millions of instructions which turn into millions of points.
