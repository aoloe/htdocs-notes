# setup sandstorm on pi

... rather than own clown with plugins...

it does not work, since sandstorm only works on x86-64

alternatives:

- https://yunohost.org/
  - seems to have very few apps officially supported
- https://cozy.io
  - documentation is not as clear...
- https://arcos.io
  - still beta
    - still beta



# streaming (the desktop) from linux

- http://realmike.org/blog/2011/02/09/live-desktop-streaming-via-dlna-on-gnulinux/
  - mediatomb
  - a set of scripts
  - This command line takes sound from PulseAudio and screen images from X11 (at 20 fps) and combines them into a Matroska file using the H.264 codec for video and AC3 for audio. It grabs a rectangular area of 1024×576 pixels, 128 pixels from the left edge of the screen and 224 pixels from the top edge of the screen:

    ~~~
    ffmpeg -f alsa -ac 2 -i pulse -f x11grab -r 20 -s 1024×576 -i :0.0+128,224 -acodec ac3 -ac 1 -vcodec libx264 -vpre fast -threads 0 -f matroska ~/Videos/capture.mkv
    ~~~

- https://www.reddit.com/r/linux/comments/1mf77q/is_there_anyway_to_stream_my_desktop_to_my_tv_via/
  - minidlna for sending
- [Capture video of a linux desktop](http://www.commandlinefu.com/commands/view/148/capture-video-of-a-linux-desktop)
- vlc?
  - <http://praxistipps.chip.de/vlc-dlna-und-upnp-streaming-einrichten-so-gehts_36568>
  - <https://software.grok.lsu.edu/Article.aspx?articleid=14625>
  - a vlc appimage is already in `~/bin`

# appimage

- create a virtualbox with ubuntu 14.4 (a older linux for a compatible libc & co)
- build the AppImageKit
- probably, it's possible to mount the current AppImage, get all the content, replace scribus with the one compiled (and its plugins) and rebuild a new image.

notes:

- `sudo mount -o loop /tmp/Scribus-1.5.3.svn.21360-x86_64.AppImage tmp/`

# lg in north italy

- http://www.bubblesfactory.it/b/?page_id=1136
- http://uidu.org/search/linux
- libre italy
- https://www.facebook.com/groups/blenderitalia/

# sinhala fonts

- https://github.com/mooniak
- https://github.com/mooniak/sinhala-font-tools/blob/gh-pages/testing/sinhala-font-test-lines.txt
- https://github.com/mooniak/sinhala-font-tools/tree/gh-pages/testing

# digital publishing toolkit

- https://github.com/DigitalPublishingToolkit/hybrideditor
- https://github.com/DigitalPublishingToolkit/epubster
- https://github.com/DigitalPublishingToolkit/sausagemachine
- https://github.com/DigitalPublishingToolkit/Hybrid-Publishing-Resources

# gottardo

http://www.sbb.ch/freizeit-ferien/ferien-kurz-trips-schweiz/regionen/gotthard/gottardino-sonderzug.html

# dell xps 13

- the usb-c dell adapter does work but...
- with lxrandr and the qumi q6 i can only get it to mirror part of the screen, position is not available for it.

- https://wiki.archlinux.org/index.php/Dell_XPS_13_%282015%29
- http://frankshin.com/installing-archlinux-on-dell-xps-13-late-2015-skylake-9350/ (older source for the archlinux wiki page)
- for hdmi/vga https://github.com/advancingu/XPS13Linux/issues/6 links to  http://www.amazon.com/Cable-Matters%C2%AE-DisplayPort-Thunderbolt-Compatible/dp/B00ESM3ISM/ref=sr_1_fkmr1_2?ie=UTF8&qid=1438355727&sr=8-2-fkmr1&keywords=CSL+-+3in1+Mini+Display+Port
- does the dell adapter work or not? https://github.com/advancingu/XPS13Linux/issues/6
- negative experience on installing debian testing: http://nerdjusttyped.blogspot.ch/2015/11/linux-debian-testing-on-dell-xps-13.html

## updgrade the bios

- it's an xps 13 9350
- `sudo cp /home/hugo/Downloads/XPS_9350_1.3.3.exe /boot/efi/`
- Then reboot your computer to the BIOS menu by pressing “F12” when the Dell Logo is displayed. Select “Bios Flash Update” and the update will be installed.
- the bios seems to be up to date...

## install debian testing

- boot with an ubuntu iso to start gparted and resize the main partition
- installig debian:
  - <https://wiki.debian.org/InstallingDebianOn/Dell/Dell%20XPS%2013>
  - <https://wiki.debian.org/InstallingDebianOn/Dell/Dell%20XPS%2013%209343>
  - get and dd the non free netinst iso (for the wifi) of debian testing: http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/
  - disable secure boot in the bios
  - get the firmware for the wifi and copy the needed files to a second usbstick
    - `git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/linux-firmware.git`
    - `cp iwlwifi-8000C-20.ucode iwlwifi-8000C-19.ucode iwlwifi-8000C-18.ucode iwlwifi-8000C-17.ucode /mnt/usb_a/`
  - minimal setup:
    - setup the wifi:
      - `iwconfig` to find out that the wlan card is called `wlp58s0`
      - configure the network interface:

        ~~~
            auto wlp58s0
            iface wlp58s0 inet dhcp 
                wpa-ssid {ssid}
                wpa-psk  {password}
        ~~~

        <http://unix.stackexchange.com/questions/92799/connecting-to-wifi-network-through-command-line>
      - `/etc/init.d/networking restart` (was `dhclient wlp58s0`)
      - i should check if i can manage the network with `ifup` and `ifdown` from `ifupdown`
    - install `sudo` and `vim` (remove `vim-tiny`)
    - set `vim` as the default editor and setup `sudo`
    - trying to force ip4:
      - add to `/etc/sysctl.conf`:

        ~~~
# IPv6 disabled
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
        ~~~

	- `sysctl -p`

    - for some "wrong" ip6 router, `wide-dhcpv6-client` must be installed? (rennes...)

## media keys

- install `xbacklight`

status:
- `xbacklight dec 10` does not work, but `xrandr --output eDP1 --brightness 0.5` does.
- no idea what the `-display`parameter in `xbacklight` is.
- `xrandr` only has set, not inc/dec
- `xrandr --prop` seems to suggest that brightness is not enabled / supported.
- <https://bbs.archlinux.org/viewtopic.php?id=77832> explains how to bind the key in dwm
- <https://bbs.archlinux.org/viewtopic.php?id=58298>
- <http://www.woozle.org/~neale/src/dwm/>
- <https://wiki.archlinux.org/index.php/Backlight#systemd-backlight_service>
- currently trying adding the parameter to grup or xorg confg
  - <http://askubuntu.com/questions/476664/cannot-change-backlight-brightness-ubuntu-14-04>
- i've added a file `./etc/X11/xorg.conf.d/20-intel_backlight.conf` with the content

  ~~~
Section "Device"
	Identifier "card0"
	Driver "intel"
	Option "Backlight" "intel_backlight"
	BusID "PCI:0:2:0"
EndSection
  ~~~

    `.local/share/xorg/Xorg.0.log` seems to confirm that the file is read... but nothing is change
- i've downloaded <https://raw.githubusercontent.com/wavexx/acpilight/master/xbacklight> and symlinked it in `/usr/local/bin` and it seems to work... i have to check if it changes the battery use.


## hidpi

- https://wiki.archlinux.org/index.php/HiDPI

## dwm

- <https://www.reddit.com/r/unixporn/comments/3cxhuj/dwm_did_someone_say_hidpi_simstim/?>

## wlan without wicd?

- <https://www.howtoforge.com/how-to-connect-to-a-wpa-wifi-using-command-lines-on-debian>
- <https://wiki.debian.org/WiFi/HowToUse>

(create a small gui tool that creates the connection? and show the status in the dwm status bar? parsing the result of `iwlist scan` & co?)

(or use connman?)

## problems

- how to get claws-mail not to be full screen
  - `xprop` gives the class that one can use for the rules in `config.h`


## problems

- how to get claws-mail not to be full screen
  - `xprop` gives the class that one can use for the rules in `config.h`
# imac as a tv

- https://kodi.tv/
- http://openelec.tv/

# raspberry pi 3

- get [minibian for raspberry pi](https://minibianpi.wordpress.com/)
- untar the file and dd it (`dd if=abc.img of=/dev/sdb` -bs 4M)
- boot the rpi with an ethernet cable attached
- find the pi's ip address (`nmap -sn 192.168.1.0/24`)

# OTS organizers meeting

- where?
  - rackspace
  - liip
  - revamp-it
  - schuel
  - zhdk
  - gloria
  - unizh
- when?
  - only one?
  - tuesday?
  - monday?
  - weekend?
- what
  - learning groups
    - c++ for beginners / c++ for not so beginners anymore
    - js and visualisation
    - python
    - web / apps frontend
  - workshops
    - python
    - scipy
    - MicroPython workshop (uche)

# gogs on mac

- download
- unzip
- move to `~/bin`
- create a `gogs` mysql database
- (eventually create a user for `git` (if we want to run it in production on mac)
- run `./gogs web`
- go to `0.0.0.0:3000`
- install
  - put the repositories in `~/gogs-repositories`
- create a user

# dashboards in js

- https://www.golden-layout.com/ (demo at https://terminal.sexy/)
- https://www.patternfly.org/ (used by http://mycontroller.org/)

# exercising c++ 11 and stl

- https://www.hackerearth.com/notes/standard-template-library//
- https://www.hackerearth.com/code-monk-c-stl/
- http://geeksquiz.com/the-c-standard-template-library-stl/
- http://cppquiz.org/quiz/question/115
- http://www.tutorialspoint.com/cplusplus/cpp_online_quiz.htm
- http://digital.cs.usu.edu/~bugs/quizzes/stl.html
- http://halpernwightsoftware.com/stdlib-scratch/exercises.html
- http://cs.brown.edu/~jak/proglang/cpp/stltut/tut.html
- http://www.codeproject.com/Articles/854127/Top-Beautiful-Cplusplus-std-Algorithms-Examples
- http://www.codeguru.com/cpp/article.php/c18131/C-Tutorial-10-New-STL-Algorithms-That-Will-Make-You-A-More-Productive-Developer.htm
- https://www.safaribooksonline.com/library/view/c-for-the/9780133257120/ch18.html
- http://www.bogotobogo.com/cplusplus/stl4_algorithms.php

- http://www.nytimes.com/interactive/2015/07/03/upshot/a-quick-puzzle-to-test-your-problem-solving.html

- http://exercism.io

# website for chloe

- hugo? static sites in go?
- or move her template to wp?
- or urubu in python?
- pelican?

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
- [HDMI2USB: Open video capture hardware + firmware](https://github.com/timvideos/HDMI2USB)
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
