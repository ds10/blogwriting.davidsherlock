---
ID: 1665
post_title: Exploring Wrestling Stables
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/exploring-wrestling-stables/
published: true
post_date: 2014-08-05 09:34:24
---
In pro wrestling a stable is a group of  wrestlers who form an alliance and wrestle together, they help each other out the way typically team mates would, for example by sneaking sledgehammers in to the ring when the referees have their backed turned. When I was younger my favorite stable were called D-Generation X - a bunch of loud mouthed rebels who broke the rules and defied all authority. Recently a childhood friend told me that one of these rebels was doing a talk in our local town with some friends and was charging £50 (!) a ticket. To go to an event in our town £50 is quite a lot of money, usually the top bands will charge £50 at an arena, you would probably get change for £50 if you went to see Metallica at a football stadium. So wondering why these performers from the  90s get to charge such a fee I looked the guy up on Wikipedia, it turns out that the performer, real name <a href="http://en.wikipedia.org/wiki/Sean_Waltman">Sean Waltman</a> had been in lots of stables and a little more research reveals that wrestling fans LOVE stables. Knowing exactly who has been in a team with seems to be part of the fun of watching wrestling and going to a live show to hear wrestlers tell stories about previous stable mates commands a higher ticket price than going to an actual wrestling event itself.

I found this fascinating and wanted to explore who Sean Waltman had been team mates with. In fact I wanted to map out ALL the wrestling stables that ever existed. I noticed on Wikipedia that there are pages dedicated to stables and these stables have entries for members and previous members.

A little data mining later and I had a list of all the stables in wrestling and who belonged to them. I mapped this out in a visualisation and created two massive maps of wrestlers. It turns out there are a lot of stables in pro wrestling. I'm thinking of digging deeper in to this but I'm not sure what I am looking for, I might ask seek out the wrestling fans of Reddit for help.
<h2>The Connection Maps</h2>
The maps are huge. About 7mb each and 3600x3600. If I click the images below in firefox it shows me a zoomed out version and then I can click it to explore it. I know they are not great at the moment because there is to much information in there, but I think my next step is to go and ask wrestling fans what sort of thing they might be interested in finding out from this data.

You do need to click the image which will take you to imgur, then you need to click it again to get to the image itself and a final click to zoom in to explore. The nodes represent people and the lines represent the fact they were in a stable together.

A community detection algorithm called the 'Louvain modularity method' has been applied to it, this tries to detect communities of people within the network. Each person has been color coded according to the network they are in.

The dots have been resized too, I have resized them according to their 'Betweenness centrality' measure. Really simply explained, this is a score that is found out by the number of shortest paths between other wrestlers that go through a wrestler. So for example, in the map the quickest way to get from Darren Young to Adam Birch is through CM Punk so CM Punk gets a point towards his Betweeness Centrality and his dot gets bigger. For a proper and better explanation you are better off reading the <a href="http://en.wikipedia.org/wiki/Betweenness_centrality">Betweeness Centrality Wikipedia page</a>.

I am also aware I have left off important information from the graph! I need my wrist slapping for missing out what they weighted by and the such.

&nbsp;

<a href="http://i.imgur.com/213nQNq.jpg"><img class="alignnone" src="http://i.imgur.com/213nQNq.jpg" alt="" width="2880" height="2880" /></a>

&nbsp;

<a href="http://i.imgur.com/rUHfs2z.jpg"><img class="alignnone" src="http://i.imgur.com/rUHfs2z.jpg" alt="" width="3240" height="3240" /></a>

&nbsp;
<h2 id="title">Updates from wrestling fans of Reddit</h2>
<ul>
	<li>So the people at <a href="http://www.reddit.com/r/SquaredCircle/comments/2coe77/creating_a_map_of_wrestlers_linked_by_the_stables/">squaredcircle</a> have the comments coming in. I've created a quick video because I find that it helps me to get my head around things and I'm uploading that at the moment. u/lykki suggested I try doing a 'Prezi' using the image, I think that might be a good way to deliver the information in chunks.</li>
	<li>Also it was pointed out that my images are JPEG.  I exported them in PNG, but it turns out IMGUR has been converting them; I'll try to find out why.</li>
	<li>I can use the d3 tree layout to make a history of who trained who. Might be a good idea to use a sankey diagram thingy.</li>
	<li>Some interest in representing this in d3 style network graphs</li>
	<li>I'm missing Rik Flair! Best check my dataset to work out why.</li>
	<li>I am completely blown away by how helpful a community can be, a follow up post on how helpful the community was might be interesting</li>
