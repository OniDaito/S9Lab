---
layout: post
title: High Performance Computing at Daresbury
strapline: I spent a week at STFC Daresbury, learning about HPC and science!
introtext: For my first outing on the company dollar, I'm whisked up to the sunny Warrington Riveria for a chance to play with one of the UK's more powerful supercomputers, at the Daresbury Laboratory, up in sunny Warrington
tags: coding programming science qmul work
---

For my first outing on the company dollar, I'm whisked up to the sunny Warrington Riveria for a chance to play with one of the UK's more powerful supercomputers, at the [Daresbury laboratory](http://www.stfc.ac.uk/about-us/where-we-work/daresbury-laboratory/). This facility used to be involved with the country's nuclear program, and includes some impressive sixties style buildings. Nowadays, they deal with High Performance Computing (among other things). Unlike a university, these laboratories just do research. As a member of another institution you can submit proposals for research and if they can match you up, away you go.

Specifically for me, I was sent to the [Hartree Centre](http://www.stfc.ac.uk/innovation/ways-to-work-with-us/the-hartree-centre/) for one of their summer-school sessions. They run schools each year, focusing this year on HPC, Big Data and Visualisation. These topics are pretty much right in our wheelhouse here at QMUL so learning a little more about the context certainly helps.


![Synchrotron Henge](https://farm1.staticflickr.com/299/19455532748_dca94356bf.jpg)

The course is broken down into about 6 main areas with a couple of extra bits bolted on. The main topics were [OpenMP](http://openmp.org/wp/), [APGAS](http://x10-lang.org/software/download-apgas/latest-apgas-release.html), [MPI](https://en.wikipedia.org/wiki/Message_Passing_Interface), [Linear Algebra](https://en.wikipedia.org/wiki/Linear_algebra), History and overview of HPC and HPC Architecture. A short session on visualisation was thrown in along with some heavy theory on simulation and the testing of computational models.

APGAS is a Java based approach that seems to mirror MPI in my opinion. I'm not a Java developer and have no real intention of following that route. QMUL really isn't a Java shop so the concepts were somewhat wasted on me. I'm not the biggest Java fan, though Virtual Machine technology is nice.

OpenMP and MPI on the other hand are extremely relevant. We deal a lot with both. There were some top tips given for both of these approaches. The general consensus is they should be used together for best effect. Some of the advanced topics like [Halo](http://stackoverflow.com/questions/17580282/exchange-data-between-mpi-processes-halo) and [Cartesian Topology](http://stackoverflow.com/questions/9476445/how-to-use-mpi-cartesian-topology-correctly), [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (as oppose to master slave) and OpenMP allocated memory were really handy topics to take on board. Clearly theres a lot to learn!

![Dark Matter](https://farm4.staticflickr.com/3750/19455574390_b896715c7b.jpg)

The Linear algebra section was quite interesting. It's a topic I need to revise an awful lot more really. Lots of shout-outs to the various libraries such as [LAPACK](http://www.netlib.org/lapack/), [BLAS](http://www.netlib.org/blas/) and [kokkos](https://github.com/kokkos/kokkos). Linear algebra seems to be used quite often for many problems in scientific computing. Simplifying down a problem into discrete units that can be massively parallelised is a skill worth learning and once learned, can be very valuable.


This was the impression I got on the course. Unlike the middle ground of programming and technology (the bit where people skin databases and create pointless iPhone apps), the small scale and large scale ends really respect talent, age and experience. Most of the lecturers were older guys but with quite a bit of experience, having built many supercomputers and serious libraries in the past. There seems to be less pretense and more serious work going on in this area.

![Synchrotron Henge](https://farm1.staticflickr.com/467/19020989924_54e8442d6f.jpg)

Daresbury is set in quite an idyllic area, even considering that the North West is overcast, damp and grey most of the time. Even the food in the canteen is reasonably priced and tasty. Set in the grounds are the remains of the first UK Xray synchrotron source (dubbed [dipole henge](http://www.stfc.ac.uk/news-events-and-publications/events/stfc-events/photowalk-daresbury-laboratory/)) and various other sculptures. 



It seems to me that it's quite an exciting time in supercomputers at the moment, and a good time to be learning about HPC.