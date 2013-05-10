---
layout: post
title: Hackspace Burger Part 1
---

Lets get something clear - I'm a big food lover! No, not big as in belly but a lover of really good food - quality food. That doesn't mean expensive or rare but embodying a more [Zen and the Art of Motorcycle maintenance](http://en.wikipedia.org/wiki/Zen_and_the_Art_of_Motorcycle_Maintenance:_An_Inquiry_into_Values) notion of quality. A few months back, I was introduced to a *hipster popup burger joint* whose name shall remain nameless. A lot of my friends seemed to like it. They had burgers with fois grais, and even a whole, softshelled crab. I thought this sounded interesting but when the food arrived, it was greasy, difficult to eat and had absolutely no nuance. I'd say style over substance but it turned out to just be hipsters trying to hard. *This would not stand!*

![Sous Vide Bot v2.0](http://farm8.staticflickr.com/7052/8690464484_692a6bf653.jpg)

So I've embarked on the quest for the perfect burger and there appears to be a lot of literature on the subject. One of my favorite books, [Modernist Cuisine](http://www.amazon.co.uk/Modernist-Cuisine-The-Science-Cooking/dp/0982761007/ref=sr_1_1?ie=UTF8&qid=1367177965&sr=8-1&keywords=modernist+cuisine) has many bonkers ideas in it that, although seem crazy and convoluted, have real science behind them. The author, Nathan Myhrvold, has a recipe for [quite an epic burger](http://aht.seriouseats.com/archives/2011/02/nathan-myhrvolds-modernist-burger.html). Not only that, but the webpage over at [Serious Eats:Burger Lab](http://aht.seriouseats.com/tags/the%20burger%20lab?ref=sectionnav) has some amazing hints and tips for the perfect burger. Armed with this information, I have begun a journey to find the essence of a good burger. I believe it takes a good bit of nerding, some romantic love of cooking, time and quality ingredients to create the ultimate, hackspace burger!


The most important factor is the patty, or the burger itself. I've chosen to use the [sous vide method](http://en.wikipedia.org/wiki/Sous-vide) to cook the burger first, followed by placing the cooked patty into a bath of liquid nitrogen, then into a deep  fat fryer. At the time of writing, [London Hackspace](http://london.hackspace.org.uk) is in the process of getting hold of some LN2 for the opening day, thus provding a good time frame. During the last few weeks, I have been perfecting my sous vide technique. [Serious Eats has a great writeup](http://aht.seriouseats.com/archives/2010/06/the-burger-lab-how-to-cook-a-burger-sous-vide-without-a-sous-vide-machine.html?ref=search) on sous-viding a burger!



![Waitrose Burgers](http://farm9.staticflickr.com/8120/8679597853_b62b5c0156.jpg) 

Sous Vide Bot v2.0 is much like the original [Cookbot](http://blog.section9.co.uk/posts/2011-01-23-cookbot.html) I spoke of previously, only this time I have integrated a 10K Pot and a [TTL Serial LCD from Sparkfun](https://www.sparkfun.com/products/9395) into the case. Rather than using an actual arduino, I've settled on the [Atmega on a breadboard](http://nathan.chantrell.net/20110819/build-your-own-arduino-for-under-10/) with the arduino bootloader. Basically, this is easier than writing my own three-wire protocol, serial protocol and all the other gubbins I would need if I was writing this all in C with llvm-gcc. One day I'll learn proper AVR programming but for now, I needed this to work. 



I picked the cheapest burgers I could find that I still deemed edible. Sorry, none of your frozen Iceland, 99p crap here! Meat is expensive and should be so. I have no truck with people who disrespect meat. However, you don't want the most expensive cuts in a burger either as the flavour would not be quite right. The intention is to find an amazing, East End butcher for the final solution but these would do for now. 



![Sous Vide Bot v2.0](http://farm8.staticflickr.com/7045/8690467088_095f9794e8.jpg)


The first test involved cooking the burger at 62C for about 2 hours. In order to get the burger into the bag, I initially tried the [Water Approach](http://aht.seriouseats.com/archives/2010/06/the-burger-lab-how-to-cook-a-burger-sous-vide-without-a-sous-vide-machine.html?ref=search) but found I couldn't get it to work very well. Zip-lock bags, it turns out, are not great at holding air in. The kind of bag that clips together without the sliding zip is much beter in my experience. However, I managed ok with a straw; sucking the air out and sealing the bag which a large clip. It's useful to note that you don't need to remove all the air and compress the burger to any high extent as this can have detrimental effects.

As a comparison, I grilled another burger until it appeared to match the sous vide burger. In order to brown them both, I applied a blow torch to the outside. Not having any LN2 at home *(I know, I know! For shame!)* I had to settle for this method. The burgers turned out a little different.


![Results](http://farm9.staticflickr.com/8387/8679597305_22cdfd073d.jpg)  

Already, the grilled burger looks the part but is much smaller and squatter. The real test however, is how they look on the inside and how they taste.


![Grilled Burger](http://farm9.staticflickr.com/8117/8680707236_61e02ca58b.jpg)


![Sous Vide Burger](http://farm9.staticflickr.com/8534/8680706492_4bce71c724.jpg)


The grilled burger doesn't look too bad as burgers go, but the sous vide burger is still red in the middle. Tasting both, the grilled burger is fine but the juice leaves quickly, giving a slight toughness and hints of the fact that it would taste quite burnt if you cooked it any further. The sous vide burger, on the other hand, tastes smooth with very little toughness at all. It doesn't taste raw either, despite looking much more red in the photo. Definitely, an improvement in cooking technique!


As a second step, I tried cooking the burger at 54C for about one and a half hours. This came out even better with almost no toughness at all. Both burgers would not brown sufficiently whilst being blow torched; I ran the risk of undoing all the slow cooking if I had carried on. The next step in the process is to assess the liquid nitrogen technique.

As for the cheese, relish and bun well, you are all in for a treat! It only begins here! The ultimate hackspace burger is taking form!