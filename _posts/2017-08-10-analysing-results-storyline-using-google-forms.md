---
ID: 2617
post_title: >
  Analysing results from Storyline using
  Google Forms
author: David
post_excerpt: ""
layout: post
permalink: >
  http://davidsherlock.co.uk/analysing-results-storyline-using-google-forms/
published: true
post_date: 2017-08-10 14:09:24
---
<!-- wp:group -->
<div class="wp-block-group"><div class="wp-block-group__inner-container"><!-- wp:group -->
<div class="wp-block-group"><div class="wp-block-group__inner-container"><!-- wp:freeform -->
<p></p>
<!-- /wp:freeform --></div></div>
<!-- /wp:group --></div></div>
<!-- /wp:group -->

<!-- wp:paragraph -->
<p>I wanted a simple CSV to analyse the results of students making decisions in the articulate 360 software. Apparently, the storyline 3 software supports xAPI, which I hope to explore, but for now I am happy with a CSV of their answers that could be accessed by anyone with a URL.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Storyline lets users insert small snippets of Javascript into their cards, this is the approach I took.</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Created a Google Form with the answer to questions or decisions being asked</li><li>Imported Jquery</li><li>Used Storyline to set variables</li><li>Use Javascript to get storyline variables and submitted these variables to the Google Form via ajax</li><li>Used Google Forms responses tab to analyse the responses or download the CSV.</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Firstly, some ‘here be dragons’; I am new to storyline having only played with it quite briefly. There may be better ways and feedback is really welcome. These are my notes, but if anybody needs to me to expand them then just ask.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Add jQuery to Storyline Slide</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Now we want to switch back to storyline. On the final slide we want to add jquery so we can submit them through an AJAX call. We are going to be revisiting this bit of Javascript and adding bits to it. For now we will just add jquery to the slide. &nbsp;To add the, head to your final slide and add some javascript as so:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>Create a new trigger</li><li>Set action to ‘Execute JavaScript’</li><li>Set 'when' to timeline starts</li></ol>
<!-- /wp:list -->

<!-- wp:image {"align":"center","id":2620,"linkDestination":"custom"} -->
<div class="wp-block-image"><figure class="aligncenter"><a href="http://davidsherlock.co.uk/wp-content/uploads/2017/08/create_a_new_trigger_storyline.png"><img src="http://davidsherlock.co.uk/wp-content/uploads/2017/08/create_a_new_trigger_storyline-1024x228.png" alt="create_a_new_trigger_storyline" class="wp-image-2620"/></a></figure></div>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>You now want to click the "…" box next to "Script" and paste in this javascript. You do not need script tags:</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group=""></pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">var head = document.getElementsByTagName('head')[0];
var script = document.createElement('script');
script.src='http://ajax.googleapis.com/ajax/libs/jquery/1.10.1/jquery.min.js';
script.type = 'text/javascript';
head.appendChild(script);</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Get Storyline to set variables</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>You now need to go back and set variables,&nbsp; this is quite a common and easy task in Storyline and you may have already done this. What we want to do here is set the variables so they are equal to whatever the data is we want to capture. For example, you might have a slide called question1 with 4 buttons to press and we want to record which button was pressed.&nbsp; Similar to the picture in section 2 we want to create a trigger on each of these 4 buttons. This time though, instead of ‘execute javascript’ we want to set a variable. So, for a question1 slide with 4 buttons we want to create a trigger on each button that sets a variable to the value of the answer.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>For the sake of this example I am going to assume we have three slides, each with a question on. Each slide has 4 buttons that send the user to the next page and save a variable (“questionone”, “questiontwo” or “questionthree”) equal to the name of the button being pressed.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Use Javascript to get storyline variables and submitted these variables to the Google Form via ajax</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Now we want to head back to the final slide and edit the javascript we started before. We are not going to delete the javascript, but going to add a function to it. So under the previous text add the following function:</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">function postToGoogle() {
var player=GetPlayer();
var questionone=player.GetVar("questionone ");
var questiontwo=player.GetVar("questiontwo ");
var questionthree=player.GetVar("questionthree ");
var field1 = questionone;
var field2 = questiontwo;
var field3 = questionthree;
$.ajax({
url: "FORM",
data: {"x ": field1, "x": field2, "x": field3},
type: "POST",
dataType: "xml",
statusCode: {
0: function() {
//Success message
},
200: function() {
//Success Message
}
}
});
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>A lot of this code is borrowed from the jquery site so I have left it as-is. However, I am not sure you will actually get a response code because of cross-domain policies. It would be good if somebody could give me feedback on that. If you have more questions then you will need to add more question variables and add extra fields in the json data element.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Edit the function with your Google Form details</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>There are 4 bits of information the above function needs to work, locate the bits that say "url: "FORM" and the bits that look like this: "x ": field1.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Firstly we need to replace the FORM with the URL that we are submitting to. To get this head over your Google Form and press the view button and then examine the html. You are looking for a url that ends in formResponse and should look like this "https://docs.google.com/forms/d/e/&lt;FORM_ID&gt;/formResponse", Copy and paste it over 'FORM'.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>We now need the ID for each field. They look something like this: 'entry.&lt;id&gt;'. You can either exaime the source looking for these, or better still just inspect the elements using your browsers dev tools. Each X needs to be replaced with the entry and id.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Use the function and try</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Inbetween the two bits of javascript call the function:</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">postToGoogle()</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>Now whenever you run that slide and set variables will be sent to the form as a response, you can download all responses or view them one by one in forms as such (mine is full of test data):</p>
<!-- /wp:paragraph -->

<!-- wp:image {"align":"center","id":2621,"linkDestination":"custom"} -->
<div class="wp-block-image"><figure class="aligncenter"><a href="http://davidsherlock.co.uk/wp-content/uploads/2017/08/do_first_question.png"><img src="http://davidsherlock.co.uk/wp-content/uploads/2017/08/do_first_question-300x127.png" alt="do_first_question" class="wp-image-2621"/></a></figure></div>
<!-- /wp:image -->