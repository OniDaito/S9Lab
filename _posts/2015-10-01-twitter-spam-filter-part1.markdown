---
layout: post
title: A Twitter Spam Filter - Part 1
strapline: Social media sucks and now I can quantify it with my very own robot.
introtext: My solution for Twitter social media is far more interesting than the one for Facebook.I've started to build a Twitter spam filter and here are the early results.
tags: hacking programming python maths
---

Social media sucks!

No really, it does, and now I can quantify it! Ok sure, it has some advantages but I'm willing to bet it probably leads to more anxiety, more stress and towards a version of humanity I'm not too fond of. I've spoken about [Facebook in a previous post](https://www.section9.co.uk/posts/2015-07-30-social-media.html) but my solution for Twitter is far more interesting. I'll keep the motivational bit and my thoughts to the end of this article. Suffice to say, I've started to build a Twitter spam filter and here are the early results. Big thanks to [multinormal](https://twitter.com/multinormal) for teaching me basic stats!

Where does one begin? Firstly, we need to collect the data and store it. For that I use my own virtual machine, running Python3 with the [twitter library](https://pypi.python.org/pypi/twitter) and a set of credentials. I'm recording data from the people I follow and the tweets I post. Secondly, we need a way to record what I think of a particular tweet. I've settled on the binary choice of 'like' or 'dislike'. At 4pm everyday, I receive an email with a set of tweets that have been run through a series of filters. If I so choose, I can click like or dislike and send an email back to the robot. The robot periodically checks it's email and updates it's filters as necessary. Using an email client on something like the iPhone is quite easy and somewhat pleasant. In addition, I can see the scores each tweet is given by each filter.


<iframe width="420" height="315" src="https://www.youtube.com/embed/Go_xdJdkcCk" frameborder="0" allowfullscreen></iframe>

So what are the filters? I'm still investigating the best kinds of filters but so far, I have three major approaches: [a chi squared test](https://en.wikipedia.org/wiki/Chi-squared_test) on the username, a series of [logistic regressions](https://en.wikipedia.org/wiki/Logistic_regression) and a [Bayesian filter](https://en.wikipedia.org/wiki/Bayes%27_theorem). The results of each filter are weighted and a threshold is set for whether a tweet is accepted or not. These weights are arbitrary and need some tweaking and testing, but more on that later. I should point out I'm not a statistician and that I totally expect to be schooled on my maths. Nevertheless, I'll present the results as best as I can.

The Chi Squared Test simply looks at the number of tweets that I like by one person, and the number of tweets I hate by the same person. I use the [scipy.stats.chisquare](http://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.chisquare.html) and if the p value is equal to or less than 0.05 I'm happy to accept the result. Put another way, I want to say I'm 95% sure that I will love or hate what a particular user will post in the future. So far, this particular filter has cut down on a lot of noisy people who generally post rubbish. This filter is rebuilt every day with the fresh data from the entire set, since I started recording. 

Some people who have made the 'good' list include:

  * CourtNewsUK
  * ID_AA_Carmack
  * SpaceFlightNow

Some people who have made the naughty list (which is sadly, much longer) include:

  * verge
  * Ragworm
  * WIRED
  * thegrugq (he'd be much better if he didn't retweet all the time - context!)
  * unity3d
  * nesta_uk
  * techwillsaveus
  * YourAnonCentral

... the list, sadly, goes on. To be honest, there are no big surprises in these lists so far. The way I've weighted the tests means they have to score pretty highly on the other two filters to make the cut.

<div class="clearfix"></div>

The second filter is a set of logistic regressions. This is where things get interesting. We basically have a set of sub-filters that measure certain aspects of a tweet. We then attempt to draw our trend line to fit the like and dislike data-points, measuring the p values and gradients of said line. There are many things we can measure within a tweet. So far, I've looked at the following:

  * The number of RTs in a message
  * The number of @ symbols in a message
  * The number of # symbols in a message
  * The time the tweet was posted
  * The [Fleisch Kincaid](https://en.wikipedia.org/wiki/Flesch–Kincaid_readability_tests) score of a message
  * A naive attempt to measure whether the message is in the present progressive tense

Because I have a lot of data, the p-values for these logistic tests turn out to be quite small. I've had to write the function myself as SciPy doesn't seem to have a logistic regression function as far as I know. This isn't really a problem as the formula is quite easy. We combine all the tests into one large filter, running the tweet past it, getting a score. 

I wondered about graphing the logistic filters somehow? Is there a clear split? One I built the filters, I decided to run the liked and disliked tweets against them. A logistic runs from 0 to 1 so in theory, we'd like to see disliked tweets clumped around one end of the scale, and liked tweets somewhere else.

<div class="clearfix"></div>
![logistic regression results](https://c2.staticflickr.com/6/5753/21850655771_43ca279d84.jpg)

The overall regression doesn't actually look to great. I've adjusted the graphs to reflect the fact there are 3 times as many dislikes as likes. Combining all the regressions gives some distinction between like and dislike but it seems a little tenuous.

<div class="clearfix"></div>
![RT Logistic Regression](https://c1.staticflickr.com/1/757/21841057125_5af9373fcf.jpg)

This graph shows the number of re-tweets and its regression. The data is clumped as the number of RTs is an integer value, not a smooth transition.  Again, nothing really amazing here.

<div class="clearfix"></div>
![Kincaid Logistic Regression](https://c1.staticflickr.com/1/741/21814919346_15dcf9dd63.jpg)

The Flesch-Kincaid score, however, does seem to discriminate, at least a little. This makes a lot of sense as tweets that involve some semblance of grammar, context and style do feature more in my 'likes' column. I've clearly got a lot more work to do with this filter.

<div class="clearfix"></div>

The final filter is a Bayesian analysis. I believe this technique is often used in the email spam filters of old. There is quite a good writeup on using [Bayesian filters for twitter sentiment analysis](http://webcache.googleusercontent.com/search?q=cache:knUOC770EFIJ:www.laurentluce.com/posts/twitter-sentiment-analysis-using-python-and-nltk/+&cd=1&hl=en&ct=clnk&gl=uk). I decided to follow this approach but replace sentiment analysis with like and dislike. In a nutshell, you end up with two lists of tuples: one list of the frequency of certain words in liked tweets, and the other being the frequency of certain words in disliked tweets. By having these figures and a known training data set, we can run a tweet past a Bayes filter and classify it.

Initially, the filter didn't work quite so well. It turns out I dislike a lot more tweets than I like, therefore the Bayes filter is not starting from the assumption that a tweet has equal likelihood of being liked or disliked. Therefore, unlike the previous filters, the Bayes filter only considers the last 500 tweets in the database. This resulted in more tweets being classified as positive.

Combining these three filters, as mentioned before, is an arbitrary task. The Chi Squared returns either a -1, +1 or 0 depending on whether or not it either dislikes, likes or is ambivalent about a person. The logistic regression filter returns a value between 0 and 1, whereas the Bayesian filter returns *either* a 0 or 1. I've arbitrarily set the weights to be 0.25, 0.5 and 0.25 with an acceptance threshold of 0.6. This gives the logistic filters a much greater say in the outcome. But is this actually any good? Well, we can test for that too.

As well as the actual email, I receive two further emails which are much smaller. The first is a 1% sample from the tweets that were rejected. I am offered the chance to say whether or not these tweets were or were not correctly rejected. Essentially testing for true negatives and false negatives. The second email is a 1% sample of the tweets that were accepted. These form the true positives and false positives. Using the data from these responses, I can make a rough guess as to how well the spam filter is working, given the current settings.

So, finally, some actual results!

    * Start date: 5/08/2014
    * Date at time of taking stats: 30/09/2015
    * Total number of liked tweets: 817
    * Total number of disliked tweets: 2455
    * Number of people on the liked list: 16
    * Number of people of the disliked list: 141
    * Number of tweets posted by me: 901
    * Average number of tweets analysed each day: 2949
    * Average number of tweets accepted each day: 583
    * Number of true positives: 22
    * Number of false positives: 15
    * Number of true negatives: 90
    * Number of false negatives: 10

There isn't quite enough data yet to say how well the filter is doing, we can see that I generally like only one quarter of all tweets in my time-line (so 75%). The robot is currently rejecting about 80% so it's performing close to my preferences. It correctly identifies true negatives 90% of the time. However only about 60% of what is sent to me I actually like. Its about 3 times easier to reject a tweet than to accept it so the robot is still slightly away from performing optimally. It still takes me about 40 minutes to skim through each email if I want to read every digest, so still a little too long. However, I can alter the weightings of the various filters to get a better result. 

Time has not really been taken into account with this analysis. With the exception of the Bayes filter, all the filters use all the data in their calculations. It is conceivable that my tastes could change over time. There are no real feedback loops in this system yet. I'm sure I could automate un-following people which would have a certain effect on the outcome. It might be the best approach is to go a little more real-time; altering sliders and values and only using the latest data.

One thing that I'd really like to understand is serendipity. Ultimately, it would be nice to have people and tweets suggested to me. I had some trouble reading from the twitter main public feed with the python API I was using. I'm sure theres a way to fix that. The next step will be to automate following and unfollowing - the first of many feedback loops.

There is clearly a lot more work to be done. I'm not convinced the logistic regressions are the best yet. There are many other [computational linguistics](https://en.wikipedia.org/wiki/Computational_linguistics) methods available to analyse this data much better. I've been looking into a few here and there. The Bayesian filter could be improved quite a bit. Indeed, writing all this in Python, while fun, is certainly not the most efficient way (the code is quite nasty, as experiment code tends to be). The email could be prettier - but email works quite well as a way of collecting data I've found, particularly if you own the email server. That said, my sent folder certainly has a lot of rubbish in it now.  Other thoughts I've had include using some kind of confidence value from the Bayes filter, and improving the words used in the frequency analysis, using some kind of neural network approach, some kind of topic mapping and a whole host of other filters.

All of this has come about for one reason really. I'm trying to channel my anger at social media into something more positive. The most interesting thing about Twitter isn't the reams and reams of words written by humans - it's the robots and the experiments taking place on the network that reveal things about ourselves. I've learned a little bit more about statistics which is no bad thing at all really. I've wanted an excuse to mess around with stats and thanks to the wonderful help from [multinormal](https://twitter.com/multinormal), I've gotten past the first hurdle.


