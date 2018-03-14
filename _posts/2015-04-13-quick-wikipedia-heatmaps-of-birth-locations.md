---
ID: 2185
post_title: >
  Problems with quick Wikipedia heatmaps
  of birth locations
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/quick-wikipedia-heatmaps-of-birth-locations/
published: true
post_date: 2015-04-13 14:04:23
---
This doesn't tell you how many people of that profession there are, it tells you how many people of that profession are in Wikipedia, with structured data on both the persons birthplace and profession. It might tell us as much about how Wikipedia is being used as how many people from that profession are actually born there. Still, thought it was interesting!

If you are interested in the process, I wrote some notes when I was playing. I was trying to do something slightly different, but you can <a title="Testing creation of intensity maps from Wikipedia" href="http://davidsherlock.co.uk/testing-creation-of-intensity-maps-from-wikipedia/">follow the method</a>. At the bottom is my script if you want to reproduce them, at the moment these use a shape file to put pins in the map.

There are some problems, I'll try to point them out as I go along...

<strong>Birthplaces of Footballers who have played in the Premier League</strong>

The first problem is that there are loads of people missing, no person from France has ever played in the league etc. This is because not everyone who has played in the premier league is a subject of <a href="http://dbpedia.org/page/Category:Premier_League_players">premier league players</a> or it may be because birth information is not available, I suspect the former has articles premier league players seem pretty fleshed out. Also, some players have been born in the pacific ocean apparently. This is either because I picked up the birthplace incorrectly or the Long/Lat data got messed up.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/footballers-premier.png"><img class="alignnone wp-image-2186 size-large" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/footballers-premier-1024x610.png" alt="footballers premier" width="605" height="360" /></a>

<strong>Birthplace of all people in Wikipedia in category 'wrestler'</strong>

Keeping in spirit with some of the previous data work I've done I did the birthplace of prowrestlers in Wikipedia. Same rules apply as for football, the wrestler must have a page in wikipedia with a city as a place of birth. I must be able to look up long lat for the wrestler.  Again there are some people in the Pacific Ocean, which makes me think some of my long lat is out or something.

So does this tell us that people from the east of the U.S,  and Japan becoming pro wrestlers? Or that people love creating fleshed out articles for these people from these areas because people from these areas write more articles and love their local heroes?

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/wrestlers.png"><img class="alignnone wp-image-2187 size-large" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/wrestlers-1024x595.png" alt="wrestlers" width="605" height="352" /></a>

<strong>Birthplace of all people in Wikipedia in category 'Ping Pong Player'</strong>

In an attempt to see if I could plot birthplaces of people who were not in the east coast or Japan I went for another sport. One which I thought might be big in Korea and East Europe. Apparently it was:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/pingpong.png"><img class="alignnone size-large wp-image-2188" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/pingpong-1024x669.png" alt="pingpong" width="605" height="395" /></a>

So before I went any further I think I discovered that the data in Wikipedia is too inconsistant to really get a big picture. It does seem to kind of tell you were hot spots are, but only the really well looked after pages seem to have the data we need. Still I could reuse the process with other data. Not all is lost.

My R script in case its useful to anybody:
<pre class="lang:default decode:true">setwd("&lt; directory with all your files&gt;")
library(rgdal)         # for readOGR(...)
library(ggplot2)
library(RColorBrewer)  # for brewer.pal(...)

UKmap  &lt;- readOGR(dsn="shape",layer="TM_WORLD_BORDERS_SIMPL-0.3")
map.df &lt;- fortify(UKmap)


endpoint &lt;- "http://dbpedia.org/sparql"
options &lt;- NULL

query = "

PREFIX owl: &lt;http://www.w3.org/2002/07/owl#&gt;
PREFIX xsd: &lt;http://www.w3.org/2001/XMLSchema#&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX rdf: &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&gt;
PREFIX foaf: &lt;http://xmlns.com/foaf/0.1/&gt;
PREFIX dc: &lt;http://purl.org/dc/elements/1.1/&gt;
PREFIX : &lt;http://dbpedia.org/resource/&gt;
PREFIX dbpedia2: &lt;http://dbpedia.org/property/&gt;
PREFIX dbpedia: &lt;http://dbpedia.org/&gt;
PREFIX skos: &lt;http://www.w3.org/2004/02/skos/core#&gt;
PREFIX dbo: &lt;http://dbpedia.org/ontology/&gt;
PREFIX dbo: &lt;http://dbpedia.org/ontology/&gt;
PREFIX dcterms: &lt;http://purl.org/dc/terms/&gt;
PREFIX category: &lt;http://dbpedia.org/resource/Category:&gt;
prefix grs: &lt;http://www.georss.org/georss/&gt;


SELECT ?person ?name ?born ?gps ?label WHERE {
?person rdf:type dbpedia-owl:TableTennisPlayer .
?person rdfs:label ?name .
?person dbpedia-owl:birthPlace ?born .
?born rdf:type dbpedia-owl:City .
?born grs:point ?gps .

}
"

qd &lt;- SPARQL(endpoint,query)
df &lt;- qd$results

read &lt;- data.frame(do.call('rbind', strsplit(as.character(df$gps),' ',fixed=TRUE)))
colnames(read) &lt;- c("lat","long")

#attempt 1, doesnt work
ggplot(read, aes(x=long, y=lat)) + 
  stat_density2d(aes(fill = ..level..), geom="polygon")+
  geom_point(colour="red")+
  geom_path(data=map.df,aes(x=long, y=lat,group=group), colour="grey50")+
  scale_fill_gradientn(colours=rev(brewer.pal(7,"Spectral")))

p</pre>
&nbsp;