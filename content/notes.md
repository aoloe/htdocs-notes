# youtube on android in the backgraound

- start playing the video
- move to the end and let it finish
- press the "home button" and get out of youtube
- swipe down and restart the video
- but it seems to crash after a few minutes...

# android development on debian

- openjdk seems to be good enough. 
- add `lib32stdc++6`: it's a 32 bits app! (otherwise you'll get a "Unable to run mksdcard SDK tool" an error on firs start / install).
- add `qemu-kvm libvirt-bin` for the emulation.
- add `lib32z1`. (libz for 32 bits; otherwise the gradle tasks runs forever)

# lua and löve

Hi there! LÖVE is an *awesome* framework you can use to make 2D games in Lua. It's free, open-source, and works on Windows, Mac OS X, Linux, Android and iOS.

https://love2d.org/

- https://love2d.org/wiki/Game_Distribution
- maybe better used with http://moonscript.org/ a programmer friendly language that compiles to lua
- https://love2d.org/wiki/Category:Tutorials
- https://github.com/kikito/love-tile-tutorial/wiki
- http://osmstudios.com/tutorials/your-first-love2d-game-in-200-lines-part-1-of-3

# c++ and gosu

a game engine for c++

# python3 and virtualenv

    virtualenv --python python3 projectname
    source projectname/bin/activate

- it is possible to activate virtualenv in multiple terminals

# geschenke

- <http://dscvr-guide.com>:  Reiseführer des Zufalls 20€

# c'est dans la vallée

