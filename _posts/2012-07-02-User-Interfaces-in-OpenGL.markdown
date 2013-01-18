---
layout: post
title: User Interfaces in OpenGL
---

###
User Interfaces are the bane of most programmer's lives. They really are. UI people don't often understand the true horror faced by a programmer when they are asked to write good UX code. This goes double for OpenGL types because we have a certain sense of design aesthetic (from what I can tell, talking to people) when it comes to such things. Most UI looks ugly. Its not cool to look at and it's certainly not cool to code. When it comes to OpenGL programs, very few UI libraries stand out. I've had a really tough time lately getting a program structure together that I actually want to use and show off. 

###
What about [QT](http://qt.nokia.com/products/) you say? Well, for starters, QT is massive, relies on C style pointers and causes segfaults a lot of the time. When it comes to OpenGL programs, you need to call a timer function for your draw calls, and heaven help you if you create a widget and have a function called update. I moved to QT because I thought their sliders and such would be useful. Sadly, the code base became quite coupled (which is a bad thing) and teasing things apart proved tricky. I'd like to be using modern C++ and not some Nokia owned library of doom. I have horror stories of learning QT 10 years back. No thanks!

##
I thought about using [ofxUI](https://github.com/rezaali/ofxUI) which looks really nice. The problem I had with it was there were no file-dialogs and [OpenFrameworks](http://www.openframeworks.cc) wasn't built around multiple windows (which I'd rather not use anyway but I have little choice when running fullscreen applications on seperate monitors). I like OpenFrameworks more than I used to, but the CS Engineer in me prefers the beauty of Cinder. It's just more sexy.

###
![glfw](http://www.glfw.org/screenshots/anttweakbar.png)

###
It turns out that [GLFW](http://www.glfw.org/) actually has support for multiple windows if you [check out version3, multi-monitor branch from git](https://github.com/elmindreda/glfw). Multi window applications *are a bad idea* I know but I have one application window, and one surrogate window that runs on a pico projector so there really is little choice. Annoying but there you go. Now GLFW doesn't actually have any GUI components of its own, so we need to add some.

[AntTweakBar](http://www.antisphere.com/Wiki/tools:anttweakbar) was adopted by Cinder and to be honest, I've found little better. I've looked around and asked on IRC and all the usual places and they all suck. They either look poor, are overkill or aren't supported anymore. AntTweakBar is easy to use and works reasonably well.

One problem, there is no file dialog. At this point I decided to give up looking for crossplatform solutions and settled with [gtkmm](http://www.gtkmm.org/en/) as I'm running under Ubuntu at the moment. Not sure what I'll do when I port my toolkit to OSX but I'll probably hook into Cocoa or something with GLFW running the show. 

Such a simple problem, and yet one that doesn't go away. I've heard designers say "We just want some nice sliders" but they are always so hard to find. Crazy huh? 