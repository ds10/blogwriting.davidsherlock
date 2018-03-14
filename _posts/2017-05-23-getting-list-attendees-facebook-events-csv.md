---
ID: 2611
post_title: >
  Getting a list of attendees from
  Facebook events in CSV
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/getting-list-attendees-facebook-events-csv/
published: true
post_date: 2017-05-23 13:27:39
---
I had a message from a subscriber asking if I could make a short video on how to get a list of attendees from a Facebook event. One super quick way to do this is through the Facepager app. Firstly download the <a href="https://github.com/strohne/Facepager/releases">app from the Github releases page and install</a>; the latest version as of today is 3.8 on Windows and 3.7 on Mac. I’ve created a quick video which shows you how to get the data and export it to CSV. You might also want to get a list of interested or declined people, the video briefly goes over that at the end.

https://www.youtube.com/watch?v=eMsexc8iGzw&feature=youtu.be

Step by step instructions:
1. Create a database by clicking the New Database picture at the top of the screen. You can call it whatever you wish and save it wherever you like.
2. Click ‘Add node; in the top area.
3. In the dialogue box that opens you want to type in the id of your event. You can get this by opening a browser and going to the facebook page of your event. In the URL there will be a load of numbers, this is the id. Copy and paste it into facepager.
4. Click the node in the menu box.
5. Next to resource select /attending
6. Change maximum pages to something high
7. Click Login to Facebook. Once logged in the Access token should fill in.
8. Press Fetch Data.
9. Select new columns and click export data.
10. Do whatever you want with the data!