---
ID: 2402
post_title: >
  More attempts to create revision apps
  using free resources
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/more-attempts-to-create-revision-apps-using-free-resources/
published: true
post_date: 2015-07-31 10:24:39
---
Over the past year I have found myself playing with ways to create new ways to revise for students, mainly based around creating quick quizzes in different forms for my students to take on the go. My personal strategy has always been to 'top up' my revision sessions by doing flashcards on the basics of a subject; I always gathered that if I knew the fundamentals of what I was revising then the rest would come easier. Group revising has also worked well for me and another reason I've always like quick quizzes is that they can be done in a group and discussion is usually built on top of the activity.

A little while ago I came across <a href="http://fungusgames.com/">Fungus</a>,a Unity Plugin for visual story telling, I have quite a few ideas of things I would like to do with Fungus, and I thought as a test to get myself used to the system, I would try and create a revision game as it would fit in with my other experiments. My thinking was that I could throw all my quick quizzes in to a revision game  that students  could use to revise on the bus to learn fundamentals, but could also play the game in a group making it the focus of a revision activity.

I have previously had a <a href="http://davidsherlock.co.uk/creating-revision-apps-as-text-adventures/">very brief go with Fungus</a> to test how possible it was to get something up and running, but a few days ago decided to spend a full day with it to see how viable an option it was to create e-learning material quickly. After the day I was quite impressed with how far I got with the tool and thought it would be a good time to take stock of what was possible in a day and write up some notes on my experiences..
<h2>The situation</h2>
Fungus claims that it is a tool for people who can't code to help them make games, from the fungus site:
<blockquote>'Fungus is popular with writers, illustrators, animators and game designers, especially visual novel &amp; interactive fiction authors. '</blockquote>
My guess is that most lecturers and tutors will be jumping at joy of the prospect of creating a game while not writing any code. I, on the other hand enjoy tinkering with a bit of C#, the language that many Unity games are based, but don't particularly enjoy graph or UI design. While Fungus makes a deal about supporting the designers, it doesn't mention people like me in it's sales pitch, it does however help us quite a lot, it gives us a solid user interface and then holds your hand by telling you where it thinks thinks like images, avatars and menus should go.

This made me think, tutors making revision applications will have different skill sets, some will be ok with graphic design, story writing, coding and they will different resources available to them. My situation is:
<ul>
	<li>I have a CSV of questions and answers that I want to turn in to an app to help students revise</li>
	<li>I am a fairly high level 'tinkerer' of code. I don't mind going in to scripts and editing, but don't really fancy writing my own frameworks</li>
	<li>I do not have any images or pictures for my application</li>
	<li>I do not have the desire to create my own</li>
	<li>I want as many options as possible for students to play my game. I would like it to be playable on the go, but it is no good as an android application.</li>
</ul>
I decided to try and find free or low cost solutions to the things that I didn't have, this in itself was, and still is a learning curve in licensing, attribution.
<h2>Gathering the Resources</h2>
I already had the questions in CSV, I'm guessing that most lecturers will also have their questions in some format or another. I found that copying and organising content in to Fungus was by far the most time consuming aspect of creating the application, but I found methods to make this easier and automate the process, which I will go in to shortly.

