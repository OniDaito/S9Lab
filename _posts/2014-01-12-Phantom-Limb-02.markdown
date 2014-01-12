---
layout: post
title: Phantom Limb Dev Diary Part 2
strapline: So Ive been working on the Seburo backend and I’ve hit that old chestnut again - textures and images. Classically, I’ve had issues with this because its something that just needs to be done, and I get frustrated with how tedious it can be. Not to be negative this time, I’ve decided to get it right. This image is under OSX and I’m using Quartz to pull in the images into C++ as its installed by default on OSX. The same cannot be said for Linux however.
---

So Ive been working on the Seburo backend and I’ve hit that old chestnut again - textures and images. Classically, I’ve had issues with this because its something that just needs to be done, and I get frustrated with how tedious it can be. Not to be negative this time, I’ve decided to get it right. This image is under OSX and I’m using Quartz to pull in the images into C++ as its installed by default on OSX. The same cannot be said for Linux however.

Linux seems to be a different kettle of fish altogether. Some people have suggested the SDL as a library to use but im steering clear of that totally. Under linux, I may have to bundle free-image which is a tad annoying but potentially it could work. All this is so we can get FBOs working nicely (which is about half done) so we can warp the screen to fit the oculus rift (which is reporting in at present).

![Depth Cameras](http://media.tumblr.com/e640e7739d6fe867a3406c9db8f32f2d/tumblr_inline_mvdzigPMKd1rjqjsc.png)

So, the new depth cameras we are using are OpenNI2 compliant Asus XtionPro Live cameras. I’ve not bothered with the Kinect for a while now as these cameras are USB only and now that they come with a visual camera, there really is no need for the Kinect, though I’ve not tested the amount of data I can get over the USB link.

These images are pretty responsive. Im using the PixelBuffer call with OpenGL so that the memory is directly mapped from the card to the CPU - makes texturing with cameras super quick. We did this for the Leeds gig so we could have 8 cameras running at once.

I’ve begun looking at the md5 format, specifically the md5mesh format as it looks really easy to get into. I thought it would be a binary format but it isn’t oddly enough. Now we have information from our depth camera, all we need is a good model format. I previously used FBX which was great but was a royal pain in the bum to get the matrices working correctly. I think MD5 should be simpler.

NiTE2 has a lot of faff around it’s C/C++ based libs. Its rather complete but there is a lot of work I had to do, getting around all the rubbish they load up the libraries with. Happily, thats more or less done.


![hellknight](http://media.tumblr.com/b1f1f3f1404b3f35a20cad46393daf34/tumblr_inline_mvqwnquFAk1rjqjsc.png)

Here is the mesh early in the process. You can just about make out this model. The classic hellknight is getting a revamp for PhantomLimb! :D Not that we’d ever use such a model in a production environment but it turns out that the MD5 Format supports bones and similar and is human readable. Not only that, but parsing it is relatively easy (well, I’m still not there yet but almost!)

Previously, I’d used FBX which was quite expansive. The libraries for FBX are quite large and not opensourced. That said, the FBX format supports everything you need and can be exported to with blender.

![hellknight](https://24.media.tumblr.com/6b08b7ef4e2260c968dd13d57f2aff63/tumblr_mvssw1G2MG1si5olwo1_500.png)

Yep! There he is looking much less weedy! :D

One of the things you don’t find a lot of, is how people organise their graphics engines or similar. I’ve begun reading up on the Doom3 engine but it’s quite extreme, or rather, quite a lot to take in at once. Im concerned with how things like three.js, Cinder, or OpenFrameworks deals with the problem of the graphics Pipeline.

Computer graphics has a pipeline and it has ways of doing things, especially with OpenGL. So really, there should be a fairly standard way of taking data from your CPU and throwing at the GPU with all the shaders and textures it needs. Turns out this is quite a hard task and it’s something I had to battle when I made CoffeeGL.

I’m not a fan of scene-graphs but I do think there is something in encapsulating the data together with some hierarchy. Assuming we have dealt with our geometry (which is the subject of the next post) how do you deal with transformations, cameras, geometry and shaders all together?


![plans](https://24.media.tumblr.com/ecbc39f61a345218e8819064b9a0948b/tumblr_mw7o44lfeD1si5olwo1_500.png)


I settled on the idea of a Node class. A Node has a minimum of a matrix; it represents a co-ordinate system or a position and orientation in space. It can have other things attached such as a camera (changes the matrices in the shader) and/or a shader, texture, geometry, etc etc.

To facilitate this in Javascript is quite easy, but in C++ its another matter. I created a NodeBase class and created several subclasses; one for each item that can be added to a Node. When I create a Node (a implicitly shared object by the way) I can add a Shape, a camera or whatever to it. When I do, a pointer to a new node is placed inside the linked list within Node, called bases. 

This linked list is ordered. The reason is that geometry should always be the last thing to be drawn, and the shader needs to be the first thing ‘drawn’ (or in reality, bound to the current context). This approach started off as the Decorator pattern but quickly changed into something more suited to this situation.

Now, Nodes can have children in the classic, tree like way. In addition Nodes can appear in many places and because everything that is added to them is an implicit shared object, I can add the same camera to different nodes or the same texture to different nodes, in order to create my scene.

Here in lies the problem I was having for most of the day. If a parent Node defines a Camera, for example, and then a child Node defines a camera, what should happen? Ideally the camera in child Node should override the parent, and indeed it does. Thats fine, but what about lights? What about the Model Matrix?

The Model matrix is the matrix used locally for any geometry, lights or what have you. This needs to be multiplied down the hierarchy in order to work. This means a child Node’s matrix needs to be a combination of its own local matrix and its parents’ matrices. So what do you do?

I remembered the stack data structure - ah classic computer science! All the NodeBases that contain the matrix have a static vector that represents the stack of matrices at this point. When we walk along the tree, we multiply the current local matrix with the last thing on the stack. We then add that result onto the stack. When we come out of our recursion, we pop the value off the stack. Job done!

To present the data to the shader, we use the ShaderVisitor. This is a static class declared only once. It has one job which is to have it’s templated sign function called by a NodeBase. When this happens, it calls the glUniform functions to pass data to the currently bound shader. This is almost identical to the Visitor pattern and allows me to make the correct OpenGL calls based on the type of the data being passed using templated functions. I use a similar approach with CoffeeGL only I create a pseudo -Node that is a collection of all the data collected as we move down the tree.