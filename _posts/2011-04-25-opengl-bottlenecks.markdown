--- 
wordpress_id: 122
layout: post
title: OpenGL Bottlenecks
wordpress_url: http://www.section9.co.uk/blog/?p=122
---
<img class="alignnone" title="OpenGL Profilier" src="http://developer.apple.com/library/mac/documentation/graphicsimaging/conceptual/OpenGL-MacProgGuide/art/opengl_profiler_window.jpg" alt="" width="611" height="440" />
<div>I must admit, there is a certain amount of bottlenecks and profiling you need to do in order to get a responsive framerate. Im currently involved in my first installation and trying to get the framerate up to something respectable is proving quite difficult. At first, I thought it was all to do with the large textures I was mashing around as I use a lot of FBOs and similar. Turns out, thanks to a little profiling, that its actually all to do with the sheer number of triangles I'm flinging around.</div>
<div></div>
<div>How did I find this out? Well, its always good to remember Valgrind, Instruments, GDB and all the old programs you used to use at Uni or College or wherever. Nowadays, these have grown into easy to use programs within an IDE. Instruments, for example, is really really good and I love using it. But what about OpenGL?</div>
<div></div>
<div>Classically, OpenGL seems to be a bit of a black box when it comes to any form of debugging. However, there are two really handy programs available on the Mac (and indeed, on most PCs I'd say).</div>
<div></div>
<div><a href="http://developer.apple.com/library/mac/#documentation/graphicsimaging/conceptual/OpenGL-MacProgGuide/opengl_performance/opengl_performance.html">Apple has some good information on the OpenGL Profiler</a>. This is pretty nifty and tells you a lot about...well, everytyhing really! It has all the details on your FBOs, the calls that take the most time. It really is excellent.</div>
<div></div>
<div>In addition, there is also the <a href="http://support.gremedy.com/default.asp?forum.1.41.3">gDebugger</a> which has a few similar features but critically, tells you the amount of vertices and triangles you are shifting. Apparently, my latest piece has at least 1800000 triangles! Eeeep!</div>
<div></div>
