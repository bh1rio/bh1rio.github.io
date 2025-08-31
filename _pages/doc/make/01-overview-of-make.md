---
layout: framework
title: 1 make 概述
permalink: /doc/make/01-overview-of-make.html
---

# 1 make 概述

The make utility automatically determines which pieces of a large program need to be recompiled, and issues commands to recompile them. This manual describes GNU make, which was implemented by Richard Stallman and Roland McGrath. Development since Version 3.76 has been handled by Paul D. Smith.

make工具会自动确定大型程序中哪些部分需要重新编译，并发出重新编译它们的命令。本手册介绍了GNU make，它由理查德·斯托曼和罗兰·麦格拉思实现。3.76版本之后的开发工作由保罗·D·史密斯负责。

GNU make conforms to section 6.2 of *IEEE Standard 1003.2-1992* (POSIX.2).

GNU make 遵循 *IEEE 标准 1003.2-1992*（POSIX.2）的第 6.2 节。

Our examples show C programs, since they are most common, but you can use make with any programming language whose compiler can be run with a shell command. Indeed, make is not limited to programs. You can use it to describe any task where some files must be updated automatically from others whenever the others change.

我们的示例展示了C程序，因为它们最为常见，但你可以将make用于任何其编译器可通过shell命令运行的编程语言。实际上，make并不局限于程序。你可以用它来描述任何任务，只要在这些任务中，当某些文件发生变化时，另一些文件必须自动从这些变化的文件更新而来。

## 1.1 如何阅读本手册

If you are new to make, or are looking for a general introduction, read the first few sections of each chapter, skipping the later sections. In each chapter, the first few sections contain introductory or general information and the later sections contain specialized or technical information. The exception is the second chapter, [An Introduction to Makefiles](01-an-introduction-to-makefiles.html), all of which is introductory.

如果你是 make 的新手，或者正在寻找一个一般性的介绍，那么阅读每章的前几节即可，跳过后面的章节。在每一章中，前几节包含入门或一般性的信息，而后几节则包含专业或技术性的信息。
例外情况是第二章[《Makefile简介》](02-an-introduction-to-makefiles.html)，整章内容都是入门级的。

If you are familiar with other make programs, see [Features of GNU make](https://www.gnu.org/software/make/manual/html_node/Features.html), which lists the enhancements GNU make has, and [Incompatibilities and Missing Features](https://www.gnu.org/software/make/manual/html_node/Missing.html), which explains the few things GNU make lacks that others have.

如果你熟悉其他make程序，请参阅[GNU make的特性](14-features-of-gnu-make.html)，其中列出了GNU make所具备的增强功能，以及[不兼容性和缺失功能](15-incompatibilities-and-missing-features.html)，其中说明了GNU make缺少而其他程序具备的少数功能。

For a quick summary, see [Summary of Options](https://www.gnu.org/software/make/manual/html_node/Options-Summary.html), [Quick Reference](https://www.gnu.org/software/make/manual/html_node/Quick-Reference.html), and [Special Built-in Target Names](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html).

如需快速概览，请参阅[选项摘要]()、[快速参考](appendix-a-quick-reference.html)以及[特殊内置目标名称]()。

## 1.2 问题与程序缺陷

If you have problems with GNU make or think you’ve found a bug, please report it to the developers; we cannot promise to do anything but we might well want to fix it.

如果您在使用GNU make 时遇到问题，或者认为自己发现了一个漏洞，请向开发者报告；我们不能保证会采取任何行动，但很可能会想要修复它。

Before reporting a bug, make sure you’ve actually found a real bug. Carefully reread the documentation and see if it really says you can do what you’re trying to do. If it’s not clear whether you should be able to do something or not, report that too; it’s a bug in the documentation!

在报告程序缺陷之前，要确保你确实发现了一个真实的程序缺陷。仔细重读文档，看看文档中是否确实说明了你可以做你正尝试做的事情。如果不清楚你是否应该能够做某件事，那也把这一点报告上来；这属于文档中的程序缺陷！

Before reporting a bug or trying to fix it yourself, try to isolate it to the smallest possible makefile that reproduces the problem. Then send us the makefile and the exact results make gave you, including any error or warning messages. Please don’t paraphrase these messages: it’s best to cut and paste them into your report. When generating this small makefile, be sure to not use any non-free or unusual tools in your recipes: you can almost always emulate what such a tool would do with simple shell commands. Finally, be sure to explain what you expected to occur; this will help us decide whether the problem was really in the documentation.

在报告漏洞或尝试自行修复之前，请尝试将其隔离到能重现该问题的最小的makefile中。然后将该makefile以及make给你的确切结果发送给我们，包括任何错误或警告信息。请不要对这些信息进行意译：最好将它们复制粘贴到你的报告中。在生成这个小的makefile时，确保在你的配方中不使用任何非免费或不常见的工具：你几乎总能用简单的shell命令来模拟这类工具的功能。最后，一定要说明你期望发生的情况；这将帮助我们判断问题是否确实出在文档中。

Once you have a precise problem you can report it in one of two ways. Either send electronic mail to:

一旦你有了明确的问题，你可以通过以下两种方式之一进行报告。要么发送电子邮件至：

```
bug-make@gnu.org
```
or use our Web-based project management tool, at:

或者使用我们基于网络的项目管理工具，网址是：

```
https://savannah.gnu.org/projects/make/
```

In addition to the information above, please be careful to include the version number of make you are using. You can get this information with the command ‘make --version’. Be sure also to include the type of machine and operating system you are using. One way to obtain this information is by looking at the final lines of output from the command ‘make --help’.

除上述信息外，请注意包含您正在使用的make的版本号。您可以通过命令`make --version`获取此信息。同时，务必包含您所使用的机器类型和操作系统。获取该信息的一种方法是查看命令`make --help`输出的最后几行。

If you have a code change you’d like to submit, see the README file section “Submitting Patches” for information.

如果你有想要提交的代码更改，请查看README文件中“提交补丁”部分的信息。
