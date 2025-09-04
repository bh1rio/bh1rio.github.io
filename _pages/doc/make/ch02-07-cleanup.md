---
layout: framework
title: 2.7 清理目录的规则
permalink: /doc/make/ch02-07-cheanup.html
---

## 2.7 清理目录的规则

编译程序并非你可能想要为之编写规则的唯一事情。Makefile通常还会说明除了编译程序之外的其他一些操作方法：例如，如何删除所有目标文件和可执行文件，以使目录“clean”。

以下是我们如何为清理示例编辑器编写一个make规则：

```makefile
clean:
        rm edit $(objects)
```

实际上，我们可能希望以一种稍微复杂些的方式来编写这条规则，以应对未预料到的情况。我们会这样做：

```makefile
.PHONY : clean
clean :
        -rm edit $(objects)
```

这可以防止make被名为clean的实际文件弄混淆，并使其即使遇到rm的错误也能继续执行。（参见[伪目标](ch04-06-phony-targets.html)和[配方中的错误](ch05-05-errors.html)。）

像这样的规则不应该放在makefile的开头，因为我们不希望它默认运行！因此，在示例makefile中，我们希望用于edit（重新编译编辑器）的规则保持为默认目标。

由于`clean`不是`edit`的先决条件，所以如果我们不带任何参数执行命令`make`，这条规则根本不会运行。为了让这条规则运行，我们必须输入`make clean`。参见[如何运行make](ch09-00-running.html)。