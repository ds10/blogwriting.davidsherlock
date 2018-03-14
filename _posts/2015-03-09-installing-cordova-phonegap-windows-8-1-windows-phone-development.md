---
ID: 2155
post_title: >
  Installing Cordova (PhoneGap) on Windows
  8.1 for Windows Phone Development
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/installing-cordova-phonegap-windows-8-1-windows-phone-development/
published: true
post_date: 2015-03-09 17:55:27
---
Some notes on installing Cordova

1) Install a Windows Phone SDK on Windows 8.1, I installed it with Visual Studio 2013 Professional because it is <a title="Developing for Windows Phone 7/8/10 for Free (Students)" href="http://davidsherlock.co.uk/developing-windows-phone-7810-free-students/">free to students.  But you should be fine with the latest community ed</a>

2)Download and install <a href="http://git-scm.com/">both git</a> and<a href="https://nodejs.org/"> node.js</a>

3)Open a command prompt (Windows Key +" S CMD") and install Cordova using the command
<pre class="prettyprint"><code>C:/ npm install -g cordova</code></pre>
4.) I created a directory on the root of my D directory to store all my cordova project, then created a project:
<pre class="prettyprint"><code><span class="pln">d:
mkdir cordova
cd cordova
cordova create hello com</span><span class="pun">.</span><span class="pln">example</span><span class="pun">.</span><span class="pln">hello </span><span class="typ">HelloWorld</span>
</code></pre>
5) changed in to project directory and added Windows 8 output, built and ran on device
<pre class="prettyprint"><code><span class="pln">cd hello
cordova platform add wp8
cordoba build
cordova run --device wp8
</span></code></pre>
For some reason it worked, when I did the same with Android<a title="Notes on publishing PhoneGap / Cordova app to Google Play store" href="http://davidsherlock.co.uk/notes-publishing-phonegap-cordova-google-play-store/"> I had a nightmare with certificates</a> which didn't seem to be a problem Windows Phone 8, but on the other hand Windows Phone Store doesn't allow self signed certificates. I guess it might be because I already <a title="Register Windows Phone and fix ‘Windows Phone IP Over USB Transport(IpOverUsbSvc) service is running’" href="http://davidsherlock.co.uk/register-windows-phone-fix-windows-phone-ip-usb-transportipoverusbsvc-service-running/">registered the device for development.</a>