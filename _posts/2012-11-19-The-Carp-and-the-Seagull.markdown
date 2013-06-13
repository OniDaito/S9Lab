---
layout: post
title: The Carp and the Seagull
category: work
strapline: An interactive movie, in WebGL, with Nexus Interactive
strapimage: seagull.jpg
---

Recently, for the past 2 months, I've been involved with a company called
[Nexus Interactive Arts](http://www.nexusinteractivearts.com/) on a webgl
project called [The Carp and the Seagull](http://www.thecarpandtheseagull.com).
Its an interactive movie directed by Evan Boehm and its rather good.

![carp](http://farm9.staticflickr.com/8483/8198734967_a160a30da6.jpg)

The story revolves around our chap, Masato. He is a fisherman who is doomed,
basically. The story is told in 4 chapters inside a cube. As the cube is spun
we see the real world and the netherworld, lighting strikes, fish jump and our
fisherman fishes. The story is a classic tale of one man's life going wrong. 

The technical challenges on this project were considerable. Initially, I was
brought in on the assets. How do you deal with animation from a production
studio in a webbrowser? Nexus has a whole fleet of professional animators
working in 3dsmax, maya and all the rest. The animation in this movie is
excellent, but the problem with animation is the filesize. 

Initially, we tried using skeletal animation; exporting the fbx file and
attempting to parse it in python, converting to JSON. This proved very tricky
and in the end, what we had were glitches.

Shame really, because skeletal animation uses less space and has the ability to
be deformed on the fly. In the end we decided to settle with morph targets. The
problem with morph targets however, is they are essentially a new set of vertex
positions everyframe. Uncompressed JSON for one character using JSON in the
three.js format would weigh in at around 8 megabytes! Quite the challenge.

![gitch](http://farm9.staticflickr.com/8066/8198670489_1541505bdf.jpg)

How do you get from 3DSMax to Three.js JSON format though? The answer, it
seems, is not easily. We decided to go with the venerable MD2 format. There is
[an exporter for max](http://thegreystudios.com/blog/?p=278) that will spit out
MD2 files. Writing a python convertor from MD2 to JSON worked a treat. Now we
had a way to combine animations from different files, export the various
animations and create the lovely assets.

![glitch](http://farm9.staticflickr.com/8203/8199825074_d377399ce6.jpg)
 
My first solution was to use GZip compression on the fly. In addition, I
modified the three.js format to encompass multiple models in one file; a sort
of library if you will. This managed to get the filesize and number of requests
down considerably at the cost of some processing time.

Another chap, the lovely [Roxlu](http://www.roxlu.com/) came up with a simple
binary format for our files. I wrote a quick JSON to binary python script and
meshed it with Roxlu's loader. The compression rate was comparable, if not
better than using gzip.

With the assets out of the way, the rest was down to the arts team. I spent
most of my time adding extra functionality, fixing bugs and working with the
remaining javascript. Three.js is quite a good library. There are a few
problems with it; documentation being one of them. I missed the fact that was a
handy class for generating vertex normals - would have been handy but it was
burried in an example.

One problem we had, and in fact, all Mac Users will have, is to do with
Anti-Aliasing. Given that the art in this project uses a lot of lines, the lack
of antialiasing was going to be a killer. Only certain cards would do this.
Annoyingly, there is no way to test for whether or not this has been enabled.
In the end, the plan was simple; render a small 4 x 4 area of the screen with a
line and then sample part of it. If you see any grey, you know you have
antialiasing enabled. This seemed to work and was quite a nice fix.

FXAA is supported in three.js through the FXComposer - a really nice class that
allows many screen based effects to be stacked together. In the end, we decided
not to use it as the effect didn't look too great. In addition, there is a
fault with certain machines and setting the line width in WebGL - lines can
only be drawn with a thickness of 1. This means you dont have anything to blend
with.

Three.js is a good library. Some of the good things are the uber-shader, the
idea of shared geometry and the FXComposer. Initially I was skeptical with the
material paradigm but actually, it works quite well. The maths library is not
so intuitive sadly and the animation format is still in its early stages but
overall, a nice library to work with.

Working for a client like Nexus is quite tough but enjoyable. As the project
progressed a learnt a little more about how a WebGL application might be
structured and the weaknesses of javascript. There is quite a bit I'd do
differently next time. I think finishing my CoffeeGL library might be a good
start.