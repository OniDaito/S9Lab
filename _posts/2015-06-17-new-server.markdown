---
layout: post
title: Running your own server, on a real box!
strapline: Decided to move away from a virtual server, towards a real one!
introtext: I used to rent a Virtual Machine from the lovely people at Bitfolk, mostly because I have a lot of domain names, websites and the like and rather fancied running a few interesting things that required a bit more intelligence and experimentation. After running my own email server, things started to pick up pace - I need more disk space and more memory. Eventually though, the VM just didn't seem to be enough, so I spoke with my friend Will from Sundive networks who sold me a Dell R210 ready for racking.
tags: thoughts server devops
---

![Server being installed](https://farm4.staticflickr.com/3806/18246706734_d876eb34b9.jpg)

I used to rent a Virtual Machine from the [lovely people at Bitfolk](http://bitfolk.com), mostly because I have a lot of domain names, websites and the like and rather fancied running a few interesting things that required a bit more intelligence and experimentation. After running my own email server, things started to pick up pace: I need more disk space and more memory. Eventually though, the VM just didn't seem to be enough, so I spoke with my friend Will from [Sundive networks](http://sundivenetworks.com) who sold me a [Dell R210](http://www.dell.com/us/business/p/poweredge-r210/pd) ready for racking.

I don't know too much about the I.T side of networking, though I taught the principles of it at University - things like the [Nyquist Limit](https://en.wikipedia.org/wiki/Nyquist_frequency) and [Shannon's Theorem](https://en.wikipedia.org/wiki/Noisy-channel_coding_theorem). Such things are little use when you are trying to get ipv6 working with your network devices that should have been bonded, or wondering about terminals over serial cables. Still, the whole thing is designed really as a learning experience and a way to get a bit more into the devops world. Not a hue fan of that phrase but it describes some of what I do.

I decided to go with [Jump](http://www.jump.net.uk), who oddly enough, seem to host both Sundive and Bitfolk. The first attempt at the install did not go so well because, as anyone knows, driving to [Telehouse](http://www.telehouse.net) anywhere near 5pm is just a really dumb idea. I thought I'd beaten the traffic. No dice! Second time around, things went better and the machine slotted in nicely to the rack. Turns out the thing draws about 40 Volt-Amps or thereabouts which is not the best, but still not too bad. I'm undecided whether or not it's more green to dispose of the existing hard-disk and use an SSD instead?

I must admit, I did rush the install a little bit. I was keen to get the machine setup and out of our flat, for various reasons. Having it kicking around the living room would not have been great, not least because the fans make quite a lot of noise. Had I taken a little more time, I might have done a few things differently, such as encrypting all of the drives and adding some internal USB devices or similar. In the end, I had about a week's worth of evenings to get it sorted, knowing very little about virtualisation.

I know a few people are keen on [FreeBSD](http://www.freebsd.org). I've not played with that before, so I figured I'd stick to what I know for now - Linux. I've gone a little off-piste and settled for [Arch Linux](http://archlinux.org). I like the Gentoo nature of it, and it's excellent wiki. I'm keen to understand a little more about [systemd](http://freedesktop.org/wiki/Software/systemd/) though I refuse to get involved in the holy wars around this topic, interesting as the debate seems to be. Sadly, Arch didn't play well with [Xen](https://wiki.archlinux.org/index.php/Xen) which seemed a shame, but other people have suggested that [KVM](https://wiki.archlinux.org/index.php/KVM), with [QEMU](https://wiki.archlinux.org/index.php/QEMU) and [Virt-Manager](https://wiki.archlinux.org/index.php/Libvirt) is the way to go. This is a [Type 2 Hypervisor](https://en.wikipedia.org/wiki/Hypervisor) which I thought would be somewhat slower but so far, I've been quite impressed. Getting that setup was not easy and I suspect I've still done it wrong, but the ability to clone and machines is really handy. I'm still not sure about the best way to do that, but at some point, I know it will come in handy.

![Server in its rack](https://farm4.staticflickr.com/3926/18842981646_73c0e883a4.jpg)

There are 8 major things I need to run on my box

  - Offsite backups
  - A Webserver
  - Several Experiments
  - E Mail Server
  - Calendar and Contacts
  - A VPN
  - IRC bouncing
  - Tor exit node

The most difficult to setup is email. Email is venerable, has evolved over several decades and has many moving parts. At present, it's still not 100% correct but is at least working. The standard approach, as described by the [Arch Linux Wiki](https://wiki.archlinux.org), introduces [Postfix](https://wiki.archlinux.org/index.php/Postfix) and [Dovecot](https://wiki.archlinux.org/index.php/Dovecot) as the main players. To that I add [Sieve](https://wiki.archlinux.org/index.php/Postfix#SpamAssassin), [Spamassassin](https://wiki.archlinux.org/index.php/Postfix#SpamAssassin) and [postfix admin](https://wiki.archlinux.org/index.php/Postfix#PostfixAdmin). I've previously used [Roundcube](https://wiki.archlinux.org/index.php/Roundcube) as well, though it was a real pain to get working on my previous virtual server. In addition, one needs to create certificates for [SSL/TLS]() security, and until [letsencrypt](https://letsencrypt.org) is released, I'll be sticking with self-signed as I need quite a few certificates to get this all rolling and they don't come cheap. I needed to add a couple of things to my postfix setup to ensure my parents could access their email but mostly, my setup follows the guide. I use [virtual domains](https://wiki.archlinux.org/index.php/Virtual_user_mail_system) with a database to store all the information. Moving that over from the previous box to this one proved quite easy. 

![Dell R210](https://farm6.staticflickr.com/5602/18842969316_7931f3b7da.jpg)

Email is also tricky because you've got to deal with the rest of world. Sure, any server does this by definition, but when you see all the spam hitting your inbox as soon as you turn it on, you get a real sense of the issues. One thing I've had to do is setup [Sender Policy Framework](https://en.wikipedia.org/wiki/Sender_Policy_Framework), which seems to just be a properly formatted TXT field in your DNS entry field. A simple, and elegant idea really, though its another thing you need to remember, along with regular backups, sieve rules, etc.

Offsite backups are a fairly easy thing to sort, with a few cronjobs from my own server at home, to an encrypted drive on the server. [Luks](https://gitlab.com/cryptsetup/cryptsetup/blob/master/README.md) with cryptfs seems to work quite well. It's not totally automatic as the whole idea is to have a human in the loop for the authentication steps. The experiments side of things is easy as well, in that there is a separate VM for me to fiddle with, that includes nginx, databases and all the rest, but is kept walled off from the production webserver. This comes in handy when you are running both Tor and an IRC bouncer. Both of these are easy to setup but places like [Freenode](https://freenode.net) get upset if you try to connect to them on a box which is also a Tor exit node.

For VPN, I use [OpenVPN](http://openvpn.org) still, and I've never had cause to change. It runs well on every device I own. One tricky problem is the use of openvpn over port 443. This means multiplexing with something like [sslh](http://www.rutschle.net/tech/sslh.shtml), which raises a couple of problems. If one is [travelling to places like China or Russia](https://www.section9.co.uk/posts/2015-04-01-transsiberian-Part-13.html) then it begins to become important. I use HTTPS for the majority of my websites though, so any SSL traffic multiplexer needs to be work really well and quickly. It may be that the VPN ends up on another VM instead. We shall see. For now though, it seems to work fine.

Calendars and contacts are tricky. I'm using [Davical](http://www.davical.org) to run both a [Caldav](https://en.wikipedia.org/wiki/CalDAV) and [CardDav](https://en.wikipedia.org/wiki/CardDAV) setup. Using caldav with Apple devices, such as an iPhone or macbook isn't too bad. Thunderbird on Windows does fine too, and with the data being held in a Postgresql database, transferring from one server to another was quite easy. Sadly, CardDav is not proving so easy to setup. In fact it likes to crash my OSX client. Terrible really. We shall see how well Windows performs. On the plus side, we now have shared calendars without the need for iCloud.

All of this is a lot of work, but it's all part and parcel of what a modern programmer needs to know, I feel. I'm sure there are people out there who ace this stuff without breaking a sweat, and I'm not one of them, but the principles are easy enough for anyone with a technical background and engineering sense. It's a machine, like any other. Having my own box is the next level up in my education.

