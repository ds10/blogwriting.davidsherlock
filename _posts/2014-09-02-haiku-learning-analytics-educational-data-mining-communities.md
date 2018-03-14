---
ID: 1774
post_title: >
  Haiku from the Learning Analytics and
  Educational Data Mining communities
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/haiku-learning-analytics-educational-data-mining-communities/
published: true
post_date: 2014-09-02 09:11:45
---
There is a <a href="http://www.reddit.com/user/haiku_robot">bot on Reddit</a> that crawls through comments and looks for <a href="http://en.wikipedia.org/wiki/Haiku">haiku</a> in the text, I like the bot because everything has more of an emotional impact when it's written as a haiku, even Reddit comments. Inspired by this I had a look online and it turns out there are a few python libraries that will find haiku in text files for you. I opened my <a href="http://www.laceproject.eu/tech/2014/07/31/getting-latest-lak-dataset-r/">LAK14 R workspace,</a> which contains both stats and the contents of papers from various learning analytic conferences and wrote the contents of those papers to a text file (papers$content if you follow the method of grabbing LAK data in the link). I then  ran the python script to pick out a haiku or two and it turns out the learning analytics community are a poetic bunch. These haiku have have been generated from the <a href="http://lak.linkededucation.org">LAK dataset,</a> they were found using a special dictionary file that contains the number of syllables a word has and therefore will have missed any words unique to the community. The script doesn't look for seasons in the text either although I'm not sure if haiku actually have to mention a season or not, I'll ask my Japanese cultural expert @wilm. It picked up hundreds of haiku, but here are some of the best:
<p style="text-align: center;">A quick answer is
that there is more room to grow
for harder items.</p>
<p style="text-align: center;">The node is hidden,
so its value cannot be
observed directly.</p>
<p style="text-align: center;">Within the network
they indicate the people
they interact with.</p>
<p style="text-align: center;">What modalities
of learning can stimulate.
Learner engagement?</p>
<p style="text-align: center;">Thus, our model will
retain its ability
to detect “aha!”</p>
<p style="text-align: center;">Code size, time between
compilations and errors,
for Luca’s logfiles</p>
<p style="text-align: center;">I wonder if as
a 45 year old I
will feel differently.</p>
<p style="text-align: left;">My  favourite perhaps sums up educational datamining:</p>
<p style="text-align: center;">Are a few key words
enough to understand what
students are saying?</p>