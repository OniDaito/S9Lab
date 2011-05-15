--- 
wordpress_id: 107
layout: post
title: ">Projection Mapping"
wordpress_url: http://www.section9.co.uk/blog/?p=107
---
><iframe title="YouTube video player" class="youtube-player" type="text/html" width="640" height="390" src="http://www.youtube.com/embed/uES0HfGAqCc" frameborder="0" allowFullScreen></iframe><br /><br />I've been wanting to play a lot with VDMX and Projection mapping. Memo over at MSA Visuals has a rather good setup which I decided to steal: <a href="http://memo.tv/projection_mapping_quad_warping_with_quartz_composer_vdmx">http://memo.tv/projection_mapping_quad_warping_with_quartz_composer_vdmx</a><br /><br />So generally, it appears that you need to mesh together quite a few things. Memo's Quartz Composer setup appears to have a few extra hooks that VDMX can get hold of. Im not sure what these are. Also, it took me aaaaaages to figure out how to get shaders to work in Quartz Composer as it's not very intuitive. Pull out the inspector on a GLSL patch and select the second tab. That gives you the vertex and pixel shaders. We can edit and play around with that there.<br /><br />VDMX is a bit of a bitch as well, but it has soooo many cool features. Loading up the quartz composer file, you can then inspect this with the media inspector. Select what you want to warp and away you go. The result? Chairman Jonty projected onto a box! Awesome!
