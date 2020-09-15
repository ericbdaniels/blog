---
layout: page
title: Resources
permalink: /resources/
---

# Learn Python
* [Real Python](www.realpython.com) - Originally Michael Herman ([TestDriven.io](https://testdriven.io/)) now owned/run by Dan Bader, Real Python provides tutorials in both text, video and course format on all things python. I've learned a great deal from Real Python and highly recommend them.

* [Talk Python To Me](https://talkpython.fm/), Audio seems like a strange medium to learn anything code related but trust me this podcast is great. If you've got a background in something other than web development/computer science Talk Python To Me is a great way to get exposed to and learn from the wider world of python. Michael Kennedy does a great job.

# Learn Geostatistics

* [GeostatsGuy](https://www.youtube.com/c/GeostatsGuyLectures/) aka Michael Pyrcz is a Professor at the University of Texas at Austin teaching Geostatistics and Machine Learning. Many (maybe all?) of his lectures are available on YouTube and they're great for everyone beginner to expert.

* [LazyModelingCrew](https://lazymodellingcrew.com/) This a group of somewhat recent graduates from the Centre for Computational Geostatistics at the University of Alberta. They've recently started sharing some easily digestible Geostatistics lessons as blog posts. I especially recommend the variogram focused posts for anyone new to geostats. 

* [Geostatistics Lessons](http://www.geostatisticslessons.com/) Thoughtfully put together lessons for some of the more complex aspects of Geostatics. Mostly supported by the Centre for Computational Geostatics at the University of Alberta.

# Tools, Packages etc for Geostatistics and Geoscience

## AR2GAS
First a plug for the product I work on day to day: [AR2GAS](http://ar2tech.com/) is c++ backed software with a Python API that can be run on your local machine, on a local cluster or on the cloud for geostatics on a regular or unstructured grid (or even gridless!). I think we're doing great work and if you're interested in learning more please reach out.

## Open Source Geostatistics
There are a number of open source python packages available for Geostatistics using Python but my experience with them is limited and I can't speak to how "production ready" they are. At some point I'd like to do a little compare/contrast/benchmark with a few of these.

### SGeMS
* [SGeMS](http://sgems.sourceforge.net/?q=node/77) is a GUI based software for Geostatistics created at Stanford University. If you prefer clicking buttons to writing code this is a great option for free software.

### GSLIB
* [GSLIB](http://www.statios.com/Quick/gslib.html) is the original Geostatics Library of software created by Clayton Deutsch that has grown over the years. Its not fancy, but it works and you can always script a few programs together with `subprocess`.

### Python(ish)
The (ish) because a few of these use FORTRAN or C++ for the heavy lifting.
* [Pygeostat](https://github.com/CcgAlberta/pygeostat) - Supported by Centre for Computational Geostatistics. Note much of the computation relies heavily on GSLIB FORTRAN programs.
* [GeostatsGuy](https://github.com/GeostatsGuy/GeostatsPy) - Michael Pyrcz's python package for geostats. There are 2 components, one is pure python the other relies on GSLIB FORTRAN programs.
* [High Performance Geostatistics Library](http://hpgl.github.io/hpgl/) written in c++ with a python API - looks interesting and they give some benchmarks showing its substantially faster than GSLIB.

I don't know much about these other offerings but they have a number of stars on github so there are some people out there using them.
* [GSTOOls](https://github.com/GeoStat-Framework/GSTools) - Last commit 6 months ago..
* [SciKit-Gstat](https://github.com/mmaelicke/scikit-gstat) - maybe still maintained? Last commit was 5 months ago.