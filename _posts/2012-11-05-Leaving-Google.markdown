---
layout: post
title: Leaving Google
---

It seems like the wrong thing to do. Anyone who is familar with the Podcast "Back-to-Work" or anyone with a goal in mind knows that its a bad idea to re-invent the wheel. If there is a good product out there that takes away a lot of hassle for you then you should use that to get what you need to get done, done! The thing is, this has various levels and for me, I like to get my hands dirty. I've been using Google for calendar and mail quite a lot and decided, just recently to step away. There were a few factors (work avoidance being one perhaps - a super form of procrastination) but lessons were learnt and good times had.

![baibai](http://images.smh.com.au/2010/01/15/1041660/googlechina5-420x0.jpg)

I run a few domains o n my own VPS. The thing about this is I need to run websites and therefore, email. I've been doing this happily on Ubuntu with Dovecot and Postfix. There are good guides and I think its more or less, running ok. I decided to use gmail because, lets face it, email anywhere, good spam filtering, multiple accounts and conversation view (probably the most import feature).

The best replacement for mail I've found is [RoundCube](http://roundcube.net/). It has all the features you'd want from Gmail with the exception of multiple accounts. You can install a series of plugins for this however. [MyRoundCube](http://myroundcube.com/) has a plugin manager that you can install by copying various PHP files. You can then download their massive set of plugins, one of which lets you add external accounts. Job done right?

![roundcube](http://roundcube.net/images/homescreen.jpg)

Well, not quite. I needed a database. I decided on PostgreSQL for most of the heavy lifting. This is where everything got hairy. I don't like PHP and since I'm using nginx and php-fastcgi to serve all this, I needed a good PHP setup. I settled on actually building my own from scratch and ignoring the default one that comes with ubuntu. It took a while to get all the options together - there are quite a few. In addition I needed some proper drivers for postgresql.

    sudo pear install -f MDB2_Driver_pgsql-1.5.0b3
    sudo pear install -f  MDB2-2.5.0b3

Roundcube also needs to use IMAP. It will use IMAP over SSL however which is good news. I don't much like the idea of using something unsecured. It took a while to get all this sorted, I must admit. However it all works now, with a HTTPS connection. So far, so good. There are still issues - contacts being the chief among them. Also, there are issues with saving all the data I currently have on google. Thunderbird does a good job of copying all that, so likely that will end up as a backup on my second server. Retroactively adding email is not what I want to do. To be fair, this hasn't yet caused a major problem as a lot of the google stuff is out of date anyway. You never know though.

Mail done. Now we have tasks / reminders and calendar. The former is interesting because I like the idea of Geofencing. Since I'm an iPhone user, I figured I'd give that a go first before I roll my own. I use Mountain Lion on my personal machine so all is well there (but for how long). Calendars are a little more complicated.

[DaviCal](http://www.davical.org/) seemed to be the thing to choose and it turned out to be much easier than I had thought. Again, Postgresql performs the heavy lifting. I had little trouble following the various guides. It seemed fairly straight forward to install.  Again, PHP is needed (shudder),  but [this ubuntu guide](http://wiki.davical.org/w/Ubuntu/Lucid) proved helpful.

With Davical, I can share calendars between various devices. At the moment, Im just using my iPhone's builtin client. Mountain Lion appears not to really like conencting to the caldav server but I reckon I can fix that.

I still need a good solution for notes. I believe Roundcube can take care of that as well. Indeed, Davical may have answers for that. If the task manager doesnt work, maybe that's what I'll do.

I have no real problems with Google, but I know quite a few people do. I've not kept up with the politics of it all but I do believe that keeping control of your data is important. Google, for my money (or not as the case may be), have never done me wrong but I guess I am part of their product. So far, I get a little more spam but not an awful lot and its quite good fun to see the rejections and n00bs trying to hammer my server. Bless.
