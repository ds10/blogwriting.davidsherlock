---
ID: 10
post_title: 'Widgets for Wookie: Getting Started'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/widgets-for-wookie-getting-started/
published: true
post_date: 2008-08-18 10:50:25
---
<em>Update: Downloading and running Wookie has changed since this was written and some of the links seem broken. please check http://incubator.apache.org/wookie/downloading-and-installing-wookie.html for latest instructions</em>

The Wookie server is open source software in development for delivering collaborative widgets that follows the w3c widget specification. Although it is early days for Wookie I desperately wanted to try my hand at writing some widgets; along the way I found that online tutorials were often written for specific platforms (Yahoo, Mac, etc) and it was quite daunting for the first few attempts.
<h2>Getting Started</h2>
First you will need download and install the Widget Server.  The easiest method is to use the 'Quick Start Distribution' which is offered by the  <a href="http://www.tencompetence.org/ldruntime/" target="_blank">Tencompetence Website</a> and includes:
<ul>
	<li>CopperCore Runtime Environment(CCRT)</li>
	<li>Sled Player</li>
	<li>Widget Server</li>
</ul>
The Quick Start Distribution is available <a href="http://www.tencompetence.org/ldruntime/downloads/ccrt_3.1_widget_system_v1_2_1.zip">here</a>

Once you have downloaded the environment unzip it with your favorite compression tool and run the file coppercore.bat.  Once the script has finished you should be able to use the following URLS a web browser:

<a href="http://localhost:8080/wookie/" target="_blank">http://localhost:8080/wookie</a> to access the Wookie Widget Server index page

<a href="http://localhost:8080/sled3" target="_blank">http://localhost:8080/sled3</a> to access the SLeD player

For this tutorial we are interested in the Wookie Player; you should now be able to access the Wookie index page via http://localhost:8080/wookie

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/calendar.jpg"><img class="aligncenter wp-image-19 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/calendar.jpg" alt="Calendar" width="229" height="210" /></a>

&nbsp;
<h3>Creating a Widget</h3>
For this example we are going to create a <em>very</em> simple widget that displays a calendar. Hopefully this will familiar ourselves with the way in which we create, upload, initiate and access widgets in Wookie; all we will need for this is any old <a href="http://notepad-plus.sourceforge.net/uk/site.htm" target="_blank">text editor</a>. The code required to make the calendar is available freely from the <a href="http://javascript.internet.com/time-date/calendar.html" target="_blank">JavaScript Source Website</a>First we need to create a directory that will contain our widgets files, I have called mine 'calendar' and stored it on my desktop. For this simple widget we will need to create four files within this directory:
<ol>
	<li>The Configuration document - To tell the server what to do with our widget</li>
	<li>HTML page - The page the user will see</li>
	<li>CSS file - A file describing the style of the HTML page</li>
	<li>A JavaScript file - To store the code that will make our calendar work.</li>
</ol>
<em>Configuration Document</em>

The configuration document is an XML file that should be named <code>config.xml</code> and is required by the Wookie server to configure the widget. To create one open up your text editor then copy and paste the following:
<pre><code>
&lt;?xml version="1.0" encoding="UTF-8" ?&gt;&lt;widget chrome="" </code></pre>
<pre><code>   height="0" id="http://www.tencompetence.org/calendarWidget"
   start ="calendar.htm" version="9" width="0"
   xmlns="http://http://www.w3.org/ns/widgets"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://http://www.w3.org/ns/widgets w3cwidgets.xsd"&gt;</code></pre>
<pre><code>  &lt;title&gt;The calendar widget!&lt;/title&gt;
  &lt;description&gt;A sample calendar widget for demonstration purpose&lt;/description&gt;
  &lt;author&gt;David Sherlock&lt;/author&gt;
&lt;/widget&gt;</code></pre>
This contains the <em>bare minimum</em> that is required by the widget server; you should change my name and details and then save the file as <code>config.xml</code>.

<em>HTML file</em>
Since the CSS and Javascript files contain detail on how to the calendar will be created and displayed the HTML file is minimal:
<pre><code>&lt;html&gt;
&lt;head&gt;
 &lt;link rel="stylesheet" href="calendar.css" type="text/css"/&gt;
 &lt;script type='text/javascript' src='calendar.js'&gt; &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;script type="text/javascript"&gt;writeCalendar()&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
This simply specifies the CSS and JavaScript files, this should now be saved within the same directory as our config.xml as calendar.htm.

<em>Javascript and CSS files</em>
Finally we need to create the Javascript and CSS that will create the calendar; this example has been taken from the <a href="http://javascript.internet.com/" target="_blank">Javascript Source</a> website.

The CSS should be copied in to a file within our directory called calendar.css:
<pre><code>

span.label {
color:black;
width:30;
height:16;
text-align:center;
margin-top:0;
background:#ffF;
font:bold 13px Arial
}

