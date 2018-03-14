---
ID: 1875
post_title: Where the English monarchs died
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/monarchs-england-died/
published: true
post_date: 2014-10-28 14:26:13
---
<strong>(according to Wikipedia)</strong>

This was a quick and dirty experiment to see how easy it is to auto generate an interactive map from Wikipedia/DBpedia. There are some caveats and things I still need to iron out.

These are people that Wikipedia has described as a Monarch of England, they must have a place of death listed in Wikipedia and that place of death must have longitude and latitude in http://www.georss.org/georss/

There are loads more things I would like to do to the map, but I was pleased at how quick you can map things from Wikipedia. I could perhaps add how they died. There also seems to be some encoding problems and the description boxes seem to cut off.

Remember this is completely automated from Wikipedia data. Data might not be completely correct; worrying about that is for part two as I just need the process in place for another project.

Click the dots for details.

<iframe width="500" height="300" scrolling="no" frameborder="no" src="https://www.google.com/fusiontables/embedviz?q=select+col1+from+1aahzr2pGDli2Dr-sKAmgMopbsWgRj1YFqMZjA3Aw&amp;viz=MAP&amp;h=false&amp;lat=48.464688175311515&amp;lng=4.127108333500029&amp;t=1&amp;z=4&amp;l=col1&amp;y=2&amp;tmplt=2&amp;hml=TWO_COL_LAT_LNG"></iframe>

The process was quite easy but there are some steps I could do with removing:

1) Write SPARQL query that looks like this:
<pre class="lang:default decode:true  ">SELECT ?person ?name ?died ?gps ?label WHERE {
      ?person dcterms:subject category:English_monarchs .
      ?person foaf:name ?name .
      ?person dbpedia-owl:deathPlace ?died .
      ?died grs:point ?gps .
      ?died rdfs:label ?label
       FILTER(LANG(?label) = '' || LANGMATCHES(LANG(?label), 'en'))
               }</pre>
2)Grab CSV based on SPARQL, use Open Refine to do some housekeeping

3)Upload to Google Fusiontables

Here is the script I wrote in R to generate the CSV:
<pre class="lang:default decode:true ">install.packages('SPARQL')
library(SPARQL)
endpoint &lt;- "http://live.dbpedia.org/sparql"
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

SELECT ?person ?name ?died ?gps ?label WHERE {
      ?person dcterms:subject category:English_monarchs .
      ?person foaf:name ?name .
      ?person dbpedia-owl:deathPlace ?died .
      ?died grs:point ?gps .
      ?died rdfs:label ?label
       FILTER(LANG(?label) = '' || LANGMATCHES(LANG(?label), 'en'))
               }
"

qd &lt;- SPARQL(endpoint,query)
df &lt;- qd$results
write.csv(df, file = "kingsanddeaths.csv")
</pre>
&nbsp;