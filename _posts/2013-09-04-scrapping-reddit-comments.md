---
ID: 276
post_title: Scrapping Reddit comments
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/scrapping-reddit-comments/
published: true
post_date: 2013-09-04 15:11:28
---
Something I had been meaning to do for a long time was write a quick script to scrape Reddit comments. A chap has beaten me to it and you can find the code here: https://github.com/ctaggart878/redditscraper.

During lunch today I had a little play with it the script (and I mean quick!). A two line script imported the function and ran it over the comments in ukpolitics for this week. The two lines:
<blockquote>source("RedditScraper.R")
redditScrape('ukpolitics','week' )</blockquote>
Here is the magical wordcloud it created:

[caption id="attachment_277" align="aligncenter" width="292"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/09/Screen-Shot-2013-09-04-at-16.04.13.png"><img class="size-medium wp-image-277 " alt="Screen Shot 2013-09-04 at 16.04.13" src="http://davidsherlock.co.uk/wp-content/uploads/2013/09/Screen-Shot-2013-09-04-at-16.04.13-292x300.png" width="292" height="300" /></a> Reddit comments in ukpolitics Aug 28th - Sep 4th[/caption]

And the top words for the week are Weapons, Many, Should, Cameron, Going. I guess you can tell what's been on peoples minds. My next steps are to have a closer look at the function, see what it does and see if I can bend it to do some of the things I am doing. I wonder if I can do something with Topic Models to explore what each subreddit is <em>really</em> about. Anyway best get back to real work.

Big thanks to <a href="http://www.reddit.com/user/Snotaphilious">/user/Snotaphilious</a>