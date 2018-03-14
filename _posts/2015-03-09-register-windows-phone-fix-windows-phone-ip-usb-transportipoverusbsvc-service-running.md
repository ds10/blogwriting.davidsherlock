---
ID: 2150
post_title: 'Register Windows Phone and fix &#8216;Windows Phone IP Over USB Transport(IpOverUsbSvc) service is running&#8217;'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/register-windows-phone-fix-windows-phone-ip-usb-transportipoverusbsvc-service-running/
published: true
post_date: 2015-03-09 10:19:50
---
One of the things I liked about Android development was that it was very easy to get up and running, you could get a phone for very cheap and you could sign your own applications so they would run on any phone. I liked the beta testing in the store so anybody you invited could download your applications before they went public.

It could also be a bit of a pain though, Google are so relaxed about what happens on Android phones that people who were new to development had to start worrying about things such as certificates and the such. One of the things I've found about Microsoft Phone 8 development is that Microsoft take care of annoying things such as certificates and signing for you. It means that the phone is slightly more locked up (but not to the extent that I have to pay £100 a year just to put an app I've developed on my own phone- Apple!) but the process is so much easier for new mobile developers like myself.

Well, it is easier up until the point where something in Microsoft's automagic app signing goes wrong. I had trouble unlocking my phone and got the error

'make sure that the Windows Phone IP Over USB Transport(IpOverUsbSvc) service is running'

There are plenty of pages on the web telling you how to fix it, the most popular is to reset the IpOverUsb service, however this still would not work for me.  In the end the key for me was to make sure that I had internet access on both my computer with Visual Studio on it and the phone. It seems quite obvious looking back, but I had forgot to set up the wifi for the phone in the location I was working from. In case you are stuck registering you Windows Development I recorded the process. As you can see I got stuck with the error message but managed to fix it:

http://youtu.be/UXqzM6uyFQE

Here were my steps:

1)Plug Phone in

2)Open Visual Studio

3)Go to 'Register Phone'

4)Make sure that Internet Access is on both the phone and computer

5)Restart IpOverUsbSvc