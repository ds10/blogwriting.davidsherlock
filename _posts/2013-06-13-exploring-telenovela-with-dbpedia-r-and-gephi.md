---
ID: 81
post_title: >
  Exploring Telenovela with DBpedia, R and
  Gephi
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/exploring-telenovela-with-dbpedia-r-and-gephi/
published: true
post_date: 2013-06-13 13:26:35
---
Today I discovered Telenovelas. Telenovelas are short limited run programs similar to soap opera, they are popular in Spanish language counties and they are serious business. I stumbled across a clip on youtube and was instantly hooked. Check this out:

http://youtu.be/OGJAUnNzbhE

I headed to Wikipedia to find out more only to find that Telenovelas is a very large phenomenon, so large there is so much information I didn’t know where to start. So I headed to DBpedia to do some basic exploring.

One of the first pages in wikipedia I stumbled across was about a popular childrens telenovela <a href="http://en.wikipedia.org/wiki/Chiquititas">chiquititas</a>. I think checking an article in DBpedia is always a good place to start, so I decided to check out the resource by its URI using DBpedias install of Virtuoso here: <a href="http://dbpedia.org/page/Chiquititas">http://dbpedia.org/page/Chiquititas</a>. I noticed there was it had the property dbprop:genre  with value  dbpedia:Telenovela.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-10.42.25.png"><img class="alignnone size-full wp-image-82" alt="dbepedia:genre" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-10.42.25.png" width="420" height="22" /></a>

&nbsp;

Using this its quite easy to write a SPARQL query that can then pull back a list of all Telenovela articles in wikipeida.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.03.55.png"><img class="alignnone size-full wp-image-84" alt="telenovela sparql" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.03.55.png" width="464" height="316" /></a>

&nbsp;

Which gave me a list of all the programs in the Genre in Wikipedia, theres 139 of them apparently, which seems a very low number, but then we don’t know how many articles are missing the structured information for the query to work.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.07.25.png"><img class="alignnone size-full wp-image-83" alt="list of telenovela from wikipedia" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.07.25.png" width="469" height="323" /></a>

&nbsp;

I wondered if we could work out which country had the most of them, I appended the query to include :

&nbsp;

<em>?show dbpprop:country ?country .</em>

<em>?country foaf:name ?countryname</em>

&nbsp;

which I could then plot with the following:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-14.17.49.png"><img class="alignnone size-full wp-image-85" alt="plotting a barchart using R" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-14.17.49.png" width="465" height="81" /></a>

&nbsp;

To get:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.51.07.png"><img class="alignnone size-full wp-image-86" alt="Telenovela articles in Wikipedia by Country" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-11.51.07.png" width="1136" height="419" /></a>

&nbsp;

So Brazilians can’t get enough of the stuff. I’m not surprised either judging from the earlier clip I saw.

I decided to take a look at the cast members members of each Telenovia series. This has to be taken lightly as Wikipedia is short on this information. The SPARQL query looked like this:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-12.29.37.png"><img class="alignnone size-full wp-image-87" alt="sparql query to find how telenovelas stars are related by the shows they are in" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-12.29.37.png" width="675" height="129" /></a>

This pulls back 645 names and the show they were in, some of the names are the same because they have appeared in more than one show. I created a matrix of who has been in shows with who and then plotted it as a GraphML so I could explore the data in Gephi.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-12.29.47.png"><img class="alignnone size-full wp-image-88" alt="creating a matrix from dataframe" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/Screen-Shot-2013-06-13-at-12.29.47.png" width="670" height="171" /></a>

&nbsp;

&nbsp;

To finally create a graph, zoom in for names. It seems Sabine Moussier, Elaine Giardine, Tony Ramos are all big names central to telenovela. The big blue circle at the top is from an american soap called Hollywood High.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/06/telenovela.png"><img class="alignnone size-full wp-image-89" alt="links of actors in telenovela" src="http://davidsherlock.co.uk/wp-content/uploads/2013/06/telenovela.png" width="2046" height="2046" /></a>

&nbsp;

The final code:

&nbsp;

&nbsp;

[codesyntax lang="text"]
<pre>library("SPARQL")
library("igraph")

endpoint = "http://dbpedia.org/sparql"

query = "SELECT ?name ?countryname {
?show dbpedia-owl:genre dbpedia:Telenovela .
?show foaf:name ?name .
?show dbpprop:country ?country .
?country foaf:name ?countryname
}"

qd= SPARQL(endpoint, query)
df = qd$results

counts &lt;-table(df$countryname)
barplot(counts, main="Telenovela articles in Wikipedia by Country", 
xlab="Country")

query = "SELECT ?name ?showname where {
?person foaf:name ?name .
?show dbpprop:starring ?person .
?show dbpedia-owl:genre dbpedia:Telenovela .
?show foaf:name ?showname .
}"

qd= SPARQL(endpoint, query)
df = qd$results

M = as.matrix( table(df) )
iMrow = graph.adjacency(Mrow, mode = "undirected")
E(iMrow)$weight &lt;- count.multiple(iMrow)
iMrow &lt;- simplify(iMrow)
write.graph(iMrow, file="graph.graphml", format="graphml");</pre>
[/codesyntax]

&nbsp;