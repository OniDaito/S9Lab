--- 
layout: post
title: Depth of Field in Cinder
---

![Depth of Field](http://4.bp.blogspot.com/-cfpyOGIR_CY/TX9SLWtJJOI/AAAAAAAAAyM/KIgyfEQIOo8/s320/depthoffield.png)


Depth of Field is a lovely effect. I thought I'd have a look at how to do this in Cinder. Oddly enough, the <a href="http://www.minecraftforum.net/viewtopic.php?f=25&t=128043&start=300">Minecraft community have a gorgeous plugin that does this exactly</a>. I have moified the shader to work with just the distance from the near plane. This means that the focus is at the near plane and then drops back. The effect is quite cool!<br /><br />Depth of  field is the effect that occurs with a thin lens when all the light rays fail to converge on the same point. A lens can only focus perfectly at one specific distance but the fall-off in sharpness or the increase in size of  the Circle of Confusion is gradual. It is this effect we want to try and recreate. To do that, we need the colour texture and the depth texture. Sampling the depth, deciding how far away it is from the focal plane and then blending with neighbouring pixels provides a good estimation of this effect.
