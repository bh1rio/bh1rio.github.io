---
layout: framework
title: 1 Overview of make
permalink: /doc/make/01-overview-of-make.html
---

# 1 Overview of make

The make utility automatically determines which pieces of a large program need to be recompiled, and issues commands to recompile them. This manual describes GNU make, which was implemented by Richard Stallman and Roland McGrath. Development since Version 3.76 has been handled by Paul D. Smith.

GNU make conforms to section 6.2 of *IEEE Standard 1003.2-1992* (POSIX.2).

Our examples show C programs, since they are most common, but you can use make with any programming language whose compiler can be run with a shell command. Indeed, make is not limited to programs. You can use it to describe any task where some files must be updated automatically from others whenever the others change.

## 1.1 How to Read This Manual

If you are new to make, or are looking for a general introduction, read the first few sections of each chapter, skipping the later sections. In each chapter, the first few sections contain introductory or general information and the later sections contain specialized or technical information. The exception is the second chapter, [An Introduction to Makefiles](https://www.gnu.org/software/make/manual/html_node/Introduction.html), all of which is introductory.

If you are familiar with other make programs, see [Features of GNU make](https://www.gnu.org/software/make/manual/html_node/Features.html), which lists the enhancements GNU make has, and [Incompatibilities and Missing Features](https://www.gnu.org/software/make/manual/html_node/Missing.html), which explains the few things GNU make lacks that others have.

For a quick summary, see [Summary of Options](https://www.gnu.org/software/make/manual/html_node/Options-Summary.html), [Quick Reference](https://www.gnu.org/software/make/manual/html_node/Quick-Reference.html), and [Special Built-in Target Names](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html).

## 1.2 Problems and Bugs
If you have problems with GNU make or think you’ve found a bug, please report it to the developers; we cannot promise to do anything but we might well want to fix it.

Before reporting a bug, make sure you’ve actually found a real bug. Carefully reread the documentation and see if it really says you can do what you’re trying to do. If it’s not clear whether you should be able to do something or not, report that too; it’s a bug in the documentation!

Before reporting a bug or trying to fix it yourself, try to isolate it to the smallest possible makefile that reproduces the problem. Then send us the makefile and the exact results make gave you, including any error or warning messages. Please don’t paraphrase these messages: it’s best to cut and paste them into your report. When generating this small makefile, be sure to not use any non-free or unusual tools in your recipes: you can almost always emulate what such a tool would do with simple shell commands. Finally, be sure to explain what you expected to occur; this will help us decide whether the problem was really in the documentation.

Once you have a precise problem you can report it in one of two ways. Either send electronic mail to:

```
    bug-make@gnu.org
```
or use our Web-based project management tool, at:

```
    https://savannah.gnu.org/projects/make/
```

In addition to the information above, please be careful to include the version number of make you are using. You can get this information with the command ‘make --version’. Be sure also to include the type of machine and operating system you are using. One way to obtain this information is by looking at the final lines of output from the command ‘make --help’.

If you have a code change you’d like to submit, see the README file section “Submitting Patches” for information.

