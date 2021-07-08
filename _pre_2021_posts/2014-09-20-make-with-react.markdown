---
title: Make for Javascript MVC Apps
layout: post
---

## Minimum Viable Makefile

A makefile is a list of tasks and dependencies for those tasks (called goals in makefile speak). The default filename for a makefile is called Makefile. Tasks are made of:

```
target: dependencies
[tab] system command
```

A target can be any name or a filename, dependencies can be the same (except you can have no dependencies as well). Looking at a simple example:

```
listfiles:
  ls -la
```

Running make against this Makefile lists the contents of the current directory.

```
ls -la
total 8
drwxr-xr-x   3 carl  staff  102 20 Sep 22:08 .
drwx------+ 27 carl  staff  918 20 Sep 22:08 ..
-rw-r--r--   1 carl  staff   19 20 Sep 22:08 Makefile
```

Make runs the first goal by default. Make shows the command that is run by default. You can hide the command from the output by adding a @ to the start of the command:

```
listfiles:
	@ls -la
```

Outputs

```
total 8
drwxr-xr-x   3 carl  staff  102 20 Sep 22:08 .
drwx------+ 27 carl  staff  918 20 Sep 22:08 ..
-rw-r--r--   1 carl  staff   20 20 Sep 22:09 Makefile
```

![Simple](http://i.imgur.com/hJi8rtN.gif)

Starting off with copying a html file over to a dist directory:

```
dist/index.html: app/index.html
	mkdir -p $(dir $@)
	cp $^ $@
```

- Ensure that the dist directory exists.
- Copy the depenency file to the goal name.

In this example:

__$^ = app/index.html__ (The dependency)

and

__$@ = dist/index.html__ (The goal target)

We also introduce a make function here:

```
$(dir $@)
```

_dir_ outputs the directory given a file name. In this case it will output _dist_.

### SASS

```
dist/css/app.css: $(shell find app/sass -name \*.scss)
	mkdir -p $(dir $@)
	sass app/sass/app.scss:$@
```

This goal gets called when ever any file in the list that is outputted from __$(shell find app/sass -name \*.scss)__ changes.

The goal runs the sass command on the app.scss and outputs the result to dist/css/app.css.

### Concatenating javascript

```
JS = $(shell find app/scripts -name \*.js)

dist/scripts/app.js: $(JS)
	mkdir -p $(dir $@)
	cat @^ > $@
```

![woot](http://media.tumblr.com/bb4818026c3a1617c1eb83794dd6af96/tumblr_inline_naubovIiuY1raprkq.gif)

__JS__ is a variable that we have introduced. It returns all the .js files under app/scripts. The goal/task here will get called whenever a .js file is changed. It will make the dist/scripts directory, then take all .js files, cat them so they are concatenated and output them to dist/scripts/app.js.

## Putting it together

```
JS = $(shell find app/scripts -name \*.js)

dist/css/app.css: $(shell find app/sass -name \*.scss)
	mkdir -p $(dir $@)
	sass app/sass/app.scss:$@

dist/scripts/app.js: $(JS)
	mkdir -p $(dir $@)
	cat @^ > $@

dist/index.html: app/index.html
	mkdir -p $(dir $@)
	cp $^ $@

all: dist/index.html dist/scripts/app.js dist/css/app.css

.DEFAULT: all
```

The default goal/task of the makefile has now been set to __all__ so you can now run it by just running: __make__.

For a full example see https://github.com/carlwoodward/react_with_make_template. If you want to get more into make please read http://www.gnu.org/software/make/manual/make.html.

![Awesome](http://i.imgur.com/8iBdYbb.gif)
