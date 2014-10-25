---
layout: post
title: Numismatic Fun
---


I've been working on a small project for the excellent girlfriend involving the recognition of coins. I've been looking into some various different applications that attempt to do this using computer vision. Turns out its a hard program.

I've also learnt a new word, clearly!

A small program called [Scybot](http://itunes.apple.com/gb/app/scybot-coin-counter/id445453916?mt=8) attempts to count US coins with the iPhone camera. Sadly, it doesnt work. It turns out it simply uses a [Hough Transform](http://en.wikipedia.org/wiki/Hough_transform) by the looks of things. I tried this and here are the results:


<iframe width="460" height="320" src="https://www.youtube.com/embed/CPrVdBdsglQ" frameborder="0" allowfullscreen></iframe>


Sadly, it isn't great on coins that aren't round or at least, not easily. It seems that perhaps training a haar classifier might be the best option? [This blog post](http://achuwilson.wordpress.com/2011/07/01/create-your-own-haar-classifier-for-detecting-objects-in-opencv/) is a great introduction to the idea of training a classifier. It's an intensive task and the jury is still out on whether or not this will actually work. I'll be sure to post my results here when I get them.

Currently, my classifier is still running, as has been for the last 3 days!


At the moment, most of the research seems to be based around the recognition of old coins as oppose to new ones?

