---
layout: post
title: Lowry to Life
category: work
tags: work kinect computervision opengl
strapline: An outdoor installation, celebrating LS Lowry
strapimage: lowry.jpg
---

While I was up in the North, working on some personal projects, I was put in touch with a couple of lovely chaps, Alastair Eilbeck and James Bailey; two artists working on some interesting projects. They came to me with an idea for promoting The University of Salford and The Lowry. I've been a fan of some of Lowry's paintings and this was an opportunity not to be missed.

The idea was to take members of the public into the painting of [Piccadilly Gardens](http://www.thelowry.com/gifts-and-souvenirs/prints-and-limited-editions/piccadilly-gardens-1954). To do this, I worked with the [ASUS Xtion](http://www.asus.com/Multimedia/Motion_Sensor/Xtion_PRO/) and the OpenNI toolkit to extract the skeletons of the passers-by. 

<div class="clearfix"></div>
<hr />
<iframe src="https://player.vimeo.com/video/33123038" width="460" height="281" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
<div class="clearfix"></div>
<hr />

The Real location is the painting  and live people are converted to lifesize Lowry characters ( we set up the stage so that it matched the painting perspective). A combination of live people beamed from the real location and those in Salford, shown as small Lowry characters within the real painting (foreground and midground) made the installation complete.

This is all quite straight-forward but of course, there are many problems. The first is the issue of calibration. Most calibrations with the kinect are personal and then stored for later use when the Kinect/Xbox actually recognises you. This is, of course, not practical in this situation, so we calibrated the system with Alastair and James and used that for all the participants.

The second issue is the environment. The Kinect and Xtion are designed to work indoors, preferably with a solid wall behind the player. We had none of these so we spent a long time testing, the results of which you can see here.

<div class="clearfix"></div>
<hr />
<iframe width="460" height="280" src="https://www.youtube.com/embed/Npw1tbOMHqk" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr />


It seems that the Xtion performs slightly better than the Kinect but the problem of tracking is a big issue. Data is often missed or incorrect. This means an attractive and artistic solution is needed. We hit on the idea of recreating the characters as puppets. This is where the wonderful [Box2D Library](http://box2d.org/) came in so handy. It's a fantastic library, so donate to them if you use it.

Working with puppets gave a much nicer effect that felt in-keeping with the Lowry style. 

![Working late at Amaze](http://farm7.staticflickr.com/6111/6231847697_0e73bf9cf2.jpg)


Of course, there is more. The University of Salford wanted the display to run over two sites. The participants in the gardens would appear inside a painting, hanging on the wall at the Lowry itself (it turned out to be at Salford University but nevermind). In order to to make this work, I wrote a simple TCP server/client setup with the [boost::asio](http://www.boost.org/doc/libs/1_48_0/doc/html/boost_asio.html) libraries that seemed to work quite well. As this is already a part of Cinder this could be integrated seemlessly.

Everyone on this project was a hero, none more so than the illustrator Maria Pearson. Without her input, this would not have worked. Maria needed to create 4 views for the same character which were then mapped using a rather large XML file to the puppets themselves.

Initially, this process was quite time consuming, so extra features were added to the program to enable faster character creation. At one point, I thought we may need to actually create a seperate editor program but that turned out not to be the case.  

It turned out to be a big event. It was covered in the [Manchester Evening News](http://menmedia.co.uk/manchestereveningnews/news/s/1464384_hi-tech-display-lets-you-join-lowrys-matchstick-men) and [BBC North West Tonight](http://www.youtube.com/watch?v=LhSUx_MlMAk&feature=youtu.be&t=3m23s) as well as the [BBC News Website](http://www.bbc.co.uk/news/uk-england-manchester-15643875)


<div class="clearfix"></div>
<hr />
<iframe width="460" height="280" src="https://www.youtube.com/embed/LhSUx_MlMAk&amp;start=203" frameborder="0" allowfullscreen></iframe>
<div class="clearfix"></div>
<hr />


I'd rather hoped the Manchester weather would actually do its usual thing of being overcast and grey as the Xtion performs better in such conditions. Sadly, this didn't happen at all. Terrible! You can never, EVER rely on the weather, even in a place as predictable as Manchester.

One interesting and tricky aspect was the idea of history. Alastair and Jimi wanted people to appear on the painting, even if there were no actual participants at that time in the gardens. This meant saving certain characters to disk. For this, I decided to use [MongoDB](http://www.mongodb.org/) with the C++ binding. The problem here is that although Cinder uses Boost, the version I had bundled was incompatibile with the version used by Mongo. Disaster! In the end, I needed to use both and simply do the usual hack of only passing simple types between the two classes. Essentially, the puppet strings are saved to the database a few times each second and recalled when there are no players on the scene.

Technically, I couldn't have done this without Github and Cinder. I've written my own classes to take care of the skeletons and players and swap them in and out as they appear and disappear. Ultimately, github is great for messing with your code, revamping and refactoring as needed. Cinder is a great tool and it's use of boost certainly helped.


Personally, I learnt quite a lot on this job. It has been going for sometime, and progress had been quite sporadic. We'd considered many different ways of illustrating the characters, setting up the network and indeed, getting the code to work on Jimi's computers. There was one long session that lasted about 3 days over in Manchester and the strain was beginning to show although James with his boundless energy certainly helped! 

![Jimi](http://farm7.staticflickr.com/6116/6231844353_8ee7631f7b.jpg)


Overall, one couldn't ask for better collaborators. A fun project that made people laugh, that paid on time and helped me learn new things. That, for me, is the perfect project.
