---
ID: 973
post_title: >
  Scraping facts from Wikipedia to MySQL
  using R and DBpedia
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/scraping-facts-wikipedia-mysql-using-r-dbpedia/
published: true
post_date: 2014-01-29 13:35:15
---
<em>This is a very basic how to, I've  just saved here this here for future reference </em>

I wanted to build game that had a life of it’s own. To do this I wanted to get lots of lists of things. A list of emotions, list of names, etc etc. If I have a look around I might be able to find lists of these things, but since there were so many different categories of things I wanted lists of I decided to scrape it from Wikipedia, well dbpedia. I did this in R because it’s what I know.
<p style="text-align: left;">First I wanted to store the list in a database, I went with MySQL because I have mamp on my machine making it easy to work with. The RMySQL package is easy to install on OS X, I’ve heard people say there isn’t a binary on Windows so you may have to compile it yourself. Anyway, for me it was a case of:</p>

<blockquote>
<p style="text-align: left;">install.packages("RMySQL")</p>
</blockquote>
I’m using dbpedia so I installed the sparql plugin
<blockquote>install.packages('SPARQL')</blockquote>
Now load the packages:
<blockquote>library(SPARQL)

library(RMySQL)</blockquote>
Define the endpoint as dbpedia’s and set options as NULL
<blockquote>endpoint &lt;- "http://live.dbpedia.org/sparql"
options &lt;- NULL</blockquote>
Even though I’m not using them all I’m stealing the sparql prefixes that the dbpedia endpoint uses
<blockquote>prefix &lt;- "PREFIX owl: &lt;http://www.w3.org/2002/07/owl#&gt;
PREFIX xsd: &lt;http://www.w3.org/2001/XMLSchema#&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX rdf: &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&gt;
PREFIX foaf: &lt;http://xmlns.com/foaf/0.1/&gt;
PREFIX dc: &lt;http://purl.org/dc/elements/1.1/&gt;
PREFIX : &lt;http://dbpedia.org/resource/&gt;
PREFIX dbpedia2: &lt;http://dbpedia.org/property/&gt;
PREFIX dbpedia: &lt;http://dbpedia.org/&gt;
"</blockquote>
I then wrote a pretty straight forward query to grab all the English labels to things in the emotion category of wikipedia and put this in to my query, along with the prefixes.
<blockquote>query &lt;- paste(prefix,
'SELECT  ?isValueOf ?name
WHERE {
?isValueOf &lt;http://purl.org/dc/terms/subject&gt; &lt;http://dbpedia.org/resource/Category:Emotions&gt; .
?isValueOf rdfs:label ?name
FILTER(LANG(?name) = "" || LANGMATCHES(LANG(?name), "en"))
}')</blockquote>
Finally
<blockquote>result &lt;- SPARQL(endpoint,q,ns=prefix,extra=options)$results</blockquote>
gets me the list of emotions in English in a table like so:

&nbsp;
<p style="text-align: center;"><a href="http://davidsherlock.co.uk/wp-content/uploads/2014/01/emotions-scraped-from-wikipedia.png"><img class="aligncenter  wp-image-974" alt="emotions scraped from wikipedia" src="http://davidsherlock.co.uk/wp-content/uploads/2014/01/emotions-scraped-from-wikipedia.png" width="383" height="202" /></a></p>
Now for my game I want these in database. Later I’m going to want more information on them, I can grab that from info Wikipedia later, but that can wait until I’m more certain that my game will work. I set up a database called classroom_story (the name of my game) and created a table to store my emotions. Because I’m using MAMP I had to create a symbolic link like so:
<blockquote>ln -s /Applications/MAMP/tmp/mysql.sock /tmp/mysql.sock</blockquote>
The results can then be written to the mysql table very easily:

con &lt;- dbConnect(MySQL(), user="username", password="password",  dbname="classroom_game", host="localhost",client.flag=CLIENT_MULTI_STATEMENTS)
# write it back
dbWriteTable(con,"emotions",result,overwrite=T)
dbDisconnect(con)

Currently this is just a list, but I could pull back whatever I want from Wikipedia, I'm going to want to pull out lots of information about lots of things to build my game.