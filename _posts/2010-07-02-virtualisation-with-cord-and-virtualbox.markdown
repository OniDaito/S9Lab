--- 
layout: post
title: Virtualisation with CoRD and Virtualbox
---

I though I'd put a little note up here regarding my thoughts on virtualisation for testing things like websites and other programs. Previously, I've used virtualbox on my linux box to run photoshop and similar and it has worked quite well considering. At work however, I thought a more distributed system with some dedicated hardware would do the trick.


We have a small, Core2 Duo 64Bit machine lying around. I installed Linux Ubuntu 10.04 with the non-free version of Virtual Box. It is important that you <span style="font-weight:bold;">DONT USE THE OSE BUNDLED VERSION as this doesn't come with RDP support and USB forwarding. You'll need to download the Oracle version from the VirtualBox page. Once this is installed, you can ssh into your box, scp over any ISOs and get installing your virtual machines.

Virtualbox comes with the command <span style="font-weight:bold;">VBoxHeadless which allows you to start your machines from a command line with no graphics. You can then RDP into these with the correct program. <a href="http://cord.sourceforge.net/">I use CoRD</a> because I've never been a fan of Chicken of the VNC or similar. Give CoRD your remote machine and the port (I've setup 5000-5003 for my machines) and away you go.


Performance wise, two XP instances run quite well. Vista causes a lot of issues though as it is much more of a memory hog. Haven't tried Windows 7 yet. I'm debating setting up a similar system with Windows 7 as the host OS running Linux and XP as the virtual machines. This may or may not be faster. The machine at home is an older Pentium4 but it does have Hyperthreading (I think) so maybe we'll get some more performance.


There are <a href="http://www.virtualbox.org/wiki/Documentation">some great guides on the Virtualbox page</a> and so far, performance hasn't been that bad. Testing the various flavors of IE is quite easy when you have 2 XP machines running side by side. Sure, it's not amazingly fast but it's made my life easier and gotten some use out of an older machine.
