---
ID: 2283
post_title: A quick Reddit autoreply bot
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/a-quick-reddit-reply-bot/
published: true
post_date: 2015-04-30 10:37:59
---
Similar to my last <a href="http://davidsherlock.co.uk/twitter-questionrevision-bot/">*nix style project</a> I wanted to write something in Python that could interact with Reddit and can be ran from a Raspberry Pi. At this stage I only wanted to see what was possible and start early, so I borrowed some code to make a bot that scanned a subreddit for a certain phrases and then replied to those comments. Similar to last time there are basically only 2 steps:
<h2>1. Setting up a *nix environment to handle it.</h2>
This project is for the Raspberry Pi so I need to make sure it works on Linux. The only things you really need is Python which comes with most *nix systems and the PRAW module which can installed with:
<blockquote>pip install praw</blockquote>
PRAW is the Python Reddit API Wrapper and gives you access the wrapper quite easily.

On Windows you will need to install Python, it should be quite easy and you can follow the instructions on the <a href="https://www.python.org/downloads/">Python site</a>. As far as I am aware pip is installed in the Windows installation too.
<h3>2. Write and run the script</h3>
Start a text document with your favorite editor, save it as something like redditreply.py and copy the following script written by <a href="http://www.reddit.com/user/shaggorama">/u/shaggorama</a>
<pre class="lang:default decode:true">import praw
from praw.helpers import comment_stream

r = praw.Reddit("Change me")
r.login()

target_text = "text"
response_text = "text"

processed = []
while True:
    for c in comment_stream(r, 'all'):
        if target_text in c.body and c.id not in processed:
            c.reply(response_text)
            processed.append(c.id)</pre>
You need to change some bits, 'change me' is the name of the user agent. The target_text is text in comments that your script will look for and response_text is the reply that your post will respond with. You need to change 'all' to the subreddit you wish to run the bot over. I used /r/sandboxtest which is a subreddit for bots.

Once you have changed the text you will need to run the script with
<blockquote>python redditreply.py</blockquote>
The script will ask you for the username and password of the bot and will then go away and reply to lots of comments. My next challenge and perhaps <a href="https://mashe.hawksey.info/2015/04/creating-a-twitter-questionrevision-bot-using-google-sheets/">tomorrows post is to turn this in to a Google Script</a>.
<h2>Got lost? Here is a video of the process:</h2>
https://youtu.be/Z8-7coYMJRk