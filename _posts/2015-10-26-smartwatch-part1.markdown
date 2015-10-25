---
layout: post
title: Building a SmartWatch Part 1
strapline: I've embarked on a project to make my own smart-watch.
introtext: Watches in general fall into one of two categories - a tool to tell the time, or a fashion statement. Increasingly, I believe the latter category is larger than the first. With the advent of the iWatch, Pebble and the like, fashion and making a statement has moved into technology. It's not quite a new thing but nevertheless, it's something I'm not too fond of. My solution? Make your own smartwatch.
tags: electronics
---

I have an issue with smart-watches. Watches in general fall into one of two categories: a tool to tell the time, or a fashion statement. Increasingly, I believe the latter category is larger than the first. With the advent of the iWatch, Pebble and the like, fashion and making a statement has moved into technology. It's not quite a new thing but nevertheless, it's something I'm not too fond of. My solution? Make your own smartwatch.

There is a precedent for this. Steve Wozniack sports [a pretty fly nixie tube watch](https://www.youtube.com/watch?v=m4R3hODnTGo) which he made himself. It's pretty cool, but also a statement of sorts too. I've been meaning to up my game with electronics anyway, so I've been working on a few initial prototypes.

![smartwatch](https://c1.staticflickr.com/1/670/22444952516_f5550abeb0.jpg)

I use [DesignSpark](http://www.rs-online.com/designspark/electronics/) on the recommendation of a sparky friend of mine who has a successful business building bespoke electronics. I have a [Stellaris Breakout Board](http://www.digikey.com/product-highlights/us/en/texas-instruments-stellaris-launchpad/2537) - the same board used in the cubesats - that I figure I can use for development. Most of the parts I've ordered from R.S Components though that might change in the future. I've previously used EAGLE, which I'd also recommend.

I decided the first stage would be to build a breakout-board with the easy components attached. This includes a display, an SD Card, a small joystick button combo and a power supply for the OLED display. I've decided to go with a colour screen, the same used in the [tricorder](https://github.com/tricorderproject/arducordermini) project, as it's fairly cheap and works with an [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus) interface. The SD card also has a straight forward interface, so I figured the only tricky part was the power supply. 

<div class="clearfix"></div>

The first board was a little large and sadly, didn't work. I'd missed out a logic high line into the OLED driver chip. These boards I had made at [seeed studios](http://www.seeedstudio.com/depot/) who you may remember I tried to visit on our [recent trip across Russia and China](https://www.section9.co.uk/posts/2015-04-08-transsiberian-Part-15.html). Sadly, the day we turned up in Shenzen was a Chinese public holiday. Oh well. The eagle-eyed amongst you will notice the wire I've hastily added in order to test whether or not I could save the board. Apparently not. In addition, the footprint for the SD Card reader wasn't quite right, so that also needed adjustment.

![first revision](https://c2.staticflickr.com/6/5629/22284149449_7abc1f39e5.jpg)

The second revision of the board is much tighter. I've added a ground-plane this time, which massively improves the layout. The number of vias is reduced as well as the number of traces. I've managed to shrink the board size down and repair the SD Card footprint. By moving it to the underside I save a lot of space. The boards were made by [DirtyPCB](http://dirtypcbs.com) who are really cheap, sarcastic but had a quick turn-around and no faffing. So far they win over both Seeed and Ragworm. 


<div class="clearfix"></div>

![underside of mark2](https://c1.staticflickr.com/1/711/22283006210_dc839efc1c.jpg)

I had some issues getting the 13V OLED line to work. I felt sure I'd fixed it but it still wasn't working. It turned out there were three things to fix. Firstly, the diode was the wrong way around (an easy mistake to make when using surface mount parts). Secondly. the inductor package I'm using is really not meant to be hand soldered and the contacts were not seated properly. Finally, there was a short on the OLED connector. A single strand of solder braid had become caught between three of the pins. Once it was removed, the 13V line spluttered into life!

With all the initial parts in place, the next step is to write some basic code and get the screen up and running. The next hardware step will probably involve mounting the actual CPU, it's timing crystal, lipoly power pack, programming headers and some sort of connecting to the outside world. I'm looking into GPRS as its practically free and low powered. 
