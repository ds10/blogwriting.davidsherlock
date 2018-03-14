---
ID: 1044
post_title: MySQL to sqlite
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/mysql-sqlite/
published: true
post_date: 2014-02-12 16:21:07
---
I'm currently writing bits of code to tell stories using a variety different data sources; one of my aims is to make the storytelling experience cross platform. My project started life as a <a title="Wikipedia Storyteller" href="http://davidsherlock.co.uk/wikipedia-storyteller/">web based thing and </a>I see if I could move some of it over to a mobile platform. I'm going to try lots of different ways to do this, I guess part of the point of me doing it is to pick up new skills. I've decided that "<a title="Losing is fun" href="http://davidsherlock.co.uk/losing-is-fun/">losing is fun</a>" is my new philosophy for life and that I'm going to have fun and refuse to worry about any of my projects failing.

So as a web based project I was using a MySQL backend, the data of which is scrapped from dbpedia on a regular basis. Eventually I'd like all my code to use dbpedia data on the fly, I can dream. For now, however , I want to use my mysql database in my mobile app. This means turning it in to a flat file, more specifically sqlite3.

I thought this would be hard to do, but it was very easy. First I <a href="https://gist.github.com/esperlu/943776">downloaded this bash script</a> some nice github user saved as a gist, then I used the following command from the command prompt:
<blockquote>./mysql2sqlite.sh classroom_game -u username -ppassword  | sqlite3 database.sqlite</blockquote>
done!

This works on OS X and I suspect I used brew to install sqlite3 some time in the past. Not sure if Windows has an ability to use the Bourne again shell or if you will need Cygwin. If you are interested this chap <a href="http://www.reigndesign.com/blog/using-your-own-sqlite-database-in-android-applications/">explains how to then put a preloaded sqlite table in to your Android app</a>.