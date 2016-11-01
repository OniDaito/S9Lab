---
layout: post
title: Twitter meets SVM and Deep Learning
introtext: It's no secret that I'm not a fan of social media generally. It has potential to be amazing but appears to be going down a route that I'm not very comfortable with. One way that I deal with this is to write robots for Twitter in order to get around the problems of noise, irrelevance and hate speech. I've been trying to find a few ways around this and I've entered into the world of SVMs and Neural Nets. 
strapline: Support Vector Machines and Deep Learning are pretty hot right now, especially when it comes to text processing. I thought I'd have a play.  
tags: programming machinelearning socialmedia maths
---

It's no secret that I'm not a fan of social media generally. It has potential to be amazing but appears to be going down a route that I'm not very comfortable with. One way that I deal with this is to write robots for Twitter in order to get around the problems of noise, irrelevance and hate speech. I've [previously written a robot](https://www.section9.co.uk/posts/2015-10-01-twitter-spam-filter-part1.html) that filters out tweets that I don't really like. This cuts out a lot of things that stress me out or are just no fun to read. The problem here is this creates an echo chamber which is another major problem of social media. I've been trying to find a few ways around this and I've entered into the world of SVMs and Neural Nets.

[Support Vector Machines](https://en.wikipedia.org/wiki/Support_vector_machine) are an odd thing I don't quite understand just yet. They seem to be a mix of methods, combined to create a system that draws a line between two classes. Think of data being labelled as either class A or class B. New data, when it arrives, will be automatically assigned one of these two categories based upon the data that has been entered previously. It's like drawing a line that divides data-points on a graph. It's possible to do this non-linearly as well, using higher dimensions than just two. I've not managed to do this yet, but it's probably next on the list.

[Deep learning for text](https://www.quora.com/What-are-some-good-books-papers-for-learning-deep-learning ) is quite a hot topic at the moment it would seem. I used [an example I was sent](https://github.com/StevenLOL/aicyber_semeval_2016_ivector/blob/master/System_1/system_1_baseline.py#L32) from StackOverflow. I've been using [Tensorflow](https://www.tensorflow.org/) for most of the time. I'm not sold on it yet, but the fact that you can mess around with it in Python is a pretty good bonus. Support for GPUs is also a plus point.

Both of these methods have one thing in common: Word Vectors. How do you represent a sentence (or tweet) as a set of numbers which both of these methods require? Typically, you end up with a vector that is mostly a bunch of zeroes; what is called a sparse vector. Put another way, if you have a dictionary of 50,000 words, you can break up a sentence into a set of words. Each word represents a dimension; a dimension that goes from 0 to 50,000. It pretty much ignores any rules of grammar or semantics, preferring to learn from simply the position of the various tokens. This sort of thing has already been done quite well by the Google program [word2vec](https://code.google.com/archive/p/word2vec/) which also has a [wikipedia page](https://en.wikipedia.org/wiki/Word2vec). In that example, the vectors are created themselves by a single layer neural net. This is a little "cart-before-the-horse" but the actual results are pretty cool.

There are some good links for Support Vector Machines when it comes to Python. [SciKitLearn](http://scikit-learn.org) is particularly good:

* [http://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html#sklearn.svm.SVC](http://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html#sklearn.svm.SVC)
* [http://scikit-learn.org/stable/auto_examples/svm/plot_iris.html](http://scikit-learn.org/stable/auto_examples/svm/plot_iris.html)
* [http://www.nltk.org/api/nltk.classify.html#module-nltk.classify.svm](http://www.nltk.org/api/nltk.classify.html#module-nltk.classify.svm)

The [NLTK](http://www.nltk.org/) tool-kit is closely aligned with scikit-learn, especially when it comes to SVMs. I found that getting the data into the formats scikit-learn needs was a little tricky

    pos_cutoff = int(len(liked_ngrams)*0.75)
    neg_cutoff = int(len(disliked_ngrams)*0.75)
     
    training_set = [ (feat, 'pos') for feat in liked_ngrams[:pos_cutoff] ]
    training_set += [ (feat, 'neg') for feat in disliked_ngrams[:neg_cutoff]]
      
    # Finally, train the classifier and return
    classif = SklearnClassifier(LinearSVC())
    classif.train(training_set)

Preparing the raw text of the tweet looks a little like this:

    tweet = row.text
    tokens = nltk.word_tokenize(tweet)
    tokens = [token.lower() for token in tokens if len(token) > 1]
    bi_tokens = nltk.bigrams(tokens)
    tri_tokens = nltk.trigrams(tokens)
    a =[(word, True) for word in tokens]
    return dict(a)

One thing you can see is that I'm creating what are known as [bigrams and trigrams](https://en.wikipedia.org/wiki/N-gram). The theory goes that rather than just using words on their own, you can create a dictionary of ngrams too. This takes into account words that occur together, either in pairs or triples. I actually found this made the accuracy of the system worse, but it might very well be that the system is becoming over-trained, as the training set is only around 3000 items long.

Tensorflow I've found to be much more complicated and I suspect a lot of that is due to the API and the kind of abstraction they've gone for. Nevertheless, there are some good resources out there. The one I've used is [this one](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/) which give a good description of the challenges.

So far, I've found that SVM works quite well, cutting down 2200 tweets to about 300 tweets a day with a pretty good accuracy (though I do need to double check that). I think there's a lot more to understand. I found the neural net to be slow and less accurate but I have a feeling the word2vec project will come in very handy. I'll have more to say on that in the coming weeks.
