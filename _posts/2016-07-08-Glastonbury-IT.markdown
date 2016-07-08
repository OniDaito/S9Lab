---
layout: post
title: Glastonbury Medical IT
introtext: I go to Glastonbury Festival most years. It's the biggest and most famous festival in the UK I'd say. This year, I volunteered to help out the Medical IT crew.
strapline: I volunteered to help out with the Festival Medical IT crew at Glastonbury this year, and this is what I learned.
tags: IT glastonbury festivals
---

I go to Glastonbury Festival most years. It's the biggest and most famous festival in the UK I'd say. I go mostly because of the experience of volunteering with [Festival Medical Services](http://www.festival-mmedical.org) as a first response, emergency medical person. i could write a lot about that  (and maybe I will in the near future) but since this blog is mostly about computing and such, I'll stick to that. This year, I volunteered to help out the Medical IT crew.

FMS's IT systems are mostly based around the triage and patient care aspects; something I've been looking into myself for [EMFCamp](http://www.emfcamp.org) later this year. The system I helped support was based at the main hospital reception, over at Big Ground. Patients often self report here and are triaged by a triage nurse. This is where the system starts.

The nurse has an iPad with a web-browser based application that consists mostly of a form. With the iPad it's also possible to take a photograph and attach that to the patient details. The patient then moves one desk along to someone operating a normal PC, who asks a few more questions and books the person in. At this point, the details are printed onto paper and placed in the appropriate tray. There are trays for doctors, dentists, nurses etc.

When the patient is ready to be seen, they take their paperwork and are treated. The health care professional (HCP) doing the treating has their own hospital paperwork which they then fill-in. It's unclear whether or not the patient gets a copy of this or not sadly - I didn't see. The HCP's paperwork is stapled to the initial paperwork and placed in another tray.

At the back of the reception is the so-called 'back office'. Here, teams of receptionist types enter the data back into the system, filling in the HCP's notes into the medical database. This interface is another web-based form. This process seems to take a while and can be error prone, not only with human errors but web-browser ones it seems.

As one of the IT support guys, most of the time you are spending covering for bad programming practices brought about by the web application being quite poor. Things like clearing the cache, restarting the browser and occasionally, clearing the ARP cache on the server. There is only one server, running over wireless, using IIS. The whole system is windows based in the main, with the iPads using safari.

There are a couple of remote sites such as Park and Cabaret that have treatment centres. I'm not sure of the network connection between these but its likely to be using the infrastructure that is actually buried into the ground in places by the festival itself, so the BBC can have all their uber fast network connections for all the video that they stream. Sometimes this connection can be a bit slow. This becomes apparent when there are many patients, back office tasks and web-requests.

Changing printer toners is another job you find yourself doing. Im actually surprised most things are still working towards the end of the festival, because if they haven't been bashed or swiped with the fingers of a thousand nurses, they are covered in mud or dust. It's certainly not a clean environment for sophisticated electronics!

Before the festival, I ended up installing Yammer, WhatsApp, Slack, Signal and I almost ended up with Telegram as well! So many different communications things these days. Yammer and the Microsoft enterprise is definitely the order of the day with FMS and it certainly threw me as I'm generally a Linux person, but it's good to switch it up now and then.

The system, as it's setup now, is quite inefficient and brittle. For starters, there didn't appear to be a backup server. An odd thing really. Most importantly, the app they are using was designed for disaster relief by a company based somewhere in South East Asia. I do wonder why they made it web-based? Native app with local storage would have been much better. Sometimes, the connection would drop out. If that happened, you couldn't actually triage more patients. Printing out only to re-enter later seemed crazy. Why not just have iPads for the HCPs as well? Storing data locally, then sending up to a server and confirming it would be better. 

The final problem comes down to the web interface itself. Certain UX decisions were poor. Apple does a good job of its UX so leveraging that with a native app would have been smarter. Often, the feedback from the application would be confusing or incorrect and cause errors to creep in. 

The problem seems to sit with the HCPs; their preference for handwritten notes means that printouts have to be taken. Perhaps there needs to be a better way around that?
