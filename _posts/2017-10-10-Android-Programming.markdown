---
layout: post
title: Android Programming and Zotero
introtext:
strapline: 
tags: code programming android zotero
---

One of the projects I'm working on whilst I'm over in the states is an Android client for [Zotero](). If you aren't familiar with this amazing program, Zotero is a way of keeping track of all your documents, especially these pdfs you use for research. If you are the kind of person who needs citations and references in your life, then this is the best program. I've tried [Mendeley]() and [Evernote]() but this is the best of the bunch. In many ways, it's because it does enough things, but not too many, and it does them well. You want metadata auto extracted from PDFs? You got it! You want multiple device syncing? Check! You want a browser plugin that can scan a webpage from a place like the IEEE and scrape the metadata? Done.

What I like to do is read papers on my tablet, either in an armchair or, more recently, the hammock we have outside :D I mean why wouldn't you? I can tell you why not - a good client for Android is hard to find. [Zandy]() is the closest I've found so far, but the project appears to have died about 3 years ago, and I found that it just didn't seem to do the business for me. Certain things wouldn't work right for me, so I thought it was time to write my own. I figure if it proves popular, I can stick it up on the Android store and charge 99p a time or something. We shall see.

In essence, the program is quite straight forward, at least at a high level. You are doing things like:

* async REST calls, leading to ...
* JSON parsing, which in turn leads to ...
* WebDav downloads of PDFS.
* Offline storage of metadata, preferably in a database of somekind (so SQLite basically).
* ACID style requests, sending data back to the Zotero servers.
* OAUTH (oh noooo!)
* Lots of User Interface testing and messing about.
* Syncing, both completely afresh and partial

So basically, the world's most boring program. But like many such things, very useful indeed for the person who needs it.

Android programming is a strange beast I have to say. It embodies both the least interesting and potentially powerful aspects of the profession. You get to make a personal and very physical item (your phone) do something. If you are successful you can easily ship it to a great many people around the world. But the day-to-day is figuring out the totally arbitrary organisational decisions a great many developers at Google and co have decided. There's usually one boring and tedious way to get something simple done. You spend hours just trying to search StackOverflow for the right bit of code because really, all I want is to put in a two tier list and *boom*, you find the one answer that *used to be right* about a year ago but now you have to do it a different way.

Annoying doesn't nearly describe my experience when it comes to getting all the styling sorted. There are so many versions of the Android OS and many different models of phone, it's frankly amazing it works at all. But make one slip-up with your project and everything will stop working as your gradle process fails to import some version of AppCompat and values-21.xml or some other bollocks you never knew was needed.

Basically, you need to fly very straight, make no slip-ups with project organisation and be sure about how you target what you are targetting. This is made harder by how all the Android versions are numbered and named. You have a number for the API, such as 22 or 26. Then there is a name like Lollipop or Icecream Sandwich and then there is a version number that goes with that, such as 4.4. Really, the only one that matters to a developer is the first one. 

But to make matters worse, you have a compilation number, a target number and a minimum number. The [Android page on the subject]() gives a reasonable overview but it did take me a while to figure out how to make my program the way I wanted it made. One thing that annoys me about the phone industry is the planned obselescence. There is nothing in my program that requires advanced features of any particular phone so I wanted to support phones running API 19 (KitKat) and above. After a lot of wrangling and failure it seemed the thing to do was set the *compile* version to the latest I had (26), but set the *minimum version* to 19 (and the target to whatever I'd tested up to, which in this case was 22). It seems counter-intutive to compile higher but target lower, but I *suspect* that unsupported features are just not included whereas newer versions of older routines that still work on earlier OSs are retained.

  
