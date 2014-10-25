---
layout: post
title: Echoforms at Lexus NX Launch 
category: work
strapline: Taking Echo-forms to the Paris launch party for Lexus NX
strapimage: lexusparis.jpg
introtext: Hellicar and Lewis and I were asked by Lexus to take EchoForms to their launch event in Paris. 
---

I've spoken about [Echo Forms](http://www.section9.co.uk/posts/2014-07-28-Kaleidoscope.html) in a previous post, but this time, [Hellicar and Lewis](http://www.hellicarandlewis.com/) and I were asked by Lexus to take it to their launch event in Paris. This involved building a different form of interaction from the mouse and pointer style and a machine with a little more grunt. 

The existing web-page uses the mouse to drag and distort a kaleidoscope. For the live setup we decided to use a Logitech camera within the browser in order to generate some kind of user feedback. The plan involved using the [Lucas-Kanade Optical Flow algorithm](https://en.wikipedia.org/wiki/Lucas%E2%80%93Kanade_method) used in the [JSFeat](https://github.com/inspirit/jsfeat) library.

![Lexus NX Gig](https://farm4.staticflickr.com/3885/15163697500_c281683ba4.jpg)

JSFeat is quite impressive! It amazes me still that we can do such things inside a browser context, even if they will always be slower than their native counterparts (although thats perhaps not entirely true). The algorithm performs reasonably well so we went with that.

Accessing the camera using [WebRTC](http://www.webrtc.org/) is fairly straight forward. It would be nice to get a little bit more control over the camera in the same way you can with UVC devices under Linux and similar but nevertheless, getting the frames into WebGL is fairly straight forward if a little slow at higher resolutions.

Live setups are a different kettle of fish though. The last thing you want to be doing is changing code on site, though I was totally prepared to do this. Pete and I turned up really early in order to test and tweak, only to find the whole setup was behind schedule and we were bottom of the bill. A damn shame. *Hurry up and wait* was the order of the day.


<iframe src="https://player.vimeo.com/video/107183168" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> 


Eventually, the setup went ahead with only two hitches. The first involved the actual interaction and the way the installation was setup. Using a plinth in a low light position means that people are not as visible as they might be, causing issues with the tracking. In addition, they are made to perform on a stage which puts people right off. Nevertheless, we kept up our end of the bargain ;)

The second issue revolved around the team wanting a live feed from the mac in order to feed it to the VJ. This request came really late and I decided to try and honor it. This is often a mistake but I was fairly confident. Sadly, I couldn't make OSX output to three displays. We had two thunderbolt to HDMI leads for both of the TVs and one HDMI to the mixing desk. OSX was not happy so we settled with just one TV. 

![Lexus NX Gig](https://farm3.staticflickr.com/2947/15350395935_ab79ae5214.jpg)

The world of such private events and shows is one I'm really not used to. There were lots of *beautiful people* there, big-wigs and celebrities. Not something I admit to knowing a lot about but never-mind. It's an interesting world to look in on, once in a while. 

![Me doing last minute fixes](https://farm3.staticflickr.com/2948/15163691320_1a5a6e238a.jpg)

Live gigs do present their own set of problems. Best advice is to bring things like gaffer-tape, cable ties, your laptop and a spork! :D