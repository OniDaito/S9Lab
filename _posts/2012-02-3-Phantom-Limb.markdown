---
layout: post
title: Phantom Limb Pain with the Kinect
---

Over the summer, I worked with [Advanced Interfaces Group](http://www.aig.cs.man.ac.uk) at [The University of Manchester](http:/www.manchester.ac.uk) on a research project to investigate [Phantom Limb Pain](http://en.wikipedia.org/wiki/Phantom_limb). Previously, Steve Pettifer and Toby Howard (the principle researchers) has tried VR and ping pong ball style tracking in order to recreate a virtual world and 'mirror' the missing limb. The idea is to create a more immersive version of the [Ramachandran Mirror Box](http://en.wikipedia.org/wiki/Mirror_box). It's a way to try and unlearn what has been learnt.

<object width="500" height="281"><param name="allowfullscreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="movie" value="http://vimeo.com/moogaloop.swf?clip_id=36085689&amp;server=vimeo.com&amp;show_title=0&amp;show_byline=0&amp;show_portrait=0&amp;color=00adef&amp;fullscreen=1&amp;autoplay=0&amp;loop=0" /><embed src="http://vimeo.com/moogaloop.swf?clip_id=36085689&amp;server=vimeo.com&amp;show_title=0&amp;show_byline=0&amp;show_portrait=0&amp;color=00adef&amp;fullscreen=1&amp;autoplay=0&amp;loop=0" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always" width="500" height="281"></embed></object>

Since the Kinect and cheaper VR goggles have become available, it seemed the right time to rebuild this system with modern technology in order to test what things affect pain relief. Although the mirror box only costs about 2 pounds, we can't easily change parameters and exercises, so there is definitely something to look at.

The technical aspects of the project were quite interesting. The first problem is how to get from the Kinect to a moving person? The OpenNI team were the first to do this with the OGRE model Sinbad:

<object width="480" height="360"><param name="movie" value="http://www.youtube.com/v/Zl6O-Rf52Co?version=3&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/Zl6O-Rf52Co?version=3&amp;hl=en_US" type="application/x-shockwave-flash" width="480" height="360" allowscriptaccess="always" allowfullscreen="true"></embed></object>

The technique is known as skinning. It works by attaching vertices to bones with weights. As the bones are transformed, the vertices follow the bones by a certain amount, relative to the weight. Imagine a lower arm bone moving up and down. The vertices in the lower arm will be attached with high weightings whereas the vertices in the leg will not. 

The problem here is there are no real APIs or similar for this. The closest modelling tool kit is the [FBX SDK](http://usa.autodesk.com/adsk/servlet/index?siteID=123112&id=7478532) which has support for skinning, textures, animation and indeed, anything you could possibly need for models. It's my goto library for this sort of thing.

OpenNI provides tracking for the skeleton, as most of us know by now. In addition, it provides a matrix for each bone. Using this matrix with the FBX SDK, one can skin a model in the normal way. First challenge over!

One thing the Kinect can't do is detect rotation. Imagine you are trying to rotate your wrist to look at your palm. That motion cannot be detected and its an open problem at the moment. As my video shows, a gyroscope can help to fix that.

![Architecture](http://farm8.staticflickr.com/7033/6811254669_fcb48f2227.jpg)

The next step is to create the visuals and immerse the user in the scene. Vuzix produce a set of reasonable headsets. The [Vuzix VR920](http://www.vuzix.com/consumer/products_vr920.html) sits in my toolbox most of the time. They are superior to the Wrap models that Vuzix are pushing. The problem is they are now discontinued. This means the drivers for OSX don't actually work properly when it comes to the gyros and accelerometers. This meant that headtracking would be a problem.

Thanks to [Adafruit Industries](http://adafruit.com/) and [Sparkfun](http://www.sparkfun.com) I decided it would be possible to create an agnostic head tracking solution using XBee wireless modules. Adafruit provided the USB dev boards for driving the XBees and Sparkfun provided the Gyro unit - The [Atomic IMU](http://www.sparkfun.com/products/9184). We tried a few other boards but this one seemed to work the best.

![Atomic](http://farm3.staticflickr.com/2130/5794083824_6cc8abfb7d.jpg)

At the time, I was up north and away from London Hackspace. Thankfully, FabLab came in with their laser cutter. I built the box and 3D Printed some cases for all the chargers and parts we needed. Rather than just have the XBee USB boards and the lipoly chargers being exposed, I figured some 3D printing might be in order.

![XBee Case](http://farm8.staticflickr.com/7014/6811365387_73f69d5541.jpg)

Google sketchup to 3D printing works quite well. Again, thanks to [FabLab Manchester]() for helping out with that.

Converting a Gyro and an Accelerometer into orientation data is not a trivial task. At first, I thought just a gyro would be fine but thats not the case at all. A gyro measures the force acting on the gyro to keep it stable, not the orientation itself. An accelerometer measures the acceleration in a particular direction. In order to understand the movement, one must have a start point and then integrate over the values. This means that errors will build up. These can be corrected with the accelerometer data and that is fine, so long as you actually have accelerometer data for that axis. You certainly don't for Yaw.

This is known as yaw drift. You can't correct for it, because gravity acts along the Y axis, the up down axis. So if you are spinning around that axis the acceleration due to gravity doesn't change. In our version, we don't have a compass to correct for that. Its definitely something we can improve on. 

Most of the code is actually related to Unmanned Aerial Vechicles. Ultimately, I settled on the [Discrete Cosine Matrix](http://en.wikipedia.org/wiki/Discrete_cosine_transform) with a set of [Kalman filters](http://en.wikipedia.org/wiki/Kalman_filter). Eventually, I'd like to implement [this imu algorithm](http://code.google.com/p/imumargalgorithm30042010sohm/) as its likely to improve things drastically. That said, it's still not too bad, though the yaw needs to be reset a little too often. We also tested the [Sparkfun Razor 6DOF](http://voidbot.net/razor-6dof.html) as well as there was quite a lot of good things said about it.

Headtracking and limb tracking complete, the next step was the graphics. Shadows were seen as important in order to gain some context about where the user appears in the scene. I tried Screen Space Ambient Occlusion and basic shadow mapping, settling with the later.

![Shadows](http://farm7.staticflickr.com/6010/5964128715_26888db203.jpg)

One problem to these who know a little about OpenNI and Kinect tracking is the PSI Pose. This is where the calibration problem comes in. How can you ask a person with one arm to stand with both arms up in the air? Fortunately, we can save a calibration from a similar person and use these with the participant. The SDK has improved since then, so this should be less of a problem.

At the same time, we needed to create some games. The participant needs to move their phantom limb in order to feel relief. I was joined on the project by a Manchester student, David Edwards who came up with a few games like Connect 4. At this point, I needed to consider documentation, APIs and similar - handing over my code to another person and asking them to run with it.

This project covered all the bases for me. Working with talented people, making physical things, software engineering, computer graphics and most importantly, making a difference in someone's life. Our first participant said his pain was going down whilst he was using our program. Theres an awful lot left to explore. Im sure the AIG will come up with something great.

The paper has been accepted at the GRAPP conference this year:

 S. Pettifer, T.L.J. Howard, B. Blundell, and D. Edwards. 
 An immersive virtual environment for phantom limb pain rehabilitation. 
 In Proceedings of the International Conference of Computer 
 Graphics Theory and Applications (GRAPP), 
 February 2012. Accepted for publication.


At the time, I was motorcycling between Southport and Manchester quite regularly. For a few months, I was the leather clad biker programmer guy. It did feel pretty damn cool! :)
