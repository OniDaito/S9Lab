---
layout: post
title: Minimus and Sega
---
My sister has been a big fan of retro gaming for some time and for her birthday I decided to make a USB convertor for the sega megadrive pad in order to play [MAME](http://mamedev.org) the way it's meant to be played.

![minimus](http://farm8.staticflickr.com/7179/7029645643_83b6a3ec75.jpg)

Now there were a few ways I could go about this. I saw a [blog post from dangerous prototypes](http://dangerousprototypes.com/forum/viewtopic.php?f=56&t=2971) that talked about using a PIC. Now I thought this would be a great time to test out the [Bus Pirate](http://dangerousprototypes.com/bus-pirate-manual/) (which is a great little toy) and learn how to program something a little different.

Sadly, it turns out that this is not the case and you need a special adaptor to program PIC chips. What an utterly stupid thing to have done.

![minimus](http://farm7.staticflickr.com/6211/7029644525_1e4d78eee4.jpg)

So instead, I managed to find out about the [minimus](http://www.minimususb.com/) thanks largely to [Tom Wyatt](http://imakethin.gs/) and [Jamie Lentin](http://jamie.lentin.co.uk/embedded/arcade-joystick/). The minimus is based on everyone's favourite, AVR! Only this particular AVR chip has USB built in! You can pick up a minimus from [Mod Traders](http://www.modtraders.co.uk/) and I highly suggest you do. The Minimus is powered by an Atmel AT90USB162. Its an 8-bit chip with 16K of memory. Its not quite as hefty as the Minimus 32 or the later arduino boards but at a fiver you'd be foolish not to buy at least 5. But here is the real clincher.

[LUFA](http://www.fourwalledcubicle.com/LUFA.php) is a full USB stack that can run on the minimus. Yes, it means your small device can run as a USB joystick, keyboard or other HID device complete with all the manufacturer lines and data that normal USB devices have. It's a wonderous thing to behold.

I used Linux and Ubuntu to build and flash my minimus. The instructions are simple enough. I've been fighting AVR and Atmel's corner for a little while now, largelty because of [AVR-GCC](http://en.wikipedia.org/wiki/GNU_Compiler_Collection#Architectures) which is brilliant! The best compiler (okokok maybe clang is good too) has support for AVR chips. No need for extra cash spent on a special programming box. Its all done over USB. Brilliant. So forget PIC, it's time is over. From now on, its AVR, FPGAs and maybe a little ARM.

![minimus](http://farm8.staticflickr.com/7229/7029644081_640d6f8fe4.jpg)

So, the actual Sega pad itself. Well the trick is to check out the latest version of LUFA and start with Jamie's joystick code, albeit somewhat adapted to having just 4 buttons. There is one major hack though for the SEGA pads. They multiplex the signals. So if you checkout [pinouts.ru](http://pinouts.ru/Game/genesiscontroller_pinout.shtml) you can see that there is a select line. What you are not told is that it is up to you to turn this on and off and check which buttons are pressed. So the minimus needs to check as fast as it can, if the various buttons are high when the select line is on and when it isn't on. This took me quite a while to find. Also, the version of LUFA in Jamie's article doesn't work outside of Linux sadly, so for OSX compatibility (and windows for that matter) use the latest from Subversion.

Finally, I ordered an adaptor from Farnell for the 9 pin Atari style port and laser cut a small perspex box to mount it all in. Some wire, a little soldering and some hot glue later and the final device works a treat! :D One happy sister and a pleased hacker! What can possibly be bad about that? So forget stupid PIC chips. It's AVR all the way baby!
