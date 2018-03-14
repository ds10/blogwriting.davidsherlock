---
ID: 1233
post_title: >
  Budget 2014. Conservative and Labour on
  Twitter
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/budget-2014-conservative-labour-twitter/
published: true
post_date: 2014-03-23 23:52:48
---
I've been playing with the Twitter API to see how easy it is to take stats about event backchat on Twitter. While playing with the API I noticed it was very easy to get data out which at first made me wonder why anybody even bothers with Twubs style tools, but the truth is the API limits and Terms and conditions are 1) not very easy to follow 2) Designed so you have to rely on the surrounding Twubs infrastructure. Still, I think that I am OK to store Tweets, as long as I don't go over the API limits, I store them locally and don't go over the 100,000 tweet storage limit. Saying that, I am pretty sure that these will rules will change and catch  to me out over time.

Still, I think there is some value in trying to save more than just the text surrounding an event. At present I think the the best way to do this is use the <a href="http://www.google.co.uk/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=3&amp;cad=rja&amp;uact=8&amp;ved=0CD0QFjAC&amp;url=http%3A%2F%2Fmashe.hawksey.info%2F2013%2F02%2Ftwitter-archive-tagsv5%2F&amp;ei=QG8vU5nWEqbB7Ab9hoGgBg&amp;usg=AFQjCNGmCrnSuauI44XyRoWjrX8YRz0WCA&amp;sig2=nNE9kFQqfx-G44LpZyMTSA&amp;bvm=bv.62922401,d.ZGU">TAGS</a> archiving service because it gives you the ability to analyse the Tweet after the event. The problem I found with this is this is that I didn't want to follow a a tag but wanted to follow a various groups of people or types of account. Perhaps TAGS does this, but I couldn't work it out. At first I tried some techniques to grab tweets from <a title="NOTES: Higher Education and Twitter. 10th -17th March" href="http://davidsherlock.co.uk/notes-higher-education-twitter-week-beginning-10th-march/">HE institution accounts</a>. The storing went OK, but the analysis fell flat.  I decided to try using the framework I came up with  while exploring HE accounts to try and do something specific around an event. I went with having a quick look at Twitter during the 2014 Budget because MPs on Twitter are comedy gold.
<h2>Tracking the 2014 Budget</h2>
I wanted to see what MPs were saying on the day rather than following a hashtag and to do this I built a spreadsheet of all the Tory and Labour MPs on Twitter. This was pretty easy to do as there are many lists of them on Twitter. PHP isn't the tool to do this in.. but I had it to hand, so sing twitteroauth I generated the spreadsheet using lists created by user Tweetminster. I did this twice, once for Labour and once for Tory, although it would have been quicker just to put an extra line in my code.. you get the idea.
<pre>$datas = $connection-&gt;get("https://api.twitter.com/1.1/lists/members.json?slug=labour&amp;owner_screen_name=Tweetminster&amp;cursor=4611686018448076708");

foreach($datas-&gt;users as $data){

$id = $database-&gt;insert("mp_accounts", [
"id" =&gt; $data-&gt;id,
"name" =&gt;$data-&gt;name,
"screen_name" =&gt; $data-&gt;screen_name,
"description" =&gt; $data-&gt;description,
"followers" =&gt; $data-&gt;followers_count,
"party" =&gt; "Labour"

]);

}</pre>
I think I am ok to share the spreadsheet, I'll double check first and then upload it to Google Drive. In fact there is already some interesting information there, I mean I wasn't expecting Ed Balls to lag behind Tom Watson in follower numbers. I then looped through the spreedsheet getting the latest Tweets for each user. I used a modified version of this to do so. Finally I deleted anything that was before or after budget day.
<h2>The dataset</h2>
From the resulting dataset is a list of tweets from MPS on budget day, I'm not sure where I stand on sharing it, if anybody could let me know I'd be happy to put it up. Some basic's I can pick up very basic information very fast:
<ul>
	<li>I managed to find, 397 MPs on Twitter, 199 Tory and 198 Labour</li>
	<li>Out of the 397, 316 MPs Tweeted on budget day, I thought this was pretty high!</li>
	<li>There were 2121 Tory Tweets, 1718 Labour Tweets,</li>
