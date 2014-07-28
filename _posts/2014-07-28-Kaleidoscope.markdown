---
layout: post
title: Kaleidoscope for Lexus
category: work
strapline: A CoffeeGL based Kaleidoscope
strapimage: kaleidoscope.jpg
introtext: It's not often I do advertising work. It all depends on who I'm working with and what the challenge is. In this case, I was approached by Hellicar & Lewis to build a WebGL based Kaleidoscope in about 4 days. No small order really, but I decided to step up and give it a bash.

---

It's not often I do advertising work. It all depends on who I'm working with and what the challenge is. In this case, I was approached by [Hellicar & Lewis](http://hellicarandlewis.com) to build a WebGL based Kaleidoscope in about 4 days. No small order really, but I decided to step up and give it a bash. The final result is called [NX Constructed](http://nxperspectives.eu/en/nx_constructed.html) and it's quite pretty.

![Kaleidoscope](https://farm3.staticflickr.com/2914/14763699654_8eb1908457.jpg)

Lexus approached Vice who approached Hellicar & Lewis who approached me! It's funny how these chains seem to happen in the freelance world. They wanted someone who was pretty handy with WebGL and available on a tight time-frame. Fortunately, my current contract is quite flexible. The final product was definitely possible in the time, but it was tight. That kind of pressure is actually quite good for me, as I am ten times more productive.

One thing that helped immensely was I could use whatever I wanted to get the job done. I chose to use [CoffeeGL](http://www.coffeegl.com) of course, because I know it back to front. This proved very handy because I needed some different geometry types for this piece, along with some fairly accurate picking and per-vertex attributes. Using any other library would have been very time consuming and pointless.

![Kaleidoscope](https://farm4.staticflickr.com/3910/14579415979_93a7fb87ae.jpg)

The project is really split into two halves. The first part involves the creation of the video. There is quite a good video of that process on [Youtube](https://www.youtube.com/watch?v=IpyAsbep3NM), that I've included here too. Taking video and projecting it, then re-recording it, seems like quite an interesting idea and it makes for a slightly rougher, yet interesting image. 

<iframe width="560" height="315" src="//www.youtube.com/embed/IpyAsbep3NM" frameborder="0" allowfullscreen></iframe>

The second half was basically to do with me messing around with the Kaleidoscope. The basic premise is you need to mirror the texture co-ordinates over a triangle mesh. Each shared edge must have the same U,V co-ordinates. From that, you get your kaleidoscope. The interaction is worked out by projecting a ray from the camera view and seeing where it hits. You can get the code for this in the [Realtime-rendering book](http://www.amazon.co.uk/Real-Time-Rendering-Third-Edition-Akenine-Moller/dp/1568814240%3FSubscriptionId%3DAKIAILSHYYTFIVPWUY6Q%26tag%3Dduc08-21%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D1568814240), which has a different take on the maths than I had.

![Kaleidoscope](https://farm4.staticflickr.com/3836/14579594587_c8a8abe0ed.jpg)

Wireframing is actually quite a hard thing to do in WebGL as the basic primitives for line drawing are not really there for you (line thickness anyone?). Thankfully, there is an excellent writeup by [Florian Boesch](http://codeflow.org/entries/2012/aug/02/easy-wireframe-display-with-barycentric-coordinates/) where he talks about Barycentric co-ordinates, which are really handy. Using that information, I can create outlines and slightly cracked looking edges to give a more organic effect. Actually, that effect was a total experiment that I decided I liked.

The movement is your basic spring function, calculated on the CPU (since the amount of geometry is low). I thought about using a web-worker and I may do that in version two. Balancing a physical system is always tricky but I think the final outcome is quite good fun to play with. We decided to mess around with some parts of the kaleidoscope; you'll notice that things don't always line up perfectly. It makes the whole thing just a little more interesting.

![Kaleidoscope](https://farm4.staticflickr.com/3916/14763699944_5a0c7607a6.jpg)

Hellicar & Lewis are fun to work with. I'd met Joel some time before, though this is the first time we'd worked together. Not only that, but another colleague, [Cai Matthews](http://caimatthews.com/) was involved too. A pretty good team I thought. Overall, I'm really happy with how it worked out, especially given how long it took. Everyone worked really hard and I'm really glad that my own libraries are starting to, literally, pay off. Looking forward to making version two!

