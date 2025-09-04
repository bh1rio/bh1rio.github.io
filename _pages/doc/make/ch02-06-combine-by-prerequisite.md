---
layout: framework
title: 2.6 Makefile的另一种风格
permalink: /doc/make/ch02-06-combine-by-prerequisite.html
---
## 2.6 Makefile的另一种风格

当一个makefile的目标文件仅通过隐式规则创建时，另一种风格的makefile是可行的。在这种风格的makefile中，你是按依赖项而非目标来对条目进行分组的。下面是一个示例：

```makefile
objects = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o

edit : $(objects)
        cc -o edit $(objects)

$(objects) : defs.h
kbd.o command.o files.o : command.h
display.o insert.o search.o files.o : buffer.h
```

这里，defs.h 被指定为所有目标文件的先决条件；command.h 和 buffer.h 是为其列出的特定目标文件的先决条件。

这种方式是否更好取决于个人喜好：它更简洁，但有些人不喜欢，因为他们觉得将每个目标的所有信息放在一个地方会更清晰。
