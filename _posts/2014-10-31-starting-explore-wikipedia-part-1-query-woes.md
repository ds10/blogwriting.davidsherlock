---
ID: 1904
post_title: 'Starting to explore Wikipedia: Part 1. Query woes.'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/starting-explore-wikipedia-part-1-query-woes/
published: true
post_date: 2014-10-31 16:40:09
---
I've started to wonder, just how much can we find out about a subject from Wikipedia? I've been wondering if I can ask serious questions and big questions to the data set to get serious and big answers out. I thought I'd start by exploring an area of Wikipedia that was reasonably well maintained, I had a hunch that the video game community would keep their hobby and interest up to date and started there. While I keep saying Wikipedia, this data is from actually taken from the <a href="http://dbpedia.org/sparql">Dbpedia endpoint</a> , which is a mirror of Wikipedia that structures its data in a way that I can query. There are some things I have noticed, the data is not mirrored exactly, for example the Wikipedia page for the game <a href="http://en.wikipedia.org/wiki/Hawken_%28video_game%29">Hawken</a>  clearly states that the game engine is Unreal Engine 3, DBpedia says it uses the Unreal Engine but does not tell me which one. I don't know  why yet. Also the data set is frozen in time, this data set is frozen mid 2014. There is a l<a href="http://wiki.dbpedia.org/DBpediaLive%20">ive version of DBpedia</a> at but it seems to break for me, or at least for my SPARQL R package.

I decide to start on one very easy question, what are the different game engines that games use. I started with a very simple query:
<pre class="lang:default decode:true">SELECT ?game ?technology WHERE {
     ?game rdf:type dbpedia-owl:VideoGame ;
           dbpedia-owl:gameEngine ?technolgy .
}</pre>
Basically this pulls out all video games  that have a game engine, it made me think. The way data is structured in Wikipedia is not always consistent, making it hard to write the perfect query. For example, User A creates a page for their new game studio and uses a certain vocabulary to describe the city that their game studio is based in. User B creates a similar page for a different game studio but uses different vocab. When I write a query to grab all the cities that have game studios based in them I have to know what vocab they both used. As articles get more popular these sort of problems get ironed out as people standardise the vocab used. The other problem is that people can have different ideas of what things are; its no good telling me off because XNA is a language and not a game engine, because Wikipedia is reporting it as a game engine. In this reguard the process might be a good way of examining and reflecting on how your hobby is represented in Wikipedia than an actual answer to the question. The other thing this doesn't do is pull out the names of the games or the engines, I could pull them out using something like this:
<pre class="lang:default decode:true">SELECT ?gametile ?technolgytitle WHERE {

     ?game rdf:type dbpedia-owl:VideoGame .
     ?game foaf:name ?gametile .
     ?game dbpedia-owl:gameEngine ?technolgy .
     ?technology foaf:name ?technolgytitle .

}</pre>
But I started to notice all sorts of funny business in my results. If a game was described as using the Unreal Engine it would putt back the names for all of engines, that is Unreal Engine 1, 2, 2.5, and 4 but for other engines, such as Id Tech, it would just pull back the one correct name.

