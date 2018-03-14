---
ID: 64
post_title: >
  Starting to Text Mine with R. Lets find
  out what’s happening in Coronation
  Street.. Stage 1
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/starting-to-text-mine-with-r-lets-find-out-whats-happening-in-coronation-street-stage-1/
published: true
post_date: 2013-06-12 09:11:42
---
There is a great text mining package in R called ‘tm’. This is a short introduction to tm and how it can be used to create what is called a Document-Term Matrix, which is a matrix showing the frequency of terms over a collection of documents. While this is quite basic it’s hopefully going to be the base of some future work into classification of documents. A video is on its way, but here are my text notes for now:

<strong>Tools</strong>
The Documents:

I had 15 documents, each document is a description of an episode of popular soap coronation street taken from the spoilers website dailyspy. That’s 3 weeks worth of story lines!

R studio:
I use R studio because it makes things nice and easy, but this isn’t a must.

<strong>Process</strong>

First I set my workspace in Rstudio via workspace-&gt;setworkspace and placed a directory CS in there. CS contains all the documents of Coronation Street spoilers. I started a new R script where I imported the tm library, imported the documents and checked the length of the corpus.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.47.16.png"><img class="alignnone size-full wp-image-65" alt="Screen Shot 2013-06-11 at 13.47.16" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.47.16.png" width="770" height="125" /></a>

I used the tm_map function to check for stop words, strip whitespace, remove punctuation/numbers and set as lowercase.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.48.50.png"><img class="alignnone size-full wp-image-68" alt="Screen Shot 2013-06-11 at 13.48.50" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.48.50.png" width="767" height="108" /></a>

From there it is quite easy to turn this into a document-term matrix with the DocumentTermMatrix method:<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.54.07.png"><img class="alignnone size-full wp-image-66" alt="Screen Shot 2013-06-11 at 13.54.07" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.54.07.png" width="757" height="54" /></a>

I used some functions to inspect the DTM, but they aren’t vital but you might want to check out: colnames(), inspect(), and findFreqTerms(). Finally I wanted to just do something with the document-term matrix, so I went with the classic wordcloud. I installed the wordcloud package and, found the word_frequency and generated the wordl as such:

<img class="alignnone size-full wp-image-67" alt="Screen Shot 2013-06-11 at 13.58.21" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.58.21.png" width="793" height="98" />

&nbsp;

The wordl in this case is made up mainly of the characters who have running story lines.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.58.29.png"><img class="alignnone size-full wp-image-72" alt="Screen Shot 2013-06-11 at 13.58.29" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-11-at-13.58.29.png" width="373" height="347" /></a>

&nbsp;

It was also possible to see how far apart words are to give us an idea of related words. I did this

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-12-at-10.04.17.png"><img class="alignnone size-full wp-image-73" alt="Screen Shot 2013-06-12 at 10.04.17" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-12-at-10.04.17.png" width="518" height="147" /></a>

&nbsp;

&nbsp;

Which gave me a cluster dendrogram, unfortunately at this stage it doesn't make much sense! The next steps would be to feed the script more data. With more coronation street spoilers the names might not be as prominent.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-12-at-10.04.09.png"><img class="alignnone size-full wp-image-74" alt="Screen Shot 2013-06-12 at 10.04.09" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-12-at-10.04.09.png" width="402" height="400" /></a>

&nbsp;

<strong>Next steps</strong>

1) Feed it more data!

2) Compare storylines to Eastenders

3) Try classification techniques

<strong>The full script</strong>

[codesyntax lang="text"]

library("tm")
corpus &lt;-Corpus(DirSource("cs"))

corpus.p &lt;-tm_map(corpus, removeWords, stopwords("english")) #removes stopwords
corpus.p &lt;-tm_map(corpus.p, stripWhitespace) #removes stopwords
corpus.p &lt;-tm_map(corpus.p, tolower)
corpus.p &lt;-tm_map(corpus.p, removeNumbers)
corpus.p &lt;-tm_map(corpus.p, removePunctuation)

dtm &lt;-DocumentTermMatrix(corpus.p)
findFreqTerms(dtm,4)
library("wordcloud")
word_frequency &lt;- colSums(as.array(dtm))
wordcloud(names(word_frequency), word_frequency, scale=c(3,.5),
max.words = 75, random.order=FALSE, colors=c("lightgray", "darkgreen", "darkblue"), rot.per=.3)

[/codesyntax]