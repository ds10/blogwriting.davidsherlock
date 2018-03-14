---
ID: 388
post_title: '3D worlds on the web using the Oculus Rift: attempt 1'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/3d-worlds-web-using-oculus-rift-attempt-1/
published: true
post_date: 2013-10-10 13:28:18
---
So far with my Rift I’ve had a go at creating a virtual world that imports data (just text at this point) <a title="An API to our Personal Corpus" href="http://davidsherlock.co.uk/api-personal-corpus/">from my personal corpus/personal api a</a>nd displaying them in a room. I wanted people to be able to go trot around a virtual world, view bits of text and stats exploring things they about themselves. <a title="Unity3D Oculus Rift Plugin setup" href="http://davidsherlock.co.uk/unity3d-oculus-rift-plugin-setup/">I had a first attempt at this in Unity 3D</a>, which is takes about 10 minutes to set up and start creating something, the problem with my current efforts is that the Unity 3D game development platform will charge you $75 after the 5 month free PRO trial.

Deciding to move to a free platform I started to build stuff in WebGl.  Poking about I found there’s a pretty good library used to build 3D worlds I came across called <a href="http://threejs.org/">three.js</a> . I nabbed an example of a <a href="https://github.com/Instrument/oculus-bridge/tree/master/examples">mini 3d blocks city in three.js from here</a> , mucked around with reading some text from some topic modelling scripts I '<a title="Personal Corpus: Update" href="http://davidsherlock.co.uk/update-personal-corpus/">prepared earlier</a>' and downloaded the <a href="https://github.com/Instrument/oculus-bridge/tree/master/examples">Oculus Bridge</a>:  to create a very rough 3d City featuring random words from my topic models in the browser.

The important thing is that the 3D world responds to the movement of my head when I wear the rift, it only took me about 5 minutes (most of is from the bridge examples, which uses three.js anyway) to mash these things together  and I had a 3D world I could put on the web importing data from a different source.  I'm hoping I can have it react in real time to things that are going on. Here’s a video of the world working in the browser on my local machine, I've got the headset on while I'm recording. It’s hard to tell from the video the feeling that the wearer gets but I did want to reach out and touch the words. The little flying cars I want to be stats about my life and the high rise buildings replaced with some kind of visual representation of the things I am doing. The movement was pretty hard because while it tracked my head it didn’t track my body, I wonder if I can get it working with an xbox pad. When I get time to actually do some proper development I’ll blog it up.

http://youtu.be/G40XDmkSr_M