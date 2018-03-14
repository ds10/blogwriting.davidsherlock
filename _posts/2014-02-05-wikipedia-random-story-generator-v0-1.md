---
ID: 1015
post_title: >
  Wikipedia as a random story generator
  v0.1
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/wikipedia-random-story-generator-v0-1/
published: true
post_date: 2014-02-05 10:48:07
---
For a while I've wanted to create a <a title="Kickstarting an old simulation project" href="http://davidsherlock.co.uk/kickstarting-an-old-simulation-project/">game/story where players are given crazy and random situations.</a> I wanted characters in the story to have relationships, feelings, own things etc,  the problem I've had is that if I predefine all these then the game won't be random to me, where is the fun in that? I'd even like to the game to create new ways for characters to interact without me defining them. I've been looking for data source to fuel such a game and can only really think of the structured data extracted from <a href="http://wikipedia.org">Wikipedia</a> from the DB<a href="http://dbpedia.org/">pedia</a> project.

I've been thinking of ways to use DBpedia to drive the story, but it's pretty hard. I thought I'd just have a first shot at doing something by using Wikipedia categories as a way to create the attributes of a character. Also to make things easier for now I'm not using the SPARQL endpoint as my back end but routinely scraping from it in to a MySQL database first. So, I haven't got very far yet, but I am creating random characters. They don't interact and the types of things they can own are predefined.

This was my first auto generated character:
<blockquote>Name: Howard

Stats:

Social Class:Village idiot

Enjoys:Naked butler

Pet: Pot-bellied pig

Favorite toy: Zoetrope

Other Facts:
Howard stole eraser from his school.</blockquote>
So I haven't got very far yet, but I like the idea that I wrote some rules about which categories in Wikipedia can be involved in my character creation and it made a character for me, even if sometimes it comes back with silly items. I'd like the data in dbpedia to decide what characteristics the how students in my story can have how how they interact with each other, but I need to come up with a good way to transverse the graph. I'm thinking I could use things such as wordnet and social media to create some extra fuzzyness.

<a title="Wikipedia Storyteller" href="http://davidsherlock.co.uk/wikipedia-storyteller/">If you want to create your own character you can do so on this page.</a>