--- 
wordpress_id: 68
layout: post
title: ">GStreamer &amp; Openframeworks Issues"
wordpress_url: http://www.section9.co.uk/blog/?p=68
---
>I've been working pretty hard with GStreamer and Openframeworks in order to get audio synchronisation and two sinks; one for preview and one for recording files to disk. So far, it's been pretty tough. Vorbis was giving be lots of Seg faults and for the life of me I couldn't figure out why.<br /><br />Turns out that the <a href="http://www.openframeworks.cc/forum/viewtopic.php?f=9&t=4068">lovely folks on the Openframeworks forums</a> had the answer. libfmodex is causing problems with GStreamer audio and one needs to comment out all references to this and the library that is linked.<br /><br />Developing with Code::Blocks is a bit of pain but once you get it all set up it's not so bad. Looking for these deep bugs though is pretty hard and getting your head into the game is half the battle. I'm glad to report though that Gstreamer is a great little package I hadn't played with before and that if you are doing anything video related, you should definitely check this out.
