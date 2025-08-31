---
layout: framework
title: 第一步
permalink: /doc/wxpython/firststep.html
---

# 第一步

在wxPython教程的这一部分中，我们将创建一些简单的示例。

## 简单例子

我们从一个非常简单的例子开始。我们的第一个脚本将只显示一个小窗口。

它不会有多大作用。我们将逐行分析剧本。

```python
#!/usr/bin/env python
 
# simple.py

import wx

app = wx.App()

frame = wx.Frame(None, title='Simple application')
frame.Show()

app.MainLoop()
```

这是我们在wxPython中的第一个例子。

```python
#!/usr/bin/env python

# simple.py
```

第一行是she-bang，后面是Python解释器的路径。第二行是一个神奇的注释，它指定了源代码的编码。第四行是提供脚本名称的注释。

```python
import wx
```

此行导入基本的wxPython模块。即core、controls、gdi、misc和windows。从技术上讲，wx是一个名称空间。基本模块中的所有函数和对象都将以wx开头。前缀下一行代码将创建一个应用程序对象。

```python
app = wx.App()
```

每个wxPython程序必须有一个应用程序对象。

```python
frame = wx.Frame(None, title='Simple application')
frame.Show()
```

在这里我们创建一个`wx.Frame`对象。一个`wx.Frame`小部件是一个重要的容器小部件。我们稍后将对此小部件进行详细分析。`wx.Frame`小部件是其他小部件的父小部件。它本身没有父对象。如果我们为父参数指定None，则表示我们的小部件没有父参数。它是小部件层次结构中的顶级小部件。在我们创建`wx.Frame`小部件，我们必须调用`Show()`方法才能在屏幕上实际显示它。

```python
app.MainLoop()
```

最后一行进入主循环。主循环是一个无休止的循环。它捕获并分派应用程序生命周期中存在的所有事件。

这是一个非常简单的例子。尽管这个窗口很简单，但我们可以用它做很多事情。我们可以调整窗口大小，最大化，最小化。此功能需要大量编码。所有这些都是隐藏的，默认情况下由wxPython工具包提供。没有理由重新发明轮子。

![简单例子](/images/doc/wxpython/simple.png)

## wx.Frame

`wx.Frame`小部件是wxPython中最重要的窗口小部件之一。它是一个容器小部件。这意味着它可以包含其他小部件。实际上，它可以包含任何不是框架或对话框的窗口。`wx.Frame`由标题栏、边框和中央容器区域组成。标题栏和边框是可选的。它们可以通过各种标志移除。

`wx.Frame`具有以下构造函数：

```python
wx.Frame(wx.Window parent, int id=-1, string title='', wx.Point pos=wx.DefaultPosition, 
    wx.Size size=wx.DefaultSize, style=wx.DEFAULT_FRAME_STYLE, string name="frame")
```

构造函数有七个参数。第一个参数没有默认值。其他六个参数确实有。这四个参数是可选的。前三项是强制性的。

`wx.DEFAULT_FRAME_STYLE`是一组默认标志：wx.MINIMIZE_BOX、 wx.MAXIMIZE_BOX、 wx.RESIZE_BORDER、 wx.SYSTEM_MENU、 wx.CAPTION、 wx.CLOSE_BOX、 wx.CLIP_CHILDREN。通过组合各种风格，我们可以改变wx的风格。框架小部件。

```python
#!/usr/bin/env python
 
# no_minimize.py

import wx

app = wx.App()
frame = wx.Frame(None, style=wx.MAXIMIZE_BOX | wx.RESIZE_BORDER
	| wx.SYSTEM_MENU | wx.CAPTION |	 wx.CLOSE_BOX)
frame.Show(True)

app.MainLoop()
```

我们的意图是展示一个没有最小化框的窗口。因此，我们没有在样式参数中指定此标志。

## 大小与位置

我们可以通过两种方式指定应用程序的大小。我们在小部件的构造函数中有一个size参数，或者我们可以调用SetSize()方法。

```python
#!/usr/bin/env python

# set_size.py

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title,
            size=(350, 250))


def main():

    app = wx.App()
    ex = Example(None, title='Sizing')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在本例中，应用程序的大小为250x200像素。

```python
def __init__(self, parent, title):
    super(Example, self).__init__(parent, title=title, 
        size=(350, 250))

```

在构造函数中，我们设置`wx.Frame`小部件的宽度到350像素。小部件的高度为250像素。

同样，我们可以在屏幕上定位我们的应用程序。默认情况下，窗口位于屏幕的左上角。但它在各种操作系统平台甚至窗口管理器上可能有所不同。一些窗口管理器自己放置应用程序窗口。其中一些进行了一些优化，这样窗口就不会重叠。程序员可以通过编程定位窗口。我们已经在wx的构造函数中看到了一个pos参数。框架小部件。通过提供默认值以外的其他值，我们可以自己控制位置。

| Method               | Description                         |
| -------------------- | ----------------------------------- |
| Move(wx.Point point) | move a window to the given position |
| MoveXY(int x, int y) | move a window to the given position |
| SetPosition(wx.Point point) | set the position of a window |
| SetDimensions(x, y, width, height, sizeFlags) | set the position and the size of a window |

有几种方法可以做到这一点。 

```python
#!/usr/bin/env python

# moving.py

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title,
            size=(300, 200))

        self.Move((800, 250))


def  main():

    app = wx.App()
    ex = Example(None, title='Moving')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

有一种特殊情况。我们可能希望最大限度地显示我们的窗口。在这种情况下，窗口位于(0，0)，并占据整个屏幕。wxPython在内部计算屏幕坐标。为了最大化我们的`wx.Framewx。Frame`，我们称之为`Maximize()`方法。

## 以屏幕为中心

如果我们想将应用程序集中在屏幕上，wxPython有一个方便的方法。`Centre()`方法只是将窗口居中放置在屏幕上。无需计算屏幕的宽度和高度。只需调用该方法。

```python
#!/usr/bin/env python

# centering.py

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title,
            size=(300, 200))

        self.Centre()


def main():

    app = wx.App()
    ex = Example(None, title='Centering')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在这个例子中，我们在屏幕上居中放置一个小窗口。

```python
self.Centre()
```

`Centre()`方法使窗口在屏幕上居中。

在本章中，我们在wxPython中创建了一些简单的代码示例。