---
ID: 1207
post_title: 'NOTES: Higher Education and Twitter. 10th -17th March'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/notes-higher-education-twitter-week-beginning-10th-march/
published: true
post_date: 2014-03-19 16:55:09
---
Recently I have been playing with the Twitter API, to get my head around how it works and what is/isn’t possible. Just to get my head going I have been looking at the ways in which UK Universities pimp themselves on Twitter. I haven’t really thought through my dataset or the kind of questions I want to ask it since I’m simply just trying out the API, but after playing I have ended up with a bunch of notes which I am dumping here because this will be the place I look in 3 months when my hard drive has died. The notes are basically just the commands I typed and the order I typed them, but I think they are straight forward enough to follow with little explanation, the process is very easy. So with that in mind here are some caveats to anybody looking for answers from a Google search:
<ul>
	<li>I haven’t thought about the best way to display data and have been playing with tools like ggplot, I know this is messy, this was a learning process for me.</li>
	<li>The notes on how I’ve gone about using SQL queries/R/Javascript were taken just to jog my memory. I’m sorry if they are not helpful. I will try and tidy this up at some point.</li>
	<li>Data is correct as far as I know, I think I’ve fixed the holes, but I haven’t gone through it with a really fine comb.</li>
	<li>I have used 163 Institutions from this list as a starting point. I needed to update some of the accounts. 160 Seemed to have twitter accounts. I had to update lots of the accounts.</li>
	<li>Institutions have different approaches to Twitter usage, Bolton has its accounts spread over the library, helpdesk etc etc and I have only captured the main account. This makes it hard to compare one University to another.</li>
	<li>Data is tweets from 10-17<sup>th</sup> March</li>
	<li>I seem to have lost the number of favourites and retweets somewhere along the line and will need to revist my scrapper</li>
</ul>
These notes are for my own use, the actual thing I’m working on doesn’t even use higher ed  tweets, still I’d welcome any friendly comments if any of this seems useful.

Here be dragons:

<strong>Check if anybody is missing</strong>
<pre>SELECT * FROM University
WHERE University.twitter_username NOT IN
(
SELECT twitter_id
FROM amt_tweets
)</pre>
The following didn’t have Twitter accounts that I was aware of:

Bishop Grosseteste University College Lincoln
Courtauld Institute of Art
Norwich University College of the Arts
Stranmillis University College

Newcastle Uni has turned in to subaccounts, I’m not following any of them.

The University of Wales and University for the Creative Arts didn’t tweet that week.

<strong>Delete anything that doesn’t belong in the week:</strong>
<pre>delete from amt_tweets where created_at &lt; "2014-03-10 00:00:01" delete from amt_tweets where created_at &gt; "2014-03-17 23:59:59"</pre>
<strong>Give me something to join</strong>
<pre>UPDATE University
SET twitter_username = SUBSTRING(twitter,20)</pre>
<strong> Check my join to Uni stats has the same number of rows as select *</strong>
<pre>SELECT *
FROM amt_tweets
LEFT JOIN University
ON amt_tweets.twitter_id=University.twitter_username;</pre>
<strong> Find Tweets per Institution in that week:
</strong>
<pre>SELECT University.Institution, count(*)
FROM amt_tweets
LEFT JOIN University
ON amt_tweets.twitter_id=University.twitter_username
GROUP BY University.Institution</pre>
<strong>Institutions with most Tweets</strong>
<table>
<tbody>
<tr>
<td>Institution</td>
<td>Tweets</td>
</tr>
<tr>
<td>The University of Essex</td>
<td>229</td>
</tr>
<tr>
<td>Coventry University</td>
<td>203</td>
</tr>
<tr>
<td>Plymouth University</td>
<td>186</td>
</tr>
<tr>
<td>Aston University</td>
<td>182</td>
</tr>
<tr>
<td>The University of Keele</td>
<td>174</td>
</tr>
</tbody>
</table>
<strong>Bottom 5 (not including the ones who didn’t tweet at all):</strong>
<table>
<tbody>
<tr>
<td>Institution</td>
<td>Tweets</td>
</tr>
<tr>
<td>The School of Pharmacy</td>
<td>2</td>
</tr>
<tr>
<td>Heriot-Watt University</td>
<td>2</td>
</tr>
<tr>
<td>The University of Oxford</td>
<td>5</td>
</tr>
<tr>
<td>York St John University</td>
<td>5</td>
</tr>
<tr>
<td>University of the Arts, Londony</td>
<td>6</td>
</tr>
</tbody>
</table>
<strong>Bored of SQL, Suck in to R</strong>
<pre>library(RMySQL)
library(tm)

