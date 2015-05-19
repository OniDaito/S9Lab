--- 
layout: post
title: Deutsche Bank Installation
category: work 
tags: work opengl
strapline: A massive installation for Deutsche Bank, written in Cinder
introtext: It's arrived! Finally, out of NDA we have the Hong Kong Deutsche Bank Installation. This was led by the rather talented Field.io who decided to pass around some of the work to local creative, programming types such as MSAVisuals. 
strapimage: deutsche.jpg
---

It's arrived! Finally, out of NDA we have the [Hong Kong Deutsche Bank Installation](http://www.msavisuals.com/deutsche_bank_hong_kong). This was led by the rather talented [Field.io](http://www.field.io) who decided to pass around some of the work to local creative, programming types such as [MSAVisuals](http://www.msavisuals.com). At the time, I'd left my job at [CASA, UCL](http://www.casa.ucl.ac.uk) to come and work for Memo because I loved his work and it was high time I got my ass in gear and tried to do the work I love to do: computer graphics art. It was a no brainer at the time but it still scared me a lot to make the jump.


Memo had already begun work on 'A Passion for the Planet' and asked me if I could work on the effects. Using MSAPhysics we came up with a particle system which I played with in order to add some dynamics to the scenes. So we had snow for the mountains, rain in the forest and, my personal favourite, sunspots for the Tea fields (giving the idea of the sun breaking through the cloud).

<div class="clearfix"></div>
<hr />
<object width="400" height="300"> <param name="flashvars" value="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626756999726%2Fshow%2F&page_show_back_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626756999726%2F&set_id=72157626756999726&jump_to="></param> <param name="movie" value="https://www.flickr.com/apps/slideshow/show.swf?v=71649"></param> <param name="allowFullScreen" value="true"></param><embed type="application/x-shockwave-flash" src="https://www.flickr.com/apps/slideshow/show.swf?v=71649" allowFullScreen="true" flashvars="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626756999726%2Fshow%2F&page_show_back_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626756999726%2F&set_id=72157626756999726&jump_to=" width="400" height="300"></embed></object>
<div class="clearfix"></div>
<hr />


A particle system requires a lot of thought when it comes to timing and precision. This went double because the system was to be synchronised across several machines in order to run on the large screen. A master clock was provided as part of the Field.kit base class we were asked to use. In addition, we were running with smaller images to begin with but we would need to scale everything up when the viewport was scaled. How big should a snowflake be on a small screen and a large screen? The same size? Smaller? Larger? Essentially, all the caluculations were made with respect to the variables coming through from the base class that Field had provided. 

The majority of the work for me came in with the "Performance and Teamwork" piece which involved the reading of Motion capture data from an FBX file. I'd never worked with FBX Files before (though I often do now) and was suprised at how powerful they were. I was given a brief from the design team who had provided both still images and short film clips (rendered in 3D with something akin to maya or max) and told to get cracking!

An early mockup was quite fast in arriving (at least for me) but much of the time was spent on refinements and other such issues. Initially, the scene was rendered in 2D with dots but it was decided to use spheres eventually. Keeping the speed high was an issue at the outset. We played around with depth testing and decided that the painters algorithm was more suitable in this instance. Remembering to keep everything synchronised with the master clock was also something to constantly keep in mind. 

<div class="clearfix"></div>
<hr />
<object width="400" height="300"> <param name="flashvars" value="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626757080626%2Fshow%2F&page_show_back_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626757080626%2F&set_id=72157626757080626&jump_to="></param> <param name="movie" value="http://www.flickr.com/apps/slideshow/show.swf?v=71649"></param> <param name="allowFullScreen" value="true"></param><embed type="application/x-shockwave-flash" src="http://www.flickr.com/apps/slideshow/show.swf?v=71649" allowFullScreen="true" flashvars="offsite=true&lang=en-us&page_show_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626757080626%2Fshow%2F&page_show_back_url=%2Fphotos%2Ffliegerhorst%2Fsets%2F72157626757080626%2F&set_id=72157626757080626&jump_to=" width="400" height="300"></embed></object>
<div class="clearfix"></div>
<hr />

Memo is a true artist and came up with many suggestions and help along the way. Little things here and there were picked up and I quickly learnt that 90% of the time is spent on 10% of the code which makes up for 99% of the overall experience. The reflections changed to sprites (hence the painters algorithm) with a custom texture and the whole particle system was revamped in order to allow for more interesting movement. 

The particle system itself is quite interesting. The FBX models create a set of 'magnets' or spring end-points if you will and these can be turned on or off depending on the circumstances. This simple physics system was enhanced by some perlin noise and a little magic tuning to create something that looked a little more alive.

The figures in the scene are quite dynamic; some move far and others not at all. We had to add constraints to keep the figures within the camera's viewing area. How was the camera's viewing area defined? With a particle system! Yes, the camera is attached to a set of springs which give it a more fluid motion around the figures. 


Add a little fog for depth perception and some subtle shader tweaks here and there and the result was quite pleasing. 


Of course, nothing ever goes completely to plan. Its the right level of improv that makes a performance they say. Performance and Teamwork caused a few issues when it was run across the linked machines. For a while, we couldn't figure it out. Eventually, thanks to help from Dean MacNamee, we figured out that logging to a console was causing issues as the stream was not correctly defined. Quite often, Memo and I will log things to stderr and stdout and that seemed to be causing memory issues with Fields setup. Not only that, we changed OS twice, swapping between Windows and OSX. Thankfully, [Cinder](http://www.libcinder.org) is great at making this almost a non-issue.


On a personal level, it was humbling. I'm so glad to see this live and it felt like proof that I can do these things I've dreamed about doing. Many thoughts I had were dispelled though; it was a lot of hard work and the bar was much higher than on some projects I've worked on. I wouldn't have managed this on my own at the time if I'd not been teamed up with Memo. Workig with someone who knows how to program really well is great for learning but you really need to let your ego go and not get upset when the person you are freelancing for points out a few schoolboy errors you make. This is common in programming teams but it feels worse when you are freelancing because you are out there, on your own, trying to impress and do good work. On this project, there were down times for me but I suspect that is the case for anything worth doing. The final result, I feel, shows the amount of effort that went into this was truly epic, from all the people involved.
