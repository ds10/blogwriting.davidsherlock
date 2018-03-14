---
ID: 2442
post_title: >
  Storing comments from a Facebook post
  for analysis
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/storing-facebook-comments-from-post-for-analysis/
published: true
post_date: 2015-09-11 14:43:22
---
I've had a lot of feedback from my post detailing how to use <a href="http://davidsherlock.co.uk/using-facepager-find-comments-facebook-page-posts/">Facepager to explore comments on facebook pages</a>. While Facepager is a neat little tool I get a lot of feedback saying that users have difficulty setting it up. Since the Github repository of the tool itself doesn't seem to have been updated in a while, I'm not sure how much time is worth investing in getting it to work for the long term usage. Many of the requests I get are simply asking for advice on how to download comments from one post. It is actually very simple to do using the Facebook Graph API explorer and there isn't much need for Facepager to do it.

Here is my recipe:
<h2>Facebook Graph API Explorer</h2>
The first thing to do is head over to the <a href="https://developers.facebook.com/tools/explorer/145634995501895/">Facebook API Graph explorer</a>, you will need to sign in to Facebook so it can create an access token for you to make queries. One this page you will see a box where we will build our requests that looks something like this:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/09/facebook_query.png"><img class="alignnone wp-image-2443 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2015/09/facebook_query.png" alt="facebook_query" width="696" height="34" /></a>

In this box we will construct out request, we are after comments on an object and the <a href="https://developers.facebook.com/docs/graph-api/reference/v2.4/object/comments">Facebook Graph documentation</a> explains the request we need is:

<strong>/{object-id}/comments</strong>

so, to build the request we need the object id. Building this is a two part process, you need the id of the page, followed by an underscore and the id of actual post. The page id can be found by viewing the source, or even easier by copying the page URL and pasting it in to this <a href="http://findmyfbid.com/">id finding service</a>. To find the post ID you need to navigate to the post and click the date. The id will then be displayed in the URL. I am using a post by XFM's facebook page, the page ID is 208559300603and my post id is: 10156099354675604, so my object-id is : 208559300603_10156099354675604,  on the Graph page I replace the me?fields=id,name with /208559300603_10156099354675604/comments and press submit. You'll see the comments appear in JSON in the box on the right like so.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/09/facebook_explorer_edge.png"><img class="alignnone wp-image-2444 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2015/09/facebook_explorer_edge.png" alt="facebook_explorer_edge" width="928" height="680" /></a>
<h2>Turn Facebook Explorer API output to CSV</h2>
JSON is no good for most the people who message me, however there is an easy way to manipulate the data and I use open-refine to do so.  Copy the JSON in to a text file, save it somewhere on your desktop and download the latest version of <a href="http://openrefine.org/">open refine</a>.

Once you've started Open Refine you will be asked to open a file to start a project and you will want to navigate to your saved JSON file, once it has imported you will be asked to pick a node, just pick the first entry like so:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/09/open_refine_nodes.png"><img class="alignnone wp-image-2445 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2015/09/open_refine_nodes.png" alt="open_refine_nodes" width="925" height="346" /></a>

In the resulting project you will want to click export-&gt;comma separated file in the menu.

Still stuck? How-to video:

https://youtu.be/onUmCtiVmuc

&nbsp;