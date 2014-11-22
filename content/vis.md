# Vis

## External commands

In vim external commands are executed as `:!ls`, if you want the current selection to be replaced by the output of the command, you just pass it to as a parameter (`:.!ls`, the shortcut being `!!ls`).

An alternative is to use `:r!ls`, which puts the command's otuput on a newly created line below the current one.

It's not possible to just add the output at the current cursor position nor define a selection that is shorter than a line.

In order to keep Vis as small as possible

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

