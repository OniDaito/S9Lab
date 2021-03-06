--- 
layout: post
title: NIN Only Tribute
strapline: A tribute to one of the best bands in the world!
tags: opengl
introtext: The best band in the world? For me, certainly. Trent Reznor has had a massive influence on me and the work that I do and it was high time that I got around to making this little experiment. I wanted to work on my shader, graphics and OpenCV computer vision skills and what better way than to try to recreate the NIN Video 'Only'.
---

<div class="clearfix"></div>
<hr/>
<iframe src="https://player.vimeo.com/video/9788437" width="460" height="280" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe> 
<div class="clearfix"></div>
<hr/>

The best band in the world? For me, certainly. Trent Reznor has had a massive influence on me and the work that I do and it was high time that I got around to making this little experiment. I wanted to work on my shader, graphics and OpenCV computer vision skills and what better way than to try to recreate the NIN Video 'Only'.

The idea is to create a depth map from the brightness of the pixels taken from the camera and then to map these depths to a pin board in real-time. I'd chosen OpenFrameworks as the basis for this as it runs in C++ and contains all the libraries required. To begin with though, I created a couple of tests in both Pyglet and PyGame; two Python libraries that allowed loading of GLSL Shaders and models.


Modelling a pin was quite easy using the free tool, Blender. Although Blender's interface is very hard to learn, the program is fully featured and getting a good object was quite easy. Sadly, however, the OBJ format for 3D objects isn't very robust and doesn't translate well over applications. So, in order to sort this out I settled for 3DS format and managed to find a very good library for OpenFrameworks apps. 

Secondly, I need to get hold of some base code to load GLSL Shaders in OpenFrameworks Apps. Fortunately, there exists such a wrapper. Creating a basic Phong Shader is quite easy and with that, the shiny pins could be drawn.

OpenCV has long been a staple of the OF community, so linking that in and processing the video was not hard. Experimenting to get the best results was the trickiest bit of the whole project and I think, there could still be some work to do. Basically, we create a greyscale image, contour it with some threshold value and then create a set of blobs. We then use the original pixel values from the camera with some added background learning algorithm to reduce the background noise. I used a sheet of black material behind me so that I culd get rid of even more noise and the results turned out to be quite good.


Finally, I tried adding some shadows. This was trickier than I thought. OpenGL under OF has some issues, the first being the rather weird scaling factor. The light is several thousand world units away from the scene which means that the accuracy of the Shadow Mapping algorithm is not so good. Also, it appears that anything outside the frustum is classed as 'in-shadow' naturally enough. Using a variant of GL_CLAMP with a white texture border and a blend mode of multiply, managed to alleviate this problem; anything outside the shadow map gets blending with a white texture and therefore is not affected but there still appears to be one or two artefacts here and there.

Nontheless, overall I am quite pleased with the result and there will certainly be more to come!
