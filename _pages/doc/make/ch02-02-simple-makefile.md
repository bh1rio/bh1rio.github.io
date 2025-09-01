---
layout: framework
title: 2.2 一个简单的 Makefile
permalink: /doc/make/ch02-02-simple-makefile.html
---

## 2.2 一个简单的 Makefile

这是一个简单的makefile，它描述了名为edit的可执行文件如何依赖于八个目标文件，而这些目标文件又反过来依赖于八个C源文件和三个头文件。

在这个示例中，所有的C文件都包含defs.h，但只有那些定义编辑命令的文件包含command.h，而只有更改编辑器缓冲区的底层文件才包含buffer.h。

```makefile
edit : main.o kbd.o command.o display.o \
       insert.o search.o files.o utils.o
        cc -o edit main.o kbd.o command.o display.o \
                   insert.o search.o files.o utils.o

main.o : main.c defs.h
        cc -c main.c
kbd.o : kbd.c defs.h command.h
        cc -c kbd.c
command.o : command.c defs.h command.h
        cc -c command.c
display.o : display.c defs.h buffer.h
        cc -c display.c
insert.o : insert.c defs.h buffer.h
        cc -c insert.c
search.o : search.c defs.h buffer.h
        cc -c search.c
files.o : files.c defs.h buffer.h command.h
        cc -c files.c
utils.o : utils.c defs.h
        cc -c utils.c
clean :
        rm edit main.o kbd.o command.o display.o \
           insert.o search.o files.o utils.o
```

我们使用反斜杠/换行符将每个长行分成两行；这就像使用一个长行，但更易于阅读。参见[拆分长行](ch03-01-01-splitting-lines.html)。

要使用这个makefile来创建名为edit的可执行文件，请输入：

```bash
make
```

要使用此Makefile从目录中删除可执行文件和所有目标文件，请输入：

```bash
make clean
```

在这个示例的makefile中，目标包括可执行文件`edit`，以及目标文件`main.o`和`kbd.o`。依赖项是诸如`main.c`和`defs.h`之类的文件。实际上，每个`.o`文件既是目标也是依赖项。规则包括`cc -c main.c`和`cc -c kbd.c`。

当目标是一个文件时，如果其任何先决条件发生变化，就需要对该文件进行重新编译或重新链接。此外，任何本身是自动生成的先决条件都应首先更新。在这个例子中，`edit`依赖于八个目标文件中的每一个；目标文件`main.o`依赖于源文件`main.c`和头文件`defs.h`。

每个包含目标和先决条件的行后面都可以跟一个处方(recipe)。这些处方说明了如何更新目标文件。处方的每一行开头都必须有一个制表符（或者由`.RECIPEPREFIX`变量指定的任何字符，参见[其他特殊变量](ch06-14-special-variables.html)），以将处方与Makefile中的其他行区分开来。（请记住，make并不了解这些处方的工作原理。提供能正确更新目标文件的规则是你的责任。当目标文件需要更新时，make所做的只是执行你指定的处方。）

目标`clean`并非文件，而仅仅是一个操作的名称。由于通常你并不想执行这条规则中的操作，所以`clean`不是任何其他规则的先决条件。因此，除非你明确指示，否则make绝不会对它进行任何操作。请注意，这条规则不仅不是其他规则的先决条件，它自身也没有任何先决条件，所以该规则的唯一目的就是运行指定的配方。那些不指向文件、仅代表操作的目标被称为伪目标。有关此类目标的信息，请参见[伪目标](ch04-06-phony-targets.html)。要了解如何让make忽略rm或其他任何命令产生的错误，请参见[处方中的错误]。