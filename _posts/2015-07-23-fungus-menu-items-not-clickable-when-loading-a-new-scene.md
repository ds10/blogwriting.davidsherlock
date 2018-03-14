---
ID: 2400
post_title: >
  Fungus menu Items not clickable when
  loading a new scene
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/fungus-menu-items-not-clickable-when-loading-a-new-scene/
published: true
post_date: 2015-07-23 09:12:22
---
Recently I've been playing around with the <a href="http://davidsherlock.co.uk/creating-revision-apps-as-text-adventures/">Unity Fungus asset</a>. Although it works very well and I have not had many problems with it, the application is just coming out of Beta and there are a few gotchas. On the <a href="http://fungusgames.com/forum">forums</a> there seems to be one recurring bug people keep getting stuck with, which for some reason doesn't seem to come up during a quick Google search. The problem is that when users call a new scene from a block using the 'Load New Scene' call option, all menu items on the new scene are not clickable. It is a known issue and an easy fix, which was kindly provided by Fungus admin C<span class="m-name">hris Gregan:</span>

On any scene that has been called by a block you need to add a EventSystem GameObject. Simply load the scene in Unity and then create the GameObject through the Unity menu through this combination: GameObject &gt; UI &gt; EventSystem.

Fungus should create this GameObject itself during play but for some reason is failing to do so on a new scene call. After you have added it manually menu items on the scene will be clickable.