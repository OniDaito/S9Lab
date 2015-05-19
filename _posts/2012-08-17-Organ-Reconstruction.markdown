---
layout: post
title:  3D Organ Reconstruction 
category: work
tags: work computervision opengl
strapline: Working with the University of Leeds on 3D reconstruction with computer vision.
strapimage: leeds.jpg
---

For the last 5 months I've been working with The University of Leeds on a rather interesting project that deals with Keyhole surgery. We are trying to recreate a 3D view from a series of cameras that are fixed inside the patient. To test these ideas we need to build a mockup of the system and work with models of the organs we wish to scan. The result looks something like this.


<div class="clearfix"></div>
<hr />
<iframe src="https://player.vimeo.com/video/47714478" width="460" height="320" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
<div class="clearfix"></div>
<hr />

I had a lot of false starts and worries about this project, not having done a lot of computer vision before. Its a tricky subject I'd like to know more about and I think some back-to-school maths courses might be needed. Initially, the plan was to work with a stereo setup, as described in the [OpenCV literature](http://docs.opencv.org/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.htmlstereorectify). This is known as disparity mapping and it relies somewhat on being able to match one point in one image to the other. One can then work out the [Epipolar Geometry](http://en.wikipedia.org/wiki/Epipolar_geometry)  and recompute the depth, creating a 2D map of disparity or depth.

The first step in any camera based solution is [Camera Resectioning](http://en.wikipedia.org/wiki/Camera_resectioning) or Camera Calibration. All cameras, especially cheap ones, have lens distortion that needs to be accounted for in each setting. These are known as the [Intrinsic Parameters](http://en.wikipedia.org/wiki/Intrinsic_parametersIntrinsic_parameters) .

You can see these arent *too* hard to understand. The issue here is that we need some object in the world that is regular. Enter the chessboard!  Yes, if you were ever wondering why chessboards are involved, now you know why. The chessboard is regular and fixed. Its planar and the points within the intersections should be regular. If they aren't,  you know you have distortion to fix. You can see how to do this in the [Lovely OpenCV tutorial](http://docs.opencv.org/doc/tutorials/calib3d/camera_calibration_square_chess/camera_calibration_square_chess.htmlcameracalibrationsquarechessboardtutorial).

![Greedy Projection](http://farm8.staticflickr.com/7269/7407179846_e4fc587e35.jpg)

The C910 does have a little lens distortion but that can be calibrated once and then saved. We then need to know the extrinsic values. This is how the camera relates to another point in the real world. In the case of stereo mapping, we are translating from one camera to another. There is an OpenCV function called [stereoRectify](http://docs.opencv.org/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.htmlstereorectify). This is fine for disparity mapping but, as seen in the video, this really proved difficult to work with; too much noise and unreliable results. The main reason is that stereo mapping is tricky. Imagine trying to map one set of pixels to another inside the human body where everything is all a little messy and homogenous. Its probably not going to work.

So, we decided we would just identify one point in all 8 cameras. For that to work, you need to reorganise the Camera Extrinsic equation.

<div class="clearfix"></div>

![Point Cloud](http://farm9.staticflickr.com/8024/7407179758_226e1e17f9.jpg)

Basically, we have a translation, a rotation and a set of intrinsic parameters that turn a 3D point into a 2D one.  Now, we have 8 2D points that *should* map onto the same depth. Of course, the above equation, when reorganised, gives the equation for a line. Remember the classic Father Ted video?


<div class="clearfix"></div>
<hr />
<iframe width="460" height="280" src="https://www.youtube.com/embed/25N-4zrk390?feature=player_detailpaget=32s" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr />

Basically, with just one frame of reference you can have a line on which this point exists in 3D space. We need at least two lines - a triangulation if you will - before we can safely say where in 3D space this point lies. There is a further problem. Due to errors and noise, these lines may not intersect, so no exact solution exists. We need to minimise these line equations. Apparently, there is a well known method (that I didn't know of at the time) called [Linear Programming](http://en.wikipedia.org/wiki/Linear_programming) . We have, in effect a system of [Linear Equations](http://en.wikipedia.org/wiki/Systems_of_linear_equations) that are [Overdetermined](http://en.wikipedia.org/wiki/Overdetermined_system).  Since they are overdetermined we can use a solver such as [cvSolve](http://opencv.willowgarage.com/documentation/cpp/core_operations_on_arrays.htmlsolve) or [LAPACK](http://www.netlib.org/lapack/).

We need to organise our equation above into a set of linear equations in terms of, U,V and 1.

<div class="clearfix"></div>
![Final Result](http://farm8.staticflickr.com/7118/7699005862_6c75aca6a4.jpg)

Initially, this setup wasn't too bad. The projector would shine a point which would be picked up by the cameras. This point is then sent to our solver and bam, we have a point in the X,Y,Z space. It does take rather a long time though and the main problem is the projector can only *see* the top of the model. We need to use a laser pointer to see the sides of the model.

So how do we go from a point cloud to an actual mesh? This bit is slightly trickier. Fortunately, we have a set of libraries - [The Point Cloud Library](http://pointclouds.org/) in fact.

<div class="clearfix"></div>
![MLS](http://farm9.staticflickr.com/8012/7449154248_e40c236777.jpg)

There are a few tutorials out there for reconstruction with the PCL  library. I tried the Greedy Projection algorithm but the results didn't quite work out. I moved over to using the Poission algorithm. This exists in MeshLab also. It requires quite a complete point cloud and a set of normals. One can estimate the normals of a point cloud by uisng the [Moving Least Squares](http://www.pointclouds.org/documentation/tutorials/resampling.php) algorithm. The results look a little like this:We can also do a little statistical analysis to remove noise and create a smoother mesh.


<div class="clearfix"></div>
![meshlab mesh](http://farm9.staticflickr.com/8017/7630835790_30dea1be0c.jpg)

The final step is to colour the mesh. Now here we have a problem. How do you choose the colour at a point? The trick is the try and match the normals. Since we know the extrinsic values of the cameras, we can work out the plane of the camera and the normal to the plane. We know the normal of the triangle so the closer the dot product is to 1, the more of that triangle can be seen from that camera. This is slightly naive but works ok. There are other considerations such as the distance between the triangle and the camera. This is something we can't work out easily unfortunately (though I'm sure there is a way). An enhancement to this algorithm is to try and reduce the patchwork look by comparing neighbouring triangles. This requires the generation of a [Winged Edge](http://en.wikipedia.org/wiki/Winged_edge) structure that is quite time consuming.

<div class="clearfix"></div>
![box setup](http://farm6.staticflickr.com/5235/7087159303_ef0ebd5a4f.jpg)

My solution to this problem is to upload the camera normals and all 8 textures to the pixel shader. We then choose the texture by comparing the normals in shader space. Although we only need to do this once, by doing this in parallel we get a much faster result. I ignore the neighbouring triangle issue as the look isn't much better.

There are quite a few improvements and other ideas I have in my head that I might get chance to try in the future. So far though, I'm quite pleased with the result. I'd like to thank Derek Magee, Peter Culmer, Katie Eagleton, Chris Paton, Roxlu and London Hackspace for all the help.

