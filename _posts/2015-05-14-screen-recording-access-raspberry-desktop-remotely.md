---
ID: 2312
post_title: 'Screen Recording Pi  / Access Raspberry Pi Desktop Remotely'
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/screen-recording-access-raspberry-desktop-remotely/
published: true
post_date: 2015-05-14 09:09:06
---
I've recently been recording the screen of my Raspberry Pi to show a friend how to do various things on it, I've been asked to share my technique for screen recording. The truth is that I am not actually running any recording software on the Pi itself, I have set up access to the Pi so that I can control it from another computer and I am recording on that computer. This means I do not have to have the Pi plugged in to a monitor and I do not need a mouse/keyboard set up. I have Raspbian installed, but I guess any Debian based operating system should be the same.

Note: I am going to do it a very easiest way that will set up your Pi is less than 5 minutes. I have done it this way because is a great way to do it if you are messing around at home or school, I guess that is the situation that most Pi users find themselves in. This method isn't super secure and I don't recommend setting it up this way if you plan on doing anything serious with it on private networks.
<h3>1. Update your Pi</h3>
Open a terminal, on Raspbian this is the program LXTerminal, in there type the following commands one at a time:
<pre class="lang:default decode:true">sudo apt-get update
sudo apt-get upgrade
</pre>
These commands first updates your operating system so it has the latest information regarding the versions of packages and dependencies available and then will upgrade to these version. This might take a while.
<h3>2. install tightvncserver</h3>
Tightvncserver is lets you connect to your Pi via VNC which is a graphical desktop sharing system, we will need to connect this way to record. Installing Tightvncserver is easy at the terminal:
<pre class="lang:default decode:true ">sudo apt-get install tightvncserver</pre>
<h3> 3. Give your Pi a static IP address</h3>
I found it was easier to give the Pi a static IP address so that I wouldn't have to go and find out the IP every time I wanted to connect you need to edit a file to do this, you can get to the file by typing:
<pre class="lang:default decode:true ">sudo nano /etc/network/interfaces</pre>
You should now see a text file in your terminal and you are editing it using a program called Nano. You want to look for a line that says
<blockquote>iface eth0 inet dhcp</blockquote>
This line is telling your network interface to get an IP address automagically, we want to change that so we know exactly which IP it has at all times. To change it you need to remove dchp and type static, followed by 5 lines of network config. Here is an example of what you could replace the line with. Obviously the settings will depend on your network setup, if you want some help then you can quit nano and see what the network config already looks like with the command ifconfig.
<pre class="lang:default decode:true">iface eth0 inet dhcp
address 192.168.0.115
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
gateway 192.168.0.1</pre>
You can quit nano with ctrl-x, dont forget to save. I like to reboot at this point, probably because I have a Windows background. Reboot with sudo shutdown -r now
<h3>4.  Start VNC server</h3>
Once you have rebooted you can run tightvncserver with the following command:
<pre class="lang:default decode:true ">tightvncserver :1 -geometry 1024x640 -depth 24 -dpi 64</pre>
This sets a new vnc connection on 'display 1', tou can change the resolution and the such if you wish.
<h3> 5. Connect</h3>
You can now connect from a machine of your choice. Your computer will need a VNC viewer, there are a few about and you can <a href="http://www.realvnc.com/download/viewer/">download some from the real vnc site</a>. When connecting you will need to know the IP address that we set before. The VNC viewer will also ask for a 'Display' we set this as 1.
<h3> Video of the process</h3>
https://youtu.be/aedxeIkzAn8

&nbsp;

&nbsp;

&nbsp;