---
ID: 2263
post_title: Creating a Twitter Question/Revision Bot
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/twitter-questionrevision-bot/
published: true
post_date: 2015-04-29 09:34:52
---
I recently wanted to a CSV of questions and answers in to a Twitter account that tweeted questions followed by the correct answers every hour like so:
<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/twitter-revision.png"><img class="alignnone size-full wp-image-2279" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/twitter-revision.png" alt="twitter revision" width="610" height="431" /></a>

My CSV looks like this when opened in excel. There are 5 columns in each row, the first of which is the question, followed by a description of the answer, the answer itself and two incorrect answers. For this project I am not going to use the description of the answer in the second column, although I will be leaving it in for a different project.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/04/bilogyrevision.png"><img class="alignnone size-full wp-image-2270" src="http://davidsherlock.co.uk/wp-content/uploads/2015/04/bilogyrevision.png" alt="Biology Revision Spreadsheet" width="800" height="301" /></a>

The process is broken down in 4 parts with a few steps in each.
<h2>1. Setting up a *nix environment to handle it.</h2>
I wanted to do this on a Raspberry Pi because it is cheap to leave on all day and I wanted to do a bunch of other stuff with it. Also I can leave the Pi on and it can push tweets to the account 24/7. Unfortunately I don't actually have a Raspberry Pi yet, I am doing this on OS X tho so the process is very similar and should be easy to follow. When I do get a Pi I will update the tutorial accordingly!

The only things I really need are Python and Cron, both of which are available on *nix systems. If you are using windows then you will have to find a way yourself to periodically run my script.

Python is already installed on MAC OS X and should be on Debian based systems. The script uses the Tweepy package which will not be installed and needs to be via:
<blockquote>pip install tweepy</blockquote>
<h2>2. Create a twitter APP</h2>
To use the Twitter API you need to create an application. I've found this to be a real pain recently as Twitter seems to be turning its back on small time developers having fun to concentrate on the big customers, I quite often get all sorts of unexplained errors while creating an app, these errors  appear to be an attempt to crack down on small time developers having a good time. To combat this it seems best to use an account that has been active for a while and has a mobile phone number associated with it.

You need to sign in to https://apps.twitter.com/ and create a new app, the details you fill in when creating the account are not that important and you can leave the callback URL blank. Once you've created the application you will see a bunch of information about your application, you need to make note of 4 things:
<ul>
	<li>consumer key</li>
	<li>secret key</li>
	<li>access key</li>
	<li>access secret</li>
</ul>
<h2>3. Write a Python Script</h2>
I want my twitter account to do the following:
<ol>
	<li>Pick a random question</li>
	<li>Tweet the Question</li>
	<li>Shuffle the answers</li>
	<li>Tweet the 3 options</li>
</ol>
The script below imports the modules we need, opens a CSV file,
<pre class="lang:default decode:true">import tweepy, time, sys
import random
import csv

CONSUMER_KEY = 'xxxxxx' #keep the quotes, replace this with your consumer key
CONSUMER_SECRET = 'xxxxxx'#keep the quotes, replace this with your co$
ACCESS_KEY = 'xxxxxx'#keep the quotes, replace this with your access $
ACCESS_SECRET = 'xxxx'#keep the quotes, replace this with your access to$
auth = tweepy.OAuthHandler(CONSUMER_KEY, CONSUMER_SECRET)
auth.set_access_token(ACCESS_KEY, ACCESS_SECRET)
api = tweepy.API(auth)

f = open('bio.csv', 'rU')
ran = random.randint(1,(len(f.readlines())))

f = open('bio.csv', 'rU')
csv_f = csv.reader(f)
tweet = ""
i = 0

for row in csv_f:
    i = i + 1
    if i == ran:
        tweet =  "Q: " + row[0]
        tweet2 =  row[2]
        tweet3 =  row[3]
        tweet4 =  row[4]

api.update_status(tweet)

array=[tweet2,tweet3,tweet4]

random.shuffle(array)

api.update_status("A: " + array[0])
api.update_status("B: " + array[1])
api.update_status("C: " + array[2])

</pre>
<h2>4. Time the script to run every hour or so</h2>
You need to add this script to add this to Cron, a system for scheduling bash commands ran at a scedule:

&nbsp;
<ul>
	<li>In Terminal: <code>crontab -e</code>.</li>
	<li>Press <kbd>i</kbd> to go into vim's insert mode.</li>
	<li>Type:
<pre><code>0,30 * * * * python &lt;path to python file&gt;
</code></pre>
</li>
	<li>Press Esc to exit vim's insert mode.</li>
</ul>
This will run the script every 30 minutes

&nbsp;

<script>// <![CDATA[
!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+"://platform.twitter.com/widgets.js";fjs.parentNode.insertBefore(js,fjs);}}(document,"script","twitter-wjs");
// ]]></script>