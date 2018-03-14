---
ID: 400
post_title: 'Thinking out loud: Can Information Theory help with my datamining?'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/thinking-loud-can-information-theory-help-datamining/
published: true
post_date: 2013-10-16 11:00:23
---
As of late I’ve been playing with lots of techniques to churn through a corpus of information related to me that I have scraped from the web. Many of these techniques pull back topics, phrases, documents and tell me that they have been identified as important; it is then left to me to work out why. I’ve been thinking about methods I could use that could give me more of an insight into what the topics, phrases and documents that are pulled back actually mean.

While working on data mining MOOC I came across the C4.5 algorithm, an algorithm used to generate a decision tree. Wondering how exactly the algorithm chooses where attributes should sit in the tree, I decided to poke around and found it does so using a concept called information entropy.

While I’m still in kick the tires mode at the moment I find the concept very interesting and am wondering how I could plug something around this into the researcher api/personal corpus. From what I can gather information entropy quantifies how much information is in a message within a communications system. It’s like a scale for information, measuring in units called bits

Communication can take many forms, this blog post, my youtube videos, a picture, somebody whistles, a drawing. etc etc and it seems that the problem in information theory is transmission and receiving of data through these form  of communication.

Now I have a large array of data that is essentially communication data and want to find out how important these bits of communications are to the things I want to say.  From what I can gather information theory decomposes my communication data into two fields, efficient and reliability. Efficiency is how the communication is compressed, is my method of communication through text, a video, whatever (I guess you may think winzip?) and reliability is about techniques that helps me understand things that have gone wrong/missing in the communication (think about the technologies that let you watch a DVD even after your little sister has scratched it). These fields are broken up further into information theory and coding theory. Where do my R scripts fit in?
<table border="1" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td valign="top" width="120"></td>
<td valign="top" width="157">Efficiency (Compression?)</td>
<td valign="top" width="149">Reliability (Error Correction?)</td>
</tr>
<tr>
<td valign="top" width="120">Information theory</td>
<td valign="top" width="157">Lossless:  Source Coding TheormKraft-McMillon

Lossy:

Rate-Distortion</td>
<td valign="top" width="149">Noisy Channel Coding Thm</td>
</tr>
<tr>
<td valign="top" width="120">Coding theory</td>
<td valign="top" width="157">HuffmanArithmetic coding

lempel

&nbsp;</td>
<td valign="top" width="149">Hemming CodesBCH Coddes

Turbocodes</td>
</tr>
</tbody>
</table>
&nbsp;