If you are interested, I went with the first query and a bit of regex to get the results, I counted them using plyrr in R, here are the top engines with more than 20 Games built on them.
<table>
<tbody>
<tr>
<td>Game Engine</td>
<td>Games Built On</td>
</tr>
<tr>
<td>Unreal Engine</td>
<td>313</td>
</tr>
<tr>
<td>Havok</td>
<td>132</td>
</tr>
<tr>
<td>Unity</td>
<td>114</td>
</tr>
<tr>
<td>RenderWare</td>
<td>84</td>
</tr>
<tr>
<td>Source</td>
<td>67</td>
</tr>
<tr>
<td>Gamebryo</td>
<td>60</td>
</tr>
<tr>
<td>Z-machine</td>
<td>49</td>
</tr>
<tr>
<td>LithTech</td>
<td>43</td>
</tr>
<tr>
<td>CryEngine</td>
<td>33</td>
</tr>
<tr>
<td>Adobe Flash</td>
<td>31</td>
</tr>
<tr>
<td>Id Tech 3</td>
<td>29</td>
</tr>
<tr>
<td>Torque</td>
<td>28</td>
</tr>
<tr>
<td>Sierra's Creative Interpreter</td>
<td>27</td>
</tr>
<tr>
<td>Ren'Py</td>
<td>26</td>
</tr>
<tr>
<td>Adventure Game Studio</td>
<td>24</td>
</tr>
<tr>
<td>PhysX</td>
<td>24</td>
</tr>
<tr>
<td>PopCap Games</td>
<td>24</td>
</tr>
<tr>
<td>Telltale Tool</td>
<td>24</td>
</tr>
<tr>
<td>GoldSrc</td>
<td>23</td>
</tr>
<tr>
<td>SCUMM</td>
<td>22</td>
</tr>
</tbody>
</table>
There is another thing fishy about this data. It is hard to believe that Id Tech is not in the list. It turns out that Id Tech IS on the list, but when a game lists Id Tech as it's Engine it has the correct Id Tech version as the attribute, where as Unreal has a more general Unreal Engine attribute.

I revisited my original SPARQL query and added the collection of dates to the query. This time I get less results, this is because I have asked the database to only return answers when it knows a year that the game was published, if there is no year there is no result. Some games have different release dates, I told the database to give me a random year. Looking back this was a bad idea because now it looks like remakes use the original engine (or originals use the remake engine) I don’t think I can find a method that will pull back the correct year with every release date when it comes to titles that were remade with different engines. Another thing to remember when writing my queries. This is what I went with:
<pre class="lang:default decode:true">SELECT ?game ?technolgy SAMPLE(?releasedate) WHERE {
     ?game rdf:type dbpedia-owl:VideoGame .
     ?game dbpedia-owl:gameEngine ?technolgy .
     ?game dbpedia-owl:releaseDate ?releasedate
}
ORDER BY ?game</pre>
I'm finding it hard to do what I want with the results when they come back as a dataframe in R. This could be because I find tools like ggplot2 hard as nails or because I'm not familar with how I should be structuring my results. Perhaps a problem for part 2. Anyway, I counted the results per year and saved as CSV, which for future reference that I'm sure I'm sure I will need:
<pre class="lang:default decode:true">df$year&lt;-substr(df$callret.2, 0, 4)
result&lt;-ddply(df2, .(technolgy, year), as.data.frame(nrow))
write.csv(result, file = "years.csv")</pre>
And just to see if it looked right, checked the popularity of the Unreal Engine per year:

[caption id="attachment_1910" align="aligncenter" width="356"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/10/Screen-Shot-2014-10-31-at-16.41.07.png"><img class="wp-image-1910 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2014/10/Screen-Shot-2014-10-31-at-16.41.07.png" alt="Unreal Engine Popularity per year according to wikipedia" width="356" height="215" /></a> Unreal Engine Popularity per year according to wikipedia[/caption]

Those that know your games might think that the numbers look low for such an engine. I think it does look low, and it is more to think about when trying to ask Wikipedia for answers. These are only articles with games that state they use Unreal and have a release date in my dataset. Because of this I thought I should look at trends rather than actual numbers. The trend shows a growth in the popularity of the Unreal engine up until 2014, most of this makes sense to me:
<ul>
	<li>Unreal Engine usage growth has seen growth year on year</li>
	<li>The dataset was frozen in the middle of 2014, I guess many entry’s for 2014 games aren’t as mature as older games, or the entry doesn’t exist yet</li>
	<li>Games in the future are pages created about a game that hasn’t been released yet.</li>
</ul>
Still, I was curious as to why we saw some games in 2018, that seems a long way off for a developer to be releasing information about a game engine they intend to use for a future game. Intrigued I looked up the 2018 game only to find out that it was an old game, released a few years ago that Wikipedia has an incorrect release data for (at the time the data set was frozen). So.. Wikipedia can be wrong.

Time to carry on playing...