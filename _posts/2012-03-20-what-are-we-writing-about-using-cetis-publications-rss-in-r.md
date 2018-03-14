---
ID: 292
post_title: >
  What are we writing about? Using CETIS
  Publications RSS in R
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/what-are-we-writing-about-using-cetis-publications-rss-in-r/
published: true
post_date: 2012-03-20 12:56:03
---
I have been poking around Adam Coopers <a href="https://github.com/arc12/Text-Mining-Weak-Signals" target="_blank">text mining weak signals in R code</a>, and being too lazy to collect data in CSV format wondered if I could come up with something similar that used RSS feeds. I discovered it was really easy to read and start to mine RSS feeds in R, but there didn't seem to be much help available on the web so I thought I'd share my findings.

My test case was the new CETIS publications site, <a href="http://blogs.cetis.ac.uk/philb/2012/03/13/cetis-publications-now-on-wordpress/">Phil has blogged </a>about how the underlying technology behind site is wordpress, which means it has an <a href="http://publications.cetis.ac.uk/feed">easy to find feed</a>. I wrote a very small script to test things out that looks something like this:
<pre>
<code>

      library("XML")
      library("tm")
      doc&lt;-xmlTreeParse(&quot;http://publications.cetis.ac.uk/feed&quot;) 
      src&lt;-xpathApply(xmlRoot(doc), &quot;//category&quot;)
      tags&lt;- NULL

      for (i in 1:length(src)) {
             tags&lt;- rbind(tags,data.frame(tag=tag&lt;-xmlSApply(src[[i]], xmlValue)) )  
      }

</code>
</pre>

This simply grabs the feed and puts all the categories tags into a dataframe. I then removed the tags that referred to the type of publication and plotted it as a piechart. I'm pretty sure this isn't the prettiest way to do this, but it was very quick and worked!
<pre>
<code>

         cats &lt;- subset(tags, tag != &quot;Briefing Paper&quot; &amp; tag != &quot;White Paper&quot; &amp; tag != &quot;Other Publication&quot; &amp; tag != &quot;Journal Paper&quot;  &amp; tag != &quot;Report&quot;)
         levels(cats$tag)
         df$tag = factor(df$tag)
         pie(table(cats$tag))

</code>
</pre>


Which gave me a visual breakdown of all the categories used on our publications site and how  much they are used:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2012/03/types.png"><img class="aligncenter size-full wp-image-293" title="types" src="http://davidsherlock.co.uk/wp-content/uploads/2012/03/types.png" alt="types" width="625" height="310" /></a>I was surprised at how much of a 5 minute job it was. It struck me that because the feed has the publication date it would be easy to do the Google Hans Rosling style chart with it. My next step would be to grab multiple feeds and use some of Adams techniques on the descriptions/content of the feed.
<h2>*UPDATE*</h2>
I had been interested in how to grab RSS and pump it into R and 'interesting things we can do with the CETIS publications RSS feed' had been a bit of an after thought. Martin brought up the idea of using the feed to drive a wordl (see comments). I stole the code from the comment and changed my code slightly so that I was grabbing the publication descriptions rather than the tags used... This is what it came up with.. Click to enlarge

<a href="http://davidsherlock.co.uk/wp-content/uploads/2012/03/wordl.png"><img class="aligncenter size-medium wp-image-307" title="wordl" src="http://davidsherlock.co.uk/wp-content/uploads/2012/03/wordl-300x283.png" alt="wordl" width="300" height="283" /></a>