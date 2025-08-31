---
layout: framework
title: 布局管理
permalink: /doc/wxpython/layout.html
---

# 布局管理

一个典型的应用程序由各种小部件组成。这些小部件被放置在容器小部件中。程序员必须管理应用程序的布局。这不是一项容易的任务。在wxPython中，可以使用绝对定位或使用sizer来布局小部件。

## 绝对定位

程序员指定每个小部件的位置和大小（以像素为单位）。绝对定位有几个缺点：

* 如果我们调整窗口的大小，小部件的大小和位置不会改变。
* 应用程序在不同的平台上看起来不同。
* 更改应用程序中的字体可能会破坏布局。
* 如果我们决定更改布局，我们必须完全重做布局，这既繁琐又耗时。

在某些情况下，我们可能会使用绝对定位。例如，小的测试示例。但大多数情况下，在现实世界的程序中，程序员使用sizer。

在我们的例子中，我们有一个文本编辑器的简单框架。如果我们调整窗口的大小，则其大小为`wx.TextCtrl `不会像我们预期的那样发生更改。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example, we lay out widgets using
absolute positioning.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title,
            size=(350, 300))

        self.InitUI()
        self.Centre()

    def InitUI(self):

        self.panel = wx.Panel(self)

        self.panel.SetBackgroundColour("gray")

        self.LoadImages()

        self.mincol.SetPosition((20, 20))
        self.bardejov.SetPosition((40, 160))
        self.rotunda.SetPosition((170, 50))


    def LoadImages(self):

        self.mincol = wx.StaticBitmap(self.panel, wx.ID_ANY,
            wx.Bitmap("mincol.jpg", wx.BITMAP_TYPE_ANY))

        self.bardejov = wx.StaticBitmap(self.panel, wx.ID_ANY,
            wx.Bitmap("bardejov.jpg", wx.BITMAP_TYPE_ANY))

        self.rotunda = wx.StaticBitmap(self.panel, wx.ID_ANY,
            wx.Bitmap("rotunda.jpg", wx.BITMAP_TYPE_ANY))


def main():

    app = wx.App()
    ex = Example(None, title='Absolute positioning')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在上面的例子中，我们使用绝对坐标定位三个图像。

```python
self.mincol.SetPosition((20, 20))
```

使用`SetPosition()`方法，我们将图像放置在x=20，y=20坐标处。

![绝对定位](/images/doc/wxpython/absolute.png)

## 使用sizer

Sizers确实通过绝对定位解决了我们提到的所有这些问题。wxPython具有以下大小调整器：

* wx.BoxSizer
* wx.StaticBoxSizer
* wx.GridSizer
* wx.FlexGridSizer
* wx.GridBagSizer

## wx.BoxSizer

`wx.BoxSizer`使我们能够将几个小部件放入一行或一列中。我们可以将另一个sizer放入现有的sizer中。通过这种方式，我们可以创建非常复杂的布局。

```python
 box = wx.BoxSizer(integer orient)
 box.Add(wx.Window window, integer proportion=0, integer flag = 0, integer border = 0)
```

方向可以是`wx.VERTICAL`或`wx.HORIZONTAL`。将小部件添加到`wx.BoxSizer`是通过`Add()`方法完成的。为了理解它，我们需要看看它的参数。

比例参数定义了小部件在定义的方向上的变化比例。假设我们有三个比例分别为0、1和2的按钮。它们被添加到水平`wx.BoxSizer`。比例为0的按钮不会发生任何变化。在水平维度中，比例为2的按钮将比比例为1的按钮变化两倍。

使用flag参数，您可以进一步配置`wx.BoxSizer`中小部件的行为。我们可以控制小部件之间的边界。我们在小部件之间添加一些像素空间。为了应用边界，我们需要定义边界使用的边。我们可以将它们与|运算符组合；例如`wx.LEFT | wx.BOTTOM`。我们可以在以下标志之间进行选择：

* wx.LEFT
* wx.RIGHT
* wx.BOTTOM
* wx.TOP
* wx.ALL

sizer是通过`setSizer()`方法设置到面板小部件的。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we place a panel inside 
another panel.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()

    def InitUI(self):

        panel = wx.Panel(self)

        panel.SetBackgroundColour('#4f5049')
        vbox = wx.BoxSizer(wx.VERTICAL)

        midPan = wx.Panel(panel)
        midPan.SetBackgroundColour('#ededed')

        vbox.Add(midPan, wx.ID_ANY, wx.EXPAND | wx.ALL, 20)
        panel.SetSizer(vbox)


