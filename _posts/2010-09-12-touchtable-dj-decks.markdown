--- 
layout: post
title: TouchTable DJ Decks
tags: electronics opengl computervision hacking
strapline: Lets make a touch turntable!
introtext: Although we didn't get this quite finished (I made the mistake of adding multiple touches too late in the game) we did get it sorted by the next hackspace tuesday meeting. Nevertheless, I soldiered on and it finally works.....ish
---

<div class="clearfix"></div>
<hr />
<iframe src="https://player.vimeo.com/video/14897790?portrait=0" width="460" height="320" frameborder="0"></iframe>
<div class="clearfix"></div>
<hr />

Although we didn't get this quite finished (I made the mistake of adding multiple touches too late in the game) we did get it sorted by the next hackspace tuesday meeting. Nevertheless, I soldiered on and it finally works.....ish


The table works using the Frustrated Total Internal Reflection technique. Essentially, infrared is emitted into the perspex sheet. Where your finger touches, the infrared leaks out which is detected by a camera with a correct filter. Using <a href="http://www.google.com/url?sa=t&source=web&cd=2&ved=0CBcQFjAB&url=http%3A%2F%2Fnuicode.com%2Fprojects%2Ftbeta&ei=lc6MTI6JIoqqngfk89iOCw&usg=AFQjCNG78NLnV_-hOPAui4VEBRNrBq2T0Q&sig2=yT9M3nNucGKVPYDpo9Gr5A">Community Core Vision</a> (which uses OpenCV and Openframeworks), one can change these bright spots into touches.

With this table already built, we decided to build a DJ deck. Now this would probably be too much for just 24 hours but there were some useful programs out there that help.


The first is <a href="http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB8QFjAA&url=http%3A%2F%2Fwww.mixxx.org%2F&ei=s86MTJq9JobQngf7pbyFCw&usg=AFQjCNHNr1Ax9CegWkr19Nqgww57oGgThA&sig2=7x6vUtImkslxUZMB7RY3jg">Mixxx</a>, the DJ program. This has midi bindings for many controllers. I figured the best bet was to write something in <a href="http://www.google.com/url?sa=t&source=web&cd=3&ved=0CCEQFjAC&url=http%3A%2F%2Fopenframeworks.cc%2F&ei=xM6MTL6mIoufnAfz8NmUCw&usg=AFQjCNGf3s4rMuk8wdEs37e8jI3Sz5YHmA&sig2=ykZd8VqQGAyzERp5D9jtkw">Openframeworks</a> that received TUIO messages from CCV, altered the controls and then sent MIDI signals to Mixxx. Linking two programs with Midi is possible under Linux using the virtual midi module and <a href="http://lintian.debian.org/full/piem@debian.org.html">AConnectGUI</a>.


The track is by the amazing <a href="http://www.pronobozo.com/remixes/NIN%20-%20Only%20(Pronobozo%20Remix)">Pronobozo. Grab it here!</a>