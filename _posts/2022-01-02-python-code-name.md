---
layout: post
title: 慎重选择python源代码文件的名字
date: 2022-01-02 04:53:21 
categories: python
tags: python
---

这两天在看matplotlib的文档，发现在文档中最简单的显示其版本的基本例子都不跑不通，显示如下错误：

> ModuleNotFoundError: No module named 'matplotlib.pyplot'; 'matplotlib' is not a package

我开始以为是python3.10导致不兼容，后来又换了3.9还是一样的问题。切换了几次都是一样的不行，后来发现例子和显示版本的错误信息不一样，于是用两个错误信息去搜索，终于找到这个兄弟的blog：https://blog.csdn.net/wwangfabei1989/article/details/79082110，根据其描述，错误原因是因为python脚本的名字是matplotlib.py，导致引用包的时候找不到相应名字的包，按照其描述修改文件名字问题得到解决。

从这可以看到，python的模块名和包名还是很容易混淆的。
