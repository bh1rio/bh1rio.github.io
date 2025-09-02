---
layout: framework
title: 2.5 让make推导配方
permalink: /doc/make/ch02-05-make-deduces.html
---
## 2.5 让make推导配方

不必详细说明编译各个C源文件的规则，因为make工具能够自行推断出来：它有一条隐式规则，即使用“cc -c”命令从同名的“.c”文件更新“.o”文件。例如，它会使用“cc -c main.c -o main.o”这条规则将main.c编译成main.o。因此，我们可以在目标文件的规则中省略这些规则。参见[使用隐式规则](ch10-00-implicit-rules.html)。

当一个‘.c’文件以这种方式被自动使用时，它也会被自动添加到先决条件列表中。因此，只要我们省略规则，就可以从先决条件中省略‘.c’文件。

以下是包含这两处修改以及如上文所建议的变量objects的完整示例：

```
objects = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o

edit : $(objects)
        cc -o edit $(objects)

main.o : defs.h
kbd.o : defs.h command.h
command.o : defs.h command.h
display.o : defs.h buffer.h
insert.o : defs.h buffer.h
search.o : defs.h buffer.h
files.o : defs.h buffer.h command.h
utils.o : defs.h

.PHONY : clean
clean :
        rm edit $(objects)
```

这就是我们在实际操作中编写Makefile的方式。（与“clean”相关的复杂情况在其他地方有描述。参见[伪目标](ch04-06-phony-targets.html)和[配方中的错误](ch05-05-errors.html)。）

由于隐式规则非常便捷，所以它们很重要。你会经常看到它们被使用。