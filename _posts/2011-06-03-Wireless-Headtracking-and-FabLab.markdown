--- 
layout: post
title: Wireless Headtracking and FabLab
---
###
![XBee Gyro unit in Custom Case](http://farm3.static.flickr.com/2130/5794083824_6cc8abfb7d.jpg "XBee Gyro Unit in Custom Case")

##
Two posts combined! I've been busy trying to figure out a good way of doing headtracking on the cheap. Vuzix have not been too helpful when it comes to their VR920 headset. I've managed to get some working results with the Windows drivers but there is an issue when it comes to OSX and Linux. It was decided we should build our own Gyro unit. Not knowing anything about such things, I went straight in.

##
I ended up buying a set of different gyros and accelerometers including [Sparkfun 6DOF Razor](http://www.sparkfun.com/products/9431) and the [Sparkfun Atomic 6DOF](http://www.sparkfun.com/products/9184). Both have been pretty easy to setup within Cinder on OSX but each has different challanges. I'll be putting it all into a Cinder Block over the next few days. The Atomic takes care of the XBee communication but requires that you write some code to decode it's frames. I had some issues with that as each value comes back as two bytes: the most significant bits and the least. There were some annoying padding bytes that gave me trouble under C++ but after that, getting some nice values out seemed fine. The razor requires that you implement the XBee standard somehow. I wrote some code in C++, based on the Java libraries from Processing. Getting reasonable values out of the Razor was not too hard.

#
The problem I had was my belief that Gyros measure absolute position. They don't. This may seem obvious to most but its the force applied to them in order to keep them steady that is measured, and they also drift. This means combining accelerometer data and gyro data together is needed and really important to get right. I have investigated Kalman filters and a few other methods to get everythong straight but its still a work in progress.

##
To keep everything in one place, I decided to build a custom case at [Manchester FabLab](http://www.fablabmanchester.org)which is a great little place indeed! They are much more strict that London Hackspace but their kit is just a little bit neater and newer. It depends what you want from a workshop really? Both are good though Fablab restricts you to just Friday's and saturdays which sucks a little. Nevertheless, using Google Sketchup with the SVG Export plugin and Inkscape, you can produce a PDF that can be sent to a Laser cutter. Throw in some 3mm acrylic and bam! One case that holds the Atomic and a LiPoly Battery.
