---
layout: framework
title: wxPython中的事件
permalink: /doc/wxpython/events.html
---

# wxPython中的事件

事件是每个GUI应用程序不可或缺的一部分。所有GUI应用程序都是事件驱动的。应用程序对其生命周期中生成的不同事件类型作出反应。事件主要由应用程序的用户生成。但它们也可以通过其他方式产生；例如，互联网连接、窗口管理器或计时器。因此，当我们调用`MainLoop()`方法时，我们的应用程序会等待生成事件。`MainLoop()`方法在我们退出应用程序时结束。

## 定义

事件是来自底层框架（通常是GUI工具包）的一段应用程序级信息。事件循环是一种在程序中等待和调度事件或消息的编程构造。事件循环反复查找要处理的事件。调度器是一个将事件映射到事件处理程序的进程。事件处理程序是对事件作出反应的方法。

Event对象是与事件相关联的对象。它通常是一扇窗户。事件类型是已生成的唯一事件。事件绑定器是一个将事件类型与事件处理程序绑定的对象。

## wxPython `wx.EVT_MOVE`示例

在下面的例子中，我们对`wx.MoveEvent`事件做出反应。当我们将窗口移动到新位置时，会生成该事件。此事件的事件绑定器是`wx.EVT_MOVE`。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

This is a wx.MoveEvent event demostration.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()


    def InitUI(self):

        wx.StaticText(self, label='x:', pos=(10,10))
        wx.StaticText(self, label='y:', pos=(10,30))

        self.st1 = wx.StaticText(self, label='', pos=(30, 10))
        self.st2 = wx.StaticText(self, label='', pos=(30, 30))

        self.Bind(wx.EVT_MOVE, self.OnMove)

        self.SetSize((350, 250))
        self.SetTitle('Move event')
        self.Centre()

    def OnMove(self, e):

        x, y = e.GetPosition()
        self.st1.SetLabel(str(x))
        self.st2.SetLabel(str(y))


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main() 
```

此示例显示窗口的当前位置。

```python
self.Bind(wx.EVT_MOVE, self.OnMove)
```

在这里我们绑定`wx.EVT_MOVE`事件绑定到`OnMove()`方法。

```python
def OnMove(self, e):
    
    x, y = e.GetPosition()
    self.st1.SetLabel(str(x))
    self.st2.SetLabel(str(y))
```

`OnMove()`方法中的事件参数是特定于特定事件类型的对象。在我们的例子中，它是一个`wx.MoveEvent`类的实例。此对象保存有关事件的信息。例如，事件对象或窗口的位置。在我们的例子中，事件对象是`wx.Frame`小部件。我们可以通过调用事件的`GetPosition()`方法来找到当前位置。

![移动事件](/images/doc/wxpython/moveevent.png)

## wxPython事件绑定

在wxPython中处理事件的三个步骤是：

* 确定事件绑定器名称：`wx.EVT_SIZE`，`wx.EVT_CLOSE`等。
* 创建一个事件处理程序。在生成事件时调用此方法。
* 将事件绑定到事件处理程序。

在wxPython中，我们说将一个方法绑定到一个事件。有时会使用单词hook。通过调用`bind()`方法绑定事件。该方法具有以下参数：

```python
Bind(event, handler, source=None, id=wx.ID_ANY, id2=wx.ID_ANY)
```

该事件是`EVT_*`对象之一。它指定事件的类型。处理程序是要调用的对象。换句话说，它是程序员绑定到事件的方法。当我们想要区分相同的事件类型和不同的小部件时，会使用`source`参数。当我们有多个按钮、菜单项等时，会使用id参数。id用于区分它们。当需要将处理程序绑定到一系列id时，例如使用`EVT_MENU_RANGE`时，会使用id2。

请注意，方法`Bind()`是在类`EvtHandler`中定义的。它继承于`wx.Window`。`wx.Window`是wxPython中大多数小部件的基类。还有一个相反的过程。如果我们想从事件中解除方法的绑定，我们调用`Unbind()`方法。它的参数与上面的参数相同。

## 撤销事件

有时我们需要停止处理一个事件。为此，我们调用`Veto()`方法。

```python
#!/usr/bin/env python

