---
ID: 1036
post_title: >
  Backing up WordPress to your dropbox
  account with UpdraftPlus
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/backing-wordpress-dropbox-account/
published: true
post_date: 2014-02-08 23:53:28
---
I have a few Wordpress installations on many different hosting companies, some of these support personal sites and some are for work. One of my big concerns is having keeping track of all my Wordpress backups; Some hosting companies do not work 24/7 which can be really frustrating when they are based in the other side of the word and only reply to your support tickets when you are in bed.  I decided that I needed backups of all my Wordpress installations in a single place that was easily accessible to me. I decided to use Dropbox because I have about 6Gb for free after convincing my friends to sign up through through my referrer link. 6Gb is more than enough for me, but the technique I use can also be used with Google Drive which heavy users might want to think about. This only works with hosted Wordpress installations on which you can install plugins and not Wordpress.org, you will also need enough avalible diskspace with your host and the php5-mcrypt PHP extension installed, I found that most of my hosts had php5-mcrypt installed but those who didn't where happy enough to install it after I left a support ticket for them.

Here are some notes so that I don't forget in the future!

1) First log in to your Wordpress instance with an admin account and click plugins-&gt;add new

2) Search for UpdraftPlus and install

3) In the UpdraftPlus setting choose

4) In the plugin settings look for "Copying Your Backup To Remote Storage" and select dropbox and click save.

5) When the page reloads click authenticate with dropbox and save

6) Press backup!