</ul>
<h2>Retweets</h2>
Its hard to get my head around how retweets work. I looked at most retweeted and it turns out that most of these were retweets in hemselves,  it counts everybody that has retweeted the tweet, also I took the dataset on friday night so the number may have changed since then. The most retweeted Tweet by an MP on budget day had 8258 retweets and was this by Andrew Gwynne and I doubt that it was him who generated the Retweets:
<blockquote class="twitter-tweet" lang="en">A Selfie in Space from <a href="https://twitter.com/NASA">@NASA</a> astronaut Mike Hopkins. RT if you think it beats the recent Oscars selfie! <a href="https://twitter.com/search?q=%23SpaceLive&amp;src=hash">#SpaceLive</a> <a href="http://t.co/buxEQ62FFX">pic.twitter.com/buxEQ62FFX</a>

— Live from Space (@SpaceLive) <a href="https://twitter.com/SpaceLive/statuses/443866164242812928">March 12, 2014</a></blockquote>
<script charset="utf-8" type="text/javascript" src="//platform.twitter.com/widgets.js" async="">// <![CDATA[
There were  s
// ]]></script>

There were quite a few popular tweets in my dataset that didn't actually originate from MPs and were just retweeted by them. I'll ignore these from now on. I bet you've already guessed the most retweeted tweet that originated from an MP and was about the budget:
<blockquote class="twitter-tweet" lang="en"><a href="https://twitter.com/search?q=%23budget2014&amp;src=hash">#budget2014</a> cuts bingo &amp; beer tax helping hardworking people do more of the things they enjoy. RT to spread the word <a href="http://t.co/5vbL7RDAg5">pic.twitter.com/5vbL7RDAg5</a>

— Grant Shapps MP (@grantshapps) <a href="https://twitter.com/grantshapps/statuses/446363611972534272">March 19, 2014</a></blockquote>
Prat. The next was from Osbourne and his plan to stimulate the economy by introducing a coin that will scratch our old phones and force us to buy new ones.
<blockquote class="twitter-tweet" lang="en">Today I will deliver a Budget for a resilient economy - starting with a resilient pound coin <a href="http://t.co/Ev2IuNpXg4">pic.twitter.com/Ev2IuNpXg4</a>

— George Osborne (@George_Osborne) <a href="https://twitter.com/George_Osborne/statuses/446190438949875712">March 19, 2014</a></blockquote>
&nbsp;
<h2>Content</h2>
Finally I wanted to see the difference in content of the Tweets. There are various online services I could use to analyse the text, or simply just use the R TM package. I'll have a think about this for next time. For now I just used R to create word clouds of Tory and Labour Tweets, I quite like word clouds because they give you a quick view of the contents of the text. I think you can see here that the main topics are similar with the words Budget and Budget2014 being the biggest in both images. The smaller words give you an insight in to what they thought about these topics, with Torys going for growth and employment and Labour going with 'outoftouch'.

[caption id="attachment_1241" align="aligncenter" width="461"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/tory_wordl_budget.png"><img class=" wp-image-1241" title="Word Cloud of Tory Tweets" alt="tory_wordl_budget" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/tory_wordl_budget.png" width="461" height="454" /></a> Word cloud of Tory Tweets[/caption]
<p style="text-align: center;"></p>


[caption id="attachment_1243" align="aligncenter" width="498"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/labour.png"><img class=" wp-image-1243" alt="labour" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/labour.png" width="498" height="481" /></a> Word cloud of Labour Tweets[/caption]
<p style="text-align: center;"></p>
So I can get stuff out quite easily and quickly. I've picked up that it's quite quick to get a framework on my locally machine to follow groups of people, but I wondered if there were any tools I could feed this information in to create a quick presentation. There is always Speaker Deck/ Slide Share but I'm not a big fan of those services, although I wonder if there is a way I can get my github to feed in to my Speaker Deck presentations?

I guess I'm getting there with the extraction bit, just need to know what to do with it!