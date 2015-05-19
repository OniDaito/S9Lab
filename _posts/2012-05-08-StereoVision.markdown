---
layout: post
title: Stereo Vision
introtext: So what have I been up to these last few months? I've not had a lot of chance to mess around in the graphics domain, largely because I've been working on a large project for The University of Leeds. I've been interested in computer vision for a while and this seemed like a good chance to get to grips with it. Im working on the reconstruction of meshes from multiple camera viewpoints. This leads me into the realms of stereo vision.
strapline: So how does stereovision actually produce 3D images then?
tags: computervision

---

So what have I been up to these last few months? I've not had a lot of chance to mess around in the graphics domain, largely because I've been working on a large project for The University of Leeds. I've been interested in computer vision for a while and this seemed like a good chance to get to grips with it. Im working on the reconstruction of meshes from multiple camera viewpoints. This leads me into the realms of stereo vision.

<div class="clearfix"></div>
<hr/>
<iframe width="460" height="360" src="https://www.youtube.com/embed/7Gx4IRoq1ow" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr/>


In the initial case, the idea is to place two cameras side-by-side. When a known point is located in both frames, one can begin to calibrate the cameras, use triangulation and work out the depth. Using OpenCV, many of these functions are defined for you. In the above video, we can see the disparity map beginning to take shape. The disparity map on the right, shows the distance from one point in the left image to the same point in the right image. This apparent distance is related to the depth.

One needs to work out two sets of parameters before we can begin to calculate the disparity. The first set of parameters are called the Intrinsic Parameters - these are related to the distortion effects that are encountered when using any lens. Barrel distortion and tangential distortion can make straight lines look curved. The second set of parameters are called Extrinsic parameters which are related the setup of the two cameras. Modelling and solving these equations for these cameras is known as [Camera Resectioning](http://en.wikipedia.org/wiki/Camera_resectioning). Thankfully, OpenCV includes a method for this. 


The issue with not having straight lines might seem trivial but you can really see the effect when you look at photographs of skyscrapers or other tall buildings; they tend to curve as they reach for the sky. Of course, this has problems for determining the right correspondances between two images.

No doubt, you'll have seen the chessboards everywhere when it comes to computer vision. Chessboards provide a good way to calibrate a camera as the intersections between the black squares form a good set of regular points on a plane. I've settled with a 9x6 chessboard with a wide, white edge, mounted on perspex. I take around 60 to 80 shots per camera when attempting to find the intrinsic values. So far, this seems to work most of the time. Im using Logitech C910 cameras for this experiment and they do have a reasonable amount of barrel distortion.


The next step is to work out the Extrinsic Values. These are related to the setup and are not independent of the the view, unlike the intrinsic parameters. Depending on how your cameras are setup, these parameters will change. Again, OpenCV has another function that makes a pretty good guess at what these paramters should be. Again, you need a chessboard to generate a set of known points that can be seen from each camera. 

<div class="clearfix"></div>
<hr/>
<iframe width="460" height="360" src="https://www.youtube.com/embed/D6DVhtsVmDE" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr/>


In the above video, I am generating a disparity map on the right hand side, then creating a simple mesh in the middle. Sadly, it's not quite perfect yet, but it's early days so far. 

I've found that OpenCV does provide a lot of useful functions but one needs to be aware that there are two versions out there, and many of the examples are not so useful. OpenCV2 is the main one to go for, and under Linux, building your own is a must. There are issues under unbuntu that revolve around the supporting libraries but these can be overcome with some clever symlinking. The [OpenCV2 cookbook](http://www.laganiere.name/opencvCookbook/) is really not a bad place to start. The O'Reilly OpenCV book is fairly canon but be aware that the code examples cover OpenCV1 only and there are a few differences.