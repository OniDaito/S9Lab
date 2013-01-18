--- 
layout: post
title: Kinect Skeleton for Skinning
---

####
<iframe src="http://player.vimeo.com/video/http://vimeo.com/21351996" width="460" height="280" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe> 

##
So I've been looking at the Kinect quite a bit in relation to skinning. The Primesense team have done a really good job when it comes to full on skeleton tracking and its quite easy to get the positions of the various limbs, but when you are performing skinning, you need a rotation matrix. As we are dealing with 3D we need 3 axes defined. This is impossible with the kinect as it can't measure 'twist'.

##
Like most hackers, I didnt buy the Kinect with an XBox and had no interest in the games at all. I was told by a friend that actually, Microsoft fakes this in the games. The way the palm faces is dependent on where the arm is and is then set in the code. So if you raise your arm above your waist, the palm is set to a certain orientation that has no basis on where your hand actually is.

##
The challenge is to work out if we can actually get this data somehow (from a glove or something) wirelessly and unobtrusively. I reckon Wiimotes are going to be the thing!
