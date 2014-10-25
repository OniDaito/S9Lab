---
layout: post
title: Oculus Rift, meet Phantom Limb Therapy
category: work
strapline: Merging the Oculus Rift, the Kinect and custom graphics to treat Phantom Limb sufferers
strapimage: oculus_plp.jpg
introtext: Working with the University of Manchester, I built a 3D engine that combines the oculus rift, the asus xtion and the MD5 Model format attempting to treat sufferers of Phantom Limb Pain This is version 3 of the project and is the best yet, thanks largely to the Oculus Rift.
---

Working with the University of Manchester, I built a 3D engine that combines the oculus rift, the asus xtion and the MD5 Model format attempting to treat sufferers of [Phantom Limb Pain](http://en.wikipedia.org/wiki/Phantom_limb). This is version 3 of the project and is the best yet, thanks largely to the Oculus Rift.

<iframe width="560" height="315" src="https://www.youtube.com/embed/RSL_a4EVBTQ" frameborder="0" allowfullscreen></iframe>

The general idea is simple. The mirror box has been shown to affect patients in a positive way. The patient places their remaining limb (their left arm, say) into the mirror box. They can then see a reflection of their arm where their missing right arm should be. By performing a set of exercises, studies have shown this can have a beneficial effect. 

Using VR, we can do more than just mirror the limb. We can copy the position (so moving the real arm left moves the virtual one left), we can create a set of games rather than just boring exercises and we can easily mirror the legs as well as the arms. In addition, we can change various parameters to investigate what works for each individual.

The early work used old VR helmets and a set of tracking devices similar to the ping-pong ball trackers, and amusingly, a sort of power glove.

![Early PLP](http://aig.cs.man.ac.uk/research/phantomlimb/plp.png)

The problem was the VR wasn't good enough and the kit difficult to use. It required special setup and the headset was much too heavy.

Version 2 used the Vuzix headset some tracking software I built using XBee Radios. Vuzix were not very forthcoming in supporting Linux or OSX so custom head-tracking hardware was needed. It was around the time the Kinect came about, which allowed us to track the user much more easily. The project was deemed interesting enough to feature at the UK Science Museum:

<iframe width="560" height="315" src="https://www.youtube.com/embed/1r-JCQ-4CcU" frameborder="0" allowfullscreen></iframe>

When the Oculus was announced, we were very excited because it means we can create something we can actually give to clinics and non-computer health care professionals to actually take to people and use. Thus began Phantom Limb Mark3

![Mark 3 PLP](https://31.media.tumblr.com/fa7b1bdbd7cb6c6b0f1ea0749d2caa73/tumblr_inline_n0bszbITiI1rjqjsc.jpg)

This is me, playing the game on delivery day. The game itself is quite simple. Balls are fired at you and you have to bat them away with whichever arm you have. It's quite good fun!

<iframe width="480" height="360" src="https://www.youtube.com/embed/APkMj9h8D-k" frameborder="0" allowfullscreen></iframe>

Technically, the code is quite simple. I wrote my own 3D library / framework in the style of LibCinder (implicit shared objects with C++), with my own MD5 and OBJ parsers. I used Blender to modify some stock models from Turbosquid and Blendswap. MD5 supports bone animation (which is what we need for this to work, as oppose to morph targets or similar) and is a simple and elegant format. Previously, I'd used FBX which is good as it provides for everything but can be overkill and the libraries are quite chunky. GLFW provides the window manger, with GTK+ giving a very simple gui. 

Bullet Physics v3 is used to model the balls flying around. I'm quite a fan of bullet; it's so much fun to play with! The skinning uses code I wrote myself. Using blender, I create a basic skin and rig, export to MD5 format and import the mesh into my program. Skinning is performed using a maximum of 4 bones on the GPU with a vertex shader. Oculus distortion takes place with an FBO, geometry and fragment shader. Calibrating the model takes place in Blender. I suspect this will move into the application itself at some point.

OpenNI2 and an Asus Xtion Pro are tracking my arms. OpenNI2 is vastly improved over version 1. Version 1 had one problem initially in that you had to stand in the PSI pose in order to calibrate your user. This is... somewhat tricky if you only have one arm! :S Thankfully, this requirement has been removed and tracking is much smoother.

I'm using a touchscreen LCD to show some simple options. The whole thing runs on Lubuntu quite happily. One reason I decided to write all this from scratch is that OpenFrameworks is the only viable framework for 3D graphics under Linux and besides, I've been keen to write my own engine for years! :) The cost of the PC and graphics card was quite low; one of the goals should this ever end up with the NHS!

The graphics are quite simple; this is by design and also restricted by the time I had to spend and the funding available. We aren't sure yet whether-or-not a highly detailed scene would be better, or a simple one. Perhaps an Augmented Reality approach would be better? At present, these are open questions.

I've been keeping a diary of my approaches and taking videos at every stage, over at [http://phantomlimbmanchester.tumblr.com/](http://phantomlimbmanchester.tumblr.com/)

There were quite a few challenges; most notably being the skinning. I'm still not convinced the stereo warping is correct (you only really get the stereo effect up close) but overall, it works and is robust and ready for its first outing. We are waiting with baited breath for the first results from using the system with real life patients.

Mark 3 is the most exciting version because, unlike the previous incarnations, this one is heading to an actual clinic to begin clinical trials. So thank-you Oculus. I hope you feel the same warm fuzzies as I do as your gear is helping people out with real problems!