---
ID: 2528
post_title: >
  Scrapping data from dbpedia for trivia
  game snippet
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/scrapping-data-from-dbpedia-for-trivia-game-snippet/
published: true
post_date: 2016-03-10 12:32:34
---
I've been trying to write scripts that can automagically create revision games for a while now. One of the problems I have is getting datasets of questions together. I've been sniffing around wikipedia/dbpedia as a way to populate revision game questions. Recently I've been interested in building 'What is it games?' where you are given a series of clues and then you try and play a hangman style game to guess what the thing is. Wikipedia seems a decent data source for this because you can get data about relationships between things very easily.

I'm still in the process of getting my unity game together, but I thought I'd get my spreadsheet ready early so I have something to play around with. Sticking with the wrestling theme I'm leaving my query here for later.
<pre class="lang:default decode:true ">SELECT * WHERE {

?person rdf:type &lt;http://dbpedia.org/ontology/Wrestler&gt; .
?person rdfs:label ?name .
?person dbp:birthPlace ?birthplace .
?person dbp:dateOfBirth ?dateofbirth .
?person dbp:debut ?debut .
?member dbpedia2:formerMembers ?person .
FILTER ( lang(?name) = 'en' ) .
?member rdfs:label ?membername .
FILTER ( lang(?membername) = 'en' )

}</pre>