span.c1 {
cursor:hand;
color:black;
width:30;
height:16;
text-align:center;
margin-top:0;
background:#ffF;
font:bold 13px Arial
}

span.c2 {
cursor:hand;
color:red;
width:30;
height:16;
text-align:center;
margin-top:0;
background:#ffF;
font:bold 13px Arial
}

span.c3 {
cursor:hand;
color:#b0b0b0;
width:30;
height:16;
text-align:center;
margin-top:0;
background:#ffF;
font:bold 12px Arial
}
</code></pre>
&nbsp;

The accompanying JavaScript should also be stored in our working directory within a file called calendar.js. you can get the required JavaScript from here:
<pre><code>

function maxDays(mm, yyyy){
var mDay;
if((mm == 3) || (mm == 5) || (mm == 8) || (mm == 10)){
mDay = 30;
}
else{
mDay = 31
if(mm == 1){
if (yyyy/4 - parseInt(yyyy/4) != 0){
mDay = 28
}
else{
mDay = 29
}
}
}
return mDay;
}
function changeBg(id){
if (eval(id).style.backgroundColor != "yellow"){
eval(id).style.backgroundColor = "yellow"
}
else{
eval(id).style.backgroundColor = "#ffffff"
}
}
function writeCalendar(){
var now = new Date
var dd = now.getDate()
var mm = now.getMonth()
var dow = now.getDay()
var yyyy = now.getFullYear()
var arrM = new Array("January","February","March","April","May","June","July","August","September","October","November","December")
var arrY = new Array()
for (ii=0;ii&lt;=4;ii++){
arrY[ii] = yyyy - 2 + ii
}
var arrD = new Array("Sun","Mon","Tue","Wed","Thu","Fri","Sat")

var text = ""
text = "&lt;form name=calForm&gt;"
text += "&lt;table border=1&gt;"
text += "&lt;tr&gt;&lt;td&gt;"
text += "&lt;table width=100%&gt;&lt;tr&gt;"
text += "&lt;td align=left&gt;"
text += "&lt;select name=selMonth onChange='changeCal()'&gt;"
for (ii=0;ii&lt;=11;ii++){
if (ii==mm){
text += "&lt;option value= " + ii + " Selected&gt;" + arrM[ii] + "&lt;/option&gt;"
}
else{
text += "&lt;option value= " + ii + "&gt;" + arrM[ii] + "&lt;/option&gt;"
}
}
text += "&lt;/select&gt;"
text += "&lt;/td&gt;"
text += "&lt;td align=right&gt;"
text += "&lt;select name=selYear onChange='changeCal()'&gt;"
for (ii=0;ii&lt;=4;ii++){
if (ii==2){
text += "&lt;option value= " + arrY[ii] + " Selected&gt;" + arrY[ii] + "&lt;/option&gt;"
}
else{
text += "&lt;option value= " + arrY[ii] + "&gt;" + arrY[ii] + "&lt;/option&gt;"
}
}
text += "&lt;/select&gt;"
text += "&lt;/td&gt;"
text += "&lt;/tr&gt;&lt;/table&gt;"
text += "&lt;/td&gt;&lt;/tr&gt;"
text += "&lt;tr&gt;&lt;td&gt;"
text += "&lt;table border=1&gt;"
text += "&lt;tr&gt;"
for (ii=0;ii&lt;=6;ii++){
text += "&lt;td align=center&gt;&lt;span class=label&gt;" + arrD[ii] + "&lt;/span&gt;&lt;/td&gt;"
}
text += "&lt;/tr&gt;"
aa = 0
for (kk=0;kk&lt;=5;kk++){
text += "&lt;tr&gt;"
for (ii=0;ii&lt;=6;ii++){
text += "&lt;td align=center&gt;&lt;span id=sp" + aa + " onClick='changeBg(this.id)'&gt;1&lt;/span&gt;&lt;/td&gt;"
aa += 1
}
text += "&lt;/tr&gt;"
}
text += "&lt;/table&gt;"
text += "&lt;/td&gt;&lt;/tr&gt;"
text += "&lt;/table&gt;"
text += "&lt;/form&gt;"
document.write(text)
changeCal()
}
function changeCal(){
var now = new Date
var dd = now.getDate()
var mm = now.getMonth()
var dow = now.getDay()
var yyyy = now.getFullYear()
var currM = parseInt(document.calForm.selMonth.value)
var prevM
if (currM!=0){
prevM = currM - 1
}
else{
prevM = 11
}
var currY = parseInt(document.calForm.selYear.value)
var mmyyyy = new Date()
mmyyyy.setFullYear(currY)
mmyyyy.setMonth(currM)
mmyyyy.setDate(1)
var day1 = mmyyyy.getDay()
if (day1 == 0){
day1 = 7
}
var arrN = new Array(41)
var aa
for (ii=0;ii&lt;day1;ii++){
arrN[ii] = maxDays((prevM),currY) - day1 + ii + 1
}
aa = 1
for (ii=day1;ii&lt;=day1+maxDays(currM,currY)-1;ii++){
arrN[ii] = aa
aa += 1
}
aa = 1
for (ii=day1+maxDays(currM,currY);ii&lt;=41;ii++){
arrN[ii] = aa
aa += 1
}
for (ii=0;ii&lt;=41;ii++){
eval("sp"+ii).style.backgroundColor = "#FFFFFF"
}
var dCount = 0
for (ii=0;ii&lt;=41;ii++){
if (((ii&lt;7)&amp;&amp;(arrN[ii]&gt;20))||((ii&gt;27)&amp;&amp;(arrN[ii]&lt;20))){
eval("sp"+ii).innerHTML = arrN[ii]
eval("sp"+ii).className = "c3"
}
else{
eval("sp"+ii).innerHTML = arrN[ii]
if ((dCount==0)||(dCount==6)){
eval("sp"+ii).className = "c2"
}
else{
eval("sp"+ii).className = "c1"
}
if ((arrN[ii]==dd)&amp;&amp;(mm==currM)&amp;&amp;(yyyy==currY)){
eval("sp"+ii).style.backgroundColor="#90EE90"
}
}
dCount += 1
if (dCount&gt;6){
dCount=0
}
}
}
</code></pre>
&nbsp;
<h3>Packing and uploading</h3>
Now we should have 4 files within our directory:
<ol>
	<li>config.xml</li>
	<li>calendar.js</li>
	<li>calendar.css</li>
	<li>calendar.htm</li>
