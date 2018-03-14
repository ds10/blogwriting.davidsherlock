---
ID: 2437
post_title: Facebook for Unity 7 Login problems
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/facebook-for-unity-7-login-problems/
published: true
post_date: 2015-08-06 10:04:44
---
Facebook for Unity 7.0.2 is still in beta and isn't officially for public consumption yet, however, Facebook for Unity 6.x.x doesn't support Unity 5 meaning that many developers have been forced to take the jump early. I've noticed quite a few people playing with the latest Facebook for Unity are having trouble logging in. The error message that you will be getting when using existing code with 7.x.x will be something like: 'FB' does not contain a definition for 'Login'. This isn't a problem with version 7, the login procedure has just changed slightly with the latest update to be more consistent with Facebook best practices for developers logging in. Straight from the <a href="https://developers.facebook.com/docs/unity/reference/beta/webgl#dialogs">Facebook </a>docs:

<code>FB.Login</code> has been replaced and split into <code>FB.LoginWithReadPermissions</code> and <code>FB.LoginWithPublishPermissions</code>.

Although the docs seem to be slightly wrong as it appears to be LogInWithReadPermission (LogIn as opposed to Login). Quick fix: you will be wanting to change your FB.Login to FM.LogInWithReadPermissions or LogInWithPublishPermissions, depending on what you want to do. I can't see much other change other than forcing best practices on us.