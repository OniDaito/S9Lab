---
layout: post
title: A Touch Wall under the M1 Motorway
category: work
strapline: Trying to build a touchscreen wall for Electromagnetic Field
strapimage: touchwall.jpg
---

It's not often you get the chance to put a massive touchscreen underneath the M1, but that is exactly what I did at this years [EMFCamp](http://www.emfcamp.org) - The first hacker camp in the UK. Many lessons were learnt in the making of this and there are many things I'd do differently in the end. The results weren't bad considering and I learnt a lot through it.

![Nose Control](http://farm9.staticflickr.com/8437/7928922666_3ee2eb9c23.jpg)


Deep underneath the M1, we had a bar and the idea was to get some sort of shiny information point going, possibly on a touch screen of sorts.  The idea I had in my head was some sort of information point that would allow people to check all the nerdy stats of the camp and similar.

![Under the M1](http://farm9.staticflickr.com/8177/7928922532_61d9575150.jpg)

Ultimately, we ended up watching Dr Who on the the screen instead. People seemed to like it.

The build itself is the most interesting thing. I had started with a basic design, mocked up in Sketchup, based around a frosted glass coffee table that I'd scrounged from a flat in Camden using eBay. I had always wanted to learn how to weld and thanks to Hipster Chris at the London Hackspace I was quickly taught how to arc weld. The [OneStopMetalShop](http://www.onestopmetalshop.co.uk) provided the box steel and the rest was blood, sweat and tears.

The overall result wasn't too bad but there were a few peroblems. I wanted to mount the glass with room for the lasers in the frame. Turns out the laser units are longer than 30mm which is the size of the box steel. Sadly, this meant that the lasers stuck out at the sides which wasn't a very good look in the end.  I thought about mounting the lasers in the corners but the glass was too large. There simply wasn't enough space between the glass and the steel. I suppose that means I did a good job with the welding in the end. Can't be too grumpy I suppose.

![Welding](http://farm9.staticflickr.com/8448/7794570486_4abb9601ca.jpg)

![Sugru-ing](http://farm9.staticflickr.com/8425/7794560496_f71403e0af.jpg)

The setup is a basic Laser Light Plane or LLP, with a PS3 eyetoy and a projector. For the event, the lovely Nigel from London Hackspace loaned me a nice projector that was quite bright. Turned out to fill the screen quite nicely which was pleasing. I used a filter from eBay that claimed to be a narrow 850nm pass and cut for the size of the PS3 Eyetoy. Without the filter, the eyetoy had real problems focusing. The problem appears to be that the filter performs some kind of focusing. There are two versions of the eyetoy - one of which can't focus at all when you remove the IR filter. From all the photos I had seen of the two versions, I felt I had the right version but I was experiencing a macro effect; everything was in perfect focus but only at ranges of a few centimetres. Adding the filter partially fixed this.

![Setup for Testing](http://farm9.staticflickr.com/8299/7794541614_34136263c9.jpg)

The lasers were initially 650nm but these proved to be too faint. I bought another set of 850nm lasers. The cost came to about £100 which was quite considerable when you add on the box steel and the glass.  The results seemed ok once I ramped up the contrast and lowered the brightness.  Natural light pretty much kills the screen unfortunately, whereas office lighting seems fine.

<object width="460" height="315"><param name="movie" value="https://www.youtube.com/v/eNyIf2tHdMk?version=3&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="https://www.youtube.com/v/eNyIf2tHdMk?version=3&amp;hl=en_US" type="application/x-shockwave-flash" width="420" height="315" allowscriptaccess="always" allowfullscreen="true"></embed></object>


In the end, I mounted the lasers inside the frame and used hot glue and Sugru to hold the lasers in place whilst doing the alignment. This is *definitely not the way to do laser alignment*. I had so much trouble getting this to work and in the end, it worked but only for a short time. By the time we got to Milton Keynes, the alignment was off again I think.


![Hot Glued Laser](http://farm9.staticflickr.com/8427/7794565790_e77520948b.jpg)


I think, if you end up using hot glue, *you are doing it wrong*!


I had mixed results during the testing phase, but ultimately, it seemed to work. I had awful trouble getting the Linux version of [Community Core Vision](http://ccv.nuigroup.com/) working sadly. I started to write my own but ran into problems with using Pixel Buffer Objects to speed up the video recording from the camera. In the end, I realised I would never get it finished in time and decided to install Windows. This is no bad thing as learning a little Visual Studio again is no bad thing. This provided much better results and the final test ran something like this:


<object width="460" height="236"><param name="movie" value="http://www.youtube.com/v/Ru7fUDkT5Kk?version=3&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/Ru7fUDkT5Kk?version=3&amp;hl=en_US" type="application/x-shockwave-flash" width="420" height="236" allowscriptaccess="always" allowfullscreen="true"></embed></object>


On arrival at Milton Keynes, I still hadn't written all the software though I had begun to. I figured I'd get chance at EMFCamp to finish it off but this was a little foolish. Though I got quite far with the concept, I had to revert to Cinder which still forces the old way of doing OpenGL upon you which I've tried really hard to get away from. That, coupled with all the other stresses meant that It was never properly working. The map idea I had was too far removed from reality to be noticeable and the whole thing was only partially ready. In the end I reverted to Memo Akten's fluid simulation but even that seemed lack luster in the end.

We had a few people playing with the calibration stuff but overall, the screen itself wasn't a big success. People asked questions and there was a bit of playing around but it wasn't really working well and wasn't finished. I actually found the whole experience of the screen at the camp to be a negative point and I realised that I'd become so obessed with finishing a shiny project in time, that I'd missed out on a lot of other good things going on.  I think I need to plan better and not get so carried away. I think a project like this requires a few more failures along the way before you end up with a great result.


![Programming under a bridge](http://farm9.staticflickr.com/8299/7928923256_ffbe54e921.jpg)


![Bar under the M1](http://farm9.staticflickr.com/8042/7909230240_b79cfbd8b4.jpg)


A lot of the problem revolves around software. I really don't like the fact that we are still using TUIO. It would be good if we could just plug a touch screen into Android and just use the built-in touch and gesture software. There is a lot of duplication and reinventing the wheel here which I really didn't like. So overall, I think I needed to have this sorted and properly ready to go at least a month in advance, with my own software, running under Linux. Ultimately, I'd consider this project a failure in terms of realising a project but a success in learning new things and prompting interesting questions at the camp.

The frame is now, either in Chris's possession as a series of small bits of steel or forever under the M1 as a testament to the awesomeness of EMF.