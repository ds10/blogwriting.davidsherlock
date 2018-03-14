---
ID: 417
post_title: >
  Help needed. Kinect, Oculus Rift and
  Javascript on OS X
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/kinect-oculus-rift-and-javascript/
published: true
post_date: 2013-10-26 12:42:48
---
Having just picked up a 2nd hand Kinect rather cheap I was poking around things I could do with it. I decided I came across some Javascript libraries and wanted to combine my Oculus Rift browser experiments with the Kinect. Unfortunately I seem to need the Windows only Kinect SDK to get started. It look's like I may be able to use something based around <a href="https://github.com/doug/depthjs">dephJS</a> but I'm not to sure how much I can do with it.

While I scratch my beard and look around the web for ways to go, I’d appreciate any advice for OS X users wanting to do stuff in the browser with Kinect.

Update: Looks like there is a stack of technologies I can use called OpenNI/NITE. I installed the whole stack including USB support with a plugin that is supposed to make it accessible to the browser. The plugin is called Zigfu, but I couldn't get that to work. I could get the tracking to work however:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/10/kinectmac.png"><img class="aligncenter size-medium wp-image-422" alt="kinectmac" src="http://davidsherlock.co.uk/wp-content/uploads/2013/10/kinectmac-300x121.png" width="300" height="121" /></a>

&nbsp;

Now if there is a javascript library to recognise the tracking and pump into three.js  that would be great.