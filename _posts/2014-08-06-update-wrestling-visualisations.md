---
ID: 1683
post_title: Update on Wrestling visualisations
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/update-wrestling-visualisations/
published: true
post_date: 2014-08-06 20:44:11
---
A few days ago I started playing with <a title="Exploring Wrestling Stables" href="http://davidsherlock.co.uk/exploring-wrestling-stables/">dbpedia data</a>. I had spent a while trying to find interesting people story lines to find information about. I had toyed with story lines in TV soaps and video games, but after a decision with a friend where I was introduced to the concept of a wrestling stable I decided to explore links between factions/team mates in the pro wrestling world. I decided to crawl through all the links between all the stables in dbpedia and and play with them in Gephi.

A few hours later I had made some Gephi style pictures, but realised I knew nothing about pro wrestling and needed some input from people who do. I headed over to Reddit’s wrestling forum <a href="http://reddit.com/r/squaredcircle">/r/squaredcircle</a> and asked them for feedback on my post. I was really taken back by how helpful an online community can be. I had lots of positive comments and interesting feedback that helped me think through the dataset. It really made me think about telling ‘stories with data’ (I hate that phrase!) and this whole thing is really a collaborative thing. Some great discussions later knew much more about the dataset. Aside from some interesting wrestling storylines I also picked up some things about mining dbpedia.

Data is frozen at June 2013, some members of the community pointed out that I had missed newer groups. Also the data is not consistent. I had chosen to use the little piece of information on a Wikipedia page that says “Member of” or “Former Member of”. This is actually pretty limited as people don’t seem to fill in these all the time. I could mine categories or something. I’m not sure there is a best way to go round this. I guess it depends on what you are mining.

For example I used the following query at dbpedia to grab members of stables:
<pre class="lang:default decode:true ">?person rdf:type dbpedia-owl:Wrestler .
?person rdfs:label ?name .
?member dbpprop:members ?person .
FILTER ( lang(?name) = 'en' ) .
?member rdfs:label ?membername .
FILTER ( lang(?membername) = 'en' ) .</pre>
&nbsp;

Some Redditors spotted major wrestlers missing, wrestlers such as Ric Flair! <a href="http://dbpedia.org/page/Ric_Flair">Looking up Ric Flair</a>  made me realise he hasn’t got a rdf:type dbpedia-owl:Wrestler, as such so he wouldn’t appear in my diagram. The addition of someone as influential as Rik Flair will seriously change the diagram I’m sure and it was a shame he was missed. I notice that most wrestlers have the word wrestler in their description, so I could get them using this instead
<pre class="lang:default decode:true ">?person dbpprop:shortDescription ?desc .
?person rdfs:label ?name .
?member dbpprop:members ?person .
FILTER regex(?desc, "wrestler", "i") .
FILTER ( lang(?name) = 'en' ) .
?member rdfs:label ?membername .
FILTER ( lang(?membername) = 'en' ) }</pre>
&nbsp;

To get the best of both worlds I can use DISTINCT and UNION in my query to grab one or the other. There is no guarantee that I won’t miss a wrestler still because they 1) Might not either 2) Might not even have been added to Wikipedia, or be in the right 'Member' or 'Former Member fields'
<h2>Next Steps</h2>
I’m not going to carry on with the visualisation that I made because dbpedia just has too many gotcha’s in the dataset. I did however have some offers to collaborate and I think I’m going to follow up on these and try and pick up some new skills from my new found friends.

While the data in DBpedia might not be perfect the one thing I am really sure about now is that it is a great way to start a discussion about something with a community! Thanks again to the members of /r/squaredcircle.