---
ID: 2138
post_title: >
  Auto generating PowerPoint presentations
  from CSV
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/auto-generating-powerpoint-presentations-csv/
published: true
post_date: 2015-02-24 16:58:06
---
I recently held an activity that captured responses to questions from a questionnaire in CSV format. I wanted to be able to convert these answers in to slides on a PowerPoint presentation. Rather than rewrite them all I remembered that Visual Basic for Applications used to be able to do this thing so I jumped on to a Windows machine to try it out. Overall I was quite pleased with how quickly I was able to get some code working, it took about 2o minutes to read through the Microsoft developer documentation and get some working code.

This VBA script will read from one CSV and create two slides for each line, a question slide with a question and a choice of answer, followed by an answer slide that had the response on it. The code is not documented well, but you should get the gist.
<pre class="lang:vb decode:true">Sub CSVReader3()

Dim dataArray() As String
Dim FullName() As String
Dim Pre As Presentation
Dim Sid As Slide
Dim i As Integer

Const strFileName As String = "\HOLLYDS10$DesktopBioquestions_binomial_system_1.csv"
Open strFileName For Input As #1

row_number = 0

Do Until EOF(1)

    Line Input #1, LineFromFile
    LineItems = Split(LineFromFile, ",")
    row_number = row_number + 1

    Set Pre = ActivePresentation
    Set Sld = Pre.Slides.Add(Index:=Pre.Slides.Count + 1, Layout:=ppLayoutText)
    Sld.Shapes(1).TextFrame.TextRange = "Question"
    Sld.Shapes(2).TextFrame.TextRange = LineItems(2) &amp; vbNewLine &amp; _
    LineItems(4) &amp; vbNewLine &amp; _
    LineItems(5) &amp; vbNewLine &amp; _
    LineItems(6) &amp; vbNewLine

    Set Sld = Pre.Slides.Add(Index:=Pre.Slides.Count + 1, Layout:=ppLayoutText)
    Sld.Shapes(1).TextFrame.TextRange = "Answer"
    Sld.Shapes(2).TextFrame.TextRange = LineItems(3)

Loop
Close #1


End Sub</pre>
ToDo: loop through a all the CSVs in a directory and then save a powerpoint file for each.