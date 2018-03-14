---
ID: 1600
post_title: Example of Facebook Friends Analysis
author: David
post_excerpt: ""
layout: page
permalink: >
  https://davidsherlock.co.uk/example-facebook-friends-analysis/
published: true
post_date: 2014-07-30 08:30:17
---
<em><strong>I often do social network analysis of Facebook data for people or communities, this page acts as an example to send people and place to have discussions around some of the work I do.</strong></em>

To do the analysis I use a GDF file containing the relationships of your friends, <a href="http://changelog.ca/log/2013/03/09/gdf">there is a good explanation of what a GDF file is here</a>. A quick and easy way to create a GDF file is to use the Netvizz Facebook app, instructions and a video explaining how to generate a GDF file can <a title="Grabbing a GDF from Facebook data" href="http://davidsherlock.co.uk/grabbing-facebook-graph-data/">be found at this post. </a> I find that around 150 friends is a good number to analyse, although we can go much bigger.
<h2>Community Detection Example</h2>
To detect communities of friends in your Facebook feed I use the <a href="https://sites.google.com/site/findcommunities/">Louvain method</a> as implemented by <a href="https://www.linkedin.com/pub/patrick-mcsweeney/19/504/650">Patrick McSweeney</a> for Gephi during the Google summer of code. The method decomposes your friend community in to smaller sub communities. Figure 1.0 shows a network graph of my Facebook friends after running the algorithm. Each little dot on the graph represents a person and each line indicates that the these people are friends of each other. The algorithm has grouped the people in to communities and I have colour coded the graph depending on the community the person is in.

[caption id="attachment_1620" align="aligncenter" width="714"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/07/community-detection-using-louvain-methid-.png"><img class="size-full wp-image-1620" src="http://davidsherlock.co.uk/wp-content/uploads/2014/07/community-detection-using-louvain-methid-.png" alt="Figure 1: Community Detection using Gephi's implementation of the Louvain method" width="714" height="786" /></a> Figure 1: Community Detection using Gephi's implementation of the Louvain method[/caption]

In my example there appear to be four distinct communities with a number of smaller communities that seem to link the larger communities together. I can have a closer look at which of my friends belong to which groups and I can tell that the four major groups are: high school friends, family, friends from my current employment and friends from a previous employment. The small group in the middle that links them together is mostly made up of friends from primary school, my local area or college. We can explore these people further by examining there names and sex. The names of my friends have been added to the graph in Figure 2 and it has now been colour coded for sex, pink for girl, blue for boy and green for people who do not have their sex filled in on facebook. It is interesting that there is an area in the middle that is all boys, this is because my college and university degrees were in computer scientist related disciplines that were very male dominated!

[caption id="attachment_1621" align="aligncenter" width="742"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/07/girls-and-boys-in-my-facebook-page.png"><img class="size-full wp-image-1621" src="http://davidsherlock.co.uk/wp-content/uploads/2014/07/girls-and-boys-in-my-facebook-page.png" alt="Figure 2.0: Girls and boys in my facebook group, with names" width="742" height="775" /></a> Figure 2: Girls and boys in my facebook group, with names[/caption]

&nbsp;

It is interesting to find out who is influential, perhaps find the influental between different communities and friends. To do this I find the <a href="http://en.wikipedia.org/wiki/Betweenness_centrality">Betweeness Centrality</a> measures of all the people in the network. Betweeness Centrality is a measure of the number of shortest paths between any two friends that pass through another friend. People with high Betweeness Centrality find themselves at the center of many relationship groups.  Figure 3 shows the nodes weighted so the names of the biggest gate keepers are shown:

[caption id="attachment_1622" align="aligncenter" width="796"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/07/betweeness-centrallity-measures.png"><img class="size-full wp-image-1622" src="http://davidsherlock.co.uk/wp-content/uploads/2014/07/betweeness-centrallity-measures.png" alt="Figure 3: Betweeness Centrality Measures" width="796" height="866" /></a> Figure 3: Betweeness Centrality Measures[/caption]

&nbsp;

An example video of exploring Facebook friends:

http://youtu.be/OgaoS7sUGZI

&nbsp;

&nbsp;