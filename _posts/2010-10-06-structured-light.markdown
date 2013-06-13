--- 
layout: post
title: Structured Light
---


![structured light](http://1.bp.blogspot.com/_WNXP2eEZSdg/TKxNmYrR5LI/AAAAAAAAAu4/uxCMLcIED8U/s1600/sl1.jpg)


A test of a simple structured light setup. The idea was to use a PS3 Eyetoy and the excellent code written by Kyle MacDonald - <a href="http://sites.google.com/site/structuredlight/" rel="nofollow">sites.google.com/site/structuredlight/</a> and Memo Akten - <a href="http://www.memo.tv/" rel="nofollow">www.memo.tv</a>. There are <a href="http://www.flickr.com/photos/section9/">more photos on my Flickr page</a> and indeed, I'll be making some movies soon!


![structured light](http://4.bp.blogspot.com/_WNXP2eEZSdg/TKxNxAh9rhI/AAAAAAAAAvA/VIfk_jpbqfk/s1600/sl4.jpg)


I strapped together Memo's code under Windows as I finally managed to get hold of the PS3 Eyetoy driver that allows you to do 60fps. There is a special OpenFrameworks 'addon' that is part of Community Core Vision that allows you to run OF programs with 60fps. They don't tell you this ANYWHERE so I'm telling you all now! 


<a href="http://nuigroup.com/forums/viewthread/2921/">There is a thread on the NUIGroup forums</a> that describe using the PS3 Eyetoy with CCV (thats a multitouch table program in Openframeworks btw) and this does work at 60fps but in order to get the structured light scanner to work, I needed the source code to drop into the capture program. Within the CCV Windows Source code, there are some classes that deal with driving the PS3Eyetoy specifically. Dropping these into the Windows version of the decoder worked really well.


I need to take some photos of the setup. Essentially the projector goes below the eyetoy which sits infront of the projector in order to zoom in. Sadly, the throw, or size of the resulting projection really wasn't good enough for this experiment but I shall persevere.

Thanks to Jonty at the <a href="http://london.hackspace.org.uk/">London Hackspace</a> for use of his PS3 Eyetoy and the Projector!
