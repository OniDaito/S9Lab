--- 
layout: post
title: Quad Warp, Dual Head
introtext: I'm wokring on many things at the moment and this is one of them. As 'Only' is going to be up at Digit this year at the Lowry im looking to get some ideas on how best to get two sides of the piece to work best. 
tags: opengl programming
strapline: Getting dual screens working for an installation
---

![Quad Warp](http://2.bp.blogspot.com/-XEBSmLA0nLI/TbL-KdnM_FI/AAAAAAAAAy0/CCBZWSEhGxM/s320/quad.png)


I'm wokring on many things at the moment and this is one of them. As 'Only' is going to be up at Digit this year at the Lowry im looking to get some ideas on how best to get two sides of the piece to work best. Previously, I've tried a TCP stream between two machines and that worked quite well. There were issues with the speed however and the receiving machine was definitely slower but the effect looked quite nice.<br /><br />The second idea is to use one, quite hefy machine and two heads. This is probably the nicest solution but doubles the amount of FBOs and space I need one one card. My little Macbook Pro has problems dealing with it for sure. Questions arise such as rendering the geometry twice or rendering both views at once onto a wide texture. In addition, what happens if we need to use projectors? If we have to keystone and warp each view seperately then we could have a problem.


So, in the above picture we have the front view in red, on the left and the rear view, on the right in green. Both are 1024x768 textures, mapped to a 12 x 12 set of quads which are warped using Memo Aktens Projection warping shader. The effect works quite well so hopefully, thats the projectors covered!


How best to improve framerates though? There are, at least, 4 1024x768 textures (rising to 6 with SSAO) and at least 4 different shaders working. So far 15fps is the best which is about half of minimum. More work to do it seems.