Fungus lets you work with all kinds of character and environment assets, I thought that the easiest game set up for a proof of concept would be to have backgrounds and a character to appear in front of the background and talk via a text prompt. While this kind of game with characters and backgrounds might sound simple, it is the foundations of a very popular game genre, the '<a href="http://store.steampowered.com/tag/en/Visual%20Novel/#p=0&amp;tab=NewReleases">Visual Novel game</a>', and probably a good place to start from. Since I didn't want to open <del>illustrator</del> paint and start designing backgrounds and characters, I started to look for places with existing assets I could use. This in itself was a new learning curve for me.
<h3>Wikimedia Commons</h3>
[caption id="attachment_2421" align="alignleft" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/churchcommons.png"><img class="wp-image-2421 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/churchcommons-300x267.png" alt="Wikicommons search" width="300" height="267" /></a> Searching 'Church interior' on Wikimedia Commons gave me a bunch of images, advice on what projects I could use these images in and information on how to credit the author[/caption]

First I took all the 'topics' that I wanted students to revise and looked for related images to use as backgrounds. I looked for the backgrounds at <a href="https://commons.wikimedia.org">Wikimedia Commons</a>, a database of freely usable media files. For somebody like myself who is finding licensing issues and the such a learning curve, Wikipedia commons is brilliant, not just because there are plenty of usable images, but also because it gives you advice on what you can and can't do with each image and gives you examples of text to use when attributing the image.

I searched for download 5 images, one for each of my 4 topics and an extra one for my main menu. I saved them in to a directory named backgrounds so later I could just drag it straight in to Fungus to use them as backgrounds.
<h3>OpenGameArt</h3>
Visual Novels also tend to have talking heads, Fungus calls these 'portraits' and they are not the sort of thing I could find in Wikimedia commons. I found another online resource for visual assets called OpenGameArt where artists share their creations for games. Similar to Wikimedia Commons, the import aspect of the site for me was that it was clear about licensing and gave me example text for assets I had used. I picked a couple of character portraits for me game. I was particularly <a href="http://opengameart.org/content/anime-portrait-for-lpc-characters">fond of this resource</a> that gave me a few characters and different states of emotion that the character could be in.  This will be useful in the future as Fungus allows you to assign multiple states to a character. I saved a few of the character portraits, a monk and a school teacher to a directory called characters.
<h3>Fungus</h3>
I had my questions and art but I also needed the tools to make the game. Fungus is an open source, adventure game asset for Unity under a pretty permissive MIT license which you can access <a href="https://github.com/FungusGames/Fungus/blob/master/LICENSE">here</a>.
<h3>Unity</h3>
Not everything I used was totally free libre, Fungus is built on Unity which is free gratis if you are not making $100,000 a year on your product. You revision app is tied in to the Unity ecosystem and in the future you will have to go along with whatever Unity decide is their business model. Since I wanted to develop apps that use Fungus, are quick to churn out and available on multiple devices, I don't think there are really any other viable solutions. It might not be free as in speech, but that is a hit I decided to take and deal with for the ease of knocking out quick apps to multiple platforms.

[caption id="attachment_2412" align="aligncenter" width="591"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/fungusunityassets.png"><img class="wp-image-2412 size-full" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/fungusunityassets.png" alt="Asset folders in Unity" width="591" height="166" /></a> These are basically all the asset folders I needed, a folder for Fungus, one for some creative commons images and a folder for to store my scenes. My questions where directly imported in to the scene workflow.[/caption]
<h2>Making the game</h2>
[caption id="attachment_2409" align="alignleft" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/flowchartlevels.png"><img class="wp-image-2409 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/flowchartlevels-300x214.png" alt="Menu Flowchart" width="300" height="214" /></a> The flowchart for my menu scene basically lets users pick a revision category and then a level. The flowchart then loads a scene that has the chosen quiz in it[/caption]

Fungus has many fancy options, but I decided to keep it simple for my first attempt. There were only two types of levels I needed, these were:
<ul>
	<li>A menu screen to pick the quiz</li>
	<li>The level screen to display a series of short 5 question quizzes</li>
</ul>
Fungus uses flowcharts to design the flow of levels, I won't go in to detail on how to do it as the Fungus tutorial playlist is full of short tutorials that can sort you out very quickly. The gist is that I created flow charts for the Menu and Quizzes. For the Menu I used a series of menu blocks that shuffle the user around the screen until they get to the level they want, then a load scene action loads a new Unity Scene with a flowchart for the new questions.

It would be possible for my game to use 1 Unity scene filled with multiple flowcharts, but I have opted to use lots of scenes each with 1 flowchart.  It is a bit confusing, but if you've used Fungus you will get the gist.

The reason for using individual scenes brings me on to the next things I needed
<ul>
	<li>A teacher to tell the questions</li>
	<li>The questions</li>
</ul>
I built one scene for my quiz levels, this was a simple flowchart that asked questions and gave the user a selection of menu items, if the write answer was clicked then a score variable would increase by one. I did a naughty things and copied and pasted this scene 25 times, one for each quiz. The reason I did this was that Fungus allows users to export and import text in to a workflow, I wanted each workflow to have the same IDs for its blocks and activities and didn't know if this was possible my work flow shared the same scene.
<h2>Importing the questions</h2>
I have my questions in a CSV and need to get them in to the question workflows that live in their own scenes. Fungus has an option to export and import text from a workflow so I wrote a short script to take my CSV and convert it into 25 text files so that I could import 1 in to each scene. I found this saved me a lot of work, I won't go in to detail on code for the transcript generator because people will have different need outs of it. My guess is that most people will want to write the content out manually; but <a href="http://webm.host/0dfea/">I recorded it briefly generating the new transcripts if you are interested in seeing it in action</a>.

The next step took a while. I loaded each scene by hand and I imported the transcript for each level, I then randomised the position of the correct answer question  and created a character to ask the questions. Although, it might have took me and hour of repetitive tasks, but in the scheme of 'how long does it take to create a free game' I don't think it was that long.
<h2>Publishing the game</h2>
I now have a working demo! It took about a day to get this very rough demo created although I think that most of the effort was in transferring content to the game and creating the Menu system. Now that I have the system in place I am going to come up with some more ways of automating conversation of content to transcripts. Like I say, it is very rough and there are quite a few things I would like to implement:
<ul>
	<li>Personal Scoreboard</li>
	<li>More varied expressions from characters</li>
	<li>Different Characters to ask questions</li>
	<li>Bigger Characters to talk</li>
	<li>More varied backgrounds</li>
	<li>More questions</li>
	<li>Friends scoreboard</li>
	<li>More complex decision tree so that the dialog changes based on correct/incorrect answers</li>
</ul>
I didn't want to publish my game to lots of marketplaces at the moment as it is still in demo phase, and will need updating and repushing to these market places. I opted to publish it to <del>Kongregate</del> (decided to go with Parse in the end) and Windows Phone market place because these are free and seem the most 'suck it and see' friendly platforms to try new things and because then I could try 1 mobile and 1 web based platform. Still, Unity lets you output to pretty much any major platform if I want to expand at a later date.

If you fancy playing my early demo you can try it on <del><a href="http://www.kongregate.com/games/happysnowman163/religious-studies-revision">Kongregate</a></del> <a href="http://religiousrevision.parseapp.com/">Parse </a>(if you have the Unity web player) or Windows Phone 8 store, although this takes a day or so to process so I don't have a link yet. There is still lots to do if I decide to carry on with it, but I think lots of the work is done and I was impressed that you could get something basic up in less than a day.  While I was playing I kept some notes of some of the obstacles I came across if you are interested:
<ul>
	<li><a href="http://davidsherlock.co.uk/fungus-menu-items-not-clickable-when-loading-a-new-scene/">Workaround for bug in loading new scene in Fungus</a></li>
	<li><a href="http://davidsherlock.co.uk/creating-revision-apps-as-text-adventures/">Getting to grips with Fungus</a></li>
	<li><a href="http://davidsherlock.co.uk/adding-adverts-to-a-unity-windows-phone-project/">Adding ads to Windows Phone 8</a></li>
</ul>
Various in game scenes:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.06.png"><img class="alignnone size-medium wp-image-2418" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.06-300x224.png" alt="Screen Shot 2015-07-30 at 14.05.06" width="300" height="224" /></a> <a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.17.png"><img class="alignnone size-medium wp-image-2419" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.17-300x219.png" alt="Screen Shot 2015-07-30 at 14.05.17" width="300" height="219" /></a> <a href="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.32.png"><img class="alignnone size-medium wp-image-2420" src="http://davidsherlock.co.uk/wp-content/uploads/2015/07/Screen-Shot-2015-07-30-at-14.05.32-300x223.png" alt="Screen Shot 2015-07-30 at 14.05.32" width="300" height="223" /></a>

&nbsp;