import wx

"""
ZetCode wxPython tutorial

In this example we veto an event.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        self.Bind(wx.EVT_CLOSE, self.OnCloseWindow)

        self.SetTitle('Event veto')
        self.Centre()

    def OnCloseWindow(self, e):

        dial = wx.MessageDialog(None, 'Are you sure to quit?', 'Question',
            wx.YES_NO | wx.NO_DEFAULT | wx.ICON_QUESTION)

        ret = dial.ShowModal()

        if ret == wx.ID_YES:
            self.Destroy()
        else:
            e.Veto()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的例子中，我们处理一个`wx.CloseEvent`。此事件称为，当我们单击标题栏上的`X`按钮，按`Alt+F4`或从系统菜单中选择关闭时。在许多应用程序中，如果我们进行了一些更改，我们希望防止意外关闭窗口。要做到这一点，我们必须绑定`wx.EVT_CLOSE`事件绑定器。

```python
dial = wx.MessageDialog(None, 'Are you sure to quit?', 'Question',
    wx.YES_NO | wx.NO_DEFAULT | wx.ICON_QUESTION)
    
ret = dial.ShowModal()
```

在处理关闭事件的过程中，我们会显示一个消息对话框。

```python
if ret == wx.ID_YES:
    self.Destroy()
else:
    event.Veto()
```

根据对话框的返回值，我们破坏窗口，或否决事件。请注意，要关闭窗口，我们必须调用`Destroy()`方法。通过调用`Close()`方法，我们将进入一个无休止的循环。

## wxPython事件传播

有两种类型的事件：基本事件和命令事件。它们的传播方式不同。事件传播是将事件从子窗口小部件传播到父窗口小部件和父窗口大部件。基本事件不会传播。命令事件确实会传播。例如`wx.CloseEvent`是一个基本事件。将此事件传播到父窗口小部件是没有意义的。

默认情况下，在事件处理程序中捕获的事件停止传播。为了继续传播，我们调用`Skip()`方法。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

This example demonstrates event propagation.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class MyPanel(wx.Panel):

    def __init__(self, *args, **kw):
        super(MyPanel, self).__init__(*args, **kw)

        self.Bind(wx.EVT_BUTTON, self.OnButtonClicked)

    def OnButtonClicked(self, e):

        print('event reached panel class')
        e.Skip()


class MyButton(wx.Button):

    def __init__(self, *args, **kw):
        super(MyButton, self).__init__(*args, **kw)

        self.Bind(wx.EVT_BUTTON, self.OnButtonClicked)

    def OnButtonClicked(self, e):

        print('event reached button class')
        e.Skip()


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()


    def InitUI(self):

        mpnl = MyPanel(self)

        MyButton(mpnl, label='Ok', pos=(15, 15))

        self.Bind(wx.EVT_BUTTON, self.OnButtonClicked)

        self.SetTitle('Propagate event')
        self.Centre()

    def OnButtonClicked(self, e):

        print('event reached frame class')
        e.Skip()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的示例中，我们在面板上有一个按钮。面板放置在框架小部件中。我们为所有小部件定义一个处理程序。

```python
def OnButtonClicked(self, e):

    print('event reached button class')
    e.Skip()
```

我们在自定义按钮类中处理按钮单击事件。`Skip()`方法将事件进一步传播到面板类。

试着省略一些`Skip()`方法，看看会发生什么。

## 窗口标识符

窗口标识符是唯一确定事件系统中窗口标识的整数。有三种方法可以创建窗口ID。

* 让系统自动创建一个id
* 使用标准标识符
* 创建您自己的id

```python
wx.Button(parent, -1)
wx.Button(parent, wx.ID_ANY)
```

如果我们提供-1或`wx.ID_ANY`对于`id`参数，我们让wxPython自动为我们创建一个id。自动创建的id总是负数，而用户指定的id必须总是正数。我们通常在不需要更改小部件状态时使用此选项。例如，在应用程序的生命周期中永远不会更改的静态文本。如果我们愿意，我们仍然可以得到身份证。有一个方法`GetId()`来确定id。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we use automatic ids
with wx.ID_ANY.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        pnl = wx.Panel(self)
        exitButton = wx.Button(pnl, wx.ID_ANY, 'Exit', (10, 10))

        self.Bind(wx.EVT_BUTTON,  self.OnExit, id=exitButton.GetId())

        self.SetTitle("Automatic ids")
        self.Centre()

    def OnExit(self, event):

        self.Close()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在这个例子中，我们不关心实际的id值。

```python
self.Bind(wx.EVT_BUTTON,  self.OnExit, id=exitButton.GetId())
```

我们通过调用`GetId()`方法来获得自动生成的id。

建议使用标准标识符。标识符可以在一些平台上提供一些标准图形或行为。

## wxPython标准ID

wxPython包含一些标准id，如`wx.ID_SAVE`或`wx.ID_NEW`。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we create buttons with standard ids.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        pnl = wx.Panel(self)
        grid = wx.GridSizer(3, 2)

        grid.AddMany([(wx.Button(pnl, wx.ID_CANCEL), 0, wx.TOP | wx.LEFT, 9),
            (wx.Button(pnl, wx.ID_DELETE), 0, wx.TOP, 9),
            (wx.Button(pnl, wx.ID_SAVE), 0, wx.LEFT, 9),
            (wx.Button(pnl, wx.ID_EXIT)),
            (wx.Button(pnl, wx.ID_STOP), 0, wx.LEFT, 9),
            (wx.Button(pnl, wx.ID_NEW))])

        self.Bind(wx.EVT_BUTTON, self.OnQuitApp, id=wx.ID_EXIT)

        pnl.SetSizer(grid)

        self.SetTitle("Standard ids")
        self.Centre()

    def OnQuitApp(self, event):

        self.Close()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的示例中，我们在按钮上使用标准标识符。在Linux上，按钮有图标。

```python
grid.AddMany([(wx.Button(pnl, wx.ID_CANCEL), 0, wx.TOP | wx.LEFT, 9),
    (wx.Button(pnl, wx.ID_DELETE), 0, wx.TOP, 9),
    (wx.Button(pnl, wx.ID_SAVE), 0, wx.LEFT, 9),
    (wx.Button(pnl, wx.ID_EXIT)),
    (wx.Button(pnl, wx.ID_STOP), 0, wx.LEFT, 9),
    (wx.Button(pnl, wx.ID_NEW))])
```

我们向网格大小调整器添加了六个按钮。`wx.ID_CANCEL`，`wx.ID_DELETE`，`wx.ID_SAVE`，`wx.ID_EXIT`，`wx.STOP`和`wx.ID_NEW`是标准标识符。

```python
self.Bind(wx.EVT_BUTTON, self.OnQuitApp, id=wx.ID_EXIT)
```

我们将按钮点击事件绑定到`OnQuitApp()`事件处理程序。id参数用于在按钮之间进行区分。我们唯一地确定事件的来源。

![标准ID](/images/doc/wxpython/standardidentifiers.png)

## 自定义事件ID

最后一种选择是使用自己的标识符。我们定义自己的全局id。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we use custom event ids.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

ID_MENU_NEW = wx.NewId()
ID_MENU_OPEN = wx.NewId()
ID_MENU_SAVE = wx.NewId()


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        self.CreateMenuBar()
        self.CreateStatusBar()

        self.SetSize((350, 250))
        self.SetTitle('Custom ids')
        self.Centre()

    def CreateMenuBar(self):

        mb = wx.MenuBar()

        fMenu = wx.Menu()
        fMenu.Append(ID_MENU_NEW, 'New')
        fMenu.Append(ID_MENU_OPEN, 'Open')
        fMenu.Append(ID_MENU_SAVE, 'Save')

        mb.Append(fMenu, '&File')
        self.SetMenuBar(mb)

        self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_NEW)
        self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_OPEN)
        self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_SAVE)

    def DisplayMessage(self, e):

        sb = self.GetStatusBar()

        eid = e.GetId()

        if eid == ID_MENU_NEW:
            msg = 'New menu item selected'
        elif eid == ID_MENU_OPEN:
            msg = 'Open menu item selected'
        elif eid == ID_MENU_SAVE:
            msg = 'Save menu item selected'

        sb.SetStatusText(msg)


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main() 
```

在代码示例中，我们创建了一个包含三个菜单项的菜单。此菜单项的ID是全局创建的。

```python
ID_MENU_NEW = wx.NewId()
ID_MENU_OPEN = wx.NewId()
ID_MENU_SAVE = wx.NewId()
```

`wx.NewId()`方法创建一个新的唯一id。

```python
self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_NEW)
self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_OPEN)
self.Bind(wx.EVT_MENU, self.DisplayMessage, id=ID_MENU_SAVE) 
```

所有三个菜单项都由其唯一id标识。

```python
eid = e.GetId()

if eid == ID_MENU_NEW:
    msg = 'New menu item selected'
elif eid == ID_MENU_OPEN:
    msg = 'Open menu item selected'
elif eid == ID_MENU_SAVE:
    msg = 'Save menu item selected'
```

我们从事件对象中检索id。根据id值，我们准备消息，该消息显示在应用程序的状态栏中。

## wx.PaintEvent

重新绘制窗口时会生成绘制事件。当我们调整窗口大小或最大化窗口时，就会发生这种情况。绘制事件也可以通过程序生成。例如，当我们调用`SetLabel()`方法来更改`wx.StaticText`小部件时。请注意，最小化窗口时，不会生成绘制事件。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we count paint events.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        self.count = 0
        self.Bind(wx.EVT_PAINT, self.OnPaint)

        self.SetTitle('Paint events')
        self.SetSize((350, 250))
        self.Centre()

    def OnPaint(self, e):

        self.count += 1
        dc = wx.PaintDC(self)
        text = "Number of paint events: {0}".format(self.count)
        dc.DrawText(text, 20, 20)


def main():

    app = wx.App()
    ex  = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的示例中，我们计算绘制事件的数量，并在窗口上绘制当前生成的事件的数量。

```python
self.Bind(wx.EVT_PAINT, self.OnPaint)
```

我们将`EVT_PAINT`事件绑定到`OnPaint()`方法。

```python
def OnPaint(self, e):

    self.count += 1
    dc = wx.PaintDC(self)
    text = "Number of paint events: {0}".format(self.count)
    dc.DrawText(text, 20, 20)
```

在`OnPaint()`事件中，我们使用`DrawText()`方法增加计数器draw窗口上绘制事件的数量。

## wx.FocusEvent

焦点表示应用程序中当前选定的小部件。从键盘输入或从剪贴板粘贴的文本将发送到具有焦点的小部件。有两种事件类型与焦点有关。`wx.EVT_SET_FOCUS`事件，该事件是在小部件接收焦点时生成的。当小部件失去焦点时，将生成`wx.EVT_KILL_FOCUS`。通过单击或通过keybord键、esually `Tab`或`Shift+Tab`来更改焦点。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we work with wx.FocusEvent.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class MyWindow(wx.Panel):

    def __init__(self, parent):
        super(MyWindow, self).__init__(parent)

        self.color = '#b3b3b3'

        self.Bind(wx.EVT_PAINT, self.OnPaint)
        self.Bind(wx.EVT_SIZE, self.OnSize)
        self.Bind(wx.EVT_SET_FOCUS, self.OnSetFocus)
        self.Bind(wx.EVT_KILL_FOCUS, self.OnKillFocus)

    def OnPaint(self, e):

        dc = wx.PaintDC(self)

        dc.SetPen(wx.Pen(self.color))
        x, y = self.GetSize()
        dc.DrawRectangle(0, 0, x, y)

    def OnSize(self, e):

        self.Refresh()

    def OnSetFocus(self, e):

        self.color = '#ff0000'
        self.Refresh()

    def OnKillFocus(self, e):

        self.color = '#b3b3b3'
        self.Refresh()


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()


    def InitUI(self):

        grid = wx.GridSizer(2, 2, 10, 10)
        grid.AddMany([(MyWindow(self), 0, wx.EXPAND|wx.TOP|wx.LEFT, 9),
            (MyWindow(self), 0, wx.EXPAND|wx.TOP|wx.RIGHT, 9),
            (MyWindow(self), 0, wx.EXPAND|wx.BOTTOM|wx.LEFT, 9),
            (MyWindow(self), 0, wx.EXPAND|wx.BOTTOM|wx.RIGHT, 9)])


        self.SetSizer(grid)

        self.SetSize((350, 250))
        self.SetTitle('Focus event')
        self.Centre()


    def OnMove(self, e):

        print(e.GetEventObject())
        x, y = e.GetPosition()
        self.st1.SetLabel(str(x))
        self.st2.SetLabel(str(y))


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的例子中，我们有四个面板。带有焦点的面板高亮显示。

```python
self.Bind(wx.EVT_SET_FOCUS, self.OnSetFocus)
self.Bind(wx.EVT_KILL_FOCUS, self.OnKillFocus)
```

我们将两个焦点事件绑定到事件处理程序。

```python
def OnPaint(self, e):
    
    dc = wx.PaintDC(self)

    dc.SetPen(wx.Pen(self.color))
    x, y = self.GetSize()
    dc.DrawRectangle(0, 0, x, y)
```

在`OnPaint()`方法中，我们在窗口上绘制。轮廓的颜色取决于窗口是否有焦点。聚焦窗口的轮廓是用红色绘制的。

```python
def OnSetFocus(self, e):

    self.color = '#ff0000'
    self.Refresh()
```

在`OnSetFocus()`方法中，我们将`self.color`变量设置为红色。我们刷新框架窗口，该窗口将为其所有子窗口生成一个绘画事件。窗户被重新绘制，有焦点的窗户轮廓有了新的颜色。

```python
def OnKillFocus(self, e):

    self.color = '#b3b3b3'
    self.Refresh()
```

当窗口失去焦点时，会调用`OnKillFocus()`方法。我们更改颜色值并刷新。

![焦点事件](/images/doc/wxpython/focusevent.png)

## wx.KeyEvent

当我们按下键盘上的一个键，生成一个`wx.KeyEvent`。此事件将发送到当前具有焦点的小部件。有三种不同的密钥处理程序：

* wx.EVT_KEY_DOWN
* wx.EVT_KEY_UP
* wx.EVT_CHAR

一个常见的请求是在按下`Esc`键时关闭应用程序。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

In this example we work with wx.KeyEvent.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx

class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()

    def InitUI(self):

        pnl = wx.Panel(self)
        pnl.Bind(wx.EVT_KEY_DOWN, self.OnKeyDown)
        pnl.SetFocus()

        self.SetSize((350, 250))
        self.SetTitle('Key event')
        self.Centre()

    def OnKeyDown(self, e):

        key = e.GetKeyCode()

        if key == wx.WXK_ESCAPE:

            ret  = wx.MessageBox('Are you sure to quit?', 'Question',
                wx.YES_NO | wx.NO_DEFAULT, self)

            if ret == wx.YES:
                self.Close()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在本例中，我们将处理按`Esc`键的过程。此时会显示一个消息框，用于确认应用程序的终止。

```python
pnl.Bind(wx.EVT_KEY_DOWN, self.OnKeyDown)
```

我们将事件处理程序绑定到`wx.EVT_KEY_DOWN`事件。

```python
key = e.GetKeyCode()
```

在这里我们可以得到按下的键的键代码。

```python
if key == wx.WXK_ESCAPE:
```

我们检查密钥代码。`Esc`键具有`wx.WXK_ESCAPE`代码。

在本章中，我们讨论了wxPython中的事件。
