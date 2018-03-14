---
ID: 1768
post_title: Playing with Wikipedia
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/playing-wikipedia/
published: true
post_date: 2014-08-29 11:18:09
---
Sometimes I like to write bits of code that poke Wikipedia, its fun and the data is a great way to start a conversation with people. I recently teamed up with the pro wrestling fans of Reddit to find out <a title="Exploring Wrestling Stables" href="http://davidsherlock.co.uk/exploring-wrestling-stables/">information on wrestling stables</a>, we did this using the structured information from Wikipedia stored in <a href="http://dbpedia.org/">DBpedia</a>, my favourite thing on the net.  I received a really warm response from them, had some interesting discussion about the data, their hobby and even had a few offers to collaborate in future work. There were a few things about the experience that really struck me:

<strong>It got us talking about how information on the subject is recorded</strong>
Using Wikipedia as a datasource the community saw how their passion was being documented online. There were great discussions about the way their hobby was being misrepresented in Wikipedia, my favourite being that apparently a wrestling stable and a wrestling faction are not the same thing, but in Wikipedia it was, and this leading to a great discussion about how they could go and change the source material.

<strong>We missed Nature Boy Ric Flair</strong>
We also found that data was not consistent or missing, in the case of DBpedia the data was pretty old (a lot happens in a year in the world of wrestling, apparently) and sometimes there were no rules to how data was being collected, for example some articles refereed to a wrestler by their real name and some by their gimmick. This led to discussions around why it was missing, and the people who really knew there wrestling facts were able to lead the discussion around what was missing and what was wrong. The communities favourite wrestler was missing from the data and spotting the mistakes or funny entries became somewhat of a game, drawing other people in to the discussion.

<strong>Better/other ways to get data put of Wikipedia?</strong>
There were also questions that I was asked by the Reddit crowd about wrestling that I knew would be in Wikipedia but didn’t have a good way to get the information out other than reading 30 000 pages on wrestling gimmicks and extracting the information by hand. It was quote easy to ask "who has been in a wrestling team with who" but quite difficult to ask anything where the data wasn't structured. Aside from scraping tables and using DBpedia I would be interested in other ways people extract information.

<strong>Its fun</strong>
The game like nature of trying to get data out of Wikipedia and then navigate the data’s oddities is what appeals to me. I also can’t get my head around just how massive the dataset is. Speaking to the folks of Reddit it would appear that databases of wrestling information are hard to come by and the general response was along the lines of ‘Wikipedia can do that?’, and they seemed to enjoy beating the machine and finding out where it went wrong (and then going and correcting the source material)

I’m really interested in finding ways to get information out of Wikipedia and think projects like DBpedia are brilliant. One of the things I would like to explore more after my experience with Reddit was finding out more about how and by whom the data in Wikipedia is collected. I had thought about checking IP addresses to see how was editing posts but had not thought about examining the outgoing links, <a href="http://ukwebfocus.wordpress.com/2014/08/28/links-from-wikipedia-to-russell-group-university-repositories/">Brian Kelly points out there is a external link checker</a> in Mediawiki and uses it to find out which University Repositories were being linked to. I haven’t had a good luck yet but I wonder if I can automate a process of giving a script a few links and then seeing where Wikipedia links to.