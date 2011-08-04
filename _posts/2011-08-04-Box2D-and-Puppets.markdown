---
layout: post
title: Box2D and Puppets
---
<iframe src="http://player.vimeo.com/video/27285196?portrait=0" width="640" height="360" frameborder="0"></iframe>

I've been looking at various physics libraries of late. I'd played a little with Bullet physics which was quite cool. I had trouble integrating it with the existing model I had for objects in my world. That said, it put me in a good position for working with [Box2D](http://www.box2d.org/) which is a great little library. My friend [Tom](http://imakethin.gs) used it in his famous iPod commerical spoof and I thought I'd give it a try for a small project I currently have going up North. The idea is to try and convert people into characters from a painting. The problem is that skeleton tracking with the kinect is not perfect and indeed, there are a lot of factor that can compound the issue.

I figured that perhaps the characters should be more like puppets after chatting with the clients. It seemed like a good idea. It turned out to be quite tricky as you have various problems arising going from 3D to 2D. Drawing order and z-buffering are the immediate issues but also collision detection becomes a problem. Obviously with the side-on views, you don't want arms to collide with the front of the body. Fortunately, Box2D has a variety of options to sort that out. More importantly, the documentation is very good, so overall, I highly recommend Box2D. No wonder the Angry Birds guys ripped them off!
