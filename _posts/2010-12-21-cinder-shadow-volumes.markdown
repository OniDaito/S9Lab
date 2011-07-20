--- 
wordpress_id: 105
layout: post
title: ">Cinder Shadow Volumes"
wordpress_url: http://www.section9.co.uk/blog/?p=105
---
><a onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}" href="http://4.bp.blogspot.com/_WNXP2eEZSdg/TRDT5e0crCI/AAAAAAAAAw8/iYnYGi-neIE/s1600/shadow1.jpg"><img style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 251px;" src="http://4.bp.blogspot.com/_WNXP2eEZSdg/TRDT5e0crCI/AAAAAAAAAw8/iYnYGi-neIE/s320/shadow1.jpg" border="0" alt=""id="BLOGGER_PHOTO_ID_5553171325026872354" /></a><br />I was asked to come up with some shadows in Openframeworks on a tight timescale.... I kinda failed on that one, having gone down the wrong route of shadow maps (I'd previously used VSM for my first NIN project). Looking it over, it seems that shadow volumes, or some hybrid approach with both is probably best. I've spent far too long on this but so far, I've managed to get a reasonable approximation of depth pass shadow volumes going.<br /><br />I first wanted to use <a href="http://http.developer.nvidia.com/GPUGems3/gpugems3_ch11.html">this approach from GPU Gems 3</a> whereby a geometry shader creates the shadow volume on the card and 'hopefully' speeds things up. This means you need to create a <a href="http://www.cgal.org/Manual/latest/doc_html/cgal_manual/HalfedgeDS/Chapter_main.html">Half-edge</a> structure that knows about twin edges so you can pass adjacency information to the geometry shader using GL_TRIANGLES_ADJACENY_EXT.<br /><br />Theres just one problem<br /><br />OSX only has shader language 1.2 (at least on snow leopard). This means I can't implement the algorithm in GPU Gems. Bugger!<br /><br />I'd gone down this road stupidly really, but I'd spent a lot of time with <a href="http://code.google.com/p/google-sparsehash/">Google Sparse Hash</a> in trying to get a fast lookup. I figure'd I'd stick with this half-edge structure (built from Cinder's Trimesh) and carry on using the default method of creating shadow volumes with the stencil buffer. This means no shaders sadly but nevermind. <br /><br />Again, another unforseen problem. Cinder on OSX doesn't create a stencil buffer by default! <br /><br />Yup, that kinda sucks really as they are quite handy though Im sure there were reasons for this. The changes are up on <a href="https://github.com/cinder/Cinder/issues#issue/21">the Github Cinder repository</a> if you use OSX. Not sure about Windows though but potentially, there is an issue there too.<br /><br />The main problem I've had is with creating the silhouette itself. This can be quite tricky and since I'm using Cinder's TriMesh, I need to make the code as unobtrusive as possible. <a href="http://prideout.net/blog/?p=54">This page</a> gives a great guide to doing this and the general approach is quite useful. One needs to find the edges facing away or towards the light, discount all the others then find edges with twin faces that arent counted. These form the edges which we then extrude away from the light. <br /><br />Overall I'm fairly pleased with the result, though it needs improvement. Depth fail + Caps and a slight softening of the edges in the GPU should work I think