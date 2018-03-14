---
ID: 2047
post_title: >
  Developing a web analytics strategy for
  a distributed organisation
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/problems-when-creating-a-web-analytics-strategy-for-a-distributed-organisation/
published: true
post_date: 2011-11-02 13:48:30
---
For as long as I have been a web developer with CETIS we have relied on<a href="http://awstats.sourceforge.net/"> analysing server logs</a> to give an indication of traffic sources and visitor trends. This approach existed long before I joined CETIS and seemed like a logical way of doing things, CETIS has had many web servers and many different developers have installed different tools and resources and since they were all using the same servers and producing the same style logs it has been a reasonable method of producing comparable stats.

While this method of collecting stats has stayed the same over the life of CETIS, the direction of CETIS and the environment that it finds itself in has changed over time and a need for a new strategy has become apparent.

<strong>Challenges from JISC CETIS and the environment</strong>
<ul>
	<li>JISC CETIS is more distributed from a technical point of view</li>
</ul>
Historically CETIS has had access to physical servers that sat in a server room somewhere in a University. A recession later and shifts in University policies mean that the abundance of resource is no longer available. While there are lots of external providers are happy to help you produce a flexible service and tie you into their hosting packages it does raise issues. Do we have access to server logs?  Are the logs the same? If not then are the stats produced similar to the stats package we use? Can we even produce stats?

Similarly JISC CETIS is moving away from bespoke code when there are popular services that do the same thing and this raises similar questions.  What stats do the services produce, are they comparable with other services, is there an API and will we have to pay to access what we’ve collected down the line.
<ul>
	<li>JISC CETIS is more distributed from a people point of view</li>
</ul>
Staff in JISC CETIS are technologically savvy and have our opinions on the services and techniques that we like. While I think it is a good thing to have such a technically diverse organisation trying new and exciting things it is also a problem from a stats analysis point of view. Are staff hosting their blogs, events and resources on cloud services and if so how do we measure the use of these resources?
<ul>
	<li>A call for more sophisticated analytics</li>
</ul>
In JISC CETIS there is an increasing call to know more about the things we do and how they are used. It is important for any organisation to respond to its environment and the questions we are asking ourselves about our resources are becoming more and more complex. Log files can only give you so much information and it seems that Javascript solutions are needed to answer these questions. Recent improvements in solutions such as Google Analytics offer real in depth analysis of your web traffic and resource usage

<strong>Implementation Woes</strong>

A simple step that we have taken is to start to role out javascript tracking  with Google Analytics over the CETIS services, but even that simple act starts to highlight issues. The first thing we noticed was that visitor numbers were hardly comparable. Some early thoughts on why this might be:
<ul>
	<li>Google Analytics is more intelligent when it comes to what is and isn’t a visitor or a bot</li>
	<li>Google Analytics is Javascript based and will not count anything if the tracking code is not executed for some reason</li>
	<li>The hacks for Google Analytics to track binary files and RSS are not very good.</li>
</ul>
<strong>A hybrid solution</strong>

Despite the changing environment and early hiccups I feel positive about working towards a new web analytics strategy. I wrote this in an attempt to get my head around the issue and I think now I have some key starting ideas. I think that a hybrid solution is required as javascript solutions are more portable and answer more complex answers but are difficult to implement in such a distributed organisation and are held back by some of the limitations of javascript. I feel that we have to become more intelligence about how we analyse the data, my view is that analytics should be taken with a pinch of salt and that it is not about how high the figures are but about trends in these figures and that a good strategy for CETIS would be to identify places in its online resources with stats that can be compared and trends identified.

Finally I think that as organisations become more distributed and stats become more personal a web analytics strategy becomes more of an individual responsibility. I’m not quite sure what an effective strategy where analysis of individuals resources trends is helped to steer the organization as a whole would look like.

More to come...