--- 
layout: post
title: iPhone RFID Reader
strapline: A small project to hack around with the iPhone and get it to read RFID tags.
introtext: The idea behind this project is to see what the iPhone's serial is capable of and to try and have a little fun with RFID along the way. This reader works with the low frequency (125Khz) tags but I have a half working version for MiFARE Hi-Frequency as well.
tags: electronics hacking
---

<div class="clearfix"></div>
<hr/>
<iframe src="https://player.vimeo.com/video/10133832" width="460" height="280" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
<div class="clearfix"></div>
<hr/>

The idea behind this project is to see what the iPhone's serial is capable of and to try and have a little fun with RFID along the way. This reader works with the low frequency (125Khz) tags but I have a half working version for MiFARE Hi-Frequency as well.

For this project you will need:
<ol>
<li>An iPhone USB Cable (genuine one is best and probably at least 3!)</li>
<li>A JAILBROKEN iPhone!</li>
<li>An <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=8419">ID-12 RFID Reader</a></li>
<li>An <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=8423">ID-12 Breakout Board</a></li>
<li>A <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=8745">Logic Level Converter</a><li>
<li>It's useful to have some IC Sockets for Soldering</li>
<li><a href="http://www.sparkfun.com/commerce/product_info.php?products_id=9416">Glass Tags</a> if you want extra fun or any
125Khz Tags</li>
<li>If you don't like the idea of taking iPhone Cables apart, use <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=8295">an iPhone Breakout Board</a></li>
<li><a href="http://www.sparkfun.com/commerce/product_info.php?products_id=8249">A Battery Pack with a 5V step up</a>
<li>Wire.</li>
<li>Some kind of switch.</li>
<li>A box to put it all in.</li>
</ol>

I should point out that I don't work for Sparkfun.