</ul>
<ul>
	<li>/u/artcarden has 3 really good points that I have copied here. I never knew stables and factions were different:</li>
</ul>
<blockquote>
<ol>
	<li>There's a debate about the differences between stables and factions; for your purposes, you could probably consider them the same thing.</li>
	<li>I like including tag teams, but I think you'll want to make sure it was a recognized team rather than a one-off or month-long deal (Rybaxel counts, Cena tagging with Roman Reigns a few times doesn't unless they combine to form the Super-Powers).</li>
	<li>A next step: calculate each performer's "Flair Number" or "Hogan Number," like a scholar's <a class="imgScanned" href="http://en.wikipedia.org/wiki/Erd%C5%91s_number">Erdos Number</a>. People who teamed directly with Flair in the Horsemen or Evolution would be Flair 1. Assuming there's no direct Flair/Waltman link, Sean Waltman would be Flair 2 because he was in DX with Triple H, who was in Evolution with Flair. Edge would be Flair 2; he was in Rated RKO with Randy Orton, who was in Evolution with Flair.</li>
</ol>
</blockquote>
<h2>Final Update</h2>
After some great discussions with the guys at squaredcircle it turns out that there are quite a few bits and bobs missing. I expected this because well, it's wikipedia so it can only really give you a representation as good as the data that goes in it. There are a few things I could do to make it a little more accurate but it doesn't seem worth the tweaking on this project. I've had a few offers of visualisation collaboration and it seems to make more sense to start again with those people who have more knowledge on the subject.

So I guess I'm parking this particular project and taking up some others with some fans I've met on Reddit. I'll write up my experiances, share it and start on something new. Here is the R script I used incase anybody finds it useful. I realise I've done the whole thing in 3 steps instead of 1 but that was for debugging reasons and now it is never going to get finished:
<pre class="lang:default decode:true ">library("SPARQL")
library("igraph")

#the first bit of this table makes a matrix like I used to, the second will create a node and edge csv. FIGHT

endpoint = "http://dbpedia.org/sparql"

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
SELECT DISTINCT ?name ?membername WHERE {

?person rdf:type dbpedia-owl:Wrestler .
?person rdfs:label ?name .
?member dbpprop:members ?person .
FILTER ( lang(?name) = 'en' ) .
?member rdfs:label ?membername .
FILTER ( lang(?membername) = 'en' ) .

}
"

qd &lt;- SPARQL(endpoint,query)
df &lt;- qd$results

query2 &lt;-"

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
SELECT ?name ?membername WHERE {

?person rdf:type dbpedia-owl:Wrestler .
?person rdfs:label ?name .
?member dbpprop:formerMembers ?person .
FILTER ( lang(?name) = 'en' ) .
?member rdfs:label ?membername .
FILTER ( lang(?membername) = 'en' ) .

}
"

qd2 &lt;- SPARQL(endpoint,query2)
df2 &lt;- qd2$results

allrelationships&lt;-rbind(df, df2)
write.csv(allrelationships, file = "allrelationships.csv")
cleanstables = read.csv("allrelationships-csv.csv")
cleanstables$x &lt;- NULL

M = as.matrix( table(cleanstables) )
Mrow = M %*% t(M)
#Mcol = t(M) %*% M
write.csv(Mrow, "test.csv")
iMrow = graph.adjacency(Mrow, mode = "undirected")
E(iMrow)$weight &lt;- count.multiple(iMrow)
iMrow &lt;- simplify(iMrow)
iMrow = graph.adjacency(Mrow, mode = "undirected")
E(iMrow)$weight &lt;- count.multiple(iMrow)
iMrow &lt;- simplify(iMrow)
write.graph(iMrow, file="graph.graphml", format="graphml");</pre>
&nbsp;

&nbsp;