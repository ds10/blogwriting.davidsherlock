---
ID: 302
post_title: >
  Getting Started with Oculus Rift SDK on
  Mac OS X (before my rift comes)
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/getting-started-oculus-rift-sdk-mac-os-x-rift-comes/
published: true
post_date: 2013-09-09 11:41:16
---
<a title="Unity3D Oculus Rift Plugin setup" href="http://davidsherlock.co.uk/unity3d-oculus-rift-plugin-setup/">EDIT: Using Oculus Rift on MAC OS X video post can be found here</a>.  This post is a failed experiment on Getting started in Xcode with the SDK. Yloly has left some useful tips to help me in the comments section of this post. If anyone else has any pointers please feel free to leave them.

I haven’t actually received my Oculus Rift yet, but that doesn’t stop me doing wanting to develop for it. There seem to be quite a few ways you can develop things for it, the easiest seem to be by using game engines such as Unity or Unreal. I however for a work project we want to do some things with the Oculus Rift with the Personal Corpus and therefore I want to get to grips with doing stuff in C++. I thought I'd make some notes as I went along.

If your on Mac OS X then you should be able to get your hands on Xcode to do some stuff with the rift. As far as I’m aware Xcode is free and available from the app store. It’s appeared on my machine somehow anyway.

OK, first things first: I’m not a very good programmer, more of a web developer who understands OO but can’t implement it very well. Secondly I am new to Xcode, I’d like to use Visual Studio but I have access to OS X more than Win 7, when I develop stuff on my Mac I usually use Eclipse as an IDE because it appears to be able to do everything; but I am assured that Xcode is the way to go for C++. I’m using the windows minimal app on the development wiki as a guide.

<strong>Step one: Download Xcode</strong>

Go to the Mac App Store, install Xcode

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/09/xcode.png"><img class="aligncenter size-medium wp-image-303" alt="xcode" src="http://davidsherlock.co.uk/wp-content/uploads/2013/09/xcode-300x169.png" width="300" height="169" /></a>

<strong>Step two: Start a C++ project.</strong>

When Xcode Starts there should be an option to start a new project. Once you’ve pressed that then look for the option to start a Command Line Tool under OSX-&gt;Application.

You’ll need to pick a product name, organization name and indentured.  I needed to pick a product name but it had already filled its self with examples for the others that would do for my hello world app. I guess for test purposes this doesn’t matter too much. I did however have to change the Type to C++.

<strong>Step three: check everything is in order</strong>

Under your project directory you should see a main.cpp. This is a prebuilt helloworld c++ program. You can click the run button to see what it does (which is push “hello world to the output program at the bottom of the scree).

<strong>Step four: include Oculus Rift SDK</strong>

This is where my lack of Xcode/C++ experience will really shine.  You need to download the Mac SDK from the Oculus Rift developers site and include the LibOVR directory in you project. I right clicked my project and went to ‘add files’ I then navigated to the LibOVR directory and clicked ok.

Now back in your main.cpp add the line:
<div>
<blockquote>#include "OVR.h"</blockquote>
</div>
under #include &lt;iostream&gt; and
<blockquote>using namespace OVR;</blockquote>
<p style="text-align: left;">beneath that</p>
<a style="font-size: 13px; line-height: 19px;" href="http://davidsherlock.co.uk/wp-content/uploads/2013/09/Screen-Shot-2013-09-09-at-12.17.01.png"><img class="aligncenter size-medium wp-image-305" alt="Screen Shot 2013-09-09 at 12.17.01" src="http://davidsherlock.co.uk/wp-content/uploads/2013/09/Screen-Shot-2013-09-09-at-12.17.01-300x222.png" width="300" height="222" /></a>
<blockquote>&nbsp;</blockquote>
Under that I created some global variables;  These were recommended by the Oculus Rift Wiki:
<blockquote>Ptr&lt;DeviceManager&gt;            pManager; Ptr&lt;HMDDevice&gt;                        pHMD; Ptr&lt;SensorDevice&gt; pSensor; SensorFusion                          FusionResult; HMDInfo</blockquote>
At this point you should be able to copile but I got this error:
<blockquote> expected predicate and/or actions following probe description,</blockquote>
but I guess this is because I don’t have a Rift connected. I guess my code will have to sit there until the postman knocks. :(

&nbsp;

EDIT: I tried this with a Oculus Rift plugged in and it still didn't work. Would be glad if anybody could help me out.