def main():

    app = wx.App()
    ex = Example(None, title='Border')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在上面的示例中，我们在面板周围放置一些空间。

```python
vbox.Add(midPan, wx.ID_ANY, wx.EXPAND | wx.ALL, 20)
```

在上面代码中，我们在midPan面板周围放置了一个20像素的边框。`wx.ALL`将边界大小应用于所有四边。

如果我们使用`wx.EXPAND`标志，我们的小部件将使用分配给它的所有空间。最后，我们还可以定义小部件的对齐方式。我们使用以下标志：

* wx.ALIGN_LEFT
* wx.ALIGN_RIGHT
* wx.ALIGN_TOP
* wx.ALIGN_BOTTOM
* wx.ALIGN_CENTER_VERTICAL
* wx.ALIGN_CENTER_HORIZONTAL
* wx.ALIGN_CENTER

![面板周围的边框](/images/doc/wxpython/border.png)

## GoToClass示例

在下面的例子中，我们介绍了几个重要的想法。

```python
#!/usr/bin/env python


"""
ZetCode wxPython tutorial

In this example we create a Go To class
layout with wx.BoxSizer.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()

    def InitUI(self):

        panel = wx.Panel(self)

        font = wx.SystemSettings.GetFont(wx.SYS_SYSTEM_FONT)

        font.SetPointSize(9)

        vbox = wx.BoxSizer(wx.VERTICAL)

        hbox1 = wx.BoxSizer(wx.HORIZONTAL)
        st1 = wx.StaticText(panel, label='Class Name')
        st1.SetFont(font)
        hbox1.Add(st1, flag=wx.RIGHT, border=8)
        tc = wx.TextCtrl(panel)
        hbox1.Add(tc, proportion=1)
        vbox.Add(hbox1, flag=wx.EXPAND|wx.LEFT|wx.RIGHT|wx.TOP, border=10)

        vbox.Add((-1, 10))

        hbox2 = wx.BoxSizer(wx.HORIZONTAL)
        st2 = wx.StaticText(panel, label='Matching Classes')
        st2.SetFont(font)
        hbox2.Add(st2)
        vbox.Add(hbox2, flag=wx.LEFT | wx.TOP, border=10)

        vbox.Add((-1, 10))

        hbox3 = wx.BoxSizer(wx.HORIZONTAL)
        tc2 = wx.TextCtrl(panel, style=wx.TE_MULTILINE)
        hbox3.Add(tc2, proportion=1, flag=wx.EXPAND)
        vbox.Add(hbox3, proportion=1, flag=wx.LEFT|wx.RIGHT|wx.EXPAND,
            border=10)

        vbox.Add((-1, 25))

        hbox4 = wx.BoxSizer(wx.HORIZONTAL)
        cb1 = wx.CheckBox(panel, label='Case Sensitive')
        cb1.SetFont(font)
        hbox4.Add(cb1)
        cb2 = wx.CheckBox(panel, label='Nested Classes')
        cb2.SetFont(font)
        hbox4.Add(cb2, flag=wx.LEFT, border=10)
        cb3 = wx.CheckBox(panel, label='Non-Project classes')
        cb3.SetFont(font)
        hbox4.Add(cb3, flag=wx.LEFT, border=10)
        vbox.Add(hbox4, flag=wx.LEFT, border=10)

        vbox.Add((-1, 25))

        hbox5 = wx.BoxSizer(wx.HORIZONTAL)
        btn1 = wx.Button(panel, label='Ok', size=(70, 30))
        hbox5.Add(btn1)
        btn2 = wx.Button(panel, label='Close', size=(70, 30))
        hbox5.Add(btn2, flag=wx.LEFT|wx.BOTTOM, border=5)
        vbox.Add(hbox5, flag=wx.ALIGN_RIGHT|wx.RIGHT, border=10)

        panel.SetSizer(vbox)


def main():

    app = wx.App()
    ex = Example(None, title='Go To Class')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

布局过于紧凑。我们创建一个垂直sizer。然后我们在里面放了五个水平分级机。

```python
font = wx.SystemSettings.GetFont(wx.SYS_SYSTEM_FONT)

