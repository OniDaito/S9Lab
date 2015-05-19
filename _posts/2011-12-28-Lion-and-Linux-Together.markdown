---
layout: post
title: Linux and Lion together at last (almost)
tags: thoughts osx
introtext: I must have spent an age getting this to work! Several forums and blog posts later I *think* I've managed to sort this. My laptop had been suffering from slow-downs with Lion installed and the wifi had begun to break. I figured it was high-time to re-install the lot. 
strapline: Dual booting on a mac isn't the easiest of things.
---

I must have spent an age getting this to work! Several forums and blog posts later I *think* I've managed to sort this. My laptop had been suffering from slow-downs with Lion installed and the wifi had begun to break. I figured it was high-time to re-install the lot. 

Backing everything up using an external drive, I set to with a snow-leopard DVD. No dice here folks. It turns out that OSX will only boot from a CD that either came with your machine or that has a higher version of the OS on the CD than on your hard-disk. 

I attempted to be clever and figured I could setup Linux after Snow Leopard and created 1 partition with some freespace afterwards. Of course, installing *ubuntu natty* is a tricky beast, especially on a newer MacBook Pro. The Ubuntu forums are full of information on setting up the various versions of the Macbook. The later versions are not actually support officially. You can burn a DVD or a USB stick but to actually get Ubuntu installed you need both.

Thats right! Burn Natty to a CD and to a USB stick. Plug both in and then either use [ReFIT](http://refit.sourceforge.net/) or hold down 'c' on the keyboard and boot from the CD. You'll get into the installer and away you go.

The reason for Ubuntu is the PCL Cloud Libraries work better under Linux at the moment, with the Kinect Fusion stuff being only just around the corner. It's worth pointing out that an nVidia card is needed in your MacBook Pro for the best stuff to work, I.E anything using CUDA. Not all MacBooks use nvidia hardware and I still don't know if mine can run CUDA under Linux.

Anyway, trying to install Lion over the top of Snow Leopard didn't work at all. Sadly, it seems Lion wants around 128meg extra after the Snow Leopard Partition. Fine, I figured. Lets just use *Disk Utility* to sort that out. No dice. "Mediakit reports no such partition" was the message here. Apparently, my partitioning of the disk using the Ubuntu installer had not gone well. 

Lion uses the GUID system for it's paritions and I figured that was worth checking. [iPartition](http://www.ipartition.com) allows you to do this with their boot CD but even this failed to fix the problem. In the end I just backed up again, downloaded a copty of Lion and burnt that to a DVD. I now have a bootable version of OSX Lion from which one can partition, install and get a system up and running. 

Having said all that, it would appear that ReFIT is nowhere to be seen now, despite having installed it. Im now greated with a password prompt straight off the bat, so no idea if Linux will even install at all. 

Not the best thing to be doing over Christmas I must admit! 
