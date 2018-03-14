---
ID: 2142
post_title: >
  VBA script to loop through directory of
  CSVs and create separate PowerPoint
  presentations for each file
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/vba-script-loop-directory-csvs-create-separate-powerpoint-presentations-file/
published: true
post_date: 2015-02-26 12:13:33
---
As per the very long title, this is a Visual Basic for Application that will loop through directory of CSVs and create separate PowerPoint presentations for each file script which I am saving this for future reference.  VBA script to loop through directory of CSVs and create separate PowerPoint presentations for each file based on the contents of the CSV. Because many of the questions in my CSV have a comma I have used ; as a delimiter, I set this when exporting from my original data source (MySQL) , but you can also change the delimiter in OpenOffice without messing with the operating system.
<pre class="lang:vb decode:true ">Sub LoopThroughFiles()
 Dim MyObj As Object, MySource As Object, file As Variant
 Dim csvnamestring() As String

 sPath = "Macintosh HD:Users:David:Desktop:projects:quizes:RS:"
 file = Dir("Macintosh HD:Users:David:Desktop:projects:quizes:RS:")
   While (file &lt;&gt; "")
      If InStr(file, "csv") &gt; 0 Then
         MsgBox "found " &amp; file
            Dim ppPres As Presentation
            Dim filenamestring As String

            filenamestring = file + "PowerPoint" '&lt;-change to your file path/name

            'Create an instance of PPT to work with
            Set ppApp = CreateObject("Powerpoint.Application")
            ppApp.Visible = True

            'Create a new presentation (or you can access an existing file with ppApp.Presentations.Open
            Set ppPres = ppApp.Presentations.Add

            'Save:
            ppPres.SaveAs filenamestring, 1

                Dim csvpath
                csvpath = sPath &amp; file
                MsgBox csvpath


                Const strFileName As String = "Macintosh HD:Users:David:Desktop:projects:quizes:RS:"
                Open csvpath For Input As #1

                row_number = 0

                Do Until EOF(1)

                    Line Input #1, LineFromFile
                    LineItems = Split(LineFromFile, ";")
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
                Close #1</pre>
&nbsp;

&nbsp;