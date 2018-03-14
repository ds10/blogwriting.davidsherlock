---
ID: 204
post_title: 'cannot allocate a new connection &#8212; maximum of 16 connections already > opened)'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/cannot-allocate-a-new-connection-maximum-of-16-connections-already-opened/
published: true
post_date: 2013-07-25 10:30:03
---
I'm currently trying to write an application in Shiny that talks to a MySQL database. While developing I got the following error message after I has started the server a few times:
<blockquote>
    <p>cannot allocate a new connection -- maximum of 16 connections already &gt; opened)</p>
</blockquote>
It turns out that the following line was opening connections and keeping them open:
<blockquote>
    <p>mydb = dbConnect(MySQL(), user='xxx', password='xxx', dbname='xxx', host='xxx')</p>
</blockquote>
The solution was to loop through any connections and delete them:
<blockquote>
cons<-dbListConnections(MySQL())
for(con in cons)
  dbDisconnect(con)
</blockquote>