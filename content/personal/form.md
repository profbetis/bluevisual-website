+++
title = "Form"
tags = ["houdini", "procedural", "python", "rendering"]
date = 2018-02-07T20:27:25-08:00
tools = ["Houdini", "Octane Render", "Cura 3D"]
active = false
# peak = false
draft = false
sections = ["Custom Slicer", "G-Code Parsing", "Conclusion"]
+++

Having recently got a 3D printer, I became really interested in creating one virtually in Houdini. There are a few different approaches, just like there are in real life. What's great is being able to break the constraints of technology and do any made-up method you want. I chose lasers because lasers are SWEET.

{{< video 1 >}}

{{< video 2 >}}
#### Renders made with Octane Render.

# Custom Slicer
The first thing I did is try to slice up a 3D model into lots of layers, as 3D printers do. I also know they typically use a nozzle to extrude from, and follow a path across the object until the layer is complete.

After these are generated I connect each layer from its last point to the next first point to get one massive open polygon, which can then be traversed to mimic the nozzle of a printer's extruder.

{{< image 1 >}}

I learned that they handle walls and infills separately, so I traced the outline of each slice, and then needed a way to fill in that layer.

{{< sbs >}}
  {{< image 2 "Shell Path">}}
  {{< image 3 "Infill Path">}}
{{< /sbs >}}

Well as it turns out, printers don't just randomly fill in a layer, they usually have a certain pattern that they follow that maximizes structural stability as well as minimizing print time. This is usually accomplished by a layer-alternating diagonal pattern. There's no functional solution to this, so I had to connect each line by walking the points and using the best next point to move to. If it wasn't directly reachable, I recorded the position as "moving" as opposed to extruding.

{{< image 4 "Overly-complicated custom VEX path walking">}}

After learning more and more about the system I realized how overwhelming it would be to add all these options like infill patterns and densities while keeping things consistent and stable. I realized that what I was doing was exactly the job of professional slicing programs that take STL files and convert them into G-Code as instructions for the printer.

# G-Code Parsing
Thankfully, unlike most file formats, G-Code is actually very simple and readable. You'll notice most lines start with a letter (command type) followed by arguments and concurrent commands. Comments start with a ';'. I learned by some quick research that 3D printers only use G0 and G1 to move. E is the extruder motor, and tells the printer how much material to extrude during the move.

{{< image 6 "Example G-Code" >}}

I realized that essentially, each instruction was a coordinate. If I could load this into Houdini, I could rebuild the model using actual machine instructions! To do this, I used Houdini's built-in Python SOP to open the G-Code file and create a point for each line in the file, with the line as a string attribute.

I thought this tool might come in handy for other projects, so I tried to design it with modularity and an open mind.

{{< image 7 "Parameters for the tool" >}}

{{< image 5 "Example 2-million instruction G-Code processed into consectutive point positions" >}}

{{< image 9 "Python SOP opening and reading the G-Code file" >}}

{{< image 8 "Further processing in VEX" >}}

While I may have been able to do a lot of parsing in Python and encode certain attributes directly, I was attracted to the parallelism and personal comfort level I have with VEX. Parallelism is especially important with large data sets such as some of these G-Code files which can have millions of instructions which all turn into points.

# Conclusion
I had a lot of fun learning and pushing myself with this project. I think it was overkill for something in a VFX production environment, but it was a great exercise with wrangling large data sets, retrieving that data from other sources, and opening my mind up to the possibilities of things that can be done with Houdini.
