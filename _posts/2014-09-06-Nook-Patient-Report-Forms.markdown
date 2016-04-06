---
layout: post
title: Nook Patient Report Forms
tags: medical hacking android emfcamp
strapline: Running Patient Report forms on a nook instead of with paper
introtext: Anyone who volunteers for St John Ambulance or similar, or works with the ambulnance service will know that patient report forms are a sort of necessary pain-in-the-backside. Paper forms generally require a flat surface, pen and dry conditions. Efforts to replace such forms with iPads and similar haven't caught on due to battery life, capacitative sensing and cost. Enter the Nook.
---

![Nook Detail](https://c2.staticflickr.com/6/5567/15106934241_4e1ae420ed.jpg)

Anyone who volunteers for St John Ambulance or similar, or works with the ambulance service will know that patient report forms are a sort of necessary pain-in-the-backside. Paper forms generally require a flat surface, pen and dry conditions. Efforts to replace such forms with iPads and similar haven't caught on due to battery life, capacitative sensing and cost. Enter the [Nook](https://en.wikipedia.org/wiki/Nook_Simple_Touch)

About a year ago, Curry's in the UK decided to sell off their supply of Nooks for around £30. Needless to say, lots of nerds went out and bought them, but did very little with them. Mine went unused in a drawer until I happened upon the idea to use them as an alternative to the paper-based PRF. As I am responsible for the first aid provision at [EMFCamp2014](http://www.emfcamp.org), I figured this was the perfect time.

Nooks run Android 2.3.3 which is fine for our purposes. I based the form on the current version of the St John PRF but with a few changes here and there. I daresay it can still be improved in terms of UX certainly, but there is time for that. Android development is slow and annoying. UX programming is also terrible so one had to dig deep to finish the project in time.

<div class="clearfix"></div>
<hr/>

<iframe width="560" height="315" src="https://www.youtube.com/embed/wOCfqCNi3HA?list=UUM-XTspgfHt2_BBRV5a3j_w" frameborder="0" allowfullscreen></iframe>

<hr/>
<div class="clearfix"></div>


![Nook Signing](https://c2.staticflickr.com/4/3889/15106946251_543fc60318.jpg)

We first trailed the application around our local St John Ambulance unit, receiving some very useful feedback. It's not often you get to write issues such as "Will it work when covered in blood or vomit?" into your github repository! A valid concern however. One interesting issue which defeats some tablets is the ability to use nitrile gloves with a touch screen. Fortunately, the Nook gets around this issue.

We added an option for minor wounds. At a festival, you typically deal with a lot of minor cuts and scratches. Filling out a full paper PRF for such things is a pain, so we have the Nook fill in most of the basics for you.

Working on the feedback, we added some more features, getting another couple of Nooks for the festival so we had enough for all the teams and one to train with. One thing people asked about, revolved around hand-over and returning patients. There is currently no support for this sort of transaction. The reasons become clear when data security comes to the fore.

![Nook Stack](https://c2.staticflickr.com/4/3886/14923294440_19c63f50bc.jpg)

We decided that each unit should be totally stand-alone, with no wifi connection of any kind. Once a PRF is completed, it is encrypted using RSA and a 1024 bit public key (yes, I shall increase the key size in the next version for sure!). This means no-one can read the PRF unless they take it to a person with the matching private key. This leads to a reasonable level of protection from prying eyes and theft but it does make patient handover tricky.

For most festivals, WiFi is, in fact, available. EMFCamp certainly has it, as do festivals such as Reading or Glastonbury. In the latter cases, the network is for medical staff only and has no connection to the Internet. In such a case, handover could be possible. It is conceivable that an ambulance crew could hold the private key on their truck, allowing a smooth handover. In our case, we just keep the PRF open and grab another nook if another patient walks in.

![EMF First Aid](https://farm6.staticflickr.com/5561/14970455747_4e2ed916d4.jpg)

Battery life is great on the Nooks, although the clock on the main page seems to drain the battery if it is left on. One thing we did was to replace the screen-saver on the Nook with a map of the EMFCamp site, along with the address and all of the emergency numbers.

Feedback at the actual event seemed to be generally positive. There is a lot more work to do but for these interested, there is a [github repository](https://github.com/OniDaito/EMFMedical) with all the details on-line, ready for feedback.

