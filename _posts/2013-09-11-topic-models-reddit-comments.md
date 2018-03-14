---
ID: 311
post_title: Topic Models in Reddit Comments
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/topic-models-reddit-comments/
published: true
post_date: 2013-09-11 13:23:23
---
Recently a user at reddit wrote a post to scrape R comments; <a title="Scrapping Reddit comments" href="http://davidsherlock.co.uk/scrapping-reddit-comments/">I had a play with it here</a>. Today I had a very quick play of combining some stuff I've written for the Personal Corpus examination tool with the function I borrowed. I found it interesting but I haven't posted code up yet because 1) I'm still getting my head around the technique 2) Google 'Ben Marwick topic models' for lots of examples and better code than mind. If you still want to follow my project <a href="https://github.com/ds10/Personal-Corpus">I do have a github</a>, but its poorly organised and this bit of code isn't in it yet.

<strong>Anyway the jist is this:</strong>

1) I scrape comments from a a subreddit. I think the code I am borrowing only does it for the first page.

2) Each comment is classed as a document

3) I assume that each document can belong to multiple topics

4) I run some topic model algorithms using Mallet to work out what those topics may be

5) It generates 30 topics. It doesn't actually tell me what the name of those topics are. Just 5 words that are likely to be in that topic.

So I ran my code over r/ukpolitics with a front page made up of the years news. It came back with 30 topics, each with 5 words likely to be in that topic:

[1] "tax mps pay home london"
[2] "left thing political doesn't sort"
[3] "party labour vote ukip votes"
[4] "british minister prime empire britain"
[5] "illegal people immigrants set elected"
[6] "asked they've wait she's i've"
[7] "twitter called high call responsibility"
[8] "didn't back post page news"
[9] "points ago point months deleted"
[10] "choose debate women made rules"
[11] "home law civil service didn't"
[12] "thatcher people death state country"
[13] "find it's agree there's don't"
[14] "porn internet child page block"
[15] "wrong made train net force"
[16] "it's people don't make they're"
[17] "money interest wonga loans credit"
[18] "women men woman actions choices"
[19] "time dawkins food hear south"
[20] "children rape school society life"
[21] "good idea isn't won't class"
[22] "you're bit i'm it's i'd"
[23] "people that's things lot don't"
[24] "marriage rights gay equal civil"
[25] "system sense number fptp time"
[26] "it's people business fact case"
[27] "trade free europe media commonwealth"
[28] "free public liberal social market"
[29] "i'm don't can't fuck give"
[30] "segregation gender attendees security ucl"

Now some of these are obvious topics. Topic 14 is about a firewall proposed to block porn access at ISP level. 24 is about gay marriage. The ones I can't nail down are interesting too. Perhaps I need a bigger dataset?

While I improve on my code I may ask the author of the original scraping script for his thoughts and report back. I think I might also have a go on the reddit front page.

edit: Love topic 29