![rfid](http://4.bp.blogspot.com/_WNXP2eEZSdg/S5uZOisQ0MI/AAAAAAAAAoA/NwIthN0PcYY/s320/IMG_0194.JPG)


The first stage is the wiring of the ID-12. You should attach it to the breakout board then attach a series of IC Sockets to the board so you can easily add and remove your wires later on. Wiring up the ID-12 is quite easy. This particular unit does need to be set to ASCII  output however. To do this you need to solder:
<ul>  
<li>A Red wire from 5V (11) to /RST (2)</li>
<li>A Black wire from FS (7) to GND (1)</li>
</ul>
This sets up the ID-12 into ASCII mode. From here we need simply need to solder in the Ground, 5V power and TX Lines 
<ul>
<li>VCC to 5V (Pin 11)</li>
<li>GND to GND (Pin 1)</li>
<li>RX-I to D0 (Pin 9)</li>
</ul>


![rfid](http://2.bp.blogspot.com/_WNXP2eEZSdg/S5uZOEhsNeI/AAAAAAAAAn4/VBBipUYHjw4/s320/IMG_0193.JPG)


If this is confusing, there is an excellent write-up <a href="http://www.instructables.com/id/Weather-proof-Bluetooth-capable-RFID-reader/">Here</a>

The next step is to wire up the Logic Level Convertor. This is needed because the iPhone works at TTL3.3V whereas the ID12 runs at TTL5V. We need  to step up and down. This little board is quite easy to use. The Schematic and Instructions can be found <a href="http://www.sparkfun.com/datasheets/BreakoutBoards/Level-Converter-v10.pdf">in this PDF</a>. The key is to Solder the ID12's 5V, GRND and signal lines to the first channel on the High Voltage Side of the Board. 

At this point, you can wire in the switch and the battery box into the High Voltage side of the circuit. Wire the positive of the battery into the switch and out of the switch into the logic board and the ID12. Wire the battery's ground wire into the GND of the logic level board and the ID12.


The next step is to work on the iPhone's connection. You should make yourself familiar with the connector. If you use a breakout board, this is quite easy. However, if you are using  an iPhone cable, things are a little trickier. Firstly, you should look at <a href="http://pinouts.ru/PortableDevices/ipod_pinout.shtml">Pinout.ru's iPod Guide</a> that lists the ports we need. We are aiming to use the iPhone's built in serial connection. The pins we need are:

<ul>
<li>Pin 1 for GND</li>
<li>Pin 13 for RX</li>
<li>Pin 18 for 3.3V(+ve)</li>
</ul>

We could use pin 12 for TX as well but the ID-12 doesn't need data sent to it and I have had significant problems in sending data FROM the iPhone. If anyone knows why this is so, do let me know. Regardless, the iPhone only needs to receive and this is well because these two pins are very close together.

First, either solder your wires into the breakout board or open up the iPhone cable. To open a genuine iPhone cable, you need to run a thin blade around the inside of the plastic case.  A small amount of force should release the clips on either side and then pulling on the metal plug with a pair of pliers should do the job. Be careful at this stage though as its  VERY HANDY TO KEEP THE PLUG INTACT. 

Taking apart the plug should reveal 4 cables. A genuine iPhone cable will have a sheath and small gold connectors. Cheaper cables will be glued in place and this can wreak the project. You dont want glue inside the unused sockets and the less force you need to remove the cables, the better.

Removing the small plugs requires a lot of force and yet, you MUST be as delicate as possible. The connectors are attached to the wires with a very small amount of solder. If the connectors snap they cannot be used and if the solder snaps, you will need to solder them again and if you use too much, the plugs will not fit back into their sockets. Also, you are limited on how many times you can place the plugs as the sockets will wear out. I personally went through 5 cables with this method; two of them were genuine. The geunine ones wear much less.



Place the black wire into the ground. You can decide which colour goes into which socket. I chose green for Pin12, white for Pin13 and Red for Pin18. Remember which is which!

The next step is to wire the cable into the LOW level side of the Logic level board. Again, you need only solder the Live, RX and GND but you may do the TX as well. The iPhone should be receiving from the TX-O pin on the board whereas the ID-12 is sending to the TX-I on the board. It can be useful to practice this on a breadboard first to make sure you get it right.

Once this is all soldered together, you can place it all in a box and begin testing. I used a custom built FTDI USB TTL adaptor and read the the values being sent with my laptop.

The next step is to design the software. Jailbroken software is really another topic all together but there are some interesting choices. In the main, I followed the advice given on <a href="http://hcgilje.wordpress.com/2010/02/15/iphone-serial-communication/">This Page</a> which talks about <a href="http://www.openframeworks.cc/">OpenFrameworks</a> and iPhone Serial. As I'm a big fan of OpenFrameworks, I chose this approach. However, I didn't use the serial class mentioned in this blog.


I had previously written some standard C++ to open serial ports for the ID-12 specifically and use it. As this worked, I decided simply to transplant it into a simple OF example. Compiling OpenFrameworks for the iPhone requires signing in order to run on a jailbroken device. There is a small program called <a href="http://www.saurik.com/id/8">LDID</a> by Saurik who is the definitive source for all iPhone development.

To generate a working program you need to:
<ol>
<li>Download the code from <a href="http://github.com/OniDaito/iPhoneRFID">GitHub</a><li>
<li>Open the project in Xcode.</li>
<li>Compile the code using your own signature fake signature or simnply don't sign at all</li>
<li>Using SSH/SCP, copy the executable .app to /private/var/stash/applications</li>
<li>Download LDID in Cydia</li>
<li>Use ldid on a terminal app to sign your app.</li>
</ol>
In short, build with Xcode and use a fake signature as written on Saurik's site.

Serial Communication on the iPhone has been covered very well on <a href="http://devdot.wikispaces.com/Iphone+Serial+Port+Tutorial">DevDots</a> page. The basic C/C++ code there
works quite well for testing if you comment out the sending code.

So now you have the ability to read RFID Tags. But you need some tags to read. For me, I quite like the idea of home automation and similar. There was an odd trend of implanting glass RFID tags into the flesh near your thumb but why bother with that when you can simply make an RFID earring? That way, you can remove it if need be or swap out the actual tag.



