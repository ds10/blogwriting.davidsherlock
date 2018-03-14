---
ID: 1454
post_title: >
  Using Facepager to find comments on
  Facebook page posts
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/using-facepager-find-comments-facebook-page-posts/
published: true
post_date: 2014-06-17 12:57:57
---
<em>If you want to grab comments from one post, the <a href="http://If you want to grab comments from one post, the Graph API Explorer might be easier.">Graph API Explorer</a> might be easier.</em>

I've been trying to find ways to poke the Facebook graph that will be easy for people who find working with the API directly difficult and currently I am using a tool called Facepager to extract data. After a few minutes working with the program it seems easy enough to get it to poke the Facebook Graph for the comments and then store them in a SQLite database. I'll be looking to work with the results in R... but one thing at a time!

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/06/facepager1.png"><img class="alignnone wp-image-1456 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2014/06/facepager1-300x225.png" alt="" width="300" height="225" /></a>

1) After downloading and extracting Facepager for your system you should see a screen like the one in the image. Click the new database button and give it a filename. This will be your SQLite database, I'll be using this in R in other posts, but for now you can just reload it it in Facepager to do stuff.

2)Then you want to click add node. The node name is the name of the Facebook page you want to explore. For example if you want to get all the comments from posts on the Minecraft page at: https://www.facebook.com/minecraft then the node name is minecraft.

3)Select what you are after in the 'Resources' Tab, I went with &lt;page&gt;/posts.

4)You need an access token to get any data out of Facebook, press the login to Facebook button and log in.

5)Press fetch data.

Easy, now you have all the results viewable in Facepager, each post only shows the first 25 comments though and I want them all. To find them all I just clicked each individual node and changed the resource to post/comments. A video on how I did it:

http://youtu.be/S9kYApoR8U4
<h2> Code</h2>
I have been asked in the comments to share my R code. I'm not sure I still have the script in the state it was in during the video, but I did find my finished thing. This script takes all the comments I have scraped from Facebook (from political party pages) and then it finds repeated phrases. If you would like to see what I did with it then <a href="http://davidsherlock.co.uk/more-reoccurring-phrases-in-the-facebook-comments-section-of-political-parties/">you can read this post about it here</a>. Hope it helps.
<pre class="lang:default decode:true ">options(mc.cores=1)

#import packages

install.packages("tm")
install.packages("RWeka")
install.package("slam")

library(tm)
library("RWeka")
library("slam")

#import csv
mydata = read.csv("5partycomments", sep = ";")  # read csv file 

#prepare text
corpus &lt;- Corpus(VectorSource(mydata$message)) # create corpus object

corpus &lt;- tm_map(corpus, mc.cores=1, removePunctuation)
corpus &lt;- tm_map(corpus, removeNumbers, mc.cores=1)
corpus &lt;- tm_map(corpus, removeWords, stopwords("english"), mc.cores=1)

# convert all text to lower case
corpus &lt;- tm_map(corpus, tolower, mc.cores=1)

#proplem with to lower means we need to make it type of plain text document again
corpus &lt;- tm_map(corpus, PlainTextDocument)

#make the term document matrix
tdm &lt;- TermDocumentMatrix(corpus)

#find the frequent terms
findFreqTerms(tdm, lowfreq = 500)

#tokenizer for tdm with ngrams
BigramTokenizer &lt;- function(x) NGramTokenizer(x, Weka_control(min = 6, max = 6))
tdm &lt;- TermDocumentMatrix(corpus, control = list(tokenize = BigramTokenizer))
findFreqTerms(tdm, lowfreq = 15)

#create dataframe and order by most used
rollup &lt;- rollup(tdm, 2, na.rm=TRUE, FUN = sum)
mydata.df &lt;- as.data.frame(inspect(rollup))
colnames(mydata.df) &lt;- c("count")
mydata.df$ngram &lt;- rownames(mydata.df) 
newdata &lt;- mydata.df[order(-count),] 
newdata&lt;-newdata[order(newdata$count, decreasing=TRUE), ]
</pre>
&nbsp;