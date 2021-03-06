--- 
layout: post
title: Apache, GIT and Mediawiki to manage design and projects
introtext: I thought I'd put down my thoughts and experiences on keeping track of your personal projects and data. I've been through a lot of various methods. Everything is intertwined; backup, code repos, security, accessibility etc etc. My method certainly wont suit everyone but it may give you some thoughts. In a nutshell, I use Apache, GIT and Mediawiki on a small MiniITX machine with USB disk cloning to run all my systems.
tags: server programming
strapline: Project management is now fun!
---

I thought I'd put down my thoughts and experiences on keeping track of your personal projects and data. I've been through a lot of various methods. Everything is intertwined; backup, code repos, security, accessibility etc etc. My method certainly wont suit everyone but it may give you some thoughts. In a nutshell, I use Apache, GIT and Mediawiki on a small MiniITX machine with USB disk cloning to run all my systems.


I've used subversion and mercurial before. Subversion was great because it support binary files; very useful when you have a large PSD to backup. However, when one of my hard-disks broke, I lost the most recent updates and couldn't get back the newer versions I had on my workstation. This was annoying. That, and subversions silly revision system meant a change was needed. Subversion doesn't really say what a repos or a directory really is. So if I updated one project, then another project the revision number for everything would go up twice! Not good.

Mercurial was dead simple though. I converted a few of the SVN based projects over but found that quite tricky. Mercurial is what I use on a daily basis at work. Because it is written in Python it is quite straight forward and works well. However, it does suffer from serious flaws when branching (apparently) but also it is limited to filesizes under 10meg. I say limited - it complains about it but tries anyway. Creating a new repository remotely was also a pain. What if I'm working remotely and need to backup to my system at home? I wrote a quick python script to do this but it wasn't particularly good.

Because of peer-pressure and the other problems, I decided to look at GIT. Github is a great site with a lot of excellent people on it. Git's commands are more esoteric but understandable after a while and support for binaries is good. Using <a href="http://hg-git.github.com/">Hg-Git</a> makes converting from Mercurial quite easy. Following <a href-"https://help.ubuntu.com/community/Git">the Ubuntu GIT Guide</a> was quite easy although I use <a href="https://git.wiki.kernel.org/index.php/Gitweb">GitWeb</a> and not GitView which is rather awful. This means I can access my repositories anywhere and indeed, create repositories remotely. Annoyingly, because I'm using gitosis, I need to keep a copy of the Gitosis repos on every machine that needs access to my home GIT Server and a custom script to make it work but it's a small price to pay for better security and efficiency. So far, I approve.


Mediawiki was a suggestion by a friend for keeping notes and thoughts and so far, it has worked a treat. Sure you can pay Omni some money and get a mac osx organiser but what about Linux or Windows? What about mobile clients? With the plethora of plugins available (GeSHI and PDF Creation being two of my favorites) having your own wiki is a great idea.

So now you can backup code, keep notes, and access anywhere. All this needs to run on something. I use a fan-less, MiniITX board with one large SATA drive to store all this, running Ubuntu. Why you ask? Well I wanted something low power and capable with an emphasis on quiet. Using one SATA drive means that disk cloning is very easy. Plug in a USB enclosure, run dd_rescue and you get an identical copy of your drive. It's already saved me once and I heartily recommend it.

If you set up all the right port forwards and certificates you can access your box over a home connection with reasonable speed. The whole thing works quite well and has some degrees of protection. Full disk encryption, arpwatch and Snort provide a good defence against intrusion and holding your wiki off-site on your webhost means you'll always have access, even if your home machine goes down (which it will once or twice)


Overall, this has met my needs for security, remote access to everything and my various requirements for source control and backup. I heartily recommend something similar. It's all free software and it all works.
