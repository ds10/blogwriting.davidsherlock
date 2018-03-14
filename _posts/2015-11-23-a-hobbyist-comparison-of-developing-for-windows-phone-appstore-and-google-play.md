---
ID: 2483
post_title: >
  A Hobbyist Comparison of developing for
  Windows Phone, Appstore and Google Play
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/a-hobbyist-comparison-of-developing-for-windows-phone-appstore-and-google-play/
published: true
post_date: 2015-11-23 14:48:35
---
I’ve been playing with submitting games to the main phone market places for about a year now and I have had a really different experience with all of them. I’m very much developing gamesfor a hobby, and I expect that due to technologies like Unity there are many other people in the same boat. These are my notes/experiances with the marketplaces as somebody using them as part of his hobby. Experts and big companies might see my pros/cons differently! Also, the market places seem to be changing so quickly that a year is a long time. I haven't really had time to write these up, but they may be helpful to somebody:
<h2>Google Play</h2>
A year ago my experiences with getting my Unity games in to <a href="https://play.google.com/apps/publish/">Google play console</a> were so dire it drove me to switch to Windows Store for a while. I can only sum up the Google policy at the time as ‘shoot first then don’t even bother asking questions later’. I received two ‘Strikes’ from Google Play for breaching small time trade marks that I was not aware of, three strikes would have been a ban. While I’m aware something has to be done about trademarks, the problem with Google’s approach was that there automated bots that checked if your app broke the rules seemed to check packages months after they were in the store, so you would submit your game, get it accepted and then months later find out you’ve broken some kind of rule and get a strike, 3 strikes and you were banned for life, looking on various forums it seems some people where banned by three autostrikes all at once. Google claimed they would investigate claims of unfair strikes, but I found they didn’t check their email unless you were EA. 12 months later and things seem to have gotten much better, the bots now check packages before they get accepted in to the store meaning that if your make a mistake you won’t get penalized down the line. Older banned accounts under the old method appear to still be banned.

Google’s developer documentation is great and the interface when uploading your game is easy to use. Although if you do get stuck or require any specialist help then you will need to ask the community because as with my experience with all Google support, they only reply to an email if you are a big player in whatever it is you are doing. Supports for hobbys are zero.

Other than the automated bots, there are very little checks in place with the Google Store, you can get pretty much anything on there and fast. This also means that the store is filled with crap.

Anybody can sign a Google App, while this means that anyone can get anything on the store, it also means that have to get your head around signing apps. This is easy if you use Unity.

If you are not using Unity, the integration with the android store and IDEs is generally terrible. There is an official Android IDE, but last time I tried it would crash at every opportunity, leaving me to use Eclipse with some plugins when I wasn't in Unity.

If you are using Unity then you can simply create an APK to upload to the store, or ‘run and build’ to a device from within Unity itself. This is easier than both Windows Phone and iPhone builds where Unity creates project files for Visual Studio or Xcode. Presumably this is because you don’t need Google/Microsoft/Apple certificate to sign the package to get it on to the device.

Beta testing is easy with Google Play, users must be added to a Google group to download the app.

Cost: $25 one time fee
<h2>Windows Market Place</h2>
Currently I find the Windows market place is a maze for people who are not up to date with Microsoft development. They are currently switching to a unified Windows Universal platform, from what I can gather this should mean that if you develop for one windows device then you develop for them all. This sounds great, but for now the casual hobbyist like me logs in to <a href="http://dev.windows.com">Windows developer store</a> and doesn’t actually understand which store they are submitting to. Moving projects from a Windows Phone to a Windows Universal app doesn’t seem to be entity painless either.

Microsoft bots check your app for things like trademark issues before it hits the store so I haven’t had any strikes for breaking rules I didn’t know existed. There does seem some inconsistency when it comes to checking the apps. I submitted and got 3 apps accepted 3 times without a problem, then suddenly on my fourth app they decided that my apps logo (which was similar to the others) was not ok, it took me 3 attempts to creae a logo that was OK. I can only guess that a random portion of submissions go to humans to test.

Microsoft appear to be quite good at replying to queries when developing games for their phone and there are also lots of incentives and reward schemes. Students get free access to the store and there are plenty of other Microsoft goodies available from the <a href="https://www.dreamspark.com/">Microsoft Dreamspark</a>.

There doesn’t seem much in the store, but there aren’t many users either with a significantly smaller user base.

If you are using Unity you might find lots of plugins don’t work with Windows. Unity does not build an executable for windows phones, but instead builds a Visual Studio Solution

I haven’t beta tested with Windows Phone, but it appears that anybody with a Live account can be added as a tester.

Cost: $25 one time fee, free for students
<h2>Apple App store</h2>
When developing for Apple mobile devices you get access to a site called <a href="https://developer.apple.com/programs/">iTunes Connect</a>, from here everything is really straight forward and easy to use. When it comes to support for developers the appstore is king, send them an email and you get a reply with 24 hours. If there are problems with your app a real person contacts you. All this ease of use is great, but at $99 a year you really are paying for the privilege. Automated bots are used to check for things like API calls to services, anything that looks odd will be emailed to you.

If you plan on using Apple services such as iad, gamecenter or in app purchases then it is incredibly easy to manage from within iTunes Connect. iTunes connect, while mostly brilliant can sometimes be agnosiingly slow.

Out of all the devices iOS is the easiest to develop for within Unity because of the similarity of the physical devices. Most Unity mobile plugins also seem to work for apple, although nuch like developing for windows, exporting the app itself is a two step process and requires building in Xcode.

Once an app is submitted it can take 7 days to hit the store as it goes through a review process. I’ve never had a problem with any of my apps, apart from Apple ocne thought I had some metadata incorrect. Once I proved my metadata was fine apple ok’ed the app without having to wait the 7 days again.

Beta testing is easy through an additional app called TestFlight, getting apps on to the TestFlight Store also goes through a review process, although this only seems to take a day.