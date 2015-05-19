---
layout: post
title: Defeating Firewalls
tags: hacking osx
introtext: In addition to my own business, I work part-time over at the University of the Arts helping out students and making cool things. The problem with such large places are their draconian I.T rules.
strapline: Getting around annoying firewalls
---

In addition to my own business, I work part-time over at the [University of the Arts](http://www.arts.ac.uk) helping out students and making cool things. The problem with such large places are their draconian I.T rules. Of course the inquistive finds ways around these. I have a pressing need for SSH - it's something any tech professional can't do without. You just can't. Port 22 is the most sacred of all ports and having it blocked was a pain.


It was suggested that I use [tor](https://www.torproject.org/) which I've had installed for a while on my Mac. I found a handy little script using the amazing [netcat](http://netcat.sourceforge.net/) to move data over Vidalia:

    ssh -o ProxyCommand="nc -X 4 -x localhost:9050 %h %p"

This worked fine but the problem with tor has always been it's speed. Mileage certainly varies but even SSH proved too unresponsive. I needed another option.


Typically, a second IP is needed to proxy traffic over a port such as 80. The problem is I didn't have a second machine available (my machine at home isn't setup yet for this kind of thing). However, after chatting with the *london-hack-space* crew, I was reminded of [sslh](http://www.rutschle.net/tech/sslh.shtml). 

sslh provides a proxy service on your webserver to effectively split any traffic arriving on port 443. Now I run a few websites on port 443 so this solution seemed perfect. sslh is included in the debian and ubuntu repositories. The only configuration needed is to swap out the listen addresses in nginx or apache to localhost and place sslh infront, listening on your servers external ip.

The speed is certainly much greater. Now I can get to work fixing my nginx setup!
