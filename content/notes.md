# External monitor on debian

for using an external monitor, just install (and run) `lxrandr`.

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
