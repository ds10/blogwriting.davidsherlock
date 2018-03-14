---
ID: 1469
post_title: >
  Installing Learning Locker on Mac OS X
  with MAMP
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/installing-learninglocker-mac-os-x-mamp/
published: true
post_date: 2014-06-26 10:57:29
---
The<a href="http://docs.learninglocker.net/docs/requirements"> Learning Locker requirements page</a> recommends a LAMP style stack to install on, I use Mac OS X, which is close enough and because I want to keep my Apache, MySQL and PHP stuff self contained I use the free version of <a href="http://www.mamp.info/de/">MAMP</a> which is great for the most part but requires a little bit of extra fidderling when you want to compile new PHP extensions, like the Mango extension that you will need for Learning Locker, although the documentation says I can use MySQL and I didn't want to go against the grain. Installing MAMP is a case of downloading the application and moving it to your applications folder.  I also use <a href="http://brew.sh/">Homebrew</a> which is a package manager for the Mac OS which I really recommend it if you looking to install *nix like tools, although be honest something like that should be included in the OS by default.
<h3>1. Install Composer</h3>
Composer is a dependency manager for PHP and required for Learning Locker, installed via Homebrew at the terminal with
<pre class="lang:default decode:true">brew update
brew tap homebrew/homebrew-php
brew tap homebrew/dupes
brew tap homebrew/versions
brew install homebrew/php/composer</pre>
<h3>2. Create Project</h3>
Then you will need to create your project. You can create it where ever you like, but it makes sense to serve it from the same directory that Apache is serving from. I don't server it from the default MAMP directory but from /Users/David/Sites. You can create the project with:
<pre class="lang:default decode:true">composer create-project learninglocker/learninglocker</pre>
<h3>3. Artisan</h3>
Change in to the learninglocker directory and run the following artisan command:
<pre class="lang:default decode:true">php artisan generate:migration add_statements</pre>
<h3> 4. Install and run MongoDB</h3>
Did this easily with brew
<pre class="lang:default decode:true">brew install mongodb
mongod –fork</pre>
<h3> 5. Install MongoDB PHP extenson</h3>
MAMP doesn't ship with the PHP source to compile I had to download PHP source in to the MAMP directory for the PHP version I was using, i.e /Applications/MAMP/bin/php/php5.5.3/includes/php . This means I had to go to the PHP site and download the source for 5.5.3 and put it in includes/php. Make sure you get the right version! Then:
<pre class="lang:default decode:true">cd /Applications/MAMP/bin/php/php5.5.3/includes/php
./configure --with-php-config=/Applications/MAMP/bin/php/php5.5.3/bin/php-config

</pre>
find the appropriate php.ini in MAMP and add this line:
<pre class="lang:default decode:true">extension=mongo.so</pre>
Reset MAMP
<h3>6. Final config</h3>
add mongodb config to database.php
<pre class="lang:default decode:true">sudo nano app/config/app.php</pre>
Add the following service provider to app/config/app.php in 'Autoloaded Service Providers'

'JenssegersMongodbAuthReminderServiceProvider'
<pre class="lang:default decode:true">sudo nano app/config/app.php</pre>
Then you can head over to localhost/learninglocker to get started