</ol>
For the Wookie server to accept these we have to turn them into a Widget Resource by creating a valid Zip archive out of them. In Windows XP this can be done by selecting all the files, right clicking one and sending it to a Zip archive:

&nbsp;
<h3>Initializing Widget</h3>
Our newly created Widget Resource is now ready to be installed on the Wookie Server. First we must make sure that the environment is running, if it is not already start the coppercore.bat that we downloaded earlier. Once this has run its course navigate a browser to the Wookie Servers index page at http://localhost:8080/wookie. From here we click on the 'admin' link (the default username and password is java/java) to get to the administration admin page:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/menu.jpg"><img class="aligncenter wp-image-1986 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/menu-300x192.jpg" alt="Menu" width="300" height="192" /></a>

There are four steps now we must follow to run our widget:
<ol>
	<li>Create a Service for it</li>
	<li>Upload the widget</li>
	<li>Set the widget as default for our service</li>
	<li>Initialize the widget</li>
</ol>
<em>Creating a Service</em>

First we are going to create a service for our Widget; by clicking 'add a new service type'.  There are four default services with the server; these are chat, discussion, forum and vote. Our calendar doesn't fit into any of these services so we will add one ourselves.  Type 'calendar' into the box on the right and press add, once the service is added we can press menu to return to the front page.

<em>Uploading </em><em>Setting Widget as Service Default</em>

From the menu screen click 'add new widget', the widget server will then ask for a valid zip file; browse to the zip file we created before and click upload. Once the widget has been uploaded it will ask which services it belongs to, choose calendar and press submit.

Now we have added the widget to our new service type we want to set it as the default widget for that service, return to the administration menu and choose 'view existing widgets'. You should now see our calendar widget on the list assigned to calendar service type. To set this as the default widget for the calendar service simply click the blue word calendar.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/service.jpg"><img class="aligncenter wp-image-1990 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/service-300x193.jpg" alt="Services" width="300" height="193" /></a>

<em>Initializing Widget</em>
Finally we can initialize and use the widget; we no longer need the Wookie administration page so navigate back to the index page at http://localhost:8080/wookie/ and click initiate. The following screen will ask for parameters for the widget you wish to create; here we will change the user ID to any name you wish and the service to the calendar service we created before.

&nbsp;

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/instance1.jpg"><img class="aligncenter size-full wp-image-2009" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/instance1.jpg" alt="instance" width="245" height="228" /></a>

Once we click submit the form should return an XML document; for now we are interested in the URL element of this document.

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/widgetxml1.jpg"><img class="aligncenter size-full wp-image-2010" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/widgetxml1.jpg" alt="widgetxml" width="564" height="235" /></a>

&nbsp;

Copy and paste the URL from your XML document into the Web browser and you should be presented with the widget we created!

<a href="http://davidsherlock.co.uk/wp-content/uploads/2008/08/calendar.jpg"><img class="aligncenter size-full wp-image-19" src="http://davidsherlock.co.uk/wp-content/uploads/2008/08/calendar.jpg" alt="Calendar" width="229" height="210" /></a>

The Javascript and CSS used to create the calendar are freely avalible <a href="http://javascript.internet.com/time-date/calendar.html" target="_blank">here.</a>
<h3>Further Reading</h3>
http://www.tencompetence.org/ldruntime/

http://javascript.internet.com/time-date/calendar.html