---
ID: 2040
post_title: Validating XCRI-CAP using Schematron
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/validating-xcri-cap-using-schematron/
published: true
post_date: 2010-01-07 13:28:44
---
Here I hope to give a quick start on how to use <a href="http://www.schematron.com/">Schematron</a> with your XCRI-CAP documents to give useful feedback.

The instructions here were originally tested on OS X but should also work on Windows or your Linux disto of choice providing you have Java. If there are any differences I am not aware of please leave a comment.
<h2>Setting up your environment</h2>
You will need:

•	ISO Schematron
•	A Schematron Schema
•	An XLST processer
•	An XCRI-CAP document for validation.

<strong>ISO Schematron</strong>
We’ll be using ISO Schematron, which is available for download from the <a href="http://www.schematron.com/" target="_blank">schematron website</a>: The file we want is iso-schematron-xslt2.zip, I recommend unzipping it to your desktop and renaming it schematron. Place the XCRI-CAP document you wish to validate into this directory.

<strong>Processor</strong>
The schematron schema is transformed into a XLST stylesheet using a XLST processor; in this example I am going to use <a href="http://saxon.sourceforge.net/" target="_blank">Saxon-B for Java</a>, which is an open source XSLT processor.

Once downloaded you will need to add saxon.jar to your classpath.  On OS X 10.5+ you can place it into your /Library/extensions/Java directory.

<strong>Schematron Schema</strong>
A Schematron schema is needed validate against your XCRI-CAP XML document. The schema takes the form of xpath expressions; I have written one based on <a href="http://www.xcri.org/wiki/index.php/XCRI_Course_Advertising_Profile" target="_blank">XCRI-CAP 1.1</a> which you can <a href="http://jisc.cetis.ac.uk/downloads/xcri.iso.sch" target="_self">download here</a>; feel free to use and modify. Once downloaded place into your schematron directory. You will also <a href="http://jisc.cetis.ac.uk/downloads/postcodes.xml">need this list of postcodes.</a>
Now you should now have a directory named schematron with multiple files; it is important that you have the following five:

•	iso_svrl_for_xlst2.xsl
•	iso_schematron_skeleton_for_saxon.xsl
•	xcri.iso.sch
•	postcodes.xml
•	your own XCRI-CAP document!
<h2>Validating your XCRI-CAP documents</h2>
First we need to create an xsl stylesheet which will be used as the validation engine against our XCRI-CAP document.
Open a terminal/prompt navigate to your schematron directory and issue the following command:
<p style="text-align: left"><em>java net.sf.saxon.Transform -o xcri.iso.sch.tmp.xsl -s xcri.iso.sch iso_svrl_for_xslt2.xsl</em></p>

This will use the Saxon processor we installed earlier to compile the schema into an XLST stylesheet (xcri.iso.sch.tmp.xsl) using our schema, Schematron xsl and the Saxon processor. The next step is to use the file we have created against our XCRI-CAP document to create an error report. To do this run the following changing 'myfile.xml' to the name of your document:
<p style="text-align: left"><em>java net.sf.saxon.Transform -o errors.report.xml -s  myfile.xml xcri.iso.sch.tmp.xsl</em></p>

You should now have an error report called errors.report.xml. The report is in SVRL format which is a simple language defined in ISO schematon. SVRL can be used as the basis for further transformations and to demonstrate this I have written a small xsl which you can use to transform this into an HTML document. If you wish to do so, <a href="http://jisc.cetis.ac.uk/downloads/svrl_transformer.xsl" target="_self">download to your schematron directory</a>, make any modifications you require and use the following:
<p style="text-align: left"><em>java net.sf.saxon.Transform -o errors.html errors.report.xml svrl_transformer.xsl</em></p>

You should now have the HTML document of errors in your schematron directory  errors.html

<strong>Line Numers</strong>
You should now be producing feedback on your XCRI-CAP documents and producing a simple html document of errors. If you are using a version of Saxon that allows access to its extensions then you we can use the <em>saxon</em>:<em>line</em>-<em>number</em><em>() </em>extension to report line numbers.

To do so replace these files in your schematron directory with these modified versions:

<a href="http://jisc.cetis.ac.uk/downloads/iso_svrl_for_xslt2.xsl" target="_self">iso_svrl_for_xslt2.xsl</a>

<a href="http://jisc.cetis.ac.uk/downloads/iso_schematron_skeleton_for_saxon.xsl" target="_self">iso_schematron_skeleton_for_saxon.xsl</a>

And run though the validation steps again with the -l flag set. eg:

<em>java net.sf.saxon.Transform -l -o xcri.iso.sch.tmp.xsl -s xcri.iso.sch iso_svrl_for_xslt2.xsl

java net.sf.saxon.Transform -l -o errors.report.xml -s  myfile.xml xcri.iso.sch.tmp.xsl

java net.sf.saxon.Transform -l -o errors.html errors.report.xml svrl_transformer.xsl</em>


Don't have time to give it a go? You can use the 'beta' web based validator that will validate your XCRI-CAP document using the same steps shown in this post. You can find the validator a:

<a href="http://galadriel.cetis.ac.uk/XCRIValidator/">http://galadriel.cetis.ac.uk/XCRIValidator/</a>

Comments very welcome!