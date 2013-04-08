---
layout: post
title: Museum of Rural Life Smart Audio Guide
category: work
strapline: An automated recommendation system for museums
strapimage: rurallife.jpg
---

##
Have you ever been in a museum and wondered about what you might be missing? Things you might not have seen but want to see? Well, this is a step towards that. A system that tries to figure out other objects you might be interested in.

###
![Rural Life](http://farm9.staticflickr.com/8530/8598489218_4fbd4774c8.jpg)

##
I was approached by Edinburgh College of Art to come up with a way of providing recommendations for museum visitors. The brief was quite wide but the timescale was extremely small. We only had around two and a half months to install, test and deploy an application. No mean feat, especially since we had quite a few ideas on what to do.

###
The victim chosen was the [Museum of Rural Life](http://www.nms.ac.uk/our_museums/museum_of_rural_life.aspx) over near Glasgow. The Museum is quite unique in that it has a working farm a large building housing exhibits and a restored farmhouse. After speaking with the museum, we learned they were interested in an audio-guide. This got us thinking - *could an audio guide collect the data we need in an unobtrusive manner?* The answer to this question is actually, yes it can.


##
Vistors generally lie. Its true! Questionnaires are not the best sources of information because people have a tendancy to either not be interested or they want to please. To get a proper sense of what people may or may not like, we need to be as un-obtrusive as possible and actually *add value* to the experience, in order to keep visitors happy and the experiment fair.

The approach we took was to create an audioguide that would play when a visitor was interested in a particular object and wanted to learn more. We decided that NFC/RFID and a hand-held device would work well in this setting. We settled on using a [Galaxy Mini 2](http://www.techradar.com/reviews/phones/mobile-phones/samsung-galaxy-mini-2-review-1099938/review) as our chosen device, as it was cheap, had a good screen and NFC support built in.

###
![Tap me](http://farm9.staticflickr.com/8522/8598487760_ea283bba84.jpg)

##
The RFID tags themselves were 13.56Mhz tags, mounted behind stickers on a 3D printed icon of the museum; a hybrid sculpture of various objects the museum displays, designed to stand out. Visitors would hold the phone near the sticker and the audio would start playing, along with written information on the object. 

####
<iframe width="460" height="315" src="http://www.youtube.com/embed/HiEQRCDwgc" frameborder="0" allowfullscreen></iframe>

##
At the end of the visit, the user would hand the phone back. At this point, anonymised data is sent back to an awaiting server (AES encrypted to a Node.js / PostGreSQL setup running behind nginx for these interested). From here, we can analyse the data to make predictions. At present, the dataset is quite small but some interesting patterns have already been seen. The items scanned, the ratings these items are given, the start and end times and whether this person is a repeat visitor are all sent for analysis.

##
So far, we have attempting clustering items together using distance metrics to see whether similar objects are *liked* in the same way or scanned at similar times. One approach that seems plausable is to use a Markov chain to predict where a user might want to go next, given what they have just scanned and what kind of vistor they are (repeat and with/without children).

####
![Markov Bot](http://farm9.staticflickr.com/8095/8588850549_1d452d1c6a_z.jpg)


###
In addition to collecting data on scans and likes, we attempted to actually track the vistor's position inside the museum. This proved quite difficult. I spent a lot of time with [WifiSLAM](http://techcrunch.com/2013/03/24/apple-acquires-indoor-gps-startup-wifislam-for-20m/) which didnt work! I have an idea why Apple decided to buy them but I had a terrible time getting accurate results. Sadly, all the data I spent collecting isn't available as the site is now down. 

The Museum of Rural Life has exceptionally bad Wifi coverage - none in fact. The building itself is well shielded from any kind of radio - 3G included. We had a terrible time of collecting data at all since no internet connection was provided. I hacked together a set of routers including 4 [TP-LINK TL-WR702](http://dx.com/p/mini-portable-150m-802-11n-wi-fi-wireless-router-green-115931) units, running OpenWRT. I had hoped these would be small enough to be un-obtrusive but provide enough signal strength to act as beacons for WifiSLAM. Though I had reasonable accuracy in my flat at home, no such luck at the museum. I am told that [Indoo.rs](http://www.indoo.rs) is a viable alternative but I'm not so sure. Indoor positioning is actually collected by museums already, as you can see from the [British Museum's Money Gallery](http://blog.britishmuseum.org/category/collection/money-gallery/) . I see no reason why, in the future, this cannot be collected automatically. The resolution at present isn't great but nevertheless, it should be useful for a whole variety of reasons. [Oona Räisänen's work](http://windytan.blogspot.co.uk/2013/02/a-science-campus-marauders-map.html) looks brilliant and I'll be paying close attention to that in the future.

###
![Prep](http://farm9.staticflickr.com/8385/8598489730_6f0877244a.jpg)

##
Android isn't so bad for this purpose. Locking down the phone proved difficult however. I had to associate the devices with one and only one wifi network and install our applciation as a *home* application, thus replacing the twLaucher that comes with the phone. Even so, it was possible for a user to enter the process manager and uninstall the application! The one way I found around this was to *root* the phone. Sadly, this proved unreliable and I only managed it with one phone in the end. I figured the visitors to the museum wouldn't exactly be hacker types, and with no wifi available, there wasn't much use in breaking them anyway.

One thing Android is terrible at, is Graphics. Maybe this is better on the later versions (we were forced to use Gingerbread due to the phone) but it is unintuitive, bloated and poorly designed in my opinion. When it comes to graphics, style and design, Apple wins hands down. Say what you like about walled gardens. While it may not be ideal, Apple got it right and Android has pretty much copied them. The sheer amount of versions, deprecated methods and devices makes Android a real pain. In this project, I needed SVG support and animation for the interactive maps. I had to implement it with third party libraries, my own hit-testing and a slew of programs to create the correct SVG files. Too much time was wasted here I feel. 

##
![Fergusson Brown](http://farm9.staticflickr.com/8390/8597388203_a7e5930d4c.jpg)

##
Feedback from our visitors was great! Everyone really enjoyed the audioguide and found it gnerally easy to use. Given the amount of time and money spent, I feel we did really well, despite the setbacks given above. There is definitely a lot more scope for experimentation and I feel there will be some interesting applications that will come from this. Museums of the World! You too, can have an audioguide that doesn't cost the earth!



