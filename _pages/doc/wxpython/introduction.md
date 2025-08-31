---
layout: framework
title: 介绍
permalink: /doc/wxpython/introduction.html
---

# 介绍

本章介绍了wxPython工具包。

wxPython是一个用于创建桌面GUI应用程序的跨平台工具包。wxPython的主要作者是Robin Dunn。使用wxPython，开发人员可以在Windows、Mac和各种Unix系统上创建应用程序。wxPython是wxWidgets的包装器，它是一个成熟的跨平台C++库。

## Python

Python是一种成功的脚本语言。它最初是由Guido van Rossum开发的。它于1991年首次发布。Python的灵感来源于ABC和Haskell编程语言。Python是一种高级、通用、多平台的解释语言。有些人更喜欢称之为动态语言。这很容易学习。Python是一种极简主义语言。它最明显的特点之一是不使用分号也不使用括号。Python使用缩进。如今，Python由世界各地的一大群志愿者维护。

为了创建图形用户界面，Python程序员可以在三个不错的选项中进行选择：PyGTK、wxPython和PyQt。

## wxPython模块

wxPython是一个用于创建桌面GUI应用程序的跨平台工具包。wxPython的主要作者是Robin Dunn。使用wxPython，开发人员可以在Windows、Mac和各种Unix系统上创建应用程序。wxPython是wxWidgets的包装器，它是一个成熟的跨平台C++库。wxPython由五个基本模块组成。

![wxPython模块](/images/doc/wxpython/modules.png)

*控件(Controls)*模块提供图形应用程序中常见的小部件。例如按钮、工具栏或笔记本。小工具在Windows操作系统下被称为控件。*核心(Core)*模块由开发中使用的基本类组成。这些类包括Object类，它是所有类的母类，Sizers，用于小部件布局，Events，基本几何类，如Point和Rectangle。图形设备接口（GDI）是一组用于绘制小部件的类。此模块包含用于操作字体、颜色、画笔、画笔或图像的类。*杂项(Misc)*模块包含各种其他类和模块函数。这些类用于日志记录、应用程序配置、系统设置、使用显示器或操纵杆。*Windows*模块由形成应用程序的各种窗口组成，例如面板、对话框、框架或滚动窗口。

## wxPython API

wxPython API是一组方法和对象。小工具是GUI应用程序的基本构建块。在Windows窗口小部件下是被调用者控件。我们可以大致将程序员分为两组：他们要么编写应用程序，要么编写库。在我们的例子中，wxPython是应用程序程序员用来编写应用程序代码的库。从技术上讲，wxPython是一个名为wxWidgets的C++GUI API的包装器。因此它不是一个原生的API；即它不是直接用Python编写的。

在wxPython中，我们有很多小部件。这些可以分为一些逻辑组。

### 基本小部件

这些小部件为派生的小部件提供了基本功能。他们被称为祖先。它们通常不直接使用。

![基本小部件](/images/doc/wxpython/base.png)

### 顶级小部件

这些小部件彼此独立存在。

![顶级小部件](/images/doc/wxpython/toplevel.png)

### 容器

容器包含其他小部件。

![容器](/images/doc/wxpython/containers.png)

### 动态小部件

这些小部件可以由用户编辑。

![动态小部件](/images/doc/wxpython/dynamic.png)

### 静态小部件

这些小部件显示信息。用户无法编辑它们。

![alt text](/images/doc/wxpython/staticwidgets.png)

### 其他小部件

这些小部件在应用程序中实现状态栏、工具栏和菜单栏。

![其他小部件](/images/doc/wxpython/bars.png)

### 继承

wxPython中的小部件之间存在特定的关系。这种关系是通过继承发展起来的。继承是面向对象编程的关键部分。小部件形成一个层次结构。小部件可以继承其他小部件的功能。现有类称为基类、父类或祖先类。继承的小部件称为派生小部件、子小部件或子部件。

![继承图](/images/doc/wxpython/inheritance.png)

假设我们在应用程序中使用按钮小部件。按钮小部件继承自四个不同的基类。最接近的类是`wx.Control`类。按钮小部件是一种小窗口。屏幕上显示的所有小部件都是窗口。因此，它们继承自`wx.Window`类。有些对象是不可见的。例如sizer、设备上下文或区域设置对象。还有一些类是可见的，但它们不是窗口。例如，颜色对象、插入符号对象或光标对象。并非所有小部件都是控件。例如`wx.Dialog`不是一种控件。控件是放置在称为容器的其他小部件上的小部件。这就是为什么我们有一个单独的`wx.Control`基类。

每个窗口都可以对事件做出反应。按钮小部件也是如此。点击按钮，我们启动`wx.EVT_COMMAND_BUTTON_CLICKED`事件。按钮小部件继承了wx.EvtHandler,通过`wwx.Window`类。每个对事件作出反应的小部件都必须继承自`wx.EvtHandler`类。最后，所有对象都继承自`wx.Object`类。

这是对wxPython的介绍。