#will need ln -s /Applications/MAMP/tmp/mysql.sock /tmp/mysql.sock
mydb = dbConnect(MySQL(), user='xxx', password='xxx', dbname='twitter_db', host='localhost')
query&lt;-paste('SELECT *
FROM amt_tweets
LEFT JOIN University
ON amt_tweets.twitter_id=University.twitter_username')
data.frame = dbGetQuery(mydb,query)
dbDisconnect(mydb)</pre>
Crate a dataframe of Institutions, when they tweeted and graph it. Realise the mistake as you press the plot button
<pre>data.frame$date &lt;- as.Date(as.POSIXct(data.frame$created_at, origin="1970-01-01"))
added_df&lt;-ddply(data.frame, .(date, Institution), summarize, freq=length(date))
ggplot(added_df, aes(x=date, y=freq, col=Institution)) + geom_line()</pre>
<strong>Try again with Russel Group Members (are we missing 3?)</strong>
<pre>mydb = dbConnect(MySQL(), user='xxx', password='xxx', dbname='twitter_db', host='localhost')
query&lt;-paste('SELECT *
FROM amt_tweets
LEFT JOIN University
ON amt_tweets.twitter_id=University.twitter_username
WHERE University.Group = "Russell" ')
data.frame = dbGetQuery(mydb,query)
dbDisconnect(mydb)
data.frame$date &lt;- as.Date(as.POSIXct(data.frame$created_at, origin="1970-01-01"))
added_df&lt;-ddply(data.frame, .(date, Institution), summarize, freq=length(date))
ggplot(added_df, aes(x=date, y=freq, col=Institution)) + geom_line()</pre>
Output:

The idea of this was to have a timeline of a group of Universities and plot when they were Tweeting over time compared to the others in the same group. Here I have used the Russel group. You can't really tell anything apart from very few Russel group Universities Tweet on the weekend, which is when the Quidditch matches take place.

[caption id="attachment_1221" align="aligncenter" width="1417"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/russelgrouptweets.png"><img class="size-full wp-image-1221" alt="russelgrouptweets" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/russelgrouptweets.png" width="1417" height="720" /></a> Number of tweets from Russel Group Twitter accounts week starting 10th March. Hard to tell what is going on[/caption]
<p style="text-align: center;"></p>
<strong>Try filling the lines.</strong>
<pre>ggplot(added_df,aes(x = date, y = freq, fill=Institution, group=Institution)) +
  geom_area() + geom_line(aes(ymax=freq), position="stack")</pre>
<strong>Output:</strong>

I wondered if it would better to have the lines stacked. Turns out it wasn't. This might be because I should have done it as a percentage instead of numbers, although I thought that ggplot2 would do that for me. Also may have worked better if removed weekend. It shouldn't be too hard to turn the dataframe in to JSON and do<a href="http://projects.flowingdata.com/tut/chart_transitions_demo/"> something like this</a>. Apparently Excel 2013 can do 'Stream Graphs' but I'm too cheap to own a copy.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/russelgroupfill.png"><img class="aligncenter size-full wp-image-1224" alt="russelgroupfill" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/russelgroupfill.png" width="1060" height="732" /></a>

<strong>Find out what tools institutions use to send out their tweets</strong>
Then tested how easy it was to put it in CSV to try Excel visuals on it.
<pre>cleanFun &lt;- function(htmlString) {
  return(gsub("&lt;.*?&gt;", "", htmlString))
}

source.frame&lt;-data.frame(table(data.frame$source))
source.frame$tool &lt;-cleanFun(source.frame$Var1)

write.csv(source.frame)</pre>
<strong>Output</strong>
This is a cheat really because the output is from Excel, I wanted to see how easy it was to give the data to somebody else. This is the top 20 tools and how many tweets were sent using them. Really interesting that iPhone and iPad take 4th and 5th place. I would have thought that they would have been hard to mange an account from. I seem to be missing axis labels. Don't tell Miss.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/use-of-twitter-tools-in-HE.png"><img class="aligncenter size-full wp-image-1225" alt="use of twitter tools in HE" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/use-of-twitter-tools-in-HE.png" width="915" height="481" /></a>
<strong> Which twitter user is sent the most messages?</strong>
<pre>SELECT amt_tweets.in_reply_to_screen_name, count(*)
FROM amt_tweets
LEFT JOIN University
ON amt_tweets.twitter_id=University.twitter_username
Group by in_reply_to_screen_name</pre>
I'm not sure about this one because I don't know Twitter well enough. Does this include Retweets? @hannah_fowler96 is the winner with 7 mentions. All of her Tweets were the University of Keele replying to her questions.

<strong>Giving Up</strong>
I've just noticed I haven't captured retweets or favourites which is something I really needed.. So I'm going to give up and rewrite my scrapping module. oh well
<strong>
Some final Text analysis
</strong>
Find most freq terms:
<pre>#text
library(tm)
documents &lt;- data.frame( text = data.frame$tweet, stringsAsFactors=FALSE)
corpus &lt;- Corpus(VectorSource(data.frame$tweet))
skipWords &lt;- function(x) removeWords(x, stopwords("english"))
funcs &lt;- list(tolower, removePunctuation, removeNumbers, stripWhitespace, skipWords)
a &lt;- tm_map(corpus, FUN = tm_reduce, tmFuns = funcs)
myDtm &lt;- TermDocumentMatrix(a, control = list(minWordLength = 1))
#find frequent terms
inspect(myDtm[266:270,31:40])
findFreqTerms(myDtm, lowfreq=15)</pre>
[1] NA "amp" "campus" "can" "congratulations"
[6] "day" "free" "get" "glasgowuni" "great"
[11] "hopefully" "know" "new" "now" "offer"
[16] "open" "receiving" "research" "see" "soon"
[21] "student" "students" "the" "today" "unibirmingham"
[26] "unisouthampton" "university" "warwick" "will"

<strong>See associated terms for some of these, for the word free:</strong>
<pre>#find  terms
findAssocs(myDtm, 'free', 0.25)</pre>
free:
game           0.35
mooc           0.35
reserve        0.35
cardiffuni     0.28
sustainability 0.28
ticket         0.28

<strong>for the word hopefully:</strong>
<pre>#find frequent terms
findAssocs(myDtm, 'hopefully', 0.25)</pre>
hopefully
receiving 0.94
warwick 0.88
soon 0.84
offer 0.81
congratulations 0.76
campus 0.74
see 0.71
will 0.60
jaiminpatel 0.34

<strong>Lets wordl this badboy:</strong>
<pre>library(wordcloud)
 m &lt;- as.matrix(myDtm)
 # calculate the frequency of words
 v &lt;- sort(rowSums(m), decreasing=TRUE)
 myNames &lt;- names(v)
 k &lt;- which(names(v)=="miners")
 myNames[k] &lt;- "mining"
 d &lt;- data.frame(word=myNames, freq=v)
 wordcloud(d$word, d$freq, min.freq=3)</pre>
<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/twitter-mps-week-wordl.png"><img class="aligncenter size-full wp-image-1229" alt="twitter mps week wordl" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/twitter-mps-week-wordl.png" width="367" height="342" /></a>

&nbsp;

&nbsp;

<strong>General notes:</strong>

Lots of Universities change their account, just a name change. Many messages saying, “we are now tweeting from this account..”

Universities have different ways of organising their twitter accounts which make all this stuff a bit wobbly. Most Unis have a ‘main’’ account with sub accounts for the library and the Union etc. While I’ve tried to analyse the main accounts it does mean that the different universities put different stuff on that account making it hard to analyse. Newcastle Uni doesn’t even seem to have a main account, just sub accounts.

I haven’t really researched in to if anybody is doing anything along these lines to compare my work as it was more a way of just trying out various techniques. However the amount of analysis along the lines of “Institution X Uses Twitter more than Institution Y. Conclusion X is good, Y is bad” was pretty shocking. There must be more out there when it took two episodes of coronation street to do a simple overlook. Maybe Twitter is stopping people, people don't care, or I didn't look hard enough.

Twitter API terms and conditions are a moving target as Twitter try to stay viable. Still, at time of writing I think I am OK to store &lt;100,000 Tweets .

&nbsp;