---
ID: 1195
post_title: 'ggplot notes: Line Graph'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/plotting-line-graph-over-time-using-two-columns-in-dataframe-in-r/
published: true
post_date: 2014-03-14 09:36:15
---
Quite often I have a dataframe in R with lots of columns with one of the columns being the year. I then want to pick another column and make averages for each year and plot it to show how things have changed over time. I know this is really easy to do, but I end up Googling it every time, I thought that this time I'd write it up so I knew exactly where to look. I won't go in to detail on what the commands do, or how to make the graph look funky.
<h2>Grab the data</h2>
In this example I have a dataframe of movies from IMDB and facts about. It looks something like this when I view it in R studio:

[caption id="attachment_1196" align="aligncenter" width="676"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/movie_dataset_ggplot.png"><img class="size-full wp-image-1196" alt="movie_dataset_ggplot" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/movie_dataset_ggplot.png" width="676" height="284" /></a> Movie dataset has title, year, length among other things[/caption]

This dataset actually comes with ggplot2, if you've installed ggplot to you can get it using 'movies'. Normally I want to use the year as the X axis, and then I want to find average of something for the Y axis, and group it by year, but I always forget how to. In this example I'll plot the average length of movies for each year in the dataset.
<h2>Grab the ggplot and plyr libraries:</h2>
The first thing I need are ggplot and plyr packages. Assuming they are installed:
<blockquote>library(ggplot2)
library(plyr)</blockquote>
The I create a new dataframe that only has two columns, the year and mean. There may be a shortcut, but I just like to do things in steps:
<blockquote>mean_df&lt;-ddply(movies, .(year), summarize, mean_value = mean(length))</blockquote>
You can then see the new dataframe has years and the mean length:

[caption id="attachment_1197" align="aligncenter" width="177"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/average.png"><img class="size-full wp-image-1197" alt="average" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/average.png" width="177" height="285" /></a> Year and mean[/caption]
<p style="text-align: left;">It is now very easy to plot them:</p>

<blockquote>
<p style="text-align: left;">ggplot(data=mean_df, aes(x=year, y=mean_value)) + geom_line() + geom_point()</p>
</blockquote>
<p style="text-align: left;">Which should leave you something like this:</p>
<p style="text-align: left;"><a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/average_length_of_movies.png"><img class="aligncenter size-full wp-image-1198" alt="average_length_of_movies" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/average_length_of_movies.png" width="560" height="442" /></a>Final code:</p>
<p style="text-align: left;">[codesyntax lang="text"]</p>

<pre>install.packages("ggplot2")
library(ggplot2)
movies&lt;-movies
library(plyr)
mean_df&lt;-ddply(movies, .(year), summarize, mean_value = mean(length))
ggplot(data=mean_df, aes(x=year, y=mean_value)) + geom_line() + geom_point()</pre>
<p style="text-align: left;">[/codesyntax]</p>
<p style="text-align: left;">On another note sometimes I like to use values from multiple columns. In the movies dataset we have counts for the number of different genres of films. I think this is just how IMDB decide to label things, but it is still a useful example to write up for when I forget 2 months down the line. The code is:</p>

<blockquote>
<p style="text-align: left;">mean_df&lt;-ddply(movies, .(year), summarize, action_films = sum(Action), animation_films = sum(Animation), comedy_films = sum(Comedy), drama_films = sum(Drama),  documentry_films = sum(Documentary) ,  romance_films = sum(Romance), short_films = sum(Short) )</p>
ggplot(data=mean_df, aes(x=year, y=mean_value)) + geom_line() + geom_point()
ggplot(mean_df, aes(year)) +
geom_line(aes(y = action_films, colour = "action_films")) +
geom_line(aes(y = animation_films, colour = "animation_films")) +
geom_line(aes(y = comedy_films, colour = "comedy_films")) +
geom_line(aes(y = drama_films, colour = "drama_films")) +
geom_line(aes(y = romance_films, colour = "romance_films")) +
geom_line(aes(y = documentry_films, colour = "documentry_films")) +
geom_line(aes(y = short_films, colour = "drama_films"))
)</blockquote>
<p style="text-align: left;">which gives you something like this:</p>
<p style="text-align: left;"><a href="http://davidsherlock.co.uk/wp-content/uploads/2014/03/movies_by_genre.png"><img class="aligncenter size-full wp-image-1202" alt="movies_by_genre" src="http://davidsherlock.co.uk/wp-content/uploads/2014/03/movies_by_genre.png" width="543" height="445" /></a></p>
<p style="text-align: left;"></p>