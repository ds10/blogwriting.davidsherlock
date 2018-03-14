---
ID: 2495
post_title: From MediaWiki to Github
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/from-mediawiki-to-github/
published: true
post_date: 2016-02-01 10:22:36
---
I have a very old mediawiki instance on a backup drive that I need to get the content off somehow, even though the content is old it is still relevant and I would still like people to be able to view it. It is slightly out of date so it would be good if the audience can still edit and update it but I can’t re-host the mediawiki instance, mainly because it is so old that I had to start up a VM with an old version of PHP just to get it working, but also because I don’t want the hassle of hosting mediawiki and protecting it from spam. Here was my recipe for getting content from a mediawiki instance to a Github repository.
<h2>Grab a HTML copy of your MediaWiki Instance</h2>
First I took a static copy of the mediawiki instance. Because of the old version of PHP the MediaWiki used I had to get it working on a virtual machine, then pointed wget to it to clone it. Wget should be avaliable from terminal if you have Linux, I had to install it via brew on OSX using
<pre class="lang:default decode:true">Brew install wget</pre>
and then copied the site with:
<pre><code>wget -mkEpnp &lt;URL&gt;</code></pre>
I don’t know about Windows, I would think there is something similar in Powershell or whatever the equivlient of that is these days, although you can download the <a href="https://eternallybored.org/misc/wget/">wget binary for windows here </a>if Windows doesn't offer anything sensible to do it with.
<h2>Create a Github repostory</h2>
You want to create a Github repository for your content; Github has a system called GitHub pages that will display your Markdown as a site. It's called <a href="https://pages.github.com/">Github Pages</a> and works using Jekyll, this is what I will be using to display the Wiki content. You can view the pages documentation for what works best for you, but the process is pretty much the same. I wanted to create an organisation and create an organisation page. To did this I had to create an organisation in the Github Settings and then create a repository with the name '&lt;organisationname&gt;.github.io' if you do this then github will automagiaclly create a site for you at &lt;organisationame&gt;.github.io .

I am generating a site from the a site called the XCRI wiki, so I created an organisation called xcri and repository called xcri.github.io.
<h2>Set Up Jekyll</h2>
I am not 100% sure that you need to do this on your local machine because Githhub does Jekyll magic on it's side, however without it you won't be able to debug locally very well. If you have <a href="https://rubygems.org/">Ruby Gems</a> installed then you can grab the github-pages Gem by running
<pre class="lang:default decode:true ">sudo gem install github-pages –v</pre>
at the command like. Or/and take a local copy of your new repository and a text file called Gemfile, in the text file add the following
<pre class="lang:default decode:true">Add gemfile to project:
source 'https://rubygems.org'
gem 'github-pages'
</pre>
&nbsp;

In terminal/CMD you need to navigate to your directory and run:
<pre class="lang:default decode:true ">bundle install</pre>
<h2>Convert from HTML to Markdown</h2>
I need to convert my Mediawiki HTML content to Markdown so that it is easy for people to view and edit in the repository, I used Pandoc to do that, so download <a href="http://pandoc.org/">pandoc</a> from the website, navigate in terminal to your MediaWiki mirror and run the following:
<pre class="lang:default decode:true ">for file in $(ls *.html); do pandoc -f html -t markdown "${file}" -o "${file%html}md"; done</pre>
Any remaining HTML I want to remove, I'm sure there is an easy sed/grep/awk way to do this, however I did it in a text editor, I used Text Wrangler, I'm sure BBedit etc can do the same:
<ol>
	<li>Open Text-Wrangler</li>
	<li> Click: Search =&gt; Multi-File Search</li>
	<li> In the Find field put:&lt;/?[^&gt;]*&gt;</li>
	<li>Check: Grep</li>
	<li>Click Replace All.</li>
</ol>
&nbsp;

For some reason Pandoc also added class names in curly brackets so I did the above again with: \{.*\}
<h2>Upload to Github</h2>
Copy the Markdown files to your local repository, add anything else you want and then sync with the remote repository. I use the Github desktop app, do it is just a case of pressing sync. Anybody who prefers the command line will already know what to type!

Here was the resulting repository: <a href="https://github.com/xcri/xcri.github.io">https://github.com/xcri/xcri.github.io</a>

And the generated site: <a href="http://xcri.github.io">http://xcri.github.io</a>