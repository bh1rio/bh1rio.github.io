---
layout: framework
title: 2.4 变量让Makefile更简单
permalink: /doc/make/ch02-04-variables-simplify.html
---
## 2.4 变量让Makefile更简单

在我们的示例中，我们必须在 edit 的规则中两次列出所有目标文件（此处重复列出）：

```makefile
edit : main.o kbd.o command.o display.o \
              insert.o search.o files.o utils.o
        cc -o edit main.o kbd.o command.o display.o \
                   insert.o search.o files.o utils.o
```

这种重复容易出错；如果向系统中添加了新的目标文件，我们可能会将其添加到一个列表中，却忘记添加到另一个列表。我们可以通过使用变量来消除这种风险并简化makefile。
变量允许先定义一个文本字符串，之后在多个地方进行替换（参见[如何使用变量](ch06-00-using-variables.html)）。

每个Makefile都有一个标准做法，即包含一个名为objects、OBJECTS、objs、OBJS、obj或OBJ的变量，该变量是所有目标文件名称的列表。我们会在Makefile中用如下一行代码来定义这样一个objects变量：

```
objects = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o
```

然后，在每个我们想要放置目标文件名称列表的地方，我们可以通过编写“$(objects)”来替换该变量的值（参见[如何使用变量](ch06-00-using-variables.html)）。

以下是当你为目标文件使用变量时，完整的简单makefile的样子：

```makefile
objects = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o

edit : $(objects)
        cc -o edit $(objects)
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
        rm edit $(objects)
```