font.SetPointSize(9)
```

我们将字体大小更改为9像素。

```python
vbox.Add(hbox3, proportion=1, flag=wx.LEFT|wx.RIGHT|wx.EXPAND, 
    border=10)

vbox.Add((-1, 25))
```

我们已经知道，我们可以通过组合flag参数和border参数来控制小部件之间的距离。但有一个真正的制约因素。在`Add()`方法中，我们只能为所有给定的边指定一个边界。在我们的例子中，我们给右边和左边10像素。但我们不能给底部25像素。我们可以做的是给底部10像素，如果我们省略`wx.BOTTOM`，则为0像素。因此，如果我们需要不同的值，我们可以添加一些额外的空间。使用`Add()`方法，我们还可以插入小部件和空间。

```python
vbox.Add(hbox5, flag=wx.ALIGN_RIGHT|wx.RIGHT, border=10)
```

我们把两个按钮放在窗户的右边。实现这一点有三件事很重要：比例、对齐标志和`wx.EXPAND`标志。比例必须为零。当我们调整窗口大小时，按钮不应该改变它们的大小。我们不能指定`wx.EXPAND`标志。按钮仅复制已附加到它们的区域。最后，我们必须指定`wx.ALIGN_RIGHT`标志。水平尺寸调整器从窗口的左侧扩展到右侧。因此，如果我们指定`wx.ALIGN_RIGHT`标志，按钮位于右侧。

![GoToClass窗口](/images/doc/wxpython/gotoclass.png)

## wx.GridSizer

`wx.GridSizer`在二维表中布置小部件。表中的每个单元格都具有相同的大小。

```python
wx.GridSizer(int rows=1, int cols=0, int vgap=0, int hgap=0)
```

在构造函数中，我们指定表中的行数和列数以及单元格之间的垂直和水平空间。

在我们的例子中，我们创建了一个计算器的骨架。

```python
#!/usr/bin/env python


