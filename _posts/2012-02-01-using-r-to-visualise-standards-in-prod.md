---
ID: 2050
post_title: >
  Standards used in JISC programmes and
  projects over time
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/using-r-to-visualise-standards-in-prod/
published: true
post_date: 2012-02-01 22:03:15
---
Today I took part in an introduction to R workshop being held at The University of Manchester. <a href="http://www.google.co.uk/url?sa=t&amp;rct=j&amp;q=r&amp;source=web&amp;cd=1&amp;ved=0CCwQFjAA&amp;url=http%3A%2F%2Fwww.r-project.org%2F&amp;ei=AKIpT9KJMM_NsgaN1vTEAQ&amp;usg=AFQjCNFq9BSTD_8y4svhPlIv_58OxEpd5A&amp;sig2=Hku39B5LDfsqbq84tGVhnA">R</a> is a software environment for statistics  and while it does all sorts of interesting things that are beyond my ability one thing that I can grasp and enjoy is exploring all the packages that are available for R, these packages extend Rs capabilities and let you do all sorts of cool things in a couple of lines of code.
<p style="text-align: left">The target I set out for myself was to use <a href="http://prod.cetis.ac.uk">JISC CETIS Project Directory</a> data and find a way of visualising standards used in JISC funded projects and programmes over time. I found a Google Visualisation package and using this I was surprised at how easy it was to generate an output , the hardest bits being manipulating the data (and thinking about how to structure it).  Although my output from the day is incomplete I thought I’d write up my experience while it is fresh in my mind.</p>

First I needed a dataset of projects, start dates, standards and programme. I got the results in CSV format by using the sparqlproxy web service that<a href="https://docs.google.com/document/pub?id=1i4STANwqrEy_XjAewo12OjWq3ZCe0tRosUhNGvhAoo0"> I use in this tutorial</a> and stole and edited a query from <a href="https://docs.google.com/document/d/1atVIAjKoZl1dUzq7jYys0c7ObMVMULmuC_eZXlMhDh8/edit?hl=en_US">Martin</a>

Sparql:
<blockquote>PREFIX rdfs:
PREFIX jisc:
PREFIX doap:
PREFIX prod:
SELECT DISTINCT ?projectID ?Project ?Programme ?Strand ?Standards ?Comments ?StartDate ?EndDate
WHERE {
?projectID a doap:Project .
?projectID prod:programme ?Programme .
?projectID jisc:start-date ?StartDate .
?projectID jisc:end-date ?EndDate .
OPTIONAL { ?projectID prod:strand ?Strand } .
# FILTER regex(?strand, "^open education", "i") .
?projectID jisc:short-name ?Project .
?techRelation doap:Project ?projectID .
?techRelation prod:technology ?TechnologyID .
FILTER regex(str(?TechnologyID), "^http://prod.cetis.ac.uk/standard/")  .
?TechnologyID rdfs:label ?Standards .
OPTIONAL { ?techRelation prod:comment ?Comments } .
}</blockquote>
From this I created a pivot table of all standards, and how much they appeared in each projects and programmes for each year (using the project start date). After importing this into R, it took two lines to grab the google visualisation package and plot this as Google Visualisation Chart.
<blockquote>library("googleVis")
M = gvisMotionChart(data=prod_csv, idvar="Standards", timevar="Year", chartid="Standards")</blockquote>
Which gives you the 'Hans Rosling' style flow chart. I can't get this to embed in my wordpress blog, but you can click the diagram to view the interaction version. The higher up a standard is the more projects it is in and the further across it goes the more programmes it spans.

<a href="http://galadriel.cetis.ac.uk/david/tmp.html"><img class="aligncenter size-full wp-image-273" title="Google Visualisation Chart" src="http://blogs.cetis.ac.uk/david/wp-content/uploads/sites/3/2012/02/hr.png" alt="Google Visualisation Chart" width="639" height="514" /></a>

Some things it made me think about:
<ol>
	<li>Data from PROD is inconsistent</li>
Standards can be spelt differently; some programmes/projects might have had a more time spent on inputting related standards than others
	<li>How useful is it?</li>
This was extremely easy to do, but is it worth doing? I feel it has value for me because its made me think about the way JISC CETIS staff use PROD and the sort of data we input. Would this be of value to anybody else?  Although it was interesting to see the high number of projects across three programmes that involved XCRI in 2008.
	<li>Do we need all that data?</li>
There are a lot of standards represented in the visualisation. Do we need them all? Can we concentrate on subsets of this data.</ol>