---
ID: 1633
post_title: >
  Getting information out of Google
  Scholar
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/getting-information-google-scholar/
published: true
post_date: 2014-08-01 15:00:16
---
The Google Scholar site doesn’t have an API, which is a shame and has left me to park one of my current projects on the sideline for now. I still spent half a day working out the best method to get information out of it so thought I would write up what I found in case it was useful to anyone else. The particular project I was working on was grabbing citations of papers and if anybody is interested it is parked because not all papers have a Cluster ID, which I naively assumed they would. It doesn’t seem worth going back and finding a work around as I’ve been down this route before trying to scrape things from websites only to find that they break after a UI tweak.

For those who still want a go at poking Google Scholar I found a python script called scholar.py, written by Christian Kreibich worked very well and can be accessed from <a href="https://github.com/ckreibich/scholar.py">Github here</a>. I found this forked repository by  <a href="https://github.com/sikoried/scholar.py">Korbinian Riedhammer</a> also adds the option to grab citations based on the Cluster ID.

It is easy to get started, on MAC OS X I went with
<ol>
	<li>sudo easy_install BeautifulSoup</li>
	<li><a href="https://github.com/sikoried/scholar.py"> Download script</a></li>
	<li>Try something like: scholar.py -c 1 --author "D Sherlock" --phrase "tools for online Habits"</li>
	<li>or  Or scholar.py --cites --cluster-id 13746912682491308133 for citations</li>
</ol>
&nbsp;