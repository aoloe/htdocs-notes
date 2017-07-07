# pyside2 on debian

https://wiki.qt.io/PySide2_GettingStarted

- i will have to build pyside2 on debian

- "5.7+ version of qt uses c++11 constructs. The c++ parser in pyside 5.6 branch can not handle that. the 5.9 branch of pyside uses clang for parsing, and thus works with qt5.7+."

# couleur3 stream

http://lsaplus.swisstxt.ch/audio/couleur3_96.stream/playlist.m3u8

# collaborating on scribus through irc

http://osp.kitchen/tools/scribus-irc/

# being on facebook

- https://stallman.org/facebook-presence.fr.html
- http://dock18.ch/medienkultur/2014/02/20/we-leave-facebook/

# westworld

- [the science of westworld](https://blog.plan99.net/the-science-of-westworld-ec624585e47) + [hn thread](https://news.ycombinator.com/item?id=13343613)

# displaylink ubs external monitor

http://foolcontrol.org/?p=1777

# companies having participated in scribus development

- http://www.newspapersystems.com/ (William Bader, Juraj Fedel)

# scribus, scripter and signals

~~~
< a-l-e> just wondering: did you work on py(qt) scripting inside of krita?

< boud> yes
I'm now finishing it up
I tested a bunch of approaches -- pythonqt, pyqt + sip, generating sip from cmake using llvm, mikro.py, and in the end went with hand-written sip files around a wrapper library.

You can read my write-up here: https://phabricator.kde.org/T1625

I took the scribus ng scripter at one point, and fixed a bunch of issues with it, but it never felt solid to me, for some reason, probably irrational.

< a-l-e> and do you think that scribus should take your approach?
< boud> it's hard to say -- I also couldn't get signals working properly with the mikro.py approach, and there was a lot of marshalling of qobjects.
But I took about four months of full-time work to wrap a dedicated subset of Krita's functionality

< boud> (we created and killed at least 3 different scripting modules, 4 if you count opengtl)
< boud> This was kinda straighforward, and Phil Thompson could answer my questions on sip easily -- and there's a lot of compile-time checking of the
        wrapper.
< boud> and I still need to figure out how to bundle python3 with a mingw-built version of krita on windows.
< boud> the signal stuff made me feel like cadwallader -- nothing works!

<boud> some improved code: it's in krita/plugins/extensions/pykrita/plugin/krita/attic
~~~

# muda and opendata

- register/login does not work anymore: http://muda.co/iooiiooi/
- scrap alt-zurich and create tags for all images: http://www.alt-zueri.ch/turicum/strassen/p/pfingstweidstrasse/pfingstweidstrasse.html
- know where undeground rivers are, how much water they carry, visualize them:
  - https://data.stadt-zuerich.ch/
  - https://www.stadt-zuerich.ch/ted/de/index/geoz/geodaten_u_plaene/leitungskataster.html
- https://www.stadt-zuerich.ch/portal/de/index/ogd.html
- https://forum.schoolofdata.ch/t/what-tools-do-we-use-for-data-wrangling/202
- https://forum.schoolofdata.ch/t/1-5-3-1001-2-muda/203/4

# a collection of (interesting) wordpress plugins

- Timber (use twig templates for your own work)
- Carbon Fields (some sort of aggregator)
- MultilingualPress (for multilanguage sites... free?)
- Coral Remote Images (link to the online uploads from the local dev mirror)
- For images, change the filename on upload (add "seo" words and ask for the topic to the user)
- The SEO Framework

# wordpress plugins with composer

this is the minimal `composer.json` file, for installing wordpress plugins that have an own `composer.json` file with the type `wordpress-plugin` (or for themes defined as `wordpress-theme`)

~~~.json
{
    "name": "aoloe/wptest",
    "authors": [
        {
            "name": "ale rimoldi",
            "email": "ale@graphicslab.org"
        }
    ],
    "require": {
        "composer/installers": "1.*",
        "anttiviljami/wp-libre-form": "^1.2"
    }
}
~~~

# chromium does not load the plugins / extension anymore

add 

    export CHROMIUM_FLAGS='--enable-remote-extensions'

to `~/.profile` and/or `~/.xinitrc`

# scribus, travis, and appimage

~~~
curl -L http://api.travis-ci.org/repos/scribusproject/scribus/builds.json
[
{
    "id":203210746,
    "repository_id":4761381,
    "number":"643",
    "state":"finished",
    "result":0,
    "started_at":"2017-02-19T18:39:05Z",
    "finished_at":"2017-02-19T19:23:00Z",
    "duration":7058,
    "commit":"51e1f0de975ec77951e397e2a7982b5eae2effe0",
    "branch":"master",
    "message":"#14630: Moving multiple items across pages using the outline panel doesn't work properly\n\ngit-svn-id: svn://scribus.net/trunk/Scribus@21790 11d20701-8431-0410-a711-e3c959e3b870",
    "event_type":"push"
},
{...
]

result:null seems to be the failing one
finished_at for the build date

curl -L https://api.travis-ci.org/repositories/scribusproject/scribus/builds/203210746.json

matrix [id: 203210747

https://travis-ci.org/scribusproject/scribus/jobs/203210747
~~~

# scribus and flatpak

jurf suggests:

so, if you want to try it, it’s a simple `flatpak install https://jurf.gitlab.io/scribus-flatpak/scribus-nightly.flatpakref`


~~~
https://paste.gnome.org/pefuvzcek
you need to put this in the same directory to compile boost however (stole it from the KDE guys): https://paste.gnome.org/pu4pkxmrt
first thing is called "net.scribus.ScribusDevel.json", the second "boost-configure"
you can compile it with a
flatpak-builder --force-clean --ccache --repo=repo scribus net.scribus.ScribusDevel.json
(if you want ccache and a generic repo name)


flatpak --user remote-add --no-gpg-verify --if-not-exists scribus-repo repo
to add the repo to flatpak’s sources
flatpak --user install scribus-repo net.scribus.ScribusDevel
to install it, the you can run it with "flatpak run net.scribus.ScribusDevel"

and to update it on a recompile or whatever a simple:
flatpak --user update net.scribus.ScribusDevel
is needed
good luck!

here are the very unfinished manifests so far: https://github.com/jurf/scribus-flatpak
~~~

# logitech mouse with short cord

M/N:M-U0017
P/N:810-001369
PID: LZ021A5

# learning rust?

- https://github.com/ctjhoa/rust-learning
- https://doc.rust-lang.org/book/
- https://zsiciarz.github.io/24daysofrust/book/vol1/day2.html
- https://github.com/cyndis/qmlrs
- https://www.quora.com/Is-Rust-worth-it-to-learn
- http://cglab.ca/~abeinges/blah/too-many-lists/book/

# OCR

how to convert a bitmap pdf to epub?

some ideas

- pdfsandwich to pre-process a PDF
- tesseract for the conversion


or

- pdfocr
- gscan2pdf
>>>>>>> d4562a5d48d673141d9c5c5160c90e8bbfa6f3de

# piping the errors

for piping both the output and the error:

    make 2>&1 | less


# getting git to work when ssh is blocked


add to your `~/.gitconfig` file:

    [url "https://github.com/"]
    	insteadOf = git://github.com/
    [url "https://github.com/"]
    	insteadOf = git@github.com:

to get in through https instead of ssh

# huawei setup

- if you want an app to give notification you have to set it as prioritary in the battery manager.

# reading a sdxc card on linux

- install fuse-exfat (or similar)
- use exfat as the formatting type in the fstab

# make scribus lighter

things i'd like to see removed from scribus:

people keep on wishing new features for scribus. today, i've put together a list of (anti-) features i'd like to see removed from scribus.

- print (replaced by a print through pdf viewer... with configuration).
- default templates (replaced by a website where somebody can download sample documents; ID does not have default templates!).
- the text tool settings (eventually, one should be able to choose a default style).
- the character tab from the paragraph styles (one should pick a character style instead; the style editor should be non modal and multiple styles should be editable at the same time).
- by default only show the tools toolbar. vertically.
- the "print preview" in the file menu (should be an external tool that works on the pdf / ps file).
- the option to make the preview mode non editable (preview should be made through a pdf viewer).
- the edit with story editor entry in the context menu. it should be replaced by an "edit" entry that start the edit mode.
- the story editor (replaced by an advanced "tags" editor).
- the property based table of contents. (even if not replaced by a style based one).
- opening pdf and svg files (they should always be imported as vectors or loaded in image frames). open and save should only work with `.sla` files.
- the script editor.
- automatic text frames (they can be useful in some corner case, but people seem to have more issues with it, than it can help; eventually moving it from the new dialog to the document settings could already help; any way, extending the multiple insert to create new pages and set the link seems to be a more useful and flexible solution).
- the pdf form functionalities, javascript included.
- do not allow restrictions on the usage of the pdf (do not print, do not annotate, password protection).
- presentation effects.
- 3D rendering.
- remove the current dialog that allows to open / new / new from template / open recent. (eventually replace with a few buttons / links on the empty desktop: "new file... / open file... / list of the n latest files / new from template...")


what are the features you would like to see removed?

why remove features?
- some features simply do not work or they are so complicated to use that one should avoid them.
- some features are misleading the user and make the UI complicated.
- some feature should be moved to external tools.

# grafiklabor

wo sind meine notizen? hier etwas dazu...

- haar freistellen
  - mit hintegrund: https://www.youtube.com/watch?v=MCZyjJ2Ps4Y
  - ohne intergrund: https://www.youtube.com/watch?v=CuhzA4wCDgY
-  panorama zeichnen: http://www.2dgameartguru.com/2016/07/create-clouds-using-circles-in-inkscape.html
- text as shape https://www.youtube.com/watch?v=l3BHcregNUs and http://forums.scribus.net/index.php/topic,2236.msg10201.html#msg10201
- http://www.yemanjalisa.net/realiser-un-flocon-de-neige-avec-inkscape/

weitere notizen in der grafiklabor repositry, als issues!

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

probono sayz: "just loop-mount the AppImage, cp -r somewhere, edit as you like, and run it though AppImageAssistant again"

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

installed
- pitivi as flatpak package in `~/bin`
- simplescreenrecorder
- `npm install gifify` (but i could not get giflossy to compile)
- or with ffmpeg: http://superuser.com/questions/556029/how-do-i-convert-a-video-to-gif-using-ffmpeg-with-reasonable-quality
  `ffmpeg -i ~/test.mkv -vf scale=320:-1 -r 10 -f image2pipe -vcodec ppm - | convert -delay 5 -loop 0 - /tmp/output.gif`

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