- Hotel Wistub Aux Mines d'Argent (complêt)
- info@bagenelles.com (requête par email)
- Auberge du Tunnel (+33 3 89 58 74 25, 1 km)
- Auberge Du Petit Haut, 56 Lieu-dit Petit Hau (http://www.valdargent.com/petit-haut/; 03 89 58 72 15; 4 km)
- http://www.auberge-sobache.com/ (5 km)
- Cicci Véronique, B & B (+33 3 89 58 70 46)
- Patris Jean-Paul, B & B (+33 3 89 58 75 24; 2.5 km)
- Auberge du Randonneur (+33 3 89 58 71 31; 3 km)
- Chambres d'hôtes - Ferme de la Fonderie (17 rue Untergrombach, Tél : 03 89 58 59 51; ferme.lafonderie4@calixo.net; http://www.fermelafonderie.com)
-  Chambre d'hôtes chez Mme Nicolaï (9 Rue du Champs de la Chatte; 06 30 57 61 31; marie-paule.nicolai@hotmail.fr)
-  Chambre d'hôte Mme pascale JUNG (26 rue Saint-Louis Tél : 03 89 58 69 05 samuel_pascale@yahoo.fr)
- camping...

http://www.valdargent-tourisme.fr/ et http://www.valdargent-tourisme.fr/chambres-hotes

# a cheap recording station

all we need is a readable capture of the screen, a preview of what is happening on the scene (if possible with two points of view) and good audio.  
and live mixing, so that we avoid the big delays related to the post processing.

- a wireless router for connecting the devices
- a laptop for mixing the streams
- an arduino (or similar) connected to a mic, streaming the audio to the internal network
- two arduinos (or similar cheap hardware) connected to two good wecams for streaming a VGA video to the internal network
- a browser and webrtc for streaming of the presentation laptop/computer screen  to the internal network
- the streams get live mixed during the presentation (if the compression cannot be done right away a second laptop can be used to batch create the mp4 (or similar) files and upload them to video sites.

alternatives:
- webcams could be connected through long usb cables

some links and notes:
- arduino, audio and video:
  - http://forum.arduino.cc/index.php?topic=188690.0
  - http://forum.arduino.cc/index.php?topic=218631.0
- mixing software too look at:
  - http://sourceforge.net/projects/webcamstudio/
  - https://www.dyne.org/software/freej/
  - http://www.opensourcebroadcast.com/category/directory/video-post-production
- other:
  - http://blog.eltrovemo.com/364/diy-broadcast-how-to-build-your-own-tv-channel-with-open-source-other-goodies/
  - http://sonicrobots.com/2015/04/01/a-multi-usb-webcam-approach-with-open-frameworks/
  
# starting the svn server

    svnserve -d -r /mnt/backup/svn/

# jogging music

- mat & kim (tablet)
- violent femmes
- pyramid vritra - intra - 04 - monkeybread
- to rococo rot - speculation - 01 - away

# inkscape 0.91 on debian jessie

download the newest debian package:

https://packages.debian.org/experimental/amd64/inkscape/download

and then run:

    dpkg -i inkscape_0.91.0+40.2_amd64.deb

(i had to install livisio and libcdr first)

and don't forget to remove inkscape before upgrading to a version that has 0.91!

(cf. <http://www.jesusda.com/blog/index.php?id=508#instalacion-debian>)

# dvd on debian

- play with `mplayer dvd://` (`dvdnav://` does not seem to work)
- rip with `handbreak`. from terminal with `HandreakCLI` (cf. script in `bin_etc/`)

# Firefox Phone

## update

- <https://hacks.mozilla.org/2013/08/pushing-a-firefox-os-web-app-to-zte-open-phone/>
- <https://hacks.mozilla.org/2014/01/upgrading-your-zte-open-to-firefox-1-1-or-1-2-fastboot-enabled/>
- <https://hacks.mozilla.org/2013/12/upgrading-your-zte-open-to-firefox-os-1-1/>

## mail on sms

- SMS Notifier (Colin): <https://gist.github.com/colinfrei/48476f365ee8f451534c>

index.html

~~~
<!DOCTYPE html>
<html>
<head>
</head>
 
<body>
<div id="stuff"></div>
<button id="button">fdoo</button>
<script type="text/javascript">
    var xmlhttp;

    // from https://developer.mozilla.org/en-US/docs/Web/API/notification
    navigator.mozSetMessageHandler('sms-received', function onSMS(sms) {
        xmlhttp = new XMLHttpRequest();

        xmlhttp.open("POST", "http://labs.colinfrei.com/gotSms", true);
        xmlhttp.send();
    });
</script>
</body>
</html>
~~~

manifest.webapp
~~~
{
    "name": "SMS Playground",
    "description": "Try and handle receiving SMS",
    "launch_path": "/index.html",
    "type": "certified",
    "permissions": {
        "sms": {},
        "backgroundservice": {},
        "desktop-notification": {}
     },
    "messages": [
        { "sms-received": "/index.html" },
        { "notification": "/index.html" }
    ]
}
~~~

# Pyhton, virtualenv and virtualenvwrapper

`virtualenvwrapper` provides a simpler enviroment around `virtualenv`.

~~~
$ apt-get install virtualenvwrapper
# restart the terminal
$  mkvirtualenv virtualenv
# enable global packages
(virualenv) $ toggleglobalsitepackages
~~~

for python 3

   mkvirtualenv -p /usr/bin/python3 glamhack

# Restoring a deleted file from a svn repository

- `svn log -v .` on the parent directory and grep / less find for the filename to find the revision deleting the file
- `svn cat svn://url.com/repository/path/to/the/file.txt@00000` (where 00000 is the last revision where the file was present) to echo the content of the file (yes, you can redirect it to a file).

# External monitor on debian

for using an external monitor, just install (and run) `lxrandr`.  
if the external monitor is not there yet, but the mouse still goes far to the right, run `xrandr --auto` to get back to the "normal" setup.


on top of it:
- https://code.google.com/p/open-pdf-presenter/
- https://github.com/jakobwesthoff/Pdf-Presenter-Console

(i have to test what `xrandr --auto` does...)

# using demnu

kajetan wrote to the suckless ML

~~~
Just want to share super-simple, crappy written yet quite useful (at
least for me) script I've written while ago.
I run it via bind with Ctrl+O

bind '"\C-o":". ~/.dbdb.sh\C-m"'

and the script

#!/bin/sh
CHOSEN="just for not being empty"
DMENU="dmenu -i -fn -*-terminus-medium-r-*-*-14-*-*-*-*-*-*-*"
COLORS=" -nb #000000 -nf #706c9a -sb #000000 -sf #dddddd"
while [ "$CHOSEN" != "" ]; do
   clear && pwd && ls -X
   CHOSEN=`( ( echo "../" && ls -1p ) | grep "/" ) | $DMENU $COLORS`
   cd "$CHOSEN"
done
~~~

# Usb tethering and Debian

- activate it on the tablet / mobile
- `dhclient usb0`
#
# Wifi and ETH0 on debian
- in `/etc/modprobe.d/local-b43.conf` set `options b43 allhwsupport=1`
- it's eth1, stupid.

# Screencasting to Gif

- http://javier.io/blog/en/2014/03/21/ffcast.html
- https://github.com/lolilolicon/FFcast
- http://unix.stackexchange.com/questions/113695/gif-screencasting-the-unix-way
- http://askubuntu.com/questions/107726/how-to-create-animated-gif-images-of-a-screencast
- http://www.maketecheasier.com/record-desktop-as-animated-gif/
- https://github.com/GNOME/byzanz
- https://github.com/DOOMer/screengrab
- https://github.com/aoloe/drawrect
- http://linux.die.net/man/3/xsetwindowattributes
- http://www.unix-manuals.com/tutorials/xlib/xlib.html
- http://tronche.com/gui/x/xlib/window/XCreateWindow.html
- http://tronche.com/gui/x/xlib/GC/manipulating.html
- http://linux.die.net/man/3/xgcvalues

alternative:

- capture the full screen
- start a gif editor
- set the size of the selection and initial size of the capture
- show each frame that is different from the previous one
- you can move the selection (keys + mouse), crop or remove the set of equal frames
- optionally let add text and a mouse highlighter (position, click, double click)

# Markdown and Github based CMS

- http://realms.io/ : Git based wiki written in Python

in [this HN discussion](https://news.ycombinator.com/item?id=9262260) there are several hints for creating a web application that allows forking documents... it might be easy to implement...

- each user (viewer?) can get to an edit view of the document.
- the main document lists the available views.
- everybody can see all the (moderated) forks.
- the redactors are notified about each fork.
- there is a way to see a diff between the main document and each fork (and export the diff?).
- accepted diffs are put in a log and the fork removed.
- for the sake of CC-BY-SA we should track all the contributors
- there should be an easy way to contribute images.

# Scribus and complex scripts

- we could need an analysis and update of [State of Text Rendering](http://behdad.org/text/)

# Programming with Scratch and Kids

- [An Educator's Guide to Scratch Programming](http://www.scratchprogramming.org/)
- http://inventwithscratch.com/ (and http://inventwithpython.com/index.html)
- http://www.campuslacamilla.it/scheda-corso-scratch/ e http://www.campuslacamilla.it/wp-content/uploads/2014/01/Scratch-2.0-Modulo-didattico.pdf
- a good website as an example for us http://coderdojomilano.it/
- a js (in browser) version of scratch: http://snap.berkeley.edu/

Python:
- http://www.briggs.net.nz/snake-wrangling-for-kids.html

# App Inventor and App Maker

- https://apps.webmaker.org/
- http://www.appinventor.org/
  - http://appinventor.mit.edu/explore/resources/beginner-app-inventor-concept-cards.html

Possible projects:
- Solitaire game
  - https://www.youtube.com/watch?v=ziDLN-lU5xE (drag and drop)
- Memory
- Pong http://www.appinventor.org/pong-steps
- LED messages
  - find width and height
  - fill with dark red dots
  - define a text that can be converted in dots
  - how to convert text to dots?
  - scroll the text
# A Fairphone with no Google in it

Sandra is asking for:
- syncing with windows
- listening to music (laptop + android)
  - on android [vanilla](https://github.com/adrian-bl/vanilla)?
  - on windows [miro](http://www.getmiro.com/)?

Fairphone:
- install f-droid
- find an alternative music player
- OSMAnd
