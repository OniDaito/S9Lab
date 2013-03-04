---
layout: post
title: Linear Rail Time Lapse 
---

##
I'm a bit of a photography nerd, it has to be said. when I was introduced to [OpenMoco](http://www.openmoco.org/) I knew I was in for some fun times! I immediately chanced upon the [Chronos](http://sourceforge.net/p/projectchronos/home/Project%20Chronos%20Home/) by Chris Field, I immediately jumped at the chance. I've enjoyed doing time-lapse stuff for a while and I figured parallax was the next thing to try.


####
<iframe width="460" height="315" src="http://www.youtube.com/embed/sluvAehKTwg" frameborder="0" allowfullscreen></iframe>

###
The Chronos is basically a linear rail with a screw thread, carriage, stepper motor and control unit. Chris has done a great job in creating a controller board, based on an Arduino. The board itself has all the points ready for the various dials and controls. Chris has a large list of parts you can order from Sparkfun. Soldering the board is not that tricky really - you can do it in about an hour if you are handy with a soldering iron.

##
![Chronos Board](http://farm9.staticflickr.com/8235/8363459833_da6f71f4a9.jpg)


##
The box itself is a little trickier. There are no designs available so you need to make one yourself which is a pain really. That said, a little QCad and a laser cutter and all is well! Im quite pleased with the box funnily enough, though I do wish I'd got it just right! There is a 1mm gap on one of the panels. Making boxes in QCad is definitely something that needs to be automated.

##
![chronos box](http://farm9.staticflickr.com/8510/8409958211_69916f16a7.jpg)

##
![Igus Rail](http://farm9.staticflickr.com/8211/8294180546_86cbf2d362.jpg)

###
The same was true of the endstops. No designs were available and Chris' metalworker wouldn't release the designs. However, the company I bought the rail from (IGUS) do provide CAD drawings for you to work with. Thankfully, they have DXF format too, so QCad, yet again, proved its worth. I had bought the recommended, 12V unipolar stepper that Chris mentioned and managed to find the designs for that. With some M10 bolts, I managed to create both the moutning points. I needed to shave off part of the rail using a kiss cut from a circular saw. The bolt for the stepper needed their heads filing down and the rail itself needed to be tapped to accept 4 M10 Bolts. Oddly enough, we had a small manual that tells you how big the hole needs to be in order to be tapped to a certain thread. Marvellous! The metalwork needed on this project was not inconsiderable.

The carriage and the drive actually proved to be quite easy, despite my dread! I couldn't find a good supplier of lead-screw in the UK! Crazy really, but its quite a specialist item. Lead screw is basically, a threaded bar with a particular kind of thread used to convert rotatary motion into linear motion. There is no play in the system which is great for this sort of thing, but ordering from the USA proved expensive. I decided to cheat and use 6mm threaded bar and two nuts with a spring.

Why two nuts with a spring? The carriage design has a small box below the main runner which the bar runs through. The two bolts are pressed outwards, against the walls of this little box by the spring. This means there is very little play in the nuts and thread. Bingo! A ghetto-anti-backlash nut for almost no money

##
In the end, the most difficult part of this project turned out to be the stepper driver. The [Pololu stepper in question](http://www.pololu.com/catalog/product/1201) simply didnt work for me. I ordered 3 from two different suppliers and all of them failed to turn the rod in both directions. I was beside myself with despair and rage, until I borrowed one from a friend and ordered a knock-off version from eBay. Both worked straight away, first time! It is indeed possible to have a bad batch and so, with the problem solved, I finally managed to get the thing built.

##

![magic arm](http://farm9.staticflickr.com/8087/8528137302_4690bb7d75.jpg)

##
In order to mount a camera to the system, I decided to buy a Manfrotto magic arm, with an SLR mount at one end, and a magic clamp at the other. It is possible to use a proper bolt, mounted upside down on the carriage but I didnt have the time to do that. I figured a clamp was nicer anyway. The motor still has enough ower to move the thing, which is great. Im using a 12v supply from the mains here but the intention is to eventually use some kind of Lipoly battery.

