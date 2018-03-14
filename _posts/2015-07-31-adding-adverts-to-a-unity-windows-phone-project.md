---
ID: 2427
post_title: >
  Adding adverts to a Unity Windows Phone
  project
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/adding-adverts-to-a-unity-windows-phone-project/
published: true
post_date: 2015-07-31 17:06:41
---
If you are building a game from Unity to deploy on Android <a href="http://davidsherlock.co.uk/integrating-adsense-unity-built-android-applications/">it is quite easy to install a plugin</a> that lets you have control over the exact positioning of adverts. If you are outputting to Windows Phone however your choice is much more limited.  I've found many of the Windows Phone advert plugins seem to have problems with Unity 5. I'm not quite sure why this is, but perhaps Microsoft's struggles with unifying the Phone/Desktop SDK, recent changes to Unity and lack of uptake of Windows Phone has left the available tool sets underdeveloped.

Still, one method that is very easy is to implement ads outside of Unity by positioning them in Visual Studio instead. Here is a quick guide on how to add adverts to the top of your game. I assume that you can control when they appear with a little bit of extra code, but to keep it simple I won't go that far here. This method should work for whatever ad network you want to use (or indeed should work for the Microsoft Ad Mediator). The steps:
<h2>Build Finished Game in Unity</h2>
[caption id="attachment_2429" align="alignnone" width="272"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/rsexport.png"><img class="wp-image-2429 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/rsexport-272x300.png" alt="rsexport" width="272" height="300" /></a> First, build a project in Unity at the familiar 'Build and Run' screen.[/caption]

Once you've finished In Unity you need to build you game as normal by navigating to file-&gt;build.  Check that you have selected Windows Phone 8, add the scenes you want and press build. This will create a Visual Studio project at the location you desire. I am not a native Windows Phone developer but as far as I can tell Unity will build you a Windows Phone 8 Silverlight project if you use this option. Perhaps this is to do with Microsoft trying to merge phone and store development practices with Windows Phone 8.1.
<h2>Open Project in Visual Studio</h2>
Navigate in Windows and open your newly created project. I've had trouble in the past with Visual Studio projects built by Unity (mainly when using NuGet) because they don't come with a solution, so the first thing I usually do is save the project again, this time within Visual Studio, to create the solution file. However, I don't actually know if this is good practice but I seem to get less headaches when I use package management bits and pieces.

To show adverts you are going to need to include the advertising SDK in your project. If you want to use Microsoft PubCentre then you simply need to make <a href="https://msdn.microsoft.com/en-us/library/advertising-mobile-windows-phone-download-install(v=msads.20).aspx">sure this is installed,</a> I'm pretty sure that you need to download the SDK targeting Silverlight for WP 8. Still, I use AdMob, its developed by Google and it seems to go in phases of working really well on Windows Phone and then suddenly deciding to be rather poor on anything except android. If this is down to the fact Google can't keep up with Microsofts new strategy for cross platform apps or the fact Google just want WP to fail I don't know. Still, if you want to use AdMob you must include references to the GoogleAds library. This is easy enough to do:

1. <a href="https://developers.google.com/admob/wp/quick-start">Download it from here and extract</a>

2. In Visual Studio right click references in solution explorer and select add reference

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/affref.png"><img class="alignnone size-medium wp-image-2431" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/affref-300x191.png" alt="Add references in visual studio 2013" width="300" height="191" /></a>

3. Navigate to the DLL you have just extracted and add it as a reference. At this point sometimes Visual Studio gives you an error when importing like 'Microsoft visual studio a reference to a higher version or incompatible assembly cannot be added to the project'. If you get this error then you need to right-click the Google DLL, select Properties and then click on the Unblock button

&nbsp;
<h3>Place Advert and configure</h3>
You need to place the advert on the mainpage.xaml file. You can do this by either opening the designer and toolbox (open file and then press ctl+alt+x) and dragging on an AdView/AdControl element. Adview is Google AdSense, AdControl is pubcentre.  Or you can directly paste the XAML:
<pre class="lang:default decode:true">For Pubcenter:
&lt;UI:AdControl ApplicationId="XXX" AdUnitId="XXX" HorizontalAlignment="Center" 
Height="80" Margin="0,0,0,0" VerticalAlignment="Top" Width="480"/&gt;

For AdSense
&lt;GoogleAds:AdView AdUnitID="XXX" Format="Banner" HorizontalAlignment="Center" 
Margin="0,0,0,0" VerticalAlignment="Top" Height="80" Width="480"/&gt; 
</pre>
You  only want one of these will need to replace XXX with your own values. Also make sure it is aligned as you want to display it.

This will display the ad in the position you choose. Don't forget you will need test values in for development, although I am guessing most development testing will be done using 'build and run' in Unity.