---
layout: framework
title: 3.1 What Makefiles Contain
permalink: /doc/make/ch03-01-makefiles-contains.html
---

## 3.1 What Makefiles Contain

Makefiles contain five kinds of things: *explicit rules*, *implicit rules*, *variable definitions*, *directives*, and *comments*. Rules, variables, and directives are described at length in later chapters.

- An explicit rule says when and how to remake one or more files, called the rule’s targets. It lists the other files that the targets depend on, called the prerequisites of the target, and may also give a recipe to use to create or update the targets. See [Writing Rules]().
*-An implicit rule says when and how to remake a class of files based on their names. It describes how a target may depend on a file with a name similar to the target and gives a recipe to create or update such a target. See [Using Implicit Rules]().
- A variable definition is a line that specifies a text string value for a variable that can be substituted into the text later. The simple makefile example shows a variable definition for objects as a list of all object files (see [Variables Make Makefiles Simpler]()).
- A directive is an instruction for make to do something special while reading the makefile. These include:
  - Reading another makefile (see [Including Other Makefiles]()).
  - Deciding (based on the values of variables) whether to use or ignore a part of the makefile (see [Conditional Parts of Makefiles]()).
  - Defining a variable from a verbatim string containing multiple lines (see [Defining Multi-Line Variables]()).
- ‘#’ in a line of a makefile starts a comment. It and the rest of the line are ignored, except that a trailing backslash not escaped by another backslash will continue the comment across multiple lines. A line containing just a comment (with perhaps spaces before it) is effectively blank, and is ignored. If you want a literal #, escape it with a backslash (e.g., \#). Comments may appear on any line in the makefile, although they are treated specially in certain situations.
  You cannot use comments within variable references or function calls: any instance of # will be treated literally (rather than as the start of a comment) inside a variable reference or function call.

  Comments within a recipe are passed to the shell, just as with any other recipe text. The shell decides how to interpret it: whether or not this is a comment is up to the shell.

  Within a define directive, comments are not ignored during the definition of the variable, but rather kept intact in the value of the variable. When the variable is expanded they will either be treated as make comments or as recipe text, depending on the context in which the variable is evaluated.

- [Splitting Long Lines](ch03-01-01-splitting-lines.html)