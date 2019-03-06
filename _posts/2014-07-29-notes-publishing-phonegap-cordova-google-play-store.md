---
ID: 1606
post_title: >
  Notes on publishing PhoneGap / Cordova
  app to Google Play store
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/notes-publishing-phonegap-cordova-google-play-store/
published: true
post_date: 2014-07-29 16:33:31
---
I’ve started making apps with Cordova / PhoneGap. My set up is somewhat unconventional as I am just creating the projects at the command line, writing the applications using web technologies and signing them myself. I am not using the <a href="https://build.phonegap.com/%20">PhoneGap</a> build service or any emulators on my machine. I am however using Eclipse because I am just used to it as an IDE, I have also been debugging the apps on a physical Nexus 4 . Since my setup is somewhat different and confusing I ended up getting information from many different places and thought I better write down some of the steps that I kept tripping up on.

I installed Cordova using terminal:
<pre class="lang:default decode:true ">npm install -g cordova</pre>
Creating a project
<pre class="lang:default decode:true">cordova create  &lt;projectname&gt; com.paddytherabbit.projectname</pre>
I’m only developing for android but I need to add this as a platform to the project.
<pre class="lang:default decode:true ">Cd &lt;projectname&gt;
cordova platform add android</pre>
I wanted to add plugins to the project. The advantage of not using Adobe Build is you can add plugins to your project that aren’t limited to the Adobe approved ones. For example to add the network information plugin for phonegap from it’s Github repository:
<pre class="lang:default decode:true ">cordova plugin add org.apache.cordova.network-information</pre>
You can check which plugins are installed with:
<pre class="lang:default decode:true ">cordova plugin ls</pre>
to build and run the project:
<pre class="lang:default decode:true ">cordova build &amp;&amp; cordova run</pre>
To get the project on the play store you need to sign it with a certificate. You can create the certificate yourself. Since I’m using Eclipse with the  I decided to use eclipse to generate the certificate as I already manage and create certificates using the eclipse keytool pluging http://keytool.sourceforge.net/update

Automating the signing process was difficult for somebody not that familiar with ant, there was a lack of clear documentation on how to do this, but I did find this guide by Adam Garrett-Harris worked perfectly : https://adam.garrett-harris.com/android-automation . I’ll duplicate his instructions for the sake of my own notes, but all credit goes to Adam:

Open platforms/android/build.xml and make sure it has/add
<pre class="lang:default decode:true ">&lt;property file="ant.properties" /&gt;
&lt;import file="custom_rules.xml" optional="true" /&gt;</pre>
Open/create platforms/android/ant.properties and add:
<pre class="lang:default decode:true ">key.store /path/to/my-eclipse-created-release-key.keystore
key.alias=app_name</pre>
Open platform/android/custom_rules.xml and somewhere in the project tag add:
<pre class="lang:default decode:true">&lt;property file="../../../secure.properties" /&gt;
</pre>
In this example the secure.properties is outside of the project directory so git /svn misses it. Create the secure.properties file and put:
<pre class="lang:default decode:true ">key.store.password=mypassword
key.alias.password=mypassword</pre>
Then you can build the project using:
<pre class="lang:default decode:true ">ant release</pre>
You can find apk in platforms/android/bin. As long as you have an updated version number of the application you should now be able to upload it to the play store.

&nbsp;

Video of the process, not including signing process:

http://youtu.be/3Uc5cSIzTr0
