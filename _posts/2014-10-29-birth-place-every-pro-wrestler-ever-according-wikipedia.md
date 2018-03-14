---
ID: 1893
post_title: 'The birth place of every pro wrestler  (according to wikipedia)'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/birth-place-every-pro-wrestler-ever-according-wikipedia/
published: true
post_date: 2014-10-29 13:22:14
---
A few days ago I mapped out the death places of <a title="Where the English monarchs died" href="http://davidsherlock.co.uk/monarchs-england-died/">Monarchs of England</a>. I wanted to try the same technique on a bigger dataset and <a href="http://davidsherlock.co.uk/exploring-wrestling-stables/" title="Exploring Wrestling Stables">keeping on trend with some other stuff I've done with Reddit</a> I decided to map the birthplace of every wrestler in Wikipedia.

This is a *rough* guide. It maps wrestlers birthplace to a random place somewhere in the city that Wikipedia says is their birthplace. If Wikpedia doesn't think that the data is a city then the data is missing. This data is from a snapshot taken a few months ago. Also, Wikipedia has been known to be wrong,

Click a dot to see who was born there and you can drag the map and such. There are some other bits of info I should add and some bits I should remove, but for now this is it.

&nbsp;

<iframe width="500" height="500" scrolling="no" frameborder="no" src="https://www.google.com/fusiontables/embedviz?q=select+col6+from+17X4OoUnR_zx7yrae1NlfjFVt1gID527Zmd8th_GB&amp;viz=MAP&amp;h=false&amp;lat=38.184985709117775&amp;lng=-84.75968222695302&amp;t=1&amp;z=3&amp;l=col6&amp;y=2&amp;tmplt=2&amp;hml=TWO_COL_LAT_LNG"></iframe>

There were a few problems/differences

1)Google Fusion Tables doesn't like it if you give it two lat+long values that are the same,<a href="http://googlerefine.blogspot.ca/2012/04/fusion-table-map-multiple-to-item-with.html"> I used this idea to get around that problem</a>.

2)I changed my SPARQL query to only include citys

code:
<pre class="lang:default decode:true">install.packages('SPARQL')
library(SPARQL)
endpoint &lt;- "http://live.dbpedia.org/sparql"
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

prefix grs: &lt;http://www.georss.org/georss/&gt;

SELECT ?person ?name ?born ?gps ?label WHERE {
?person rdf:type dbpedia-owl:Wrestler .
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
write.csv(df, file = "wrestlersborn.csv")
</pre>
&nbsp;

&nbsp;