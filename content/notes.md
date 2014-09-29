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
index 0bd5037..c2863c3 100644
--- a/vis.c
+++ b/vis.c
@@ -37,6 +37,10 @@
 #include "text-objects.h"
 #include "util.h"
 
+// #define _DARWIN_C_SOURCE
+#if (!defined(SIGWINCH))
+#define SIGWINCH 28
+#endif
+
 #ifdef PDCURSES
 int ESCDELAY;
 #endif
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
