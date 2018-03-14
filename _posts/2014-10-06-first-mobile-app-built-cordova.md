---
ID: 1849
post_title: >
  My first mobile app –built with
  Cordova
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/first-mobile-app-built-cordova/
published: true
post_date: 2014-10-06 16:03:26
---
I’ve been contemplating getting started with mobile development for a while. On the one hand it feels like there is something very powerful about writing software for portable devices, on the other hand it just felt like there were too many barriers in the way. Cost was always major issue for me and because I am not in the business of writing Apps for a living I hate the idea of paying Apple £100 a year for the privilege of writing applications for a device which costs way more than it should in the first place. When the first Android devices started trickling out I don’t think there was anybody who doubted that it’s market share would soon leave iOS in the dust, I was excited and with the cost being so much lower I thought that I was going to start developing applications for it as soon as I could.

As soon as I got my hands on an Android phone I poked about the development kit… and came to the conclusion that I couldn’t be bothered. I thought it would be nice to knock something up for my phone, but I’ve always been the sort of person to knock out lots of personal projects quickly rather than have my head stuck in a project for 6 months. Despite already knowing my way around Eclipse, the learning curve just seemed to steep for somebody wanting to knock things out quickly. Plus, why should I learn how to do something for Android when it will be different for iOS/Windows Phone/Web?

It annoyed me somewhat that I couldn’t just do it with web technologies with some sort of special middleware that could somehow allow me to access the phones features that a regular native application would do and also allow me to get around some of the issues of hosting software on the web.  Particularly since Google is clearly headed towards a world of HTML and Javascript applications/

This apparently annoyed a lot of people and it wasn’t long before a project surfaced that was basically that. <a href="http://cordova.apache.org/">Cordova</a> is a set of APIs that allow developers to build phone applications and access the functions of the phone using html/css/javascript. I believe the original project was called PhoneGap but this has since been purchased by Adobe, the underlying functionality is still nice and safe in an Apache project, so you can develop using tjat with your soul in tact.

It’s taken me a few hours of throwing stuff together here and there to get a very basic application together. While it is not a very good application, I’m amazed that I can get something on to the Google play store in a few hours. Here are some thoughts:

<strong>It is not quite as simple as 'make a website, stick it on your phone'.</strong> If like me, you have some web development experience but no mobile development experience then the hardest bit will be working out how to package up your application for the different platforms. I have only used Android which lets you self sign your applications making it not too hard, I suspect that publishing to iPhone will be harder as I think you’ll need to sign with a certificate you get from Apple (I’m guessing that’s what the £100 a year buys you).  Adobe runs a service that will do the packaging for you, but it only seems to support certain plugins. <a href="http://davidsherlock.co.uk/notes-publishing-phonegap-cordova-google-play-store/" title="Notes on publishing PhoneGap / Cordova app to Google Play store">I wrote some notes about the bits that tripped me up</a>.

<strong>Plugin support is amazing</strong>. You will need a plugin for anything that is using your mobile phones features. Core functionality is provided by the Cordova project, but there are lots of plugins on Github that extend functionality future, although you will have to be careful they are up to date and the developer wants to continue with them.
<strong>
You learn a lot about Android development, despite your app being written with web technologies.</strong> I’ve had to go in and fix a few plugins or configuration problems which have helped me to understand the Android way of thinking.

<strong>It took me a while to work out how I wanted my configuration</strong>. You are using web technologies this is tied to bits of Java. Even though you may not be interested in the Java, the compiler will be, so do you use a Java IDE with web support, or forget the Java and pray the command line Cordova tools just work? At first I used Cordova at the command line mixed with a eclipse with web tools. I then decided to use Eclipse with the android development kit integrated with Cordova.

Most of all, it is fun and you can throw things up quickly. I've enjoyed using Unity too, but that is for another post.

My app is very much just a test case, but I like the fact that Cordova supports the idea of just creating 'test cases'. The Android play store also  seems to support the philosophy of letting people play without hassle since it only takes a few hours from submission of something before it appears on the play. I’m not charging for my app or in app purchases and Google seem to be lighter on those kind of apps.

<a href="https://play.google.com/store/apps/details?id=com.paddytherabbit.triviaquizzes">If you are interested, the app currently lives here and is very much in beta.</a>