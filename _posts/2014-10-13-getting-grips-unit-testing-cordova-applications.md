---
ID: 1860
post_title: >
  Getting to grips with unit testing
  Cordova applications
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/getting-grips-unit-testing-cordova-applications/
published: true
post_date: 2014-10-13 13:16:33
---
I have really enjoyed using Cordova to build Android apps because I can knock things up quick and easy. I do have a problem though, sometimes I knock something up quickly and decide that I want to take it further, I then wish that I had thought harder at the start of the project about things such as how I am going to structure and test my code.

One of the problems I have with my latest project, <a href="https://play.google.com/store/apps/details?id=com.paddytherabbit.triviaquizzes">Trivia Quizzes</a>, is that it is a basically bits of code I have pulled out of other projects while getting to grips with Cordova. I quite like Trivia Quizzes and want to go on to expand on it a little; I’m thinking it would be a good base project to learn some new Cordova techniques, I'm thinking of extending it to include Google Play Services scoreboards and achievements. Before I'ed expand I decided to go back and restructure the project properly.

The restructuring was not an easy task. I would move things around in the project only for them to break. I would remove code I thought was redundant only to notice quite quickly that it wasn't. Since I am writing my application in Javascript I would forget that some things that work on a desktop don't work so well on a Mobile Phone and I quite often reintroduce bugs in to the code; I think that the programming gods call this a regression. After a bit of searching I found that the the way to fight these is to add little tests to your code to check that units of code still work despite you fiddling with stuff, these tests, believe it or not are called Unit Tests.

<strong>Unit Testing in Cordova</strong>
I have heard of Unit Testing before, in fact a whole ago I had read '<a href="http://www.manning.com/osherove/">The art of Unit Testing</a>' by Roy Osherove. I just hadn't really implemented many tests in to my code. My experiences with Cordova, especially my reorganisation of the Trivia Quizzes project has taught me a lesson.  I'm also hoping it will help with my debugging as I have to admit that debugging in Cordova is not going well for me.  While I have been reading up on debugging on a mobile device or simulator device it is difficult to synchronize breakpoints or retrieve stack traces. Since Cordova is basically HTML/CSS/Javascript it can be debugged in a desktop web browser, but I have found that things such as JavaScript Performance and the phone API availability are difficult things to emulate in the browser. There are a few projects that attempt to get around that, projects such as <a href="http://emulate.phonegap.com/">emulate</a> and <a href="https://www.genuitec.com/products/gapdebug">gapdebug</a> but it is hard to know what to go with.

I’ve had a poke around different frameworks for unit testing and debugging in Javascript and have come up with a way forward. I am going to create a series of unit tests that I can access from within both the application and when debugging on the desktop. I’m not sure how I am going to write tests for Phone specific activities, like accessing parts of the Phone API, but I am going use unit testing as a way of evaluating the debugging tools.

<strong>Creating the testing infrastructure</strong>

As far as unit testing in Javascript goes, I like the sound of <a href="http://qunitjs.com/">QUnit</a> as it appears to be regularly updated and as part of the hugely popular JQuery suite has a large user base. JQuery also seems quite simple to set; I created a new folder in my project that with an HTML page, this included QUnits CSS/JS files and  two div’s with specific ID's in the page. I also included the javascript file that I wanted to start creating tests for (functions.js) and an empty file I was going to plonk my tests in (tests.js):
<pre class="lang:default decode:true ">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta charset="utf-8"&gt;
&lt;title&gt;Unit Tests&lt;/title&gt;
&lt;link rel="stylesheet" href="qunit-1.15.0.css"&gt;
&lt;script src="qunit-1.15.0.js"&gt;&lt;/script&gt;
&lt;script src="../js/functions.js"&gt;&lt;/script&gt;
&lt;script src="tests.js"&gt;&lt;/script&gt;

&lt;/head&gt;
&lt;body&gt;
&lt;div id="qunit"&gt;&lt;/div&gt;
&lt;div id="qunit-fixture"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
Heading to that page now gives you a rundown of your tests:

<img class="size-full wp-image-1861 aligncenter" src="http://davidsherlock.co.uk/wp-content/uploads/2014/10/Screen-Shot-2014-10-13-at-10.54.16.png" alt="Screen Shot 2014-10-13 at 10.54.16" width="557" height="173" />

With that the framework all you need to do is write the tests, QUnit documentation has some great examples. The first thing that went through my head when writing the Unit tests was ‘What exactly is a Unit?’. While it sounds like a silly question ut I found it a great place to start as it makes you think about how your code is structured. This is particularly useful for somebody like me who likes to knock up ideas with bits of code from previous projects I’ve been working on, projects where I may have structured my code slightly differently between them. My first test simply checks that a string is returned from one of my functions:
<pre class="lang:default decode:true">test('getParameterByName()', function() {
    ok( getParameterByName("quiz?topic=value"), "Value is True" );
})</pre>
The key thing I'm taking from this at present isn't that the Unit Tests check if my code works, but it is making me think about how my code is structured. I was hoping at this point to be writing more tests, but the exercise has made me think about restructuring my code again. I'm going to give it a go and I am hoping that it will be easier this time I have Qunit to help me.

&nbsp;