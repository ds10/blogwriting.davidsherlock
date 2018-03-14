---
ID: 2046
post_title: Validating XCRI 1.2 with Schematron
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/validating-xcri-12-with-schematron/
published: true
post_date: 2011-09-23 09:31:18
---
I’ve started writing a Schematron ruleset that can be used to validate your own XCRI-CAP document so that you can get something that looks like this.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2011/09/screen-shot-2011-09-23-at-091113.png"><img class="aligncenter size-full wp-image-210" title="Validation" src="http://davidsherlock.co.uk/wp-content/uploads/2011/09/screen-shot-2011-09-23-at-091113.png" alt="Validation" width="714" height="331" /></a>

You can grab my <a href="https://code.google.com/p/xcri-schemas/source/browse/trunk/schematron/xcri12.iso.sch" target="_blank">work so far from google code</a>. So far the ruleset only checks the <a href="http://www.xcri.org/wiki/index.php/XCRI_1.2#Core_Elements" target="_blank">core elements</a> but I intend to work on it further soon. If your new to schematron you I recommend a scan of the <a href="http://www.schematron.com/" target="_blank">schematron site</a> and should be able to work out what to do with the ruleset by following the <a href="http://blogs.cetis.ac.uk/david/2010/01/07/validating-xcri-cap-using-schematron/" target="_blank">instructions on an old post of mine</a>.

If anybody feels the urge to update or improve the ruleset please feel free too :)