---
ID: 837
post_title: >
  Word counts of individual words in a CSV
  file
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/word-counts-individual-words-csv-file/
published: true
post_date: 2013-12-23 17:14:19
---
&nbsp;

I recently got a request from <a href="https://plus.google.com/115746512979556676267/">Ali Kourtiche</a>  asking how I would go about finding term frequency and the such from Facebook posts. Ali had a CSV file which he had created using an application called <a href="https://github.com/strohne/Facepager">Facepager</a>.

While Facepager looks interesting I haven’t played with it yet so I don't know what the data structure is like. So I will assume that Ali has a CSV and that he can get his data in to two columns, an id column and a column with the content of each post. I’ve got 31 posts from a blog that I have access to. In Excel it looks something like this:

[caption id="attachment_838" align="aligncenter" width="240"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/csv.png"><img class="size-medium wp-image-838" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/csv-240x300.png" alt="csv" width="240" height="300" /></a> Sort your data so it looks like this[/caption]

To  play with text and find things like term frequency I use tools called <a href="http://www.r-project.org/">R</a> and <a href="http://www.rstudio.com/">Rstudio</a>. I won't go through the installation but once you have them up and running open up Rstudio. We will also need an R package called tm. To install this look for the packages tab in Rstudio, click Install Packages and type “tm” in the dialog box that opens up and click install.

[caption id="attachment_839" align="aligncenter" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/install.png"><img class="size-medium wp-image-839" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/install-300x24.png" alt="install" width="300" height="24" /></a> The option to install packages in RStudio[/caption]

Now we are going to get the posts in to Rstudio and get the term frequency.

First create a new R script in Rstudio by clicking the little plus button in the top right corner and selecting “R Script”.  In the script that we’ve created we want to first enabled the tm library. To do this add the following line to the top of your script:
<blockquote>“library(tm)”</blockquote>
Now we want to import the CSV in to the environment. I saved mine on a Mac OS X desktop. To load it in to the environment we use the following line:
<blockquote><em>posts&lt;- read.csv("/Users/David/Desktop/posts.csv", header = TRUE)</em></blockquote>
This will read the CSV and put it in to a datastructure in R. The header = true should be set in my example because the first row contains the column names. To run both these commands that you have put in your script press the ‘source’ button. You should now have a dataframe that you can explore in R. Under the global environments tab you should see ‘posts’, clicking the little table next to it should show you your csv:

[caption id="attachment_840" align="aligncenter" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/rdataframe.png"><img class="size-medium wp-image-840" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/rdataframe-300x131.png" alt="rdataframe" width="300" height="131" /></a> Your CSV is now in R[/caption]

Before we do anything we want to create a corpus out of this dataframe, we can also prepare the text so that it is easier to analyse. When I prepare the text I useually make it all lower case and remove punctuation numbers and remove common words. To do this put the following code at the bottom of your current script. The tm package has a list of stopwords to remove, I’m using the English list, but you can change this as you wish:
<blockquote>corpus &lt;- Corpus(VectorSource(tw.df$text)) # create corpus object
corpus &lt;- tm_map(a, tolower) # convert all text to lower case
corpus &lt;- tm_map(a, removePunctuation)
corpus &lt;- tm_map(a, removeNumbers)
corpus &lt;- tm_map(a, removeWords, stopwords("english"))</blockquote>
There was a bug on Mac OS X to do with the number of cores my processor has, if you get this error then try this instead:
<blockquote>
<p style="text-align: left;">corpus &lt;- Corpus(VectorSource(posts$Post)) # create corpus object
corpus &lt;- tm_map(corpus, tolower, mc.cores=1) # convert all text to lower case
corpus &lt;- tm_map(corpus, mc.cores=1, removePunctuation)
corpus &lt;- tm_map(corpus, removeNumbers, mc.cores=1)
corpus &lt;- tm_map(corpus, removeWords, stopwords("english"), mc.cores=1)</p>
</blockquote>
Now we can find play with the data to find a few things that may be of interest.

1. We can create a term document matrix to find how often each term is found in each document using the following:
<blockquote>tdm &lt;- TermDocumentMatrix(corpus)</blockquote>
Or, if you want to weigh the DocumentTermMatrix
<blockquote>dtm &lt;- DocumentTermMatrix(crude, control = list(weighting = weightTfIdf))</blockquote>
2. Ali wanted a list of all the words and how much they were used. I created a dataframe from the matrix, added up the total times the words were used, then reordered the dataframe so that we could see the list:
<blockquote>count&lt;- as.data.frame(inspect(tdm))
count$word = rownames(count)
colnames(count) &lt;- c("count","word" )
count&lt;-count[order(count$count, decreasing=TRUE), ]</blockquote>
You can then press the little table next to count to see the word counts:

[caption id="attachment_842" align="aligncenter" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/wordcounts.png"><img class="size-medium wp-image-842" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/wordcounts-300x270.png" alt="wordcounts" width="300" height="270" /></a> easy![/caption]

There are lots you can do with a document term matrix/table of wordcounts and I’ll leave it for Ali to do some googling for ideas.

The finished R Script
<pre class="lang:default decode:true">library("tm")
library("SnowballC")
posts&lt;- read.csv("/Users/David/Desktop/posts.csv", header = TRUE,  fileEncoding="latin1")
corpus &lt;- Corpus(VectorSource(posts$Post)) # create corpus object
corpus &lt;- tm_map(corpus, tolower, mc.cores=1) # convert all text to lower case
corpus &lt;- tm_map(corpus, mc.cores=1, removePunctuation)
corpus &lt;- tm_map(corpus, removeNumbers, mc.cores=1)
corpus &lt;- tm_map(corpus, removeWords, stopwords("english"), mc.cores=1)

tdm &lt;- TermDocumentMatrix(corpus)
#tdm &lt;- TermDocumentMatrix(corpus, control = list(weighting = weightTfIdf))

mydata.df &lt;- as.data.frame(inspect(tdm))
count&lt;- as.data.frame(rowSums(mydata.df))
count$word = rownames(count)
colnames(count) &lt;- c("count","word" )
count&lt;-count[order(count$count, decreasing=TRUE), ]</pre>