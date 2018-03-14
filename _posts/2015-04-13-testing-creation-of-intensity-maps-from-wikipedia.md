---
ID: 2179
post_title: >
  Testing creation of intensity maps from
  Wikipedia
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/testing-creation-of-intensity-maps-from-wikipedia/
published: true
post_date: 2015-04-13 10:04:29
---
I wanted to come up with a quick method that I could reuse where I could ask Wikipedia a quick question, get some numbers and create a heat map. I still haven't come up with the quick process, and when I mess with data I tend to stick with what I know for a 'first pass' at the process and then cut down the steps when I know that it works. I guess other people who play with R packages will understand the frustration of spending 3 hours with a new R package only to learn that the process doesn't work anyway and it would have been quicker just to have do the data mangling in Excel first before trying to create a repeatable process. These are the steps I went through to see if it was possible. I know that the data is incorrect, this seems to mainly be because of a problem with my SPARQL query.

1) Grab the data

I'm using DBpedia to get the data. I wanted to write query where I could just grab all the instances of something and then be able to put them on an intensity map. I picked any old question. I went with birthplace of all footballers that have played in the Premier League and using DBpedia this SPARQL query I came up with, this will get their town with its long and lat data:
<pre class="lang:default decode:true">SELECT ?person ?name ?born ?gps ?label WHERE {
?person dcterms:subject category:Premier_League_players.
?person rdfs:label ?name
FILTER ( lang(?name) = 'en' ) .
?person dbpedia-owl:birthPlace ?born .
?born rdf:type dbpedia-owl:City .
?born grs:point ?gps .
?born rdfs:label ?label
FILTER(LANG(?label) = '' || LANGMATCHES(LANG(?label), 'en'))</pre>
I used the SPARQL package in R to to do the query and write the results to CSV:
<pre class="lang:default decode:true ">endpoint &lt;- "http://live.dbpedia.org/sparql"
endpoint &lt;- "http://dbpedia.org/sparql"
options &lt;- NULL

query = "

PREFIX owl: &lt;http://www.w3.org/2002/07/owl#&gt;
PREFIX xsd: &lt;http://www.w3.org/2001/XMLSchema#&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX rdf: &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&gt;
PREFIX dc: &lt;http://purl.org/dc/elements/1.1/&gt;
PREFIX dbpedia: &lt;http://dbpedia.org/&gt;
PREFIX dcterms: &lt;http://purl.org/dc/terms/&gt;
PREFIX category: &lt;http://dbpedia.org/resource/Category:&gt;
PREFIX grs: &lt;http://www.georss.org/georss/&gt;

SELECT ?person ?name ?born ?gps ?label WHERE {
?person dcterms:subject category:Premier_League_players.
?person rdfs:label ?name
FILTER ( lang(?name) = 'en' ) .
?person dbpedia-owl:birthPlace ?born .
?born rdf:type dbpedia-owl:City .
?born grs:point ?gps .
?born rdfs:label ?label
FILTER(LANG(?label) = '' || LANGMATCHES(LANG(?label), 'en'))
}
"

qd &lt;- SPARQL(endpoint,query)
df &lt;- qd$results
write.csv(df, file = "footballersborn.csv")</pre>
I like to play with my data in OpenRefine before I do anything.. this isn't a step that I would really need to do as I'm sure I could do some of my data cleansing in R, but for a first pass at things its just easier and quicker to have a look at the data and see what sort of stuff I need to clean up. In this case I just created two new columns, these were separate long and lat columns based from the GPS column.

At this stage I noticed something fishey about my dataset, I'm guessing that there was either  something wrong with my query or the dataset, the biggest giveaway seemed to be that according to my dataset there were no footballers who have played in Premier League from France. I decided to press on anyway as this exercise was more about creating a repeatable process for now. At this stage it is very easy to plot the data as a punch of pins on Google Maps using Google Fusion Tables, I've done something similar before using the <a title="The birth place of every pro wrestler  (according to wikipedia)" href="http://davidsherlock.co.uk/birth-place-every-pro-wrestler-ever-according-wikipedia/">birth place of wrestlers</a>. However, I wanted to create an intensity/choropleth map which is slightly different, Google Fusion Tables classic is supposed to do this, but the new version only creates heatmaps.

To have a go at doing this I needed to count up the number of occurrences of births of footballs from each country. I didn't have country information in my dataset, so I quickly wrote a function to take the long and lat columns and create a dataframe of countriy codes. I then attached this dataframe to my old one, anybody who copies this will need to create an account at geonames.org and replace the username:
<pre class="lang:default decode:true ">test &lt;- function(test) {connectStr &lt;- paste('http://ws.geonames.org/countryCode?lat=',test[7],'&amp;lng=',test[6],'&amp;username=user' , sep="")
                        con &lt;- url(connectStr)
                        data&lt;-readLines(con)
                        close(con)
                        return (data)}

ccodes&lt;-apply(footlonglat, 1, test)
footlonglat$ccodes &lt;- ccodes</pre>
I then counted the occurrences of county codes and wrote it to CSV.
<pre class="lang:default decode:true ">number_of_players&lt;-table(footlonglat$ccodes)
write.csv(number_of_players, file = "noplayers.csv")</pre>
The aim of this was to get it in to Google Fusion Tables and merge the table with a public table that had country codes and kmz details. This worked and the classic view was able to create an intensity map. The problem was while the process seemed to work, the map didn't do anything. It could be because the data was small, or that Google Fusion Classic is on the way out, or that I just can't use Google Fusion Tables properly... more experiments required.

I was able to load the CSV straight to <a href="chatsbin">chartsbin</a>, which created this:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/maps.png"><img class="alignnone wp-image-2181 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/maps.png" alt="maps" width="862" height="459" /></a>

There is a <a href="http://cran.r-project.org/web/packages/choroplethr/choroplethr.pdf">choropleth package for R</a>, which is the next thing to try to cut down the steps.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;