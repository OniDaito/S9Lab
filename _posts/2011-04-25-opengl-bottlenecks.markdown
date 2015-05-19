--- 
layout: post
title: OpenGL Bottlenecks
tags: opengl programming
introtext: I must admit, there is a certain amount of bottlenecks and profiling you need to do in order to get a responsive framerate.
strapline: Looking at where the bottle is a bit tight
---

![Profiler for OpenGL](http://developer.apple.com/library/mac/documentation/graphicsimaging/conceptual/OpenGL-MacProgGuide/art/opengl_profiler_window.jpg)


I must admit, there is a certain amount of bottlenecks and profiling you need to do in order to get a responsive framerate. Im currently involved in my first installation and trying to get the framerate up to something respectable is proving quite difficult. At first, I thought it was all to do with the large textures I was mashing around as I use a lot of FBOs and similar. Turns out, thanks to a little profiling, that its actually all to do with the sheer number of triangles I'm flinging around.


How did I find this out? Well, its always good to remember Valgrind, Instruments, GDB and all the old programs you used to use at Uni or College or wherever. Nowadays, these have grown into easy to use programs within an IDE. Instruments, for example, is really really good and I love using it. But what about OpenGL?


Classically, OpenGL seems to be a bit of a black box when it comes to any form of debugging. However, there are two really handy programs available on the Mac (and indeed, on most PCs I'd say).


<a href="http://developer.apple.com/library/mac/documentation/graphicsimaging/conceptual/OpenGL-MacProgGuide/opengl_performance/opengl_performance.html">Apple has some good information on the OpenGL Profiler</a>. This is pretty nifty and tells you a lot about...well, everytyhing really! It has all the details on your FBOs, the calls that take the most time. It really is excellent.


In addition, there is also the <a href="http://support.gremedy.com/default.asp?forum.1.41.3">gDebugger</a> which has a few similar features but critically, tells you the amount of vertices and triangles you are shifting. Apparently, my latest piece has at least 1800000 triangles! Eeeep!

