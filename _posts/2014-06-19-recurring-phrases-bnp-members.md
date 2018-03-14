---
ID: 1460
post_title: The recurring phrases of BNP members.
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/recurring-phrases-bnp-members/
published: true
post_date: 2014-06-19 16:29:56
---
I wanted to find out what people were saying on the facebook pages of extreme political parties. At this stage I wasn't bothered so much about what the party was saying, but what the comments on the posts where saying. The task was to find n-grams in a CSV file and  I decided to do it in R. Originally the CSV was created from comments on 10 pages of BNP Facebook posts, I generated the CSV quite quickly using an application called FacePager, <a title="Using Facepager to find comments on Facebook page posts" href="http://davidsherlock.co.uk/using-facepager-find-comments-facebook-page-posts/">it was very easy to do and if you are interested you can find instructions on this post here</a>.

The final script is here and is quite easy to follow:
<pre class="lang:default decode:true">options(mc.cores=1)

#import packages

install.packages("tm")
install.packages("RWeka")
install.package("slam")

library(tm)
library("RWeka")
library("slam")

#import csv
mydata = read.csv("bnpwcomments.csv", sep = ";")  # read csv file

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
BigramTokenizer &lt;- function(x) NGramTokenizer(x, Weka_control(min = 4, max = 4))
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
To change the number of words in the sequence you want to look for this line and change the number to whatever you want:
<pre class="lang:default decode:true">BigramTokenizer &lt;- function(x) NGramTokenizer(x, Weka_control(min = 4, max = 4))</pre>
I haven't finished playing with the data yet, but if you are interested I have dug the most popular phrases out, it is quite obvious that 'at the end of the day' to the BNP it's a case of us Vs them.
<h3>3 Word phases</h3>
Count Phrase

156    in this country
130    all the way
103    a lot of
99    bnp all the
89    to do with
87    got my vote
85    in our country
80    in the uk
78    dont like it
78    if you dont
75    the bnp are
75    the rest of
75    the right to
73    we need to
72    the british people
<h3>4 word  phrases:</h3>
Count Phrase

49    in our own country
47    nothing to do with
43    if they dont like
39    if you dont like
35    the rest of the
34    the end of the
32    have the right to
30    if you want to
30    in the first place
30    they don't like it
29    at the end of
29    end of the day
28    in the name of
28    this is our country
26    our way of life
26    send them all back
<h3>5 word  phrases:</h3>
Count Phrase

26    at the end of the
26    if they dont like it
26    the end of the day
16    has nothing to do with
14    if you dont like it
12    for the sole purpose of
12    sole purpose of child exploitation
12    the sole purpose of child
11    bring back the death penalty
<h3>6 word phrases</h3>
Count Phrase

25    at the end of the day
12    for the sole purpose of child
12    the sole purpose of child exploitation
8    any plans for you to review
5    for you to review cannabis laws