---
ID: 2735
post_title: 'Unity: Taking the correct resolution screenshots for Appstore connect'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/unity-taking-the-correct-resolution-screenshots-for-appstore-connect/
published: true
post_date: 2020-05-12 08:30:39
---
<!-- wp:paragraph -->
<p>Taking the correct size of app image for Apples App Store Connect is a pain when using Unity. There are some pretty good tools for creating simulation iPhones and iPads in OS X, but Unity requires you to build the project with slightly different settings – and due to a bug in Unity it does not always work.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I resort to taking pictures within Unity itself, at first I used an asset to take the pictures for me, the issue was the asset seemed to take multiple screenshots of the correct size for the app store. The problem I had was that the assets only seemed to use the camera objects to take pictures, and I have lots of overlays.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>To be able to take the pictures during playtesting is easy. Just create a script with an if statement on an otherwise empty game object, check if a button is pressed, then take a screenshot and save to the desktop.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The way to get the correct sizes is just to change the resolution in the game object tab as you play. Unity comes with some presents to do this for you.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Here is a gist of the code:</p>
<!-- /wp:paragraph -->

<!-- wp:ghostkit/gist {"url":"https://gist.github.com/ds10/0d5c09cbe452ace89ec635e54161bdab"} -->
<div class="ghostkit-gist" data-url="https://gist.github.com/ds10/0d5c09cbe452ace89ec635e54161bdab" data-file="" data-caption="" data-show-footer="true" data-show-line-numbers="true"></div>
<!-- /wp:ghostkit/gist -->

<!-- wp:paragraph -->
<p>and a video:</p>
<!-- /wp:paragraph -->

<!-- wp:core-embed/youtube {"url":"https://www.youtube.com/watch?v=u6p9k8g81WM\u0026feature=youtu.be","type":"video","providerNameSlug":"youtube","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
https://www.youtube.com/watch?v=u6p9k8g81WM&amp;feature=youtu.be
</div></figure>
<!-- /wp:core-embed/youtube -->