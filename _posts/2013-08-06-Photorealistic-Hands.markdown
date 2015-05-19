---
layout: post
title: Photo-realistic hands 
category: work
tags: work blender
strapline: Rendering photorealistic hands for Manchester University
strapimage: creepyhand.jpg
introtext: The University of Manchester came to me, asking if I could render a series of hands that were as realistic as possible. The plan is to fool a human into thinking the resulting images are real. With that in place, certain parameters can be tweeked in order to facilitate an experiment into mirror neurons.
---

The University of Manchester came to me, asking if I could render a series of hands that were as realistic as possible. The plan is to fool a human into thinking the resulting images are real. With that in place, certain parameters can be tweeked in order to facilitate an experiment into mirror neurons.

The goal is to see which parameters effect the perception of realism the most or least and what effects these have on mirroring the actions the hand performs. I was tasked to render these hands. Previously, I had attempted this with 3D studio max, which I've never been very happy with. I find it a little messy, bloated and somewhat hard to control. I felt it was time to give blender a shot.

![Max Hand Post Process](http://farm8.staticflickr.com/7415/9308189446_ccafb86b77.jpg)

Blender uses the Cycles renderer. This has evolved quite a lot over the last few months. It now supports [Sub Surface Scattering](), which is essential for rendering things like Skin, marble, milk, apples or anything with that creamy, opaque look. I'd previously been looking over the best of the best when it comes to Blender Photo-realism and the results looked promising. I figured Blender might be able to punch at the same weight as 3DSMax

![Blender Hand](http://farm6.staticflickr.com/5348/8949103559_1c9bcb5e54.jpg)

The state of Blender can be seen in the second image. This hand was found for free at [BlendSwap](http://www.blendswap.com/) - an excellent page for free blender models. I attempted to render it with Subsurface scattering, but the results were less than optimal. At present, the displacement setting within the Blender Cycles material node doesn't seem to work, which is a shame. One needs to use the displacement modifier in order to get all these lovely pits and creases in the human skin. Sadly, the resolution of these textures is not quite good enough for realism.

![Creepy Hand](http://farm4.staticflickr.com/3705/9296833206_8aaee57a6d.jpg)

Previously, we had spent around $80 USD on a hand for 3DSMax. The textures were very high resolution and included a set of textures for the Epidermal and Subdermal layers of skin, which we can set as parameters to our Suburface materials within Blender. In the previous image, you can see this model exaggerated, with all the creases and pits in their full glory. This doesn't look too bad, and is certainly closer. The problem here is that 3DSMax rigging and skinning doesn't translate into Blender, which meant I had to rig the model myself. This is not my forte at all and its a very tricky job. When the hand was posed, you could easily make out some problems with distortion. In addition, the nails on this model are a dead giveaway. They don't look real, no matter what I ended up doing.

![Distorted Hand](http://farm6.staticflickr.com/5491/9316499708_166c87f492.jpg)

Finally, I decided it might be better to go back to [Turbosquid](http://www.turbosquid.com) and look for another hand that might have better nails and resonable textures. I found one and decided to rig it msyelf. It looked alright but I suddenly hit on the idea that placing the hand in a natural setting is one way to fool a person. I took both my desk and the chair I sit on and used these as backdrops for the blend using a technique known as [Camera Mapping](http://www.blenderguru.com/videos/camera-mapping/). This is quite easy to do in Blender and gives quite a pleasing result, especially if you use a SLR


![Chair Hand](http://farm3.staticflickr.com/2858/9320407303_e0621e39db.jpg)

One thing none of these models have is hair. Hair has been one of the hardest things to render in computer graphics for a long time. Cycles supports hair at present though I found it quite difficult to get the look I was going for as the hairs were quite thin and occasionally didn't show up at all. Given the problems I had with it, I decided to leave it off the model for now and hope that it wouldn't affect things too much.

![Hair Cube](http://farm6.staticflickr.com/5466/9255089894_4789c6f46a.jpg)

The final hurdle involved actually rendering the scene. We had 3 variables to change: the blockiness, the shininess and the colour / texture. Each variable had 10 frames and we had another 10 frames where all the variables were combined. Overall, 40 frames at 25% resolution (around 1024 x 768px) with 2000 samples per ray. That 99 tiles thereabouts. When I tried to render one frame on my desktop, Windows 7 actually broke! Clearly this would not do.

In the end [London Hackspace](https://london.hackspace.org.uk/) and [Amazon EC2](http://aws.amazon.com/ec2/) came to the rescue. I tried the latter first; spinning up a Linux instance and downloading Blender. The render took about 30 minutes the first time around and worked a treat. I was then informed that we had a server machine with a great many cores and memory over at the London hackspace, so I moved to using that. It ran at about 1 Kilowatt hour, so it was easy enough to work out the power costs. Still, despite the power it took around 36 hours to render all the frames at a reasonable resolution.

![Blender Materials](http://farm4.staticflickr.com/3699/9400527972_4a58f00d7a.jpg)

Overall, it was a fun project and quite a difficult one. Skinning and rigging is perhaps the hardest part of this, along with having textures big enough to provide enough realism. You need at least 6 textures for anything involving skin, along with a really good lighting solution. Hands are really hard to get right, as we are all very familiar with our hands. I can think of only faces as being harder.