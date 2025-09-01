---
layout: framework
title: 2 Makefile简介
permalink: /doc/make/ch02-00-an-introduction-to-makefiles.html
---

# 2 Makefile简介

你需要一个名为 *makefile* 的文件来告诉make该做什么。大多数情况下，makefile会告诉make如何编译和链接程序。

在本章中，我们将讨论一个简单的makefile，它描述了如何编译和链接一个由八个C源文件和三个头文件组成的文本编辑器。这个makefile还可以告诉make在被明确要求时如何运行各种命令（例如，删除某些文件以进行清理操作）。要查看更复杂的makefile示例，请参见[复杂的makefile示例](appendix-c-complex-makefile.html)。

当make重新编译编辑器时，每个已更改的C源文件都必须重新编译。如果头文件发生了更改，为了安全起见，每个包含该头文件的C源文件都必须重新编译。每次编译都会生成一个与源文件对应的目标文件。最后，如果有任何源文件已被重新编译，所有的目标文件（无论是新生成的还是从之前的编译中保存下来的）都必须链接在一起，以生成新的可执行编辑器。
