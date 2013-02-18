---
layout: post
title: Coin Detection at the British Museum
category: work
strapline: Using OpenCV to extract, clean and stitch coins
strapimage: britishcoin.jpg
---

##
The Coins and Medals Department at the British Museum have a problem. They need to keep records of their collection. This involves scanning each and every coin, cropping the images, rotating them, stitching the two sides together and processing the filename. You can quickly imagine how labour intensive and tedious this job can be.

###
![Greek Coin](http://farm9.staticflickr.com/8334/8357960664_2ec6f31cec.jpg)

##
The challenge was to speed-up this process so it became at least bareable. Rather than use cameras, the BM tends to use a varying array of scanners. Some of these are high grade and the others not. The results vary. Sometimes scanners pickup dust and scratches. Othertimes, the edge of the coin is out of focus. Some coins, such as the silver Greek coin tend to reflect a little too much.


#
One solution is to scan a coin with the lid of scanner left up. On some scanners, this produces a sharp edge, with the remaining area black. This makes computer vision easy but the depth of the coin is lost. Losing data like this is not acceptable, so another solution needed to be found

##
![Scanner with Cloche](http://farm9.staticflickr.com/8217/8269948452_689fe76d87.jpg)

##
Katie and I tried a variety of different cloches with lights. Depending on the material and lights, different effects were achieved. In order to extract a coin from a background, one needs to have as distinct an edge as possible. The best result, we found, was a cloche made from frosted perspex. This cloche had two sides, allowing light to escape around the edges but with a lamp held above, provided a diffuse light source that minimised shadows and provided reasonable edges.

##
![Missed Coin](http://farm9.staticflickr.com/8490/8267197054_2f13ff0bb9.jpg)

###
The software proveded to be rather tricky. Firstly, how do you package a program for Windows XP that can be run straight from the desktop with no drivers? The answer? Package a python program using [pyinstaller](http://www.pyinstaller.org/). This packages up PyOpenCV rather nicely. I decided to go with pyGTK for the user-interface - simple and effective. 

The technique I settled on basically involved extracting edges and performing a series of morphological operations on a reduced size of image. From there, one can extract the largest contour and find the coin. The technique works fairly well though does require good lighting conditions. The longest operation is, in-fact, the final alpha blending of the extracted coin with its background. The edges are ever so slightly alpha blended to give a smoother, anti-aliased edge which works quite well, without losing data.

##
![More Coins](http://farm9.staticflickr.com/8046/8356888267_4d242e54e1.jpg)