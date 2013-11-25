---
layout: post
title: Phantom Limb Dev Diary Part 1
strapline: The first installment of the Phantom Limb Project
introtext: So the time has begun to start on Phantom Limb Part 3. For these who have not seen the previous versions of this project, the idea is to immerse a person, who suffers from phantom limb pain, inside a Virtual Reality simulation in order to learn more about the condition and hopefully, provide some comfort for the person in question. 
---

So the time has begun to start on Phantom Limb Part 3. For these who have not seen the previous versions of this project, the idea is to immerse a person, who suffers from phantom limb pain, inside a Virtual Reality simulation in order to learn more about the condition and hopefully, provide some comfort for the person in question. 

![Phantom Limb at the Science Museum](http://media.tumblr.com/52c65092d1993c62efa4d84c6b68f155/tumblr_inline_mswjsajXDS1qz4rgp.jpg)

This is a project between [The Advanced Interfaces Group (AIG) at the University of Manchester](http://aig.cs.man.ac.uk) and Section9.co.uk . We’ve worked together on Version 2 of the Phantom Limb Project which was presented at the Science Museum in London. One of the major problems with Version 2 was the lack of a good headset. Vuzix, at the time, had discontinued their best model of headset, which meant we had to create our own head-tracking hardware. Whilst this worked, it wasn’t quite good enough to enter clinical trials.

Now, thanks to better depth cameras and the rise of the Oculus Rift, it becomes possible to create something even more immersive and robust. As I plan the development of this project, I’m beginning to think of the technologies we’ll be using. This is really the software engineering and geeky side of things that some people will find quite interesting. 

We are fortunate to have a couple of Oculus Rifts to work with over the course of this project, which is great! They replace the rather nasty Vuzix headset we were using previously. I’ve not yet tackled the API for this yet but from little I’ve seen it looks fairly robust.

![Oculus Rift](http://24.media.tumblr.com/dfcbd8076abd2c8d3ef52283d20b1453/tumblr_mutiauWpQy1si5olwo1_1280.jpg)

In previous versions, we used OpenNI and NITE to perform the tracking of the skeleton, mapped to an FBX model. FBX, an autodesk model format, is pretty cool. Despite it being proprietary, it works quite well, though MD5 from ID, being open, may be a better solution. That has yet to be decided.

- C++ with Clang and CMake
- Sublime Text 2
- Linux
- OpenNI / Nite
- Oculus Rift Libraries
- Seburo C++ Library (in-house lib)
- MD5 Models

So its been a while since I’ve looked at C++ and a few things have changed. No longer is GCC King of the hill! It seems that there are a couple of options for the discerning coder these days; icc and clang. Now I’ve not tried icc but I’ve noticed Clang gaining a lot of traction these days. It certainly does kick out nicer error messages and I can see why Apple decided to use it. I’ve been playing with LLVM over in Javascript land and I can see the appeal.

C++11 / C++0x is the real deal it seems. There has been a lot added recently that makes C++ quite a joy to use and not what it once was. Im still reading up but it looks like a lot of what boost once offered, is now in the core of C++11 which is great news. What isn’t so great is ubuntu and its support for newer technologies. Im trying to go for pure C++11 with clang but in Precise Pangolin LTS, that seems to be a bit of a problem. A lot of the libstdc++ libs are a little too old. Much has to be built from scratch, including GCC 4.8 and Clang itself. Thats a bit of a pain but I figure it saves trouble in the long run.

In the meantime, OpenNI2 is looking rather nice and already works quite well with the new ASUS depth cameras we have. So far so good. I’ve been looking at my old C++ code for the previous Phantom Limb and going over the developments in OpenNI and NiTE and things have changed somewhat since I was last on this.

The main problem I hit was threading. Looking things over, a lot of the threading support for C++11 lives inside the library libc++. This is an alternative to libstdc++ apparently, which I didn’t know. libc++ claims to run better with Clang and all the rest. This is fine on OSX as there is a good version of libc++ already built. However, under Linux, things are not so good.

After spending far too long going around the houses as it were, I’ve managed to build libc++ with clang, under Ubuntu 12.04 using the instructions they actually give on the libc++ page! :O Shocker! Next time I’ll read more closely. Good news is, the code is neater and the builds are tight.

I’ve recently been reading this book - [Modern C++ Design](http://www.amazon.co.uk/Modern-Design-Applied-Generic-Patterns/dp/0201704315/ref=wl_it_dp_o_pd_S_nC?ie=UTF8&colid=2OVJQTBU03K7I&coliid=IR2MO35GXT8YU). For a while, I’ve had a small Library called [Seburo](https://www.github.com/OniDaito/Seburo) that I’ve used for previous work. It was… ok, but a little too complicated. In recent years I’ve paid very close attention to how professional programmers such as John Carmack, write C based engines and similar. Given C++11, Clang, OpenGL4+ and such, it seemed time to properly upgrade the library for the new phantom limb.

Ever since I started using Cinder, I have been writing code that fits the [Implicitly Shared Object Model](http://qt-project.org/doc/qt-5.0/qtcore/implicit-sharing.html). What this means is that you can copy and pass around objects without having to worry about their memory not being cleaned up. To do this, you need to use shared_pointers quite a lot which is no bad thing.

The principle is an object can be part of another object definition but perhaps it only needs initialising later on, or has some kind of dynamic memory layout or pointers. Lets take the example of a texture. Chances are, you’ll have a class that represents some geometry and it has a texture. In the class definition, if you define Texture t; you’ll end up constructing that texture when your geometry is constructed. Thats fine. But presumably, you need to load a texture in, given a URL or filename. You may not have that until runtime. So you might define a load function.

![A not so boring cuboid](http://24.media.tumblr.com/dc6c576cb9bcd116beb22bbbd877ea22/tumblr_mus2qaVFY31si5olwo1_500.png)

So if you load a texture, which can have any size, you probably have a pointer to some memory. How best to keep track of that? Also, maybe you want to have another reference to that texture, maybe passing it as a variable to another class? Do you really want to copy an entire texture, just to pass it around? The trick comes from the flyweight design pattern. Basically, all the pointers and specific data for that texture are held, not as class variables, but inside a struct that is pointed to by a shared pointer.

What this means is, when we initialise our texture, we end up with the shared pointer pointing to the data in question. If we assign another variable to this texture or pass the texture as a parameter, we can do, without specifying a reference  as we just end up passing a shared pointer around instead. This is quite handy for objects owning data blocks assigned with new or malloc. I use this a lot in Seburo and [Cinder](http://libcinder.org/docs/dev/guide__impl_shared.html) use it a lot too!