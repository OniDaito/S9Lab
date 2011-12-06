---
layout: post
title: Smiling-Film-Student-Geekery
---

<object width="480" height="320"><param name="movie" value="http://www.youtube.com/v/mhAcRlNq9JU?version=3&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/mhAcRlNq9JU?version=3&amp;hl=en_US" type="application/x-shockwave-flash" width="480" height="320" allowscriptaccess="always" allowfullscreen="true"></embed></object>

The above video was recorded by Opheila Finke; one of the students at CSM. She came to me with a request that blew me out of the water because I'd had a similar idea myself. She wanted all the machines in our lab to play a video at the same time. I've spent quite a bit of time on this but I'd never gotten to the stage where I could take over a screen remotely. It turns out this is indeed possible with one subtle command.

Using the screensaver, written in Quartz Composer by a colleague of mine, Sion Fletcher, seemed like the best idea as we could probably activate it remotely. Since I had the list of IP addresses and full sudo on all the boxes, setting up the screensaver was a doddle. Most of the leg work had been done. 

    /System/Library/Frameworks/ScreenSaver.framework/Versions/
    A/Resources/ScreenSaverEngine.app/Contents/MacOS/ScreenSaverEngine 

Running this starts the screen saver. So far so good. Of course, you'll get a lot of errors if you try and run this remotely over SSH, even with Sudo. These of you used to Linux (and lets face it, you are if you read this) will know all about XSessions and similar. Something like this didnt work:

    sudo su student -c '/System/Library/Frameworks/ScreenSaver.framework/Versions/A
    /Resources/ScreenSaverEngine.app/Contents/MacOS/ScreenSaverEngine'


Now *student* is the logged in user and therefore, I figured we could attach to their XSession (or whatever the OSX equivalent is). This means there has to be a logged in user for attachment to work; I don't know of any way to connect when just the login screen is visible.

The problem is, this didn't work! I was pulling my hair out until a good friend, MS7821 on the #london-hack-space IRC channel pointed out that I wasn't setting the environment over the *su* command. Now I'd seen this before when playing with the Python subprocess module - you could indeed set the ENV variable. Can you spot the difference in the working command?

    sudo su - student -c '/System/Library/Frameworks/ScreenSaver.framework/Versions/
    A/Resources/ScreenSaverEngine.app/Contents/MacOS/ScreenSaverEngine'


The *-* is quite important after the su. It sets up the environment properly and that's great - it means the process can attach to the screen itself.

![1.8 tonnes of iMac doing my evil bidding](http://farm7.static.flickr.com/6100/6328718926_27f90ba92a.jpg)

If you scroll in to 2:45 on the video, you can see the effect we came up with. It's great when a student has the same or similar idea as you. You get to look like the worlds greatest hero when it goes well. Smiles, hugs and laughter was had! That day was a good day!