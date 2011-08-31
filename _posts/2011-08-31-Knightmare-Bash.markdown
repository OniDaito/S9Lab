---
layout: post
title: Knightmare Bash
---

So I came up with this today:

	#!/bin/bash
	a=$(echo $1 | tr '[:lower:]' '[:upper:]')
	e=$(echo $a | sed 's/\(.\)/\1 /g')
	echo -n "SPELLCASTING: "
	for i in $e; do
  		echo -n $i" "
  		sleep 1
	done;
	echo ""
	$1

This little piece of bash script is the geekiest and therfore *coolest* thing I've written for the past few weeks. But it's had me thinking a little about programming, life and the universe. 

It was born out of a semi-drunken chat with my good friend [Steve](http://www.casa.ucl.ac.uk/people/person.asp?ID=260). After cooking a *rather splendid* roast dinner, the conversation turned, as it inevitably does, to TV programmes we used to watch as kids. I don't know why that always happens after a certain age but it's something that has occurred between my friends and I many times. I suspect it's not just me either. Of course, we had to talk about [Knightmare](http://www.knightmare.com/).

Steve hit on the idea of a spellcasting script of some kind so I thought I'd write one. I was bored at work this morning and figured it would be a good warm-up. I'm no bash ninja sadly, though I've often thought about learning more and there indeed is the rub. It's important to take little steps and to do that, you *have to want to take them*. 

I think this simple example is quite similar to the [Thermoptic Camouflage](http://www.vimeo.com/26788575) play-thing I wrote. It's what you might call a *speed project*. It's a little bit fun, the outcome is known, and you have a pretty good idea of what you need to do but with scope for learning and finally, most importantly, it doesn't matter.

The last bit is important. There is no real pressure save whatever you bring to it. 