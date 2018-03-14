---
ID: 814
post_title: >
  A MORPG engine masquerading as a
  participatory agent based model
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/morpg-engine-masquerading-participatory-agent-based-model/
published: true
post_date: 2013-12-17 07:40:55
---
&nbsp;

Or is it an agent based model enviroment masquerading as a MORPG engine?

<a href="https://github.com/scottbw/untiled">Untiled</a> is a cleverly titled experimental html 5 RPG engine without tiles being developed by Scott Wilson. It’s  got some neat capabilities in which everything in the engine is an object that can be handled in the same way by the engine; no matter what that 'thing' is. To me this is a similar way of thinking to tools like Netlogo and I was thinking of exploiting to make simple agent based models with. The biggest difference between this engine and other smallish html 5 games engines is it's multiplayer capabilities, you can read more on the github page but I guess the way to think about it is as a networking/IO project with a game tacked on to it (Rather than a game with multiplayer tacked on)

I found setup very easy on the Mac, I use brew:
<ol>
	<li>Brew install redis</li>
	<li>Brew install node</li>
	<li>Download zip file from github and unzip on Desktop</li>
	<li>cd ~/Desktop/untiled-master/</li>
	<li>npm install</li>
	<li>open a separate terminal window to start redis with command “redis-server”</li>
	<li>node game.js</li>
</ol>
You can join the game at <a href="http://localhost:3000/sara.html">http://localhost:3000/ a</a>nd a second player can join at: <a href="http://localhost:3000/sara.html">http://localhost:3000/sara.html</a>

Now I have a game engine up, but I’m interested in using this for participatory agent based models modelling. I think already the concepts of the engine map quite well on to agent based modelling tools such as Netlogo. Some agent based moddeling thinking maps on to Untiled quite well. The game features:
<ol>
	<li>A scene, which I guess Netlogo’s would call a [patch].</li>
	<li>Agents, which the game calls stickers</li>
	<li>Agent properties  (Things you would set in netlogo with [turtles-own])</li>
	<li>Triggers which cause events</li>
</ol>
To make things even more like an agent based modelling environment we can give the stickers conditions and simple movement rules such as PATH, RANDOM, FOLLOW or FLEE. This made me think it would be a good environment to teach programming… which I guess is kind of obvious if I’m already thinking that it maps to logo style thinking.

While I think you could do some pretty fun agent based models in the environment anyway, I think the exciting bit is the multiplayer aspect. Since every sticker in the model is an agent we can have people playing the role of agents in the model themselves.

I think the next step is to go and have a little play..

[caption id="attachment_815" align="aligncenter" width="300"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/untiled.png"><img class="size-medium wp-image-815" alt="untiled" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/untiled-300x195.png" width="300" height="195" /></a> Two browsers side by side simulating two player, with agent one following a ruleset. Logic shown in Terminal[/caption]

&nbsp;

&nbsp;

&nbsp;