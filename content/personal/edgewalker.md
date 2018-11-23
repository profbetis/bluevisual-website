---
title: "Edgewalker"
date: 2018-11-20T14:10:36-08:00

tags: ["houdini", "procedural", "tool"]
tools: ["Houdini"]

sections: ["Overview", "Controls", "Setup", "Solver", "Post-Process"]
---

# Overview
The Edgewalker tool starts at a group of points, and walks along edges to neighboring points to create an edge group or polyline.

{{< image 5 "A progression of snapshots of the algorithm. A frame is skipped between each stage for demonstration purposes." >}}

While the look can seem similar to the Find Shortest Path SOP or perhaps Edge Network, those nodes don't avoid current edges and have many merges or splits.

{{< vimeo 301523437 540 "Here's a small project that uses the output of the edgewalker. Rendered in Octane Render." >}}

For this video, I took the attribute created upon creating an edge called "path_time". I capture a rest position after the final solve, then set the Y position to this attribute. After that I use a Clip SOP (as opposed to Blast) to smoothly remove any path geometry ahead of a certain amount and then return the rest position. I then pushed points away from the center based on their "path_time" attribute as well, giving some depth and layering to the final shape. Finally, instancing some spheres at corners and carve positions for some extra life.

# Controls
The controls are split up into three main groups that don't much affect the others.

One of the most powerful tools in this is the direction attribute, which lets you use a vector point attribute to guide the neighbor preference algorithm. This allows for very nice swirls and parallel pathing that can look natural and interesting.

{{< image 4 "The three tabs of controls." >}}

# Setup

The setup involves a few basic things, like creating the initial starting group, creating attributes, but most importantly doing some heavy calculations in parallel before the solver, which has to process things linearly do avoid racing problems.

{{< image 1 "Network for the setup. After this it pipes into the Solver node.">}}

Other things can be calculated once here instead of at every walk iteration. You can gather the neighbors once and also sort that list once to be easily looked up during the walk loop. If a certain neighbor is unavailable the neighbor list doesn't need to be recalculated, you just need to choose a different index.

{{< highlight cs "linenos=table">}}

// Parameters
string dir_type = chs("../dir_type");
string dir_vec_style = chs("../dir_vec_style");
string dir_attr = chs("../dir_attr");
int norm_dir = chi("../norm_dir");
int rev_dir = chi("../rev_dir");
vector dir_vec = chv("../dir_vec");

// Pre-process the direction vector
vector dir;
if( dir_type == "vec" ){ dir = dir_vec; }
else{
    dir = point(0, dir_attr, @ptnum);
    if( norm_dir ){ dir = normalize(dir); }
    if( rev_dir ){ dir *= -1; }
}

if( dir_vec_style == "local" ){
    dir *= @N;
}

/* Compute dot product between the direction to each neighbor
and the current point's direction attribute */
int nbs[] = i[]@neighborhood; // Neighborhood
float values[]; // Array to store the values to rank neighbors by
foreach( int nbpt; nbs){
    vector nb_pos = point(0, "P", nbpt);
    float dot = dot(normalize(nb_pos - @P), dir);
    push(values, dot);
}

/* Sort the neighborhood by dot product values via argsort
 Note: argsort would normally return an ascending list so
 we have to reverse it in order to get highest values first.*/
i[]@neighborhood = reorder(nbs, reverse(argsort(values)));

{{< / highlight >}}
{{< caption "VEX code for the 'Sort By Direction' node." >}}


# Solver
The heart of the walk algorithm is to choose from a sorted list of candidate points and add the edge between them to an edge group. If there are no candidate points, start with a new point in a list of open points.

A few point attributes are necessary to solve this. One is a group of "active" points, pretty standard in most solver/growth algorithms. The other is a "closed" group. This evolved from a "processed" state that other algorithms have because I wanted points with only one connected edge to remain open to be closed later on by a path that finds it.

{{< image 2 "Solver network with a bypass branch if there are no more paths to create or consider." >}}

The walk has to be done in a non-parallel fashion since two points competing for the same point need to be able to find a resolution. One will take it, and the other won't see it as an option anymore. I've been thinking about ways to make it parallel again though, at least for the most part since most points are not next to each other.

{{< highlight cs "linenos=table" >}}
// Parameters
string path_closing = chs("../../../../path_closing");
int merging = chi("../../../../merging");

int pt = chi("../loop_meta/point"); // Which point to process
int nbs[] = point(0, "neighborhood", pt);

// Gather candidate points
int candidates[];
int active_candidates[];
int inactive_candidates[];
foreach( int nbpt; nbs ){
    int closed = inpointgroup(0, "closed", nbpt);
    int active = inpointgroup(0, "active", nbpt);
    int connected = inedgegroup(0, "edges", pt, nbpt);
    int no_closing = (path_closing == "no_closing");
    int offlimits = inpointgroup(0, "offlimits", nbpt);

    if( !(closed&!merging) && !connected && !(active&&no_closing) && !offlimits ){
        if( path_closing == "no_pref" || no_closing ){ push(candidates, nbpt); }
        else{
            if( active ){ push(active_candidates, nbpt); }
            else        { push(inactive_candidates, nbpt); }
        }
    }
}

