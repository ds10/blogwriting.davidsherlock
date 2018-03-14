---
ID: 1692
post_title: Ric Flair Promotion Jumps
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/ric-flair-promotion-jumps/
published: true
post_date: 2014-08-07 16:49:52
---
I posted an experiment on a wrestling subreddit a few days <a title="Exploring Wrestling Stables" href="http://davidsherlock.co.uk/exploring-wrestling-stables/">where I used DBpedia to explore the links between wrestling stables/</a> .To my surprise wrestling fans are really interested in the things you can find out using structured data from wikipedia. I was contacted by a graphic  designer asking if I wanted to collaborate on doing some wrestling visualisations together. I thought it would be a great idea and we have both gone away to think about visualisation ideas. Mining the following data was not my idea, but the idea of a fan on reddit, these are some experiments that I have made getting that data ready for a visualisation for this. I've found this a really interesting project to work on because pro wrestling databases seem to be very tightly guarded!

The idea was to grab the different promotions that wrestlers had worked for and visualise them. I couldn't find a decent data set with this in, but have found a site that lists all a wrestlers matches over multiple pages. Here is an example for <a href="http://www.cagematch.net/?id=2&amp;nr=1091&amp;page=4&amp;s=">Ric Flair.</a> I decided that the way I would decide which promotion a wrestler worked for was by using the last date a wrestler worked for a promotion on TV. That means if Ric wrestled for the WWE on 1st August and then was next seen on TV for WCW on 1st of September, I would create a visualisation where Ric worked for WWE throughout August. I've gone for this because I think I can work with the data that way and because I think it fits in with the reasons why the community would like this to be visualised. I'll have to ask the fans later if this is correct or not!

First I scrapped all the results in to R using the following:
<pre class="lang:default decode:true ">library(XML)
theurl &lt;- "http://www.cagematch.net/?id=2&amp;nr=1091&amp;page=4&amp;s=0"
data_frame_of_table &lt;- readHTMLTable(theurl,which=6,as.data.frame = TRUE)

x=100
while( x &lt; 2600 ){

  theurl &lt;- paste("http://www.cagematch.net/?id=2&amp;nr=1091&amp;page=4&amp;s=",x, sep="")
  x&lt;-x+ 100
  toadd &lt;- readHTMLTable(theurl,which=6,as.data.frame = TRUE)
  data_frame_of_table&lt;-rbind(data_frame_of_table,toadd)

}</pre>
Not pretty, but it works.

I then realised the promotion field was blank! This was because the webpage uses images for this field. I noticed that promotion names were in the match Title and created my own using grep on likes something like this:
<pre class="lang:default decode:true">data_frame_of_table$Match &lt;- as.character(data_frame_of_table$Match)
data_frame_of_table[grep('TNA|tna|IMPACT', data_frame_of_table$Match), "pro"] &lt;- "TNA"</pre>
I wrote this to csv:
<pre class="lang:default decode:true ">write.csv(data_frame_of_table,"matches.csv")</pre>
I then deleted what I didn't want by hand and bunged the result in Google charts. <a href="http://davidsherlock.co.uk/lab/wrestler/ric.html">You can see the interactive version here.</a>

There are a few things I'm not happy about. I did a little in hand in CSV which makes it prone to my lazy mistakes. I'm also not sure that TV events were the best way to do things. I'm also missing my labels and the such, its a start.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/08/Ric-Flair-jumps.png"><img class="aligncenter size-full wp-image-1695" src="http://davidsherlock.co.uk/wp-content/uploads/2014/08/Ric-Flair-jumps.png" alt="Ric Flair jumps" width="934" height="287" /></a>

&nbsp;