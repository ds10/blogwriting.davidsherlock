---
ID: 121
post_title: Maven 3, program mvn not found
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/maven-3-program-mvn-not-found/
published: true
post_date: 2013-06-19 10:31:35
---
I'm not a Java developer and don't have to compile much Java. Unfortunately sometimes I do, and on those rare occasions it usually goes wrong.

Today my problem was with Maven 3. I installed using apt-get install maven 3, however when I tried to use the mvn command I got the error "program mvn not found". This is a because the command is mvn3! So there are two options.

1) Use mvn3 install

2)create a symbolic link like so:

sudo ln -s /usr/share/maven3/bin/mvn /usr/bin/mvn