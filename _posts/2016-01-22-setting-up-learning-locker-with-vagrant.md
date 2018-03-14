---
ID: 2491
post_title: Setting up Learning Locker with Vagrant
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/setting-up-learning-locker-with-vagrant/
published: true
post_date: 2016-01-22 16:37:17
---
A couple of years ago I wanted to install <a href="http://davidsherlock.co.uk/installing-learninglocker-mac-os-x-mamp/">Learning Locker on OSX</a>, I blogged about it to help me remember what to it and I found it pretty useful to return to when I got stuck. I need to install Learning Locker again, but looking through my old post reminded me that it is a little bit of a pain, mostly because it relies on various PHP extensions which are extra fiddly when you are using MAMP/XXAMP/etc across various platforms.

I decided to run a light weight virtual machine that I could move from machine to machine, after having a look around at what is possible I decided to do it on Vagrant, which is virtualization software type thing that I've never played with. If you just want to throw an instance up then <a href="http://www.jmblog.org/blog/2015/02/03/learning-locker-vagrant">Jim Baker has already done it here</a> which has a configured box for you to download, he seems to have made from a AWS image. Having never used vagrant before I wanted to do it myself, but also I wanted a barebones Ubuntu box that I had put together myself (with apt-get..).

I think it is relatively straight forward and should be similar on Windows, but once again I will write down the steps incase it helps this time next year… infact I should make sure I put the image somewhere safe..
<h2>1. Install Vagrant, borrow a barebones Ubuntu VM</h2>
Download and <a href="https://www.vagrantup.com/">install Vagrant</a> from their site, it is a stright forward . Once installed you can create a virtual machine from the command line. I created a new directory under ~/Documents to store the virtual machine. I opened Terminal, created a new directory, created a Ubuntu instance and brought the machine up like so:
<pre class="lang:default decode:true">cd ~/Documents
mkdir vagrant
cd vagrant
mkdir vanillubuntu
cd vanillaubuntu
vagrant init ubuntu/trusty64; vagrant up --provider virtualbox
vagrant up</pre>
<h2>2. Set box up with LAMP + Mongo</h2>
You can now SSH on to your machine using:
<pre class="lang:default decode:true">vagrant ssh</pre>
On the box I set up LAMP, MongoDB and MongoDB, Curl mmycrpt PHP extensions, using apt this is very easy:
<pre class="lang:default decode:true">sudo apt-get install lamp-server^
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
sudo apt-get update
sudo apt-get install mongodb-org
sudo apt-get install php-pear php5-dev
sudo apt-get install libsasl2-dev
sudo pecl install mongo
sudo apt-get install php5-curl
apt-get install php5-mcrypt
php –ini (to find the ini file)
sudo nano /etc/php5/apache2/php.ini (add extension=mongo.so &amp; extension=mcrypt.so)
sudo service apache2 restart</pre>
<h2>3. Configure port forwarding:</h2>
Back on your Mac use Finder to navigate to the directory where you ran the 'vagrant init' command, in there should be a file, open the file and uncomment this line so that you can access Learning Locker (when it's up_ on Port 8080
<pre class="lang:default decode:true ">config.vm.network "forwarded_port", guest: 80, host: 8080</pre>
Reload the machine with:
<pre class="lang:default decode:true ">vagrant reload</pre>
Then you can check http://127.0.0.1:8080/ in a browser, you should see the Apache welcome page.
<h2>4. Install Learning Locker</h2>
Now I want to install learning locker and config on the box, clean the box up and save it .  I installed Learning Locker mostly, the way it says on the site changing a few bits to suit my enviroment
<pre class="lang:default decode:true">sudo apt-get install git
sd /var/www
sudo git clone https://github.com/LearningLocker/learninglocker.git learninglocker
cd learninglocker
sudo suphp -r "readfile('https://getcomposer.org/installer');" | php
exit
php composer.phar update
php composer.phar install --no-interaction --no-dev</pre>
<h2>5. Create MangoDB user</h2>
You need to create a user and password in Mongo that will work with a collection:
<pre class="lang:default decode:true ">Mongo
&gt;Use learninglocker
&gt;db.addUser( { user: "pickausername", pwd: "pickapassword", roles: [ "readWrite" ] } )
&gt;exit</pre>
Then create a database file in Learning Locker that users these credentals:
<pre class="lang:default decode:true">Sudo nano app/config/local/database.php</pre>
<!--?php return [     'connections' =&gt; [         'mongodb' =&gt; [             'driver'   =&gt; 'mongodb',             'host'     =&gt; 'localhost',             'port'     =&gt; 27017,             'username' =&gt; 'YOUR_DATABASE_USERNAME',             'password' =&gt; 'YOUR_DATABASE_PASSWORD',             'database' =&gt; 'YOUR_DATABASE_NAME'         ],     ]&lt;br ?-->
<pre class="highlight"><code>&lt;?php
return [
    'connections' =&gt; [
        'mongodb' =&gt; [
            'driver'   =&gt; 'mongodb',
            'host'     =&gt; 'localhost',
            'port'     =&gt; 27017,
            'username' =&gt; 'YOUR_DATABASE_USERNAME',
            'password' =&gt; 'YOUR_DATABASE_PASSWORD',
            'database' =&gt; 'YOUR_DATABASE_NAME'
        ],
    ]
];
</code></pre>
<h2>6. Modrewrite and the such</h2>
In theory it should work now, for some reason mod_rewrite wasn't enabled by default; I always thought that it was, but incase not here all the steps:
<pre class="lang:default decode:true">sudo a2enmod rewrite negotiation php5
sudo service apache2 restart</pre>
and add Allowoverride All in directory tags to your apache config in sites-avalible.
<h2>7. GO</h2>
So I exited the instance using 'exi't and saved the box. To do this I first had to find out the ID of the box, which you can find back in terminal with:
<pre class="lang:default decode:true ">vboxmanage list vms</pre>
and then you can save it with
<pre class="lang:default decode:true ">vagrant package --base &lt;id&gt;  --output ~/Documents/vagrantboxes/learninglocker.box</pre>
Now whenever I boot up that box I head to:

http://127.0.0.1:8080/learninglocker/public/

to register and start.
<h2>8. Save the box</h2>
Then I created a new vagrant from this box, first I add the box to the list with:
<pre class="lang:default decode:true">vagrant box add learninglocker.box --name learninglocker</pre>
And then create it in a directory with:
<pre class="lang:default decode:true">vagrant init learninglocker
vagrant up then starts learning locker</pre>
Note: I've been having problems with the insecure keypair since doing this. <a href="https://github.com/mitchellh/vagrant/issues/5186">Aparently so have lots of other Ubuntu users</a>. Still, I can ssh in with the default username/password recommended by vagrant.

&nbsp;