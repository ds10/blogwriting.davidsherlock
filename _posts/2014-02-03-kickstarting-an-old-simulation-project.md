---
ID: 1013
post_title: Kickstarting an old simulation project
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/kickstarting-an-old-simulation-project/
published: true
post_date: 2014-02-03 17:37:25
---
A while ago I started to create a simulation game of a classroom. The idea, loosely based on Dwarf Fortress , was to create stories where crazy things happened in the classroom. I wanted so many random things to happen that it was just impossible the player to manage the situation and ultimately fail. To do this I wanted to create an almost unlimited amount of things that could go wrong.

In Dwarf Fortress there are basically ‘things’ and rules on how the ‘things’ can interact. I am going to over simplify and guess at some of attributes in the game but here is an example of the style random events that in dwarf fortress; It is possible for a Dwarf to fall in love with certain objects, a pair of socks is an object that has the ‘fall in love’ attribute switched on. Dwarfs can carve things on to other objects. It so happens that socks are objects with the ‘can depict’ attribute set. A dwarf smitten with socks decides to carve socks on every item with the ‘can depict on’ attribute set. Socks start appearing on walls, statues, armour. An human merchant comes to town, the merchant comes from a town where they have a hate for a certain item. Socks are flagged as ‘can hate’ . The humans so happen to hate socks so much they go to war with the Dwarfs… the end is coming.

I decided to start my simulation of a classroom based on the Dwarf Fortress idea again. I didn’t want to define the things in the classroom because almost anything can happen and by defining the different situations I was limiting what could happen. So instead I decided to use dbpedia as the backend. I thought since each item will be ‘of something’ I can decide how things interact. I could even use dbpedia to choose things like emotions or the way things reacted.

This has turned out much harder than I expected! So I’ve decided just to create mysql tables and populate them with dbpedia data. Then I’m deciding how things in these tables can interact. I think I’ll go back to the idea of using dbpedia once I’ve worked out what exactly it is that I am trying to do..

On another note, I found <a href="http://medoo.in/">this library</a> really useful to carry the database functionality.