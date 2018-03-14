---
ID: 811
post_title: >
  Oculus Rift, web based 3D world/video
  viewer
author: David
post_excerpt: ""
layout: post
permalink: >
  https://davidsherlock.co.uk/oculus-rift-web-based-3d-world-video-viewer/
published: true
post_date: 2013-12-16 17:02:32
---
I had a go at creating a web based 3D world that held a series of videos of it it. I wanted people to be able to work around a world checking out videos and turning them on and off. It didn’t work too well but though I might as well blog it in the hope that it helps anybody else trying to do the same thing. I used the <a href="https://github.com/Instrument/oculus-bridge">Oculus Bridge e</a>xamples as a start base.  You can find the example I used in examples/js/first_person.js. There other ways to do web based stuff, Oculus-Rest seems promising but seems to be broken out of the box with the latest Mac update. Plus I like hacking around the examples in the Oculus Bridge library as they are well written and easy to get in to. I recommend anybody starting with the web based Rift development to have a look.

To start you need to locate the function initGeometry and delete all the lines within the function below scene.add(floor), this should be lines 92 to 106 . This will remove the current set up of flying boxes etc and leave you with just floor.  I don’t like the default floor because it reminds me of the an <a href="http://en.wikipedia.org/wiki/Trafford_Centre">evil castle in Manchester</a>,  so I  changed the texture so it was grass. I found a grass texture <a href="http://en.cze.cz/Textures ">I liked here</a> , I downloaded the file, put it in the texture folder, renamed it to tile2.jpg. Now look for the line
<blockquote>floorTexture = new THREE.ImageUtils.loadTexture( "textures/tile.jpg" );</blockquote>
and change it to
<blockquote>floorTexture = new THREE.ImageUtils.loadTexture( "textures/tile2.jpg" );</blockquote>
Now I have a flat glass floor with nothing on it.

[caption id="attachment_812" align="aligncenter" width="455"]<a href="http://davidsherlock.co.uk/wp-content/uploads/2013/12/flatland-Oculus-Rift.png"><img class=" wp-image-812" alt="flatland" src="http://davidsherlock.co.uk/wp-content/uploads/2013/12/flatland-Oculus-Rift.png" width="455" height="413" /></a> Flatland[/caption]
<p style="text-align: left;">This is quite useful in itself because it creates a blank canvas for you to work on. This is how I start most of my Oculus Rift on the web projects.</p>
Now you can add whatever you like to this scene. I wanted to create a large video screen. Once that was working I wanted to add a few more and give users the option to turn the on and off.

Fortunatly there are loads of examples on how to add things to three.js, which is the Javascript library that the Oculus Bridge uses.  First create a new folder under the examples folder in the Oculus Bridge project folder, name this folder ‘videos<a href="https://code.google.com/p/bennugd-vlc/downloads/detail?name=big_buck_bunny_480p.ogv">’. I borrowed a trailer for a film in ogv</a> and put it in to the newly created videos folder.

To then add a video to the scene<a href="http://stemkoski.github.io/Three.js/"> I borrowed  an example here</a>.  But that It boils down to placing the following in the initGeo function below scene.add(floor):

&nbsp;

[codesyntax lang="javascript"]
<pre>//create the video element
video = document.createElement( 'video' );
// video.id = 'video';
// video.type = ' video/ogg; codecs="theora, vorbis" ';
video.src = "video/big_buck_bunny_480p.ogv";
video.load(); // must call after setting/changing source
video.play();

// alternative method --
// create DIV in HTML:
//
// and set JS variable:
// video = document.getElementById( 'myVideo' );

videoImage = document.createElement( 'canvas' );
videoImage.width = 480;
videoImage.height = 204;

videoImageContext = videoImage.getContext( '2d' );
// background color if no video present
videoImageContext.fillStyle = '#000000';
videoImageContext.fillRect( 0, 0, videoImage.width, videoImage.height );

videoTexture = new THREE.Texture( videoImage );
videoTexture.minFilter = THREE.LinearFilter;
videoTexture.magFilter = THREE.LinearFilter;

var movieMaterial = new THREE.MeshBasicMaterial( { map: videoTexture, overdraw: true, side:THREE.DoubleSide } );
// the geometry on which the movie will be displayed;
// movie image will be scaled to fit these dimensions.
var movieGeometry = new THREE.PlaneGeometry( 240, 100, 4, 4 );
var movieScreen = new THREE.Mesh( movieGeometry, movieMaterial );
movieScreen.position.set(0,50,0);
scene.add(movieScreen);

camera.position.set(0,150,300);
camera.lookAt(movieScreen.position);</pre>
[/codesyntax]

&nbsp;

and the following at the top of your render() function:

i[codesyntax lang="javascript"]
<pre>f ( video.readyState === video.HAVE_ENOUGH_DATA )
{
videoImageContext.drawImage( video, 0, 0 );
if ( videoTexture )
videoTexture.needsUpdate = true;
}</pre>
[/codesyntax]

This put the video in my scene, which seems to work… until I switched to Oculus Rift view.. which seemed to break it. Here is a video of it breaking.

http://youtu.be/4Z8amHpns0c

I think the problem may be around the camera I am using and video. Will dig further.