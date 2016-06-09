---
layout: post
title: BSides London 2016
introtext: I try to make it every year to BSides. It's a great litle conference, which is saying a lot for someone who isn't really a conference fan. I'm not particularly involved in the Security Industry but it's something I'm interested in, both as a hobby and professionally, as all software engineers should be really. 
strapline: Possibly the best little security conference in London. This year, docker, R and static analysis, with some Linux Rootkits thrown in.
tags: security hacking conference
---

I try to make it every year to [BSides](https://www.securitybsides.org.uk/); I've written about the previous times [before](https://www.section9.co.uk/posts/2012-04-27-BSides.html). It's a great little conference, which is saying a lot for someone who isn't really a conference fan. I'm not particularly involved in the Security Industry but it's something I'm interested in, both as a hobby and professionally, as all software engineers should be really. 

The event is free, though I missed the tickets this year. Thankfully, if you turn up a little early you can get a ticket on the door so long as they haven't run out. Risky but it worked in my case! For a free event, there is a lot to get your teeth into: workshops, talks, challenges and networking. The attendees are what you would expect at a security conference; a combination of your classic geek-come-metaller, young men (predominantly) who are attempting to dress smart and don't really like it, and your older, shirt and tie wearing exec. There are more women this year, and about the same number of minority groups.

I tend to divide my time between a workshop and talks, as the workshops are free and you can really learn a lot. It's a good opportunity to ask questions. They tend to be very crowded, however unlike infosec types (I'm told) I arrive nice and early. The first workshop is all about using R to cut and slice logfiles for analysis, given by [Steph Locke](http://www.twitter.com/SteffLocke). The slides and code are available [here](http://stephlocke.github.io/rtraining). I've been wanting to learn a little [R](http://r-project.org), mostly because data scientists (and indeed, scientists of all kinds) like to use it. Apparently regex is still handy and therefore [RegExp.com](http://www.regexp.com) is a good site to have in your bookmarks bar.

One great thing about BSides is the free lunch! Its pretty good with salad, baguettes, biscuits fruit and the like. Most of that is down to the sponsors and their logos are everywhere. That said, the event really doesn't feel that corporate; the balance is just about right, which is a hard thing to do I think.

The talk on Static analysis was a brief introduction to using various tools to catch bugs early. Some tools are based on RegEx - looking for known patterns. These tools tend to create a lot of false positives as they lack context. Tools that incorporate lexers, parsers and state are more complicated but fair better. [FlawFinder](http://www.dwheeler.com/flawfinder/), [Graudit](http://www.justanotherhacker.com/projects/graudit.html), [RATS / Fortify](http://www.softpedia.com/get/Security/Security-Related/RATS.shtml), [Veracode](https://www.veracode.com/) and [Klocwork](http://www.klocwork.com/) were recommended, as well as rolling your own. Clang Analyzer and the LLVM tools were mentioned as being the best starting points (which I can totally believe). This is something, along with a good Linter, that I need to insert into my coding workflow.

![Chip Whisperer](https://c2.staticflickr.com/8/7789/27458490112_0c16571c6b.jpg)

The Lightning talks are often some of the most interesting, along with these on the Rookie track. I popped into a talk on Linux Rootkits - a fascinating topic. The technique being described was "debug systemcall hooking" and was demonstrated by creating a Linux module that can hide itself by intercepting syscalls. Messing around with the hardware registers was discussed, along with the caveat of really needing to know your x86 architecture. Reading [Phrack63](http://phrack.org/issues/63/1.html) was recommended along with checking out [this guys github page](https://github.com/gfudge?tab=repositories) which I shall certainly do.

I briefly popped into a second workshop about Glitch attacks. The idea is to get an embedded device to trip over itself by sending a clock signal that is a little too fast or slow. Using the [chip whisperer](https://www.assembla.com/spaces/chipwhisperer/wiki) board one can hookup various attacks with ease. That said though, the software is tricky to install and I failed to get my VirtualBox setup in time on my little x220, so in the end, I left the workshop and caught the end of the iOS malware talk. Seems like it's pretty tricky to get malware onto an iPhone but there are ways. Extensions for things like the keyboard is one way of getting keyboard loggers in there; apparently this was used by Hacking Team in some of their work. USB style AV might be in the near future potentially.

The last talk I went to was on Docker security. In my job I use Docker a lot, but for development it's largely ok. It's when it comes to deployment however, things are much harder. One has to be really careful and setup many things to make docker more secure. Some of the key points I came away with were:

- Always read the very latest docs. Docker changes pretty quick
- Docker diff and docker compose are really handy tools in creating a pentest environment for things like malware analysis, CSS, SQL inject etc
- Using Linux namespaces helps to lock docker down
- User namespaces should make root in the dock not root outside the dock but this is *not turned on by default in docker*
- Capabilities in Linux help break-up what users can and cannot have access to and this can help
- CGroups are a good way of reducing problems with resources
- Keeping docker updated to the latest version is a big job but worth it.
- SECCOMP - the locking down of syscalls from the dock can help
- Do not allow mounting of docker.sock
- Do not allow --privileged to be used in production

It still seems like access to the docker command basically gives you root which is the major problem, but I hear this might be changing. Hardening your containers is a good start, so not trusting dockerhub is a good idea. Clearing the history in the containers is another good idea as passwords and the like could be revealed. Basically there's a lot of work but the presenter, [Rory McCune](http://www.twitter.com/raesene) has some good resources [here](https://www.nccgroup.trust/globalassets/our-research/us/whitepapers/2016/april/ncc_group_understanding_hardening_linux_containers-10pdf/), [there](https://www.nccgroup.trust/globalassets/our-research/us/whitepapers/2016/june/abusing-privileged-and-unprivileged-linux-containerspdf/), and [perhaps here too](https://raesene.github.io/) where you can learn more.

BSides is a great little security conference. I think it's definitely a good idea to check out the major talks first as the headings don't often tell you what you need to know. Taking a laptop with a good VirtualBox install is a good idea, along with some way of tethering to the internet (in case you end up in a small room where the wifi doesn't reach). Maybe one of these days I'll pluck up the courage to take part in the competitions :) 

