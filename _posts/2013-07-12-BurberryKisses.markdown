---
layout: post
title: Burberry Kisses, with Google and Grow Interactive
category: work
tags: work webgl
strapline: WebGL based map scenes
strapimage: burberry.jpg
introtext: Recently, I was approached to work on the new Burberry Kisses campaign with many other people, in order to help Google and Grow Interactive get their interactve maps in order.This involved working in WebGL, javascript and a little bit of Unity.
---

![Day Mode](http://farm8.staticflickr.com/7290/9270441620_4dd2e4a3c7.jpg)

Recently, I was approached to work on the new Burberry Kisses campaign as part of a large team helping Grow (www.thisisgrow.com) with the map sections of this site. The project is part of Google’s Art, Copy & Code initiative.

The result? [Burberry Kisses](http://kisses.burberry.com). So far, the press has been pretty good on this project, with [the telegraph](http://fashion.telegraph.co.uk/news-features/TMG10113717/Sealed-with-a-kiss-Burberrys-latest-innovation.html) and [Google](http://googleblog.blogspot.co.uk/2013/06/art-copy-code-sending-kisses-around.html) talking about it! There is much to say on this project but for now, I'll focus on the bits I had a hand in.


This involved working with WebGL and javascript. The assets were designed by the art team over at Grow, inside Unity. The upshot of this was a consistent look and feel for all the assets, as we had an export script from Unity into WebGL. The campaign is cross platform, with mobile and desktop being supported. Using Unity gave the artists and asset creators access to a useful tool for content creation; these assets could be exported wherever we wanted, including straight into WebGL, thanks to a handy plugin.
 
<div class="clearfix"></div>
<hr />

<iframe src="https://player.vimeo.com/video/68856268" width="500" height="333" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>


<div class="clearfix"></div>
<hr />

The idea is you can send a kiss to anyone else in the world from your phone or desktop. The final concept is quite nice. 

I was asked to look at the different map scenes. The daylight scene has a series of trails, with little envelopes flying from one place to the other. The map itself is close to being equi-rectangular but is slightly off, due to the artistic nature of the coastline. Nevermind though - it seems close enough for the trails at least. Each trail is a cubic bezier triangle strip, sent through a shader with another drawn on top additively. I tried using gaussian blur and glow shaders but they tended to look a lot more like lasers as opposed to anything vapor like. A small particle system, written to run on the CPU, is added as well. The final tweaks come from the legend, Inigo Quilez and his [deformation functions](http://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm) adding a cheap bend to the envelopes as they fly. The little spots on the map are a single quad with an animated field effect, written into the shader.


<div class="clearfix"></div>
<hr />

<iframe width="560" height="315" src="https://www.youtube.com/embed/LRiZMVEIhas" frameborder="0" allowfullscreen></iframe>


<div class="clearfix"></div>
<hr />

Night mode was actually trickier in some ways. With day mode, the path ahead is quite straightforward as one can apply more classical graphics effects such as bezier paths, additive blending and similar. Indeed, the data is also quite straightforward; each curve is specified individually. With night mode, the development path was more experimental and the data more abstract.

Given a series of lat/lon points and a value, how do you create an effect similar to NASA's famous Black Marble image?<br/><br/>The answer, I felt, was a little cellular automata!

I figured out that we'd need several layers, one on top of the other to get the additive effect but also a little blurring and a little growth. If two population centres have a high value of activity, then neighbouring areas should light up and eventually a path should go between them. The solution was to create a texture with the initial values and render that to an FBO then feed that FBO texture back into the shader and keep going for a few iterations. Do this for, say 4 textures, each of differing resolutions and then combine them into one image, stacking each layer on top of each other.

![Night Mode](http://farm6.staticflickr.com/5442/9270441650_a426b4276c.jpg) 

The final result isn't too bad at all. I'd made some improvements to the algorithm after it went live; hopefully they will make it into the live system at some point.

Working for a company in the States is a little odd when you are in the UK, due to the time differences mostly, and the manner of working in a large team with many people working on many different aspects of a coherent product. I learnt quite a lot working for Grow; many things I'll most likely take on board and write about in the future.
