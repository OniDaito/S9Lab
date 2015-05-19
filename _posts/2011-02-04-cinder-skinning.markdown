--- 
layout: post
title: Cinder Skinning
tags: opengl
introtext: I've been having quite a hard time getting this working, but its finally done! Skinning inside Cinder has been the goal for the last week or so. Its been damn tricky as the FBX format is a beast to work with. However, in the end, I have emerged victorious.
strapline: Learning how to skin a mesh!
---

<div class="clearfix"></div>
<hr />
<iframe width="460" height="320" src="https://www.youtube.com/embed/K994B9EeNC0" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr />

I've been having quite a hard time getting this working, but its finally done! Skinning inside Cinder has been the goal for the last week or so. Its been damn tricky as the FBX format is a beast to work with. However, in the end, I have emerged victorious.


FBX has support for bones and Cluster deformation. Using Blender, one can export to FBX and load everything up in Cinder. There are bugs though. For some reason, leaf bones don't properly show up as far as I can tell within the export though everything else seems to generally work.

The idea is that the rotations need to cascade down the tree to all the subnodes. This is the tricky bit and with FBX, you need to keep a seperate structure that holds the matrices. You can then modify the bones which in turn, modifies the weighted mesh.


This really should be deformed in a vertex shader which is the next step really. That and getting some texture support (which i tool out temporarily to make the code a little simpler). In the end, im pleased with the result. Code will end up on github. Might make a cinder block too!
