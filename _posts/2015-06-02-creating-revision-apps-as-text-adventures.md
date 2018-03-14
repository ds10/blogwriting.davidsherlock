---
ID: 2366
post_title: >
  Creating Revision Apps as Text
  Adventures
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/creating-revision-apps-as-text-adventures/
published: true
post_date: 2015-06-02 15:29:23
---
Since finding out about the <a href="http://fungusgames.com/">RAGE project</a> I've become very interested in just how easy it can be for somebody who is not a game developer (like me) to make simple and distribute them on market places. Unity goes a long way in making game development easy but there are still many skill sets required to get a game up and running, personally I find animation, character modeling and UI design quite challenging. While poking around assets for Unity I discovered <a href="http://fungusgames.com/">Fungus Games</a>, an open source interactive storytelling kit. The storytelling kit itself is an easy to install add on for Unity that adds a 'Workflow' window to the IDE. In window tool you can create a decision tree where users can create text and present the player options that change the flow of the story. There are options to add characters, backgrounds, variables and the such that I haven't really got in to but seem really easy to use. As a test to see just how easy it is to use I decided to take some questions from my <a href="http://davidsherlock.co.uk/twitter-questionrevision-bot/">Revision Bot</a> and create a quick 10 question game. It was easy and quick to get something basic up:
<h3>1. Download and install Unity</h3>
<a href="https://unity3d.com/">I opted for Unity 5</a>, some developers are staying on 4 for now, but I guess this is due to compatibility with their existing assets. I recommend 5.
<h3>2. Install Fungus</h3>
Once you have started a new Unity project you need to import the <a href="http://fungusgames.com/download/">fungus package</a>. First download the package from the Fungus site, then you can either click 'import package' from within Unity or just double click the .unitypackage file from within Explorer/Finder.
<h3>3. Create a workflow for the game</h3>
[caption id="attachment_2369" align="alignleft" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/06/unityfungus.png"><img class="wp-image-2369 size-medium" src="http://davidsherlock.co.uk/wp-content/uploads/2015/06/unityfungus-300x224.png" alt="Unity IDE after installing Fungus" width="300" height="224" /></a> Unity IDE after installing Fungus[/caption]

The Fungus option should have been added to your menu bar when you installed the Fungus plugin. To start creating a simple game you need a workflow which can be added from this menu via Fungus-&gt;Tools-&gt;Create-&gt;Flowchart in Unity (A). This will add a workflow component in the hierarchy, you can change the name and such in the inspector. By clicking the workflow component you should be able to explore a new window called 'workflow' (C) where you can add blocks of text/menus/decisions.  By clicking the plus icon in the top left of the workflow window you can add a block to the workflow and then by then clicking the block you can add all sorts of events to your games. I added simple 'say' blocks which ask the user a question, then I added three menu items. One of these menu items increases a variable callled 'score' while the other simply moves on to the next question without increasing the score.
<h3></h3>
<h3>4. Edit your story</h3>
At this point I had only added placeholders for the text. To add questions and answers I found the best way was to export the story as a text file, fill in my questions and then import it back in Unity/Fungus. This can be done by creating a 'Localization' and clicking the export button.

After adding 5 questions I thought I would see if the game would export and play on various devices. It worked straight away on my windows phone so I have no reason to expect it wouldn't work on other phones. One feature I didn't play with, but was impressed by was the 'view' component. This makes shows the developer where different screen sizes are on 99% of android devices making it really easy to get something running that will look ok on most devices. I also tested it out by exporting to HTML 5, which seemed to work, but the large file size seems to be a problem when I host it online, if you really want to you can try <a href="http://quiz.paddytherabbit.com/html/">out the skeleton of my app here, </a>but no promises it will work well.
<h3>5. (TODO) Add graphics, score at the end, options etc</h3>
There is lots to add to the game, but I was just so impressed at how easy it was to get started. The whole process took about 30 mins, the longest bit was adding the questions. I am interested in being able to auto populate the questions. Maybe I could randomise them from my database of questions?

&nbsp;

How the question and answer blocks display in game:

<a href="http://davidsherlock.co.uk/wp-content/uploads/2015/06/questionblock.png"><img class="alignnone size-medium wp-image-2372" src="http://davidsherlock.co.uk/wp-content/uploads/2015/06/questionblock-300x68.png" alt="questionblock" width="300" height="68" /></a><a href="http://davidsherlock.co.uk/wp-content/uploads/2015/06/answerblock.png"><img class="alignnone size-medium wp-image-2371" src="http://davidsherlock.co.uk/wp-content/uploads/2015/06/answerblock-300x93.png" alt="answerblock" width="300" height="93" /></a>