"""
ZetCode wxPython tutorial

In this example we create a layout
of a calculator with wx.GridSizer.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()


    def InitUI(self):

        menubar = wx.MenuBar()
        fileMenu = wx.Menu()
        menubar.Append(fileMenu, '&File')
        self.SetMenuBar(menubar)

        vbox = wx.BoxSizer(wx.VERTICAL)
        self.display = wx.TextCtrl(self, style=wx.TE_RIGHT)
        vbox.Add(self.display, flag=wx.EXPAND|wx.TOP|wx.BOTTOM, border=4)
        gs = wx.GridSizer(5, 4, 5, 5)

        gs.AddMany( [(wx.Button(self, label='Cls'), 0, wx.EXPAND),
            (wx.Button(self, label='Bck'), 0, wx.EXPAND),
            (wx.StaticText(self), wx.EXPAND),
            (wx.Button(self, label='Close'), 0, wx.EXPAND),
            (wx.Button(self, label='7'), 0, wx.EXPAND),
            (wx.Button(self, label='8'), 0, wx.EXPAND),
            (wx.Button(self, label='9'), 0, wx.EXPAND),
            (wx.Button(self, label='/'), 0, wx.EXPAND),
            (wx.Button(self, label='4'), 0, wx.EXPAND),
            (wx.Button(self, label='5'), 0, wx.EXPAND),
            (wx.Button(self, label='6'), 0, wx.EXPAND),
            (wx.Button(self, label='*'), 0, wx.EXPAND),
            (wx.Button(self, label='1'), 0, wx.EXPAND),
            (wx.Button(self, label='2'), 0, wx.EXPAND),
            (wx.Button(self, label='3'), 0, wx.EXPAND),
            (wx.Button(self, label='-'), 0, wx.EXPAND),
            (wx.Button(self, label='0'), 0, wx.EXPAND),
            (wx.Button(self, label='.'), 0, wx.EXPAND),
            (wx.Button(self, label='='), 0, wx.EXPAND),
            (wx.Button(self, label='+'), 0, wx.EXPAND) ])

        vbox.Add(gs, proportion=1, flag=wx.EXPAND)
        self.SetSizer(vbox)


def main():

    app = wx.App()
    ex = Example(None, title='Calculator')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

请注意，我们是如何设法在“Bck”和“Close”按钮之间留出一个空格的。我们只是放一个空的`wx.StaticText`在那里。

在我们的示例中，我们使用了`AddMany()`方法。这是一种同时添加多个小部件的方便方法。

```python
gs.AddMany([(wx.Button(self, label='Cls'), 0, wx.EXPAND),
...
```

小部件按照添加的顺序放置在表格内。首先填充第一行，然后填充第二行等。

![计算器](/images/doc/wxpython/calculator.png)

## wx.FlexGridSizer

这个sizer类似于`wx.GridSizer`。它还将其小部件放在一个二维表中。它增加了一些灵活性。`wx.GridSizer`单元格大小相同。`wx.FlexGridSizer`中的所有单元格在一行中具有相同的高度。列中的所有单元格都具有相同的宽度。但并非所有的行和列都必须具有相同的高度或宽度。

```python
wx.FlexGridSizer(int rows=1, int cols=0, int vgap=0, int hgap=0)
```

`rows`和`cols`指定sizer中的行数和列数。`vgap`和`hgap`在两个方向的小部件之间增加了一些空间。

很多时候，开发人员必须开发用于数据输入和修改的对话框。我找到`wx.FlexGridSizer`适用于此类任务的。开发人员可以使用此sizer轻松地设置对话框窗口。也可以用`wx.GridSizer`来实现这一点，但它看起来不太好，因为每个单元格必须具有相同的大小。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we create review
layout with wx.FlexGridSizer.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()
        self.Show()

    def InitUI(self):

        panel = wx.Panel(self)

        hbox = wx.BoxSizer(wx.HORIZONTAL)

        fgs = wx.FlexGridSizer(3, 2, 9, 25)

        title = wx.StaticText(panel, label="Title")
        author = wx.StaticText(panel, label="Author")
        review = wx.StaticText(panel, label="Review")

        tc1 = wx.TextCtrl(panel)
        tc2 = wx.TextCtrl(panel)
        tc3 = wx.TextCtrl(panel, style=wx.TE_MULTILINE)

        fgs.AddMany([(title), (tc1, 1, wx.EXPAND), (author),
            (tc2, 1, wx.EXPAND), (review, 1, wx.EXPAND), (tc3, 1, wx.EXPAND)])

        fgs.AddGrowableRow(2, 1)
        fgs.AddGrowableCol(1, 1)

        hbox.Add(fgs, proportion=1, flag=wx.ALL|wx.EXPAND, border=15)
        panel.SetSizer(hbox)


def main():

    app = wx.App()
    ex = Example(None, title='Review')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在上面的代码示例中，我们使用`FlexGridSizer`创建了一个Review窗口。

```python
hbox = wx.BoxSizer(wx.HORIZONTAL)
...
hbox.Add(fgs, proportion=1, flag=wx.ALL|wx.EXPAND, border=15)
```

我们创建了一个水平的框大小调整器，以便在小部件表周围放置一些空间（15像素）。

```python
fgs.AddMany([(title), (tc1, 1, wx.EXPAND), (author), 
    (tc2, 1, wx.EXPAND), (review, 1, wx.EXPAND), (tc3, 1, wx.EXPAND)])
```

我们使用`AddMany()`方法将小部件添加到sizer中。两个`wx.FlexGridSizer`和`wx.GridSizer`共享此方法。

```python
fgs.AddGrowableRow(2, 1)
fgs.AddGrowableCol(1, 1)
```

我们使第三行和第二列可增长。通过这种方式，我们可以在调整窗口大小时让文本控件增长。前两个文本控件将沿水平方向增长，第三个控件将沿两个方向增长。我们决不能忘记使用`wx.EXPAND`使小部件可扩展以使其工作。

![Review例子](/images/doc/wxpython/review.png)

## wx.GridBagSizer

`wx.GridBagSizer`是wxPython中最灵活使用的sizer。这种sizer并非仅适用于wxPython。我们也可以在其他工具包中找到它。

此sizer可以显式定位项目。项目也可以选择跨越多行或多列。`wx.GridBagSizer`有一个简单的构造函数。

```python
wx.GridBagSizer(integer vgap, integer hgap)
```

垂直和水平间隙定义了所有子对象之间使用的像素空间。我们使用`Add()`方法将项添加到网格中。

```python
Add(self, item, tuple pos, tuple span=wx.DefaultSpan, integer flag=0, 
    integer border=0, userData=None)
```

Item是插入到网格中的小部件。`pos`指定虚拟网格中的位置。左上角单元格的`pos`为(0,0)。跨度是小部件的可选跨度;例如，span(3,2)将一个小部件跨3行2列。早些时候讨论过`wx.BoxSizer`的flag和border问题。调整窗口大小时，网格中的项目可以更改其大小或保持默认大小。如果我们希望您的item增长和收缩，我们可以使用以下两种方法：

```python
AddGrowableRow(integer row)
AddGrowableCol(integer col)
```

## 重命名窗口示例

在我们的第一个示例中，我们创建了一个重命名窗口。它将有一个`wx.StaticText`，一个`wx.TextCtrl`和两个`wx.Button`小部件。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we create a rename layout
with wx.GridBagSizer.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()

    def InitUI(self):

        panel = wx.Panel(self)
        sizer = wx.GridBagSizer(4, 4)

        text = wx.StaticText(panel, label="Rename To")
        sizer.Add(text, pos=(0, 0), flag=wx.TOP|wx.LEFT|wx.BOTTOM, border=5)

        tc = wx.TextCtrl(panel)
        sizer.Add(tc, pos=(1, 0), span=(1, 5),
            flag=wx.EXPAND|wx.LEFT|wx.RIGHT, border=5)

        buttonOk = wx.Button(panel, label="Ok", size=(90, 28))
        buttonClose = wx.Button(panel, label="Close", size=(90, 28))
        sizer.Add(buttonOk, pos=(3, 3))
        sizer.Add(buttonClose, pos=(3, 4), flag=wx.RIGHT|wx.BOTTOM, border=10)

        sizer.AddGrowableCol(1)
        sizer.AddGrowableRow(2)
        panel.SetSizer(sizer)


def main():

    app = wx.App()
    ex = Example(None, title='Rename')
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

我们必须把窗户看作一张大格子桌子。

```python
text = wx.StaticText(panel, label="Rename To")
sizer.Add(text, pos=(0, 0), flag=wx.TOP|wx.LEFT|wx.BOTTOM, border=10)
```

文本“重命名为”位于左上角。因此，我们指定（0，0）位置。我们在底部、左侧和底部添加一些空间。

```python
tc = wx.TextCtrl(panel)
sizer.Add(tc, pos=(1, 0), span=(1, 5), 
    flag=wx.EXPAND|wx.LEFT|wx.RIGHT, border=5)
```

`wx.TextCtrl`转到第二行（1，0）的开头。记住，我们从零开始计数。它扩展了1行5列（1，5）。我们在小部件的左侧和右侧放置了5个像素的空间。

```python
sizer.Add(buttonOk, pos=(3, 3))
sizer.Add(buttonClose, pos=(3, 4), flag=wx.RIGHT|wx.BOTTOM, border=10)
```

我们在第四排放了两个按钮。第三行是空的，所以`wx.TextCtrl`和按钮之间有一些空间。我们将“确定”按钮放入第四列，将“关闭”按钮置于第五列。请注意，一旦我们将一些空间应用于一个小部件，它就会应用于整行。这就是为什么我们没有为“确定”按钮指定底部空间的原因。细心的读者可能会注意到，我们没有指定两个按钮之间的任何间距；也就是说，我们没有在OK按钮的右侧或Close按钮的右侧放置任何空格。在`wx.GridBagSizer`，我们在所有小部件之间留出一些空间。所以已经有一些空间了。

```python
sizer.AddGrowableCol(1)
sizer.AddGrowableRow(2)
```

我们必须做的最后一件事是调整对话框的大小。我们使第二列和第三行可增长。现在我们可以扩大或缩小我们的窗口。试着评论这两行，看看会发生什么。

![重命名窗口](/images/doc/wxpython/rename.png)


## 新类示例

在下一个示例中，我们将创建一个窗口，该窗口可以在JDeveloper中找到。这是一个用Java创建新类的窗口。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we create a new class layout
with wx.GridBagSizer.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, parent, title):
        super(Example, self).__init__(parent, title=title)

        self.InitUI()
        self.Centre()

    def InitUI(self):

        panel = wx.Panel(self)

        sizer = wx.GridBagSizer(5, 5)

        text1 = wx.StaticText(panel, label="Java Class")
        sizer.Add(text1, pos=(0, 0), flag=wx.TOP|wx.LEFT|wx.BOTTOM,
            border=15)

        icon = wx.StaticBitmap(panel, bitmap=wx.Bitmap('exec.png'))
        sizer.Add(icon, pos=(0, 4), flag=wx.TOP|wx.RIGHT|wx.ALIGN_RIGHT,
            border=5)

        line = wx.StaticLine(panel)
        sizer.Add(line, pos=(1, 0), span=(1, 5),
            flag=wx.EXPAND|wx.BOTTOM, border=10)

        text2 = wx.StaticText(panel, label="Name")
        sizer.Add(text2, pos=(2, 0), flag=wx.LEFT, border=10)

        tc1 = wx.TextCtrl(panel)
        sizer.Add(tc1, pos=(2, 1), span=(1, 3), flag=wx.TOP|wx.EXPAND)

        text3 = wx.StaticText(panel, label="Package")
        sizer.Add(text3, pos=(3, 0), flag=wx.LEFT|wx.TOP, border=10)

        tc2 = wx.TextCtrl(panel)
        sizer.Add(tc2, pos=(3, 1), span=(1, 3), flag=wx.TOP|wx.EXPAND,
            border=5)

        button1 = wx.Button(panel, label="Browse...")
        sizer.Add(button1, pos=(3, 4), flag=wx.TOP|wx.RIGHT, border=5)

        text4 = wx.StaticText(panel, label="Extends")
        sizer.Add(text4, pos=(4, 0), flag=wx.TOP|wx.LEFT, border=10)

        combo = wx.ComboBox(panel)
        sizer.Add(combo, pos=(4, 1), span=(1, 3),
            flag=wx.TOP|wx.EXPAND, border=5)

        button2 = wx.Button(panel, label="Browse...")
        sizer.Add(button2, pos=(4, 4), flag=wx.TOP|wx.RIGHT, border=5)

        sb = wx.StaticBox(panel, label="Optional Attributes")

        boxsizer = wx.StaticBoxSizer(sb, wx.VERTICAL)
        boxsizer.Add(wx.CheckBox(panel, label="Public"),
            flag=wx.LEFT|wx.TOP, border=5)
        boxsizer.Add(wx.CheckBox(panel, label="Generate Default Constructor"),
            flag=wx.LEFT, border=5)
        boxsizer.Add(wx.CheckBox(panel, label="Generate Main Method"),
            flag=wx.LEFT|wx.BOTTOM, border=5)
        sizer.Add(boxsizer, pos=(5, 0), span=(1, 5),
            flag=wx.EXPAND|wx.TOP|wx.LEFT|wx.RIGHT , border=10)

        button3 = wx.Button(panel, label='Help')
        sizer.Add(button3, pos=(7, 0), flag=wx.LEFT, border=10)

        button4 = wx.Button(panel, label="Ok")
        sizer.Add(button4, pos=(7, 3))

        button5 = wx.Button(panel, label="Cancel")
        sizer.Add(button5, pos=(7, 4), span=(1, 1),
            flag=wx.BOTTOM|wx.RIGHT, border=10)

        sizer.AddGrowableCol(2)

        panel.SetSizer(sizer)
        sizer.Fit(self)
        

def main():

    app = wx.App()
    ex = Example(None, title="Create Java Class")
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

这是一个更复杂的布局。我们都用`wx.GridBagSizer`和一个`wx.StaticBoxsizer`。

```python
line = wx.StaticLine(panel)
sizer.Add(line, pos=(1, 0), span=(1, 5), 
    flag=wx.EXPAND|wx.BOTTOM, border=10)
```

这是一行，用于分隔布局中的小部件组。

```python
icon = wx.StaticBitmap(panel, bitmap=wx.Bitmap('exec.png'))
sizer.Add(icon, pos=(0, 4), flag=wx.TOP|wx.RIGHT|wx.ALIGN_RIGHT, 
    border=5)
```

我们放了一个`wx.StaticBitmap`到网格的第一行。我们将其放置在该行的右侧。

```python
sb = wx.StaticBox(panel, label="Optional Attributes")
boxsizer = wx.StaticBoxSizer(sb, wx.VERTICAL)
```

`wx.StaticBoxSizer`类似于普通的`wx.BoxSizer`，但它在sizer周围添加了一个静态框。我们将复选框放入静态框大小调整器中。

![新类窗口](/images/doc/wxpython/newclass.png)

wxPython教程的这一部分专门介绍布局管理。