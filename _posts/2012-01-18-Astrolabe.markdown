---
layout: post
title: Astrolabe
tags: lasercutting
introtext: I've always been fascinated by space, the planets, their maps and photos. The Curator is one of only a handful of experts in the world studying medieval scientific instruments and the astrolabe definitely fits that category.
strapline: I thought I'd have a go at making an astrolabe.
---


I've always been fascinated by space, the planets, their maps and photos. The Curator is one of only a handful of experts in the world studying medieval scientific instruments and the astrolabe definitely fits that category.

![Astrolabe](http://farm8.staticflickr.com/7011/6716956337_ee19b570ff.jpg)


As part of a project I'm working on, I decided to build my own Astrolabes - one from paper and another from perspex, in order to get a feel for their construction. The goal is to create a WebGL version for display. This version is taken from [the one available at Thingiverse](http://www.thingiverse.com/thing:3271).

Technically, this was quite a challenge. [LondonHackspace](http://london.hackspace.org.uk) has a laser cutter but the software for it is awful. In addition it is quite often worn out which is clearly no good. Nevertheless I persevered. 

The format for this file was a Corel Draw CDR. Seriously, do people still use these? Anyway, I needed a program to convert that down. [Uniconvertor](http://sk1project.org/modules.php?name=Products&product=uniconvertor) seemed like the thing, but getting it to compile and build on OSX was not an easy job at all. In fact, I had a lot of issues with it. Nevertheless, I converted the CDR into an illustrator file. No dice! CDR to SVG worked a lot better.

Loading the SVG into Illustrator allowed me to see the various problems and options available. Two front plates were included, one for the southern and one for the northern hemisphere. The first thing was to seperate out all of the various components as each would be etched and cut into a seperate sheet of coloured perspex at 3mm. 

![astrolabe](http://farm8.staticflickr.com/7158/6716964469_2057259913.jpg)

Further conversion from SVG was needed. Inkscape makes a good job of loading the SVG correctly. Exporting from Inkscape to a DXF is the next step, making sure LWPOLYLINE and ROBOMASTER were NOT selected. Finally, for the hackspace laser cutter, importing into QCAD was needed, because the laser cutter software does not support layers. The front plate, rete, pointers and bevel both have cutting and etching sections, so layering (or in our case, colouring) with QCAD was needed.

So, after a about 5 programs later and a lot of swearing and bitching, the Astrolabe was ready. There are problems with it. The text has not come out at all and there are a few markings missing. Etching on the backplate is slightly out of alingnment and the rete is incomplete; the star map should appear on it as well. I may use acetate glued to the back of the rete. Also, the outer bevel should be fixed and not move with the rete but the tolerance is too tight and despite my efforts to file down the edges, it still wouldn't move.

But this is fast prototyping in plastic! Its only the first step.