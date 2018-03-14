---
ID: 193
post_title: >
  Installing Guest Additions on Cloudera
  Virtualbox VM
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/installing-guest-additions-on-cloudera-virtualbox-vm/
published: true
post_date: 2013-07-12 13:29:46
---
This was a real pain in the ass for me. There are a few steps, I did them all in the terminal because I don't really know my way around  CentOS 6.

Firstly I got an error about the Cloudera-search Repo not being able to find a certain file. This was because it didn't exist. I had to
<blockquote>sudo nano /etc/yum.repos.d/Cloudera-search.repo</blockquote>
and edit the baseurl so that it ended with /search/0.9.1 instead of 0.9.

That error probably wasn't important.. but it corrected it anyway. Next I needed to install my kernal headers, this is done using a repo that isn't in CentOS by default so I had to add it:
<blockquote>wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
rpm -K rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm</blockquote>
and then to install kernal headers:
<blockquote> sudo yum install dkms</blockquote>
I then reset my machine. While it was powered down I added a virtual dvd drive, when it was powered up I selected devices-&gt;install guest additions from virtual box and it ran... finally..

&nbsp;