if( path_closing == "close" ){
    if( len(active_candidates) > 0 ){ candidates = active_candidates; }
    else{ candidates = inactive_candidates; }
} else if( path_closing == "avoid" ){
    if( len(inactive_candidates) > 0 ){ candidates = inactive_candidates; }
    else{ candidates = active_candidates; }
}

/* A candidate list is stored at the detail for efficient access since
it's only used once in the next node and then discarded */
setdetailattrib(0, "candidates", candidates);
{{< / highlight >}}
{{< caption "VEX code for the 'Get Candidates' node, which generates a list of which neighbors can be connected to." >}}

{{< highlight cs "linenos=table" >}}
// Parameters
string pre = "../../../../";

string new_path_behavior = chs(pre+"new_path_behavior");
string deadend_behavior = chs(pre+"deadend_behavior");
string path_closing = chs(pre+"path_closing");

int do_time_attr = chi(pre+"do_time_attr");
string time_attr = chs(pre+"time_attr");

int do_dist_attr = chi(pre+"do_dist_attr");
string dist_attr = chs(pre+"dist_attr");

float seed = ch(pre+"seed");

float dop_time = chf("doptime");
float dop_time_delta = chf("doptimedelta");


int pt = chi("../loop_meta/point"); // Which point to process
int next = -1; // Initialize next point index
int candidates[] = detail(0, "candidates");


int deadend = 0;
if( len(candidates) == 0 ){ deadend = 1; } // If all neighbors are unmatchable, deadend

if( !deadend ){
    next = candidates[0]; // Choose the first element in the candidate list

    // Apply Path Time attribute to the new point
    if( do_time_attr && point(0, time_attr, next) < 0){
        setpointattrib(0, time_attr, next, dop_time + dop_time_delta);
    }

    // Apply Path Distance attribute to the new point
    if( do_time_attr && point(0, dist_attr, next) < 0){
        float dist = distance(vector(point(0, "P", pt)), vector(point(0, "P", next)));
        setpointattrib(0, dist_attr, next, dist);
    }

    setedgegroup(0, "edges", pt, next, 1); // Connect the points
    setdetailattrib(0, "next_pt", next);
}


// If next point is an active point
if( inpointgroup(0, "active", next) ){
    setpointgroup(0, "closed", next, 1);
    setpointgroup(0, "active", next, 0);
    setpointgroup(0, "closed", pt, 1);
    deadend = 1; // Path is now closed
}
// Otherwise
else {
    setpointgroup(0, "active", next, 1); // Set next point to active

    if( new_path_behavior == "one" ){ // Prevent branching if appropriate
        setpointgroup(0, "active", pt, 0); // Set self to inactive
    }
    if( path_closing == "no_closing" ){
        setpointgroup(0, "closed", pt, 1); // Set self to closed
    }
}

// If the next point is a closed point
if( inpointgroup(0, "closed", next) ){
    setpointgroup(0, "closed", pt, 1); // Set self to closed
    deadend = 1;
}


// Deadend Behavior
if( deadend ){
    if( deadend_behavior == "new" ){
        int open[] = detail(1, "open_pts"); // Available points to start at
        int num_open = len(open);
        if( num_open > 0 ){
            int new = open[floor(rand(pt*14.23421+seed)*num_open)]; // Select random index
            setpointgroup(0, "active", new, 1); // Set selected point to active
        }
    }
    setpointgroup(0, "active", pt, 0); // Set self to inactive
    setpointgroup(0, "closed", pt, 1); // Set self to closed
}

if( do_time_attr && point(0, time_attr, pt) < 0){
    setpointattrib(0, time_attr, pt, dop_time);
}
{{< / highlight >}}
{{< caption "VEX code for the Walk node. This connects points to the next best point available." >}}

{{< highlight cs "linenos=table" >}}
string path_closing = chs("../../../../path_closing");

int pts[];
push(pts, chi("../loop_meta/point"));

int next_pt = detail(0, "next_pt");
if( next_pt != 0 ){
    push(pts, next_pt);
}

foreach( int pt; pts ){
    int connections = 0;
    int nbs[] = point(0, "neighborhood", pt);

    foreach( int nbpt; nbs ){
        if( inedgegroup(0, "edges", pt, nbpt) ){ // If connected
            connections++;
        }

        if( connections > 1 ){ // If more than one connection
            setpointgroup(0, "closed", pt, 1);
            setpointgroup(0, "active", pt, 0);
            break;
        }
        else{
            if( path_closing != "no_closing" ){
                setpointgroup(0, "closed", pt, 0);
            }
        }
    }

    if( inpointgroup(0, "closed", pt) ){
        setpointgroup(0, "active", pt, 0);
    }
}
{{< / highlight >}}
{{< caption "VEX code for the Set Closed Group node. This code polishes up any incorrect point groups." >}}

# Output

The final output of the solver is not lines, it's actually an edge group. This lets you receive your geometry unharmed, if that's what you need. Mostly though, the edge group is used to create polylines out of each path.
Later, temporary attributes and groups are cleaned up, unless otherwise decided.
{{< image 3 "Output network for post-processing." >}}
