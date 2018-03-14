---
ID: 2147
post_title: >
  Transferring Data From a Microsoft Phone
  App using ISeTool.exe
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/transferring-data-microsoft-phone-app-using-istool-exe/
published: true
post_date: 2015-03-06 18:08:15
---
A while ago I wrote some revision apps for the Android Market place, these are not currently on the store as I have parted ways with the Android Marketplace and have started working with the Windows Phone tools instead. One of the things that used to annoy me about my Android application was that the application used to ship with CSV files. Then during its first boot it would load its local SQLite datastore with the contents of the CSV files. I always wondered why I couldn't just ship my application with a loaded database.

In Windows Phone you apparently can, although it is not recommended to ship it with a SQL CE file you have made yourself. It appears instead that Microsoft want you to create a 'helper' application that creates your database, you can then ship you database with your application. While I am still relatively new to mobile development I still don't really get why there isn't just a database creation tool that can help me design and populate my database, I guess it has to do with the Windows Mobile 8 database storage APIs and needing access to Windows Mobile 8 itself to create and populate the database? If anybody knows I would appreciate an explanation. Still, having an helper application makes me code feel 'cleaner', and the creation of the data is separate from the application that does stuff. I'm still getting used to the MVVM model, but it doesn't seem a million miles away from MVC.

As I say, I'm new to this but my work process for creating an application is now

1) Build helper application as <a href="https://msdn.microsoft.com/en-us/library/windows/apps/hh202876%28v=vs.105%29.aspx">per the instructions here.</a> If you poke about on Google you can find the Visual Studio solution download for the project.

2)Edit the application so that it has your data model.

3)Run application from Visual Studio

4)You now need to transfer the data from the emulator or physical phone. I'm using a physical phone because <del>Microsoft have this stupid layered windows scheme where you can't do simple stuff without the version of Windows above what you have</del> I don't have Windows 8.1 Pro.

To transfer from the phone you need a tool that is installed with the Windows Phone SDK called the IsolatedStorageTool and the GUID of the application, I found this in the output dialog of Visual Studio. It is a command line tool and can be run from the prompt like so:

C:Program Files (x86)Microsoft SDKsWindows Phonev8.1ToolsI
solatedStorageExplorerToolISETool.exe" ts de 77A80316-384D-40DC-A8C3-C4054676E8
5C d:

ts is the argument to download the filesystem and de dictates a physical device, just run ISETool for a list of commands.

I have noticed that there is a SQLite download for Windows Phone 8. I wonder if all this was worth it? I guess so, I'd never even heard of LINQ before I got started! I recorded myself downloading the database:

http://youtu.be/BV1MXgRZbuw