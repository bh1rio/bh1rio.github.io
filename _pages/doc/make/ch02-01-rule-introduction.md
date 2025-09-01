---
layout: framework
title: 2.1 规则是什么样子的
permalink: /doc/make/ch02-01-rule-introduction.html
---
## 2.1 规则是什么样子的

A simple makefile consists of “rules” with the following shape:
一个简单的makefile由具有以下形式的“规则”组成：

```makefile
target … : prerequisites …
        recipe
        …
        …
```

*目标*(target)通常是由程序生成的文件的名称；目标的示例包括可执行文件或目标文件。目标也可以是要执行的操作的名称，例如“clean”（参见[伪目标](ch04-06-phony-targets.html)）。

*先决条件*(prerequisite)是用作创建目标的输入文件。一个目标通常依赖于多个文件。

*配方*(recipe)是make执行的一个操作。一个配方可以包含多个命令，这些命令可以在同一行，也可以每行一个。
**请注意：**你需要在每一行配方的开头放置一个制表符！这是一个容易让粗心者出错的不明显之处。如果你希望用制表符以外的字符作为配方的前缀，可以将`.RECIPEPREFIX`变量设置为另一个字符（参见[其他特殊变量](ch06-14-special-variables.html)）。

通常，一个规则中的配方会带有先决条件，其作用是在任何先决条件发生变化时创建目标文件。不过，为目标指定配方的规则不一定非要包含先决条件。例如，与目标“clean”相关联、包含删除命令的规则就没有先决条件。

那么，一条规则就说明了如何以及何时重新生成作为该特定规则目标的某些文件。make会根据先决条件执行指令，以创建或更新目标。一条规则还可以说明如何以及何时执行某个操作。参见[编写规则](ch04-00-rules.html)。

除了规则之外，Makefile 可能还包含其他文本，但一个简单的 Makefile 只需包含规则即可。规则看起来可能比本模板中展示的要复杂一些，但或多或少都符合这种模式。