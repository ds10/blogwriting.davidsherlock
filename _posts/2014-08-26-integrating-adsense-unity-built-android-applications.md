---
ID: 1760
post_title: Adsense in Unity Android Applications
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/integrating-adsense-unity-built-android-applications/
published: true
post_date: 2014-08-26 13:46:19
---
Now that Google create and maintain their own Adsense for Unity plugin it is really easy to get ads on your Unity built games. The process can trip you up and there seems to be conflicting information out there, this may be because the process has changed as the admobSDK has changed and because there are a few paid Unity assets that will do it for you. It's very easy to do tho and there is no need to pay. This little run through will show you how to create a blank project with nothing but buttons that call adverts. You can then take that example integrate that in to your own app.

II've tried this on both Windows and Mac OS X. It worked fine on both and the only differences were OS stuff that I won't bother highlighting. I assume the process is similar with iOS but there will be some differences when setting up the dependencies. So this might be helpful to you iOS folk, but I don't know to what degree. It would be helpful if somebody could leave a comment highlighting the different things Apple developers need to do.

You will need:
<ol>
	<li>Latest version of Unity. Free version is fine.</li>
	<li>The Android SDK</li>
</ol>
Also, make sure that you have done the very minimum to set up an android project, that is change your build settings so that your target is set to Android, you have the SDK location set in Edit-&gt;Preferences and have proper identifier up that looks something like com.paddytherabbit.applicationame.
<h2> Android SDK Configuration</h2>
Navigate to the directory where your Android SDK resides and look for the SDK Manager executable. Run it and you should get a screen that looks like this:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/08/androidsdkmanager.png"><img class="size-full wp-image-1763 aligncenter" src="http://davidsherlock.co.uk/wp-content/uploads/2014/08/androidsdkmanager.png" alt="androidsdkmanager" width="694" height="492" /></a>

This shows you what packages you have installed. You want to make sure you have Google Play Services and Google Admob Ads SDK installed. In my screenshot they are both installed, if the say not installed for you then click the little boxes next to them both and press the install packages button. You will need to agree to a terms and services document that I presume sells your soul over to Google.
<h2>Install the Admob Plugin and dependencies</h2>
Open Unity and start a blank project. Next head over to this <a href="https://github.com/googleads/googleads-mobile-plugins">Google AdMob Plugin Github repository</a> and look for the downloads section and get the latest .unitypackage download. You should now have two folders in your project, these are plugins and GoogleMobileAds. You will also need the Google Play Services library. To get this navigate to your android SDK and look for sdkextrasgooglegoogle_play_serviceslibproject and copy the Google-play-services_lib folder in yo your assetspluginsAndroid folder in your Unity project.
<h2>Grab the HelloWorld project</h2>
Back at the Google AdMob Plugin Github download the project as a zip and import the two assets under HelloWorld. You should find a script and a Unity scene, once import open the scene, check the camera and see if the script is attached, if not then attach it.
<h2>Edit script and build and run</h2>
Edit the example script by placing you AdMob SDK IDS on lines 73 and 98. Check your project is set to target android and that the SDK is in the correct place and you have an identifier. Done!

Video of the process:

http://youtu.be/rvhot-x5dA4

&nbsp;

&nbsp;