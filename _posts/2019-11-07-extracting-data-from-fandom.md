---
ID: 2702
post_title: Extracting data from fandom
author: David
post_excerpt: ""
layout: post
permalink: >
  http://davidsherlock.co.uk/extracting-data-from-fandom/
published: true
post_date: 2019-11-07 08:45:12
---
<!-- wp:paragraph -->
<p>I have not had much time to ‘techy things’ due to writing up
a thesis, finding myself this week with a few hours on a train try something
new. I decided , wanted to look at some data tools and techniques that had been
on my radar for a little while. I began by poking about some stuff on my list
that began with K: Kaggle, Knime and Keras. Being honest, I found looking
through examples of getting into these technologies very uninspiring and
boring; I’m not currently sure if I am ‘burnt out’ with technology or if I am
‘burnt out’ with examples that don’t interest me. Trying to find something
interesting to do I looked back on some of the things I had played with
previously. I have found that the most interesting data is on Wikipedia, and
have been fond of using DBpedia to extract interesting datasets. However,
Wikipedia has rules about what should and shouldn’t be on there, and articles must
be “worthy of notice”.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Looking for something interesting to poke about, I wondered
where I would find things “not worthy of notice”. Perhaps there is a shitty
Wikipedia with articles that nobody except the most hardcore enthusiasts cares
about? </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>It turns out there is; start started exploring Fandom.com ,a
website that hosts lots of Mediawiki instances for fans of obscure things, and &nbsp;decided I wanted to start to mine this
information in there, but fell into a few traps. Structured data still exists
in the infoboxes, but:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>There is no DBpedia or Wikidata for fandom, so there
is no way to query the data with sparql etc</li><li>The Mediawiki API seems to have been tampered
with. Or at least I couldn’t get wptools to work properly. Wptools does support
custom endpoints now, but it broke for me and I didn’t have the patience to work
out why. Help would be appreciated if anybody does use wptools with fandom</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Anyway, <a href="https://github.com/ds10/fandom_scraper">I wrote a very quick python script that will extract all the items in a category, then loop through them and scrape information from all their infoboxes</a>. It then writes this to a JSON file. The script is in GitHub: It is very quick and dirty, so you actually have to change the URL on to the category you want before running the code. Due to the never-ending pitfalls of web scraping, I don’t think I will update and maintain this but will look for other ways into the data; being a bunch of Mediawiki instances, it must be there!</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>The data is saved in a JSON file; each infobox item is the
key and result is the value. If a BR tag or something splits the value then it
will be converted into an array.</p>
<!-- /wp:paragraph -->