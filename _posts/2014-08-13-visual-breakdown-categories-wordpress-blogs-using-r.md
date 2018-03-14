---
ID: 1739
post_title: 'Visual breakdown of categories on wordpress blogs using  R'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/visual-breakdown-categories-wordpress-blogs-using-r/
published: true
post_date: 2014-08-13 10:07:29
---
This is a very simple recipe, just a few lines to get an indication of tags/categories being used on a Wordpress site. The idea is that I use R to read the RSS feed of the blog, pick out the tags and categories and display a pie chart of the tags being used. Since tags and categories in wordpress are set by the user it gives you an indication of what subjects the authors think their posts fit in to. It might be a useful script in keyword planning and seo, but I just use it to see how my interests are changing.

<!--more-->

1.Pick RSS Feed

I used the RSS of my personal website, http://davidsherlock.co.uk/feed".- It is worth noting that by default Wordpress RSS displays the last 10. If I wanted more I could use yourwebsite.com/feed/?paged=2 to give me the next 10, I could write a loop to the categories for as many posts as I wanted, but I like the idea of being able to compare tags at different times of my blogging life.

2.Read RSS feed

We need  the XML package, so we need to import this packge, read the RSS feed and find all the tags. First we import the library package, parse the XML feed in to an R structure and search using xpath for categorys:
<pre class="lang:default decode:true">library("XML")
doc&lt;-xmlTreeParse("http://davidsherlock.co.uk/feed")
src&lt;-xpathApply(xmlRoot(doc), "//category")</pre>
3. Pull out tags and chart:

I then loop through all the categories, put them in a dataframe and create the pie chart
<pre class="lang:default decode:true ">for (i in 1:length(src)) {
  tags&lt;- rbind(tags,data.frame(tag=tag&lt;-xmlSApply(src[[i]], xmlValue)) )
}

pie(table(tags$tag))</pre>
There is quite possibly easier ways to do this, but it's only a few lines and works. Here is the produced  pie chart form this script:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/08/pie_chart_of_categories.png"><img src="http://davidsherlock.co.uk/wp-content/uploads/2014/08/pie_chart_of_categories.png" alt="pie_chart_of_categories" width="785" height="524" /></a>

Perhaps I'm getting fed up of my blog and want to be more like Perez Hilton, just change the feed to 'http://perezhilton.com/feed' and compare. Turns out I need more gifs.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/08/perez-hilton-topics.png"><img class="size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2014/08/perez-hilton-topics.png" alt="perez hilton topics" width="929" height="581" /></a>

<a title="Data Analysis" href="http://davidsherlock.co.uk/data-analytics/"><img class="wp-image-1745 size-full " src="http://davidsherlock.co.uk/wp-content/uploads/2014/08/data_analysis_paddytherabbit.png" alt="data_analysis_paddytherabbit" width="688" height="152" /></a>