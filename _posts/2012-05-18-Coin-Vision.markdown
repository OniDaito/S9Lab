---
layout: post
title: Coin Vision
---
I've been pretty busy with OpenCV these days I have to say. Its been tricky to get to grips with but one thing that helps is having a good project to work on that has simple goals and can help a few people out. I've been looking at coins a lot - why, I can't possibly tell! But nevertheless, it's a thing I'm into.

![http://farm6.staticflickr.com/5467/7221567676_f86234b2d1.jpg](Coin1)

OpenCV has a lovely Python binding which you can build to work on OSX if you are comfortable in working from source. Under OSX Lion you may need to move the cv.so library into your Python path (you can find out where this is by loading python interactive with the *-v* switch and take a look at the paths) as the install script didn't do this for me. Once that is in the right place, play around with the examples in the source; they are quite good.

When it comes to coins, scanning them seems better than using a camera. Holding the lid open gives quite a contrast, with the background turning black as you might imagine. Trying to recognise coins is very tricky and an unsolved problem, but finding the outlines is somewhat easier.

![http://farm8.staticflickr.com/7073/7221569168_20378f8ae0.jpg](Coin2)

Of course, finding where the shadows are and removing these is a little harder! That said, I do like a challenge. I've done a little work previously on detecting colours on coins as a way of checking denomination but I suspect there are better ways. Using contours and what is known as *blob detection* is great so far, especially if you just use one level of hierarchy. I'll post more source code and what not, once I learn more.

![http://farm8.staticflickr.com/7091/7221567328_a314c9d707.jpg](coin3)