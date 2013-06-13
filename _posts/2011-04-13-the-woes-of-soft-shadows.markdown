--- 
layout: post
title: The Woes of Soft Shadows
category: work
strapline: Soft shadows in Quartz Composer
strapimage: quartzshadows.jpg
introtext: I've been playing with soft shadows for a client and it's been one hell of a rocky ride I must say. There isn't really a nice way of doing it that I'm happy with. I've gone through PCF, PCSS, VSM and SAVSM and none of them seem to work right. I must admit, we are on the verge of very hardcore OpenGL here. But the basics of shadowmapping are quite simple.
---

I've been playing with soft shadows for a client and it's been one hell of a rocky ride I must say. There isn't really a nice way of doing it that I'm happy with. I've gone through PCF, PCSS, VSM and SAVSM and none of them seem to work right. I must admit, we are on the verge of very hardcore OpenGL here. But the basics of shadowmapping are quite simple.


So, Percentage Closer Filtering was the first I tried. It was a bit tricky until I realised its pretty much offset sampling and thats it. Bang. Take an average of a set amount of pixels. Job done. Problem is, this is quite slow when you are averaging over 64 texels. The effect isn't great and a bit wasteful as well. So, that means Percentage Closer Soft Shadows is an option. Doesnt look that bad but its rather slow and the falloff isn't really big enough. The shadows need to fade away a lot quicker and when the filter gets past about 8x8 you can see lots of artefacts. Not good.


![Soft Shadows](http://4.bp.blogspot.com/-xG5__l4M08Y/TaV5PGF4HHI/AAAAAAAAAyk/-Jdch5Mp4xo/s320/pcss.jpg)


So, PCSS and PCF have failed me. Thats really annoying. So, people say that VSM is better. Its certainly simpler in code though you do need to use a colour texture and not a depth buffer. Still, once you are happy with FBOs you can get to it. 


![Soft Shadows](http://farm6.static.flickr.com/5067/5609017825_7937375e5b.jpg)


They are smooth but look at the falloff... the shadows are stronger the further away. Clearly that's wrong. I've no idea why VSM does this because Shadows dont work that way in the real world. Im convinced it looks wrong. Boo and hiss!

Nevetheless, it was close and it seems to be quite fast in comparison to PCF and the effects are smoother.


Summed Area Tables apparently allow us to smooth out and fade the shadows. This is pretty much what we need. Summed Area Tables is an old technique from the 80s that, like most older algorithms, has a new lease of life because of shader technology. So, with that in mind, I managed to write a shader and Ping Pong FBO from scratch and it actually worked! Marvellous. A summed table basically adds up the sums of the texels from the top left to the bottom right (or similar). This means that you can get the sum of any rectangle within the table in constant time. So a 128 x 128 lookup for the average is the same cost as a 2 x 2 with Summed Area Tables. Thats great because we can alter the filter size at any point with our VSM shadows. Brilliant! 

There is a problem however. Summed Area Tables end up with big big numbers. You are, in effect summing, say 512 x 512 numbers so the last number is going to be very large. You then need to subtract another large number from this which means a loss of precision which results in artefacts like this:


![Soft Shadows](http://farm6.static.flickr.com/5146/5614133967_c57d44dfdc.jpg)


There is a certain amount of noise which is really sad because when that doesnt occur, we do get nice soft shadows on the cheap. Pretty cool! So, very close but no cigar yet!
