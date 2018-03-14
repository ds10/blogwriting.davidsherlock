---
ID: 2498
post_title: 'Notes: setting up a xAPI dev enviroment'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/notes-setting-up-a-xapi-dev-enviroment/
published: true
post_date: 2016-02-01 18:06:51
---
While in theory it is quite easy to start firing xAPI to a Learning Record Store there are quite a few things you need and it can get confusing wondering where to start. I’ve played in this space before but found there are so many things to get my head around again I forget what order I did things the time. This time I’ve been recording notes on the things I’ve been doing to make it quicker for myself when I inevitably return to the space. Here are my latest notes:

Its as easy as:
<ol>
	<li>Finding an LRS you can use. Use the demo Learning Locker or install one yourself</li>
	<li>Find a place with experience to capture, perhaps use an extisting instance of Moodle or install one yourself.</li>
	<li>Fire xAPI statements at LRS.</li>
</ol>
The first thing I always end up spending time doing is installing a Learning Record Store to fire statements at. This time I decided in <a href="http://davidsherlock.co.uk/setting-up-learning-locker-with-vagrant/">this post to create a virtual machine just for this purpose</a> and used Vagrant. You don’t need to do this though, in fact you can just use the demo lrs at: <a href="http://demo.learninglocker.net/data/xAPI">http://demo.learninglocker.net/data/xAPI</a>.

Next I wanted an instance of Moodle on my local machine, Moodle is very easy to install by <a href="https://download.moodle.org/">downloading the .zip file</a> and unarchiving in directory that your webserver is serving from. The problem with doing this is that your Moodle instance will be empty and the whole point is to capture learning experience’s?

As long as you have the correct dbsocket configuration information in the config.php set up you can populate your database with some test data. I’m not sure how much test data this will give you yet, but it does seem to fill in some entries in logstore_standard_log. To generate the data open terminal and change directory to the where moodle is installed and run:
<pre class="lang:default decode:true">php admin/tool/generator/cli/maketestcourse.php --shortname=SIZE_S --size=S</pre>
Once you’ve ran this command use your favourite mysql tool to connect to your database and check that it has put some data in logstore_standard_log.

Now that you have a Moodle instance with data and an empty LRS we probably want to have a go at throwing things at your LRS endpoint with Moodle Data.

As far as I’ve always understood it there are 3 important steps to getting data in to a store, these are

Expand: Expand any log you have by merging with other database entries

Translate: Turn them in to xAPI recipe options

Emit: Send them to the store.

I’m using Moodle and the easiest way to do this in Moodle is to install the plugin which does all three and is available from: <a href="https://github.com/jlowe64/moodle-logstore-xapi/blob/master/xapi.zip?raw=true">https://github.com/jlowe64/moodle-logstore-xapi/blob/master/xapi.zip?raw=true</a>

The instructions at the download page are easy to follow along, this bit is always the same:
<pre class="lang:default decode:true">Go to “http://www.example.com/admin/tool/installaddon/index.php” (replacing “www.example.com” with your own domain).
Drag and drop your download from step 1.
Click “Install plugin from the ZIP file”.
Click “Install plugin!”.
Click “Upgrade Moodle database now”.
Click “Continue”.</pre>
But this bit depends on your LRS set up. I am using my own Learning Locker instance on my vagrant virtual machine, to find the details you need to log in to Learning Locker, create a LRS instance and then click settings on the right hand side. You can just use the demo learning locker with the credentials in the example:
<pre class="lang:default decode:true">Set your “endpoint” to “http://demo.learninglocker.net/data/xAPI”.
Set your “username” to “d416e6220812740d3922eb09813ebb4163e8eb3e”.
Set your “password” to “bc7e0a2edd5d1969b6d774e679d4eb4e7a35be13”.
Click “Save changes”.
Go to “http://www.example.com/admin/settings.php?section=managelogging” (replacing “www.example.com” with your own domain).
Enable the “Logstore xAPI” plugin.</pre>
This will create an extra table in your database, if you have a poke you should see the mdl_logstore_xapi_log table, but it will be empty. The plugin you have installed emits message from the Moodle Logstore, it will convert them from the Moodle log table first and store them in the new table if you decide to select ‘Send statements by scheduled task? ‘ in the plugin options. It is worth selecting this option and doing something just to see some examples fill up in this database. Otherwise statements are fired on the fly, which is also fine, its just nice to see how things work.

To check if things work then just generate more data again with:
<pre class="lang:default decode:true">php admin/tool/generator/cli/maketestcourse.php --shortname=SIZE_S --size=S</pre>
You can then check your Learning Locker store for statement.

&nbsp;