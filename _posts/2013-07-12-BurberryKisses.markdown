---
layout: post
title: Burberry Kisses, with Google and Grow Interactive
category: work
strapline: WebGL based map scenes
strapimage: bk0.jpg
introtext: Recently, I was approached to work on the new Burberry Kisses campaign with many other people, in order to help Google and Grow Interactive get their interactve maps in order.This involved working in WebGL, javascript and a little bit of Unity.
---

Recently, I was approached to work on the new Burberry Kisses campaign with many other people, in order to help Google and Grow Interactive get their interactve maps in order. This involved working in WebGL, javascript and a little bit of Unity. The result? [Burberry Kisses](http://kisses.burberry.com). So far, the press has been pretty good on this project, with [the telegraph](http://fashion.telegraph.co.uk/news-features/TMG10113717/Sealed-with-a-kiss-Burberrys-latest-innovation.html) and [Google](http://googleblog.blogspot.co.uk/2013/06/art-copy-code-sending-kisses-around.html) talking about it! There is much to say on this project but for now, I'll focus on the bits I had a hand in.

<iframe width="560" height="315" src="//www.youtube.com/embed/LRiZMVEIhas" frameborder="0" allowfullscreen></iframe>

The campaign is cross device, with iOS being the main feature. The idea is you can send a kiss to anyone else in the world from your phone ofr desktop. The idea is quite nice. Initially I had looked at capturing the kiss with a webcam. The problem here is that lip detection, whilst possible, is a hard process and one that hasn't made it over to the web browser yet, sadly. The accepted method is to use either an [Active Shape Model](http://en.wikipedia.org/wiki/Active_shape_model) or [Active Appearance Model](http://en.wikipedia.org/wiki/Active_appearance_model) but these tend to be a little computationally expensive at present.

I was asked to look at the different map scenes. The daylight seen has a series of trails, with little envelopes flying from one place to the other. The map itself is close to being equi-rectangular but is slightly off. Nevermind though, it seems close enough for the trails. Each trail is a cubic bezier triangle strip, sent through a shader with another drawn on top additively. I tried using gaussian blur and glow shaders but they tended to look a lot more like lasers as oppose to anything vapor like. A small particle system, written to run on the CPU, is added as well. The final tweaks come from the legend Inigo Quilez and his [deformation functions](http://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm) adding a cheap bend to the envelopes as they fly. The little spots on the map are a single quad with an animated field effect, written into the shader.

![Day Mode](http://farm8.staticflickr.com/7290/9270441620_4dd2e4a3c7.jpg)

Night mode was actually trickier in some ways. There was less in the way of feedback and indeed, the effects were much more subtle and less well defined. Given a series of lat/lon points and a value, how do you create an effect similar to NASA's famous Black Marble image?


![NASA Globe at Night](http://sociable.co/wp-content/uploads/2012/12/NASA-earth-at-night.jpg)

The answer, I felt, was a little cellular automata!

I figured out that we'd need several layers, one on top of the other to get the additive effect but also a little blurring and a little growth. If two population centres have a high value of activity, then neighbouring areas should light up and eventually a path should go between them. The solution was to create a texture with the initial values and render that to an FBO then feed that FBO texture back into the shader and keep going for a few iterations. Do this for, say 4 textures, each of differing resolutions and then combine them into one image, stacking each layer on top of each other.

![Night Mode](http://farm6.staticflickr.com/5442/9270441650_a426b4276c.jpg) 

The final result isn't too bad at all. I'd made some improvements to the algorithm after it went live; hopefully they will make it into the live system at some point.

Working for a company in the States is a little odd, when you are in th UK dues to the time differences. I learnt quite a lot working for Grow Interactive; many things I'll write about in the near future but for now, enjoy the page!