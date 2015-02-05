---
layout: post
title: Personal Cloud
strapline: Your own, personal, cloud. Somewhere to keep your files. It gives you smiles!
introtext: I wanted to write a small bit about the cloud. I've never really trusted it, and with all the leaks we've been seeing I think it best to keep certain things off the net altogether. Also, I take great joy in setting up my own solutions.

---

The first blog post of the new year. It's been a hectic time here at section9. We've moved office for one thing and are still in the process of sorting everything out. Exciting times are ahead though.

I wanted to write a small bit about the cloud. I've never really trusted it, and with all the leaks we've been seeing I think it best to keep certain things off the net altogether. Also, I take great joy in setting up my own solutions.

Starting at the bottom end, I rely on two, 3TB drives. Both of these are formatted with [btrfs](https://en.wikipedia.org/wiki/Btrfs) which I quite like the sound of. At present, one is slaved inside my large desktop machine. The other operates as the live disk, attached to a rather nifty [cubietruck](http://cubieboard.org/tag/cubietruck/). This small ARM based board is capable of running Linux and operating a SATA disk. Because of its lower power draw and the fact I can run software on it easily, I use it as my primary server machine. Both of these drives are encryped and use [luks](https://code.google.com/p/cryptsetup/) to access them. So far good. Getting btrfs support for Cubietruck was a little tricky but possible.

Linking laptops and all the other machines I have across the internet really needs a VPN and that means [openvpn](https://openvpn.net/index.php/open-source.html) realistically. It runs on iPhone, Android, Mac and all the rest pretty easily. Setting up exit points for the outside world and internal static ips allows me to get to my files, securely wherever I am. It's not the fastest but it doesnt need to be really. I have a VPS sitting here in the UK that deals with all that traffic and setup.

Organising the various different files is another matter. Code is largely taken care of with git and rsync. I've decided that one machine and iTunes takes care of music. The library is synced with the master server where other machines can get to the music collection if they so please. I have to say though, my favourite solution is the one I have for ebooks and pdfs.

[Zotero](https://www.zotero.org) is a fantastic product. People think it's just for citation but it really isnt. Since the cubietruck is a fully fledged machine, I can run [nginx](http://nginx.org) with some added webdav support and have all my PDFs synced via Zotero wherever I am. Since they are organised, it's easy to find what book I want. Installing [zandy](https://play.google.com/store/apps/details?id=com.gimranov.zandy.app) on my Android tablet and you are all set to have a personal library at your fingertips!

Backup is usually done with rsync scripts of various kinds. This seems to work for now, though a little more automation on that score might improve things I suspect. I use a USB harddisk to backup my main laptop, with Apple's time machine as an extra measure, since I carry the lappy with me everywhere.

The setup still isn't perfect. The ideal would include an offsite backup somewhere else, which is next move. Speeding up OpenVPN might also help things though it's not been too bad since the switch to UDP. I hear certain countries are begining to block vpn traffic, but there are some tactics to get around this that I shall be investigating. I'd like to use gitlab at some point too, but there isn't support for ARM just yet and it's a rather heavy program to run.

What is your setup? Which backup programs do you prefer? Always enjoy hearing the solutions people have come up with!


