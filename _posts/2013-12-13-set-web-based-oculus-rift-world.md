---
ID: 806
post_title: 'How to: Set up a web based Oculus Rift world'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/set-web-based-oculus-rift-world/
published: true
post_date: 2013-12-13 00:10:46
---
You can create virtual world for the Oculus Rift and host it on the web very easily. It's free and works on Windows and Mac OS X.  I won't go in to detail in to this post, but this is how I set my environment up and got something working in less than 20 minutes. To create worlds this way you will need some web development skills as this is based on the html5 canvas element/WebGL, but you should be able to hack something up even if you aren't that good at html5. I think that in the future there are going to be some pretty good drag and drop tools to create webgl based worlds, but for now we will use a javascript library (which is very good, just not easy for people without web development skills)

1. First you will need a way for your Oculus Rift to talk to your browser. There seems to be a few people fiddling with ways to do this but my favorite so far is Oculus bridge. You can download the Oculus Bridge program from github, <a href="https://github.com/Instrument/oculus-bridge">head over to here and download the zip file</a>.

2.Unzip the this to your desktop and look under Desktop/oculus-bridge-master/app/build for a zip file that corresponds to your system (windows or mac) extract the correct one. This should give you the Oculus Rift program. Running this when a rift is connected will send your movements to the browser (over netsockets I think). Click the extracted program so that it is running.

3. Before you start developing anything on the web you'll need a decent browser. The Oculus Rift needs websocket, this means you will need a newish browser so you are best to upgrade if you haven't in a while. Also I'm not sure if IE will work. I've not tried it with IE, but you'll be much better off with Firefox or Chrome.

4. Now you need to to create a virtual world. Fortunately the zip you downloaded actually has some pretty good examples that use three.js, a javascript library for creating some pretty cool graphics using open web based standards. If you head over to the <a href="http://threejs.org/">three.js site</a> you can see some very impressive examples; now imagine them in the rift! Anyway we'll start by using the first person demo in your extracted folder. Open  oculus-bridge-master/examples/first_person.html in your browser. The window that opens should have a button that says "Toggle Display mode" press this to make it Oculus compatible.

[caption id="attachment_807" align="alignleft" width="397"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/oculus-bridge.png"><img class="size-full wp-image-807 " alt="If a square isn't filled in then something is wrong. Here the Rift is not connected" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/oculus-bridge.png" width="397" height="163" /></a> If a square isn't filled in then something is wrong. Here the Rift is not connected[/caption]

&nbsp;

This should give you a working 3D world on the web. If something isn't working then check your Oculus-Bridge program. There should be two filled in squares, if 'netsocket' is blank then your browser doesn't support websockets. If Oculus is blank then you need to check that your rift is set up correctly.

You might also need to check your resolution setting. If things don't look right check your resolution and check the browser is not zoomed in.

Now you might want to edit the example, you can do this by simply editing the file in the js folder, open first_person.js file in a text editor (or something like eclipse). I'm saving a detailed 'how to use three.js with Oculus Rift tutorial' for another post (and there are lot of three.js tutorials on the web already) so for now we'll just edit one thing to prove that you can.  Line 124 should look something like this:

'for(var i = 0; i &lt; 100; i++){'

This is the start of a loop that creates those little flying blocks in the demo. Try changing 100 to 1000, save and run the demo again. You should now see loads of those little things (it set my computer fan off..)! After about 10 minutes I as able to put in some text that it as pulling from my twitter account, it wasn't that interesting but I thought it gave a good indication of how we can create 3D worlds in the web combined with real time data.

The next step is to start from scratch creating a 3D world using three.js and Oculus Rift. I plan on writing a tutorial, but there are lots of three.js tutorials already out there. This is the little world I created in 10 minutes:

http://youtu.be/G40XDmkSr_M

&nbsp;