+++
title = "SHNOPs Toolset"
tags = ["houdini", "tool"]
date = 2018-09-27T21:18:39-08:00
tools = ["Houdini"]
sections = ["Process"]
active = false
+++

[SHNOPs](https://github.com/profbetis/SHNOPs) (visit the repo!) is an open-source toolset designed in and to use with SideFX's Houdini.

It stands for Simple Houdini Number OPerators. Its purpose is to provide a simple and cohesive framework to manipulate and analyze datasets into meaningful and interesting geometric respresentations.

I was originally inspired to create this toolset when I had data of my own that I wanted to visualize and analyze myself instead of relying on another program that could do it differently or not offer the tools I wanted.

{{< image 1 >}}

# Process
The general process is to have a data source, process/filter it, run some analyses, and plot it. Each stage has tools designed for that process.

{{< image 2 >}}

Sourcing usually brings in a CSV file, or lets you generate datasets to manipulate, either for testing purposes or just for fun.

Processing is designed to (ethically) manipulate datasets. This includes filters for removing entries that are duplicated, fall outside a threshold, or don't match a certain value. Transforming is also a process, for example turning a 0-1 value into a better representative range.

Analysis tools create new data from existing data, like integrating a dataset, fourier transforming it, or calculating a "velocity".

Plotting is the final stage, and is meant to create geometry from your dataset in different forms, whichever is the most interesting-looking, or most appropriate to visualize it in.

{{< image 3 >}}
