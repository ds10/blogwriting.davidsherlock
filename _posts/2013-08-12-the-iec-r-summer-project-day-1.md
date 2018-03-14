---
ID: 221
post_title: 'The IEC R summer project: Day 1'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/the-iec-r-summer-project-day-1/
published: true
post_date: 2013-08-12 09:10:51
---
Mark Johnson at the IEC has posted a description about a personal analytics tool hat basically text mines all the text you leave around the web. He calls it the Personal Corpus. In fact I worked with him on a project about 5 years ago where you could 'Like' resources and then resources could be shared with other people. It may have been a flop when it came to uptake but it sounds very familiar!

I'm going to take his idea and try and implement something basic. I slept on it last night and I think this is my check list for version 1:

1) Rather than aggregate I want a quick script that  takes data exports and puts them in a database. Since Facebook, Twitter seem to be tightening up access to data I think version 1 should concentrate on taking the 'export my data' XML file and putting it into a mysql database. I've been playing with R and mysql and it shouldn't be a problem to connect the too up.

2)Connect R and mysql up, do some simple ngram stuff or whatever

3)Create a shiny front end

OK, lets get cracking.