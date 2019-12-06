---
ID: 2720
post_title: >
  Installing R scripting Extension in
  Knime
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/installing-r-scripting-extension-in-knime/
published: true
post_date: 2019-12-06 17:06:00
---
<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Setting up R for use in Knime is pretty easy, the biggest issue is usually forgetting to install the Rserve package, or not realising that you need additional tools to compile Rserve from Source as Knime suggests you do, chances are you are getting the error:  <em>ERROR: configuration failed for package ‘Rserve’ .</em></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li> First, you need to install R. Just head over to the<a href="https://cran.r-project.org/"> CRAN repository</a> and click download. When installing remember the install location</li><li>You then need to install the install the Knime R Statisitics Integration packages, just open KNIME, goto help-> install new software. Select the analytics-platform repository and search for r stat and install. See the below image.</li></ul>
<!-- /wp:list -->

<!-- wp:image {"id":2722,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="https://davidsherlock.co.uk/wp-content/uploads/2019/12/knime_6pfjSOcqWU.png" alt="" class="wp-image-2722"/></figure>
<!-- /wp:image -->

<!-- wp:list -->
<ul><li> Set up R in Knime, by going to file->preferences->knime->r and set the path, like in the image below  </li></ul>
<!-- /wp:list -->

<!-- wp:image {"id":2723,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="https://davidsherlock.co.uk/wp-content/uploads/2019/12/knime_0qSeCVriTn.png" alt="" class="wp-image-2723"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Installing Rserve</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>This is the bit that that seems to trip most people. The issue
is that there is no binary for Rserve, at least on Windows, so Knime gives you the
following command to install the Rserve package:</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">install.packages('Rserve',,'http://rforge.net/',type='source')</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>What it doesn’t tell you is that on Windows you won’t be
able to compile from source without Rtools install. Head over to the Rtools
site (https://cran.r-project.org/bin/windows/Rtools/) and install. During the
install process it might ask if you want to add the rtool binary to PATH, make
sure that you say yes.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>You are good to go! Here is a quick video of the process</p>
<!-- /wp:paragraph -->

<!-- wp:core-embed/youtube {"url":"https://www.youtube.com/watch?v=DC95yTgEa8I","type":"video","providerNameSlug":"youtube","className":"wp-embed-aspect-16-9 wp-has-aspect-ratio"} -->
<figure class="wp-block-embed-youtube wp-block-embed is-type-video is-provider-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper">
https://www.youtube.com/watch?v=DC95yTgEa8I
</div></figure>
<!-- /wp:core-embed/youtube -->