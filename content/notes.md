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

# Vis and digraph

A nice vim feature that has little chances to be implemented into vis are digraphs.

- `:digraph` shows all available digraphs
- a nice sorted list: http://linuxprograms.wordpress.com/tag/vim-diagraphs/
- the name digraph is already taken <http://linux.die.net/man/3/digraph_utils>
- [RFC 1345 - Character Mnemonics and Character Sets](http://www.faqs.org/rfcs/rfc1345.html) seems to have better mnemonics than vim
- insert on next line with `:r!kk +-` (personally i'm for !! at the cursor position: why add a new line?)

What about making it my first go project? Mmmm...

- `kk +-` returns `±`
- output is utf8
- `kk -l` list of all digraphs
- `kk -l` list of all math didgraphs
- `kk -s quote` list of all digraphs with quote in the description
- what to do with digraphs that start with '-' and match an option? `kk -- -s` ?
- is it possible to check if `kk` has been started in "pipe" mode?


# Usb tethering and Debian

- activate it on the tablet / mobile
- `dhclient usb0`

# Running external commands in Vis

- only implement the command (starting with `:`)
- `:!ls` shows result of ls in a popup
- `:!!ls` insert the result of `ls` at the current cursor position
- if there is a selection, it's passed as parameter to the filter and it gets replaces by the result of the command (`:!!filter` in visual mode or `:range!!filter`)

`exec_command`:
- run any command with the same rights as the program
- get the standard output of the program and store it in a string
- insert the string at the currrent cursor position (while keeping the ends of line)
- `ctrl-c` breaks the program and gets back to normal mode

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

# Vis automcomplete

For my workflows, vis would need autocomplete for:
- :e filename (tab to browse and ctrl-d to show the list)
- ctrp-p / ctrl-n in insert mode (list of all entries in all open buffers)
- 

for this to happen we need
- a way to create the list out of a text
- if possible, a popup showing the list of choices


# Vis and window management

- vis only has simple h and v split
- more complex windows management should go through an external window manager

in order to work with a window manager, vis instances should be able to share:
- the registers
- the list of open buffers
- the unsaved content of buffer
- it should be possible to have two vis instances on screen showing the same file (at different positions)
- the current cursor position (warning: split view at different positions; hide one of the buffers; switch back to it)

# Vis and visual mode

- i need the block mode. really.
- linewise visual mode should extend by full lines when searching
- using / leaves the visual mode in an instable state (basically: no way to get out of it)
- in vim:
    - leaving the linewise linemode leaves the cursor where it is (current vim behavior)
    - leaving the linewise linemode by yanking moves the cursor to the beginning of the last line yanked (current vim behavior)
    - leaving the linewise linemode by indenting moves the cursor to the beginning of the last line yanked (current vim behavior)
  in vis the cursor is always left where it is, which -- possibly because of my habits in vim? -- mostly feels wrong.
 
# Vis and buffers management

It should be possible to hide unsaved buffers.

Use case:

- `!!grep something *.c`
- gf to open the file under the cursor
- edit the file
- close the buffer and go back to the grep listing

I should be able to this without saving the buffer with grep's result

# Feature and bug requests for vis

Bugs:

- after inserting the content of the register with ctrl-r, the cursor should be at the end of the inserted text
- zb does not work good enough even if there is no line wrapping (too far away from the bottom)
- a at the beginning of a line starting the edit on the next line feels strange.

Features:

- % register: mostly for running commands with the current files as the argument or inserting the filename in the current file
- ctrl-r for registers should also work in command mode
- :! runs a command and shows the standard output in a "pop up"
- !! runs a command and inserts the standard output into the current line (replacing it)
- == should intend the current line (or the visual selection) to indenting that would have been applied with autoindent
- stdout should go to the terminal (it seems to be captured from vis; stdin is also captured by vis, but this is probably correct)

btw: check `git format-patch`

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

# Getting vis to compile on mac

~~~
diff --git a/config.mk b/config.mk
index c570914..27e6991 100644
--- a/config.mk
+++ b/config.mk
@@ -6,8 +6,14 @@ VERSION = devel
 PREFIX = /usr/local
 MANPREFIX = ${PREFIX}/share/man
 
+OS := $(shell uname)
+
 INCS = -I.
-LIBS = -lc -lncursesw
+ifeq ($(OS),Darwin)
+    LIBS = -lc -lncurses
+else
+	LIBS = -lc -lncursesw
+endif
 
 CFLAGS += -std=c99 -Os ${INCS} -DVERSION=\"${VERSION}\" -DNDEBUG
 LDFLAGS += ${LIBS}
diff --git a/vis.c b/vis.c
index 0bd5037..73a958e 100644
--- a/vis.c
+++ b/vis.c
@@ -17,6 +17,8 @@
 #define _POSIX_SOURCE
 /* Necessary for SIGWINCH on OpenBSD */
 #define _BSD_SOURCE
+/* Necessary for SIGWINCH on OS X */
+#define _DARWIN_C_SOURCE 1
 #include <locale.h>
 #include <stdlib.h>
 #include <unistd.h>

~~~


# Using gdb to debug vis

~~~
$make debug
$gdb ./vis
(gdb) break prompt_enter
(gdb) run
...
(gdb) step // step (into) the next command
(gdb) next // go to the next line
(gdb) print s // prints a string
(gdb) print *arg // prints the content of a pointer to a structure
~~~

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
