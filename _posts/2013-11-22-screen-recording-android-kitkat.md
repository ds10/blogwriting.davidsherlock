---
ID: 759
post_title: Screen Recording with Android KitKat
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/screen-recording-android-kitkat/
published: true
post_date: 2013-11-22 10:22:40
---
Depending on your hardware/Android version screen recording on Android could be absolute pain. Google have tried to fix the problem by putting native screen recording in to the latest release of android, and actually it's pretty good. If you own a Nexus 4/7 you should be getting your rollout soon and it really is worth a look.

For this you will need a) A Kitkat android phone (4.4?) and b) <a href="http://developer.android.com/sdk/index.html#download">The android sdk from here</a> . I've created a little video of me going through the process:

http://youtu.be/yM0MV0ayt0o

For those who get the gist and are to lazy to watch a 5 minute video here are the main points:
<ol>
	<li>Download the SDK</li>
	<li>Go to phone turn on MTP, and debugging (may have to press build number 7 times)</li>
	<li>Use CMD to navigate to android folder/sdk/platform-tools</li>
	<li>Command: adb shell screenrecord /sdcard/demo.mp4 to record</li>
	<li>Command: adb pull /sdcard/demo.mp4 to pull</li>
</ol>
Easy!