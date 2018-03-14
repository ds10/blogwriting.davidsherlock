---
ID: 2041
post_title: Deploying Content Transcoder
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/deploying-content-transcoder/
published: true
post_date: 2010-04-28 11:22:55
---
I have had a few requests for help on deploying the <a href="http://purl.oclc.org/NET/transcoder" target="_blank">Content Transcoder</a> on a local machine. The process is simple but has one or two gotchas. I have done this on OS X and Ubuntu but it should be pretty similar  on Windows.

You will need:

<a href="http://java.com/en/" target="_blank">Java</a>

<a href="http://tomcat.apache.org/download-60.cgi" target="_blank">Tomcat 6.x</a> As far as I can tell it must be 6+ since the transcoder doesn't seem to play nice with the XSLT processor packed with earlier versions.

<a href="http://projects.k-int.com:8081/nexus-webapp-1.4.0/content/repositories/snapshots/com/k-int/transcoder/transcoder-web/1.0-SNAPSHOT/" target="_blank">Latest snapshot build of the </a><a href="http://projects.k-int.com:8081/nexus-webapp-1.4.0/content/repositories/snapshots/com/k-int/transcoder/transcoder-web/1.0-SNAPSHOT/" target="_blank">transcoder</a>.  You are looking for the latest modified .war file. Once downloaded you will want to rename it transcoder.war

<strong>Set up Tomcat</strong>

1)You will need to unpack tomcat; I unpacked mine to the desktop.

2)Set permissions on Tomcat directory; I opened  a terminal (/Applications/Terminal) and typing something along the following:

sudo chmod -R 755  /Users/david/Desktop/tomcat/

You may also need to set the environment variable JAVA_HOME.  On OS X you may find <a href="http://www.mehtanirav.com/2008/09/02/setting-java_home-on-mac-os-x-105" target="_blank">this guide </a>helpful.  On Windows Right click computer-&gt;properties and go to the Advanced tab. Select Environment Variables and add JAVA_HOME setting it to point at the JDK. i.e c:Program FilesJavajdk1.*

<strong>Deploy Transcoder</strong>

Deploying the transcoder is as simple as placing the war file into your /tomcat/webapps folder. Tomcat will do the dirty work for you.

<strong>Run Tomcat</strong>

Tomcat can then by run running the startup.sh script or startup.bat for windows; in your terminal this can by done by  something like this:

/Users/david/Desktop/tomcat/bin/startup.sh

Now you should be able to see tomcat in your web browser at <a href="http://localhost:8080" target="_blank">localhost:8080</a> and transcoder at <a href="http://localhost:8080/transcoder" target="_blank">localhost:8080/transcoder</a>.

<strong>Tweek Transcoder configurations</strong>

You may want to make some changes to how transcoder is set up. You will need to change the configuration to use Apache Derby instead of the default MySQL. This can be done by editing the file at:

tomcat/webapps/transcoderWEB-INF/deployment.properties

This should be a text file with two sets of properties with the bottom set commented out, you need to switch these around so the files look like this:

#hibernate.jdbc_driver=org.gjt.mm.mysql.Driver
#hibernate.username=k-int
#hibernate.password=k-int
#hibernate.default_auto_commit=false
#hibernate.url=jdbc:mysql://localhost/transcoder
#hibernate.hbm2ddl.auto=update
#hibernate.dialect=org.hibernate.dialect.MySQLDialect

hibernate.jdbc_driver=org.apache.derby.jdbc.EmbeddedDriver
hibernate.username=APP
hibernate.password=APP
hibernate.url=jdbc:derby:derbydb;create=true
hibernate.dialect=org.hibernate.dialect.DerbyDialect
hibernate.default_auto_commit=false
hibernate.hbm2ddl.auto=update

<strong>Restart tomcat</strong>

You may then wish to stop and start tomcat:

Users/david/Desktop/tomcat/bin/shutdown.sh

Users/david/Desktop/tomcat/bin/startup.sh

On windows you are looking for startup.bat and shutdown.bat

Now you should be ready to go simply by pointing your favorite web browser at localhost:8080/transcoder

<strong>Help its not working!</strong>

<em>I see tomcat at localhost:8080 but nothing at localhost:8080/transcoder.</em>
If you didn't rename your war you will need to navigate to localhost:8080/transcoder-web-****

<em>I see transcoder but it won't convert packages.</em>
If you changed the properties above and still have no luck the chances are that your JAVA_HOME is not set correctly. <a href="http://www.google.co.uk/search?hl=en&amp;client=firefox-a&amp;hs=725&amp;rls=org.mozilla%3Aen-US%3Aofficial&amp;q=set+java_home+tomcat+6&amp;meta=&amp;aq=f&amp;aqi=&amp;aql=&amp;oq=&amp;gs_rfai=" target="_blank">Google and a bit of tinkering should sort you out</a>.