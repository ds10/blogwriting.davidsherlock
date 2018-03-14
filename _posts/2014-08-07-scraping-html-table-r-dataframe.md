---
ID: 1689
post_title: >
  Scraping a HTML table into an R
  dataframe
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/scraping-html-table-r-dataframe/
published: true
post_date: 2014-08-07 11:15:13
---
For some work I plan on doing for the LACE tech focus blog I wanted to get some information off a webpage and in to an R dataframe. It turns out this is a three line solution (1 line if you throw your URL straight to the function paramaters and have the XML package already installed).
<pre class="lang:default decode:true  ">library(XML)
theurl &lt;- "&lt;URL STRING&gt;"
data_frame_of_table &lt;- readHTMLTable(theurl,which=&lt;table number&gt;,as.data.frame = TRUE</pre>
I'm pretty sure this is something I will need later in life.. thought I better blog it somewhere..