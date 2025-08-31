---
layout: framework
title: wxPython对话框
permalink: /doc/wxpython/dialogs.html
---

# wxPython对话框

对话框窗口或对话框是大多数现代GUI应用程序不可或缺的一部分。对话被定义为两个或多个人之间的对话。在计算机应用程序中，对话框是用于与应用程序“对话”的窗口。对话框用于输入数据、修改数据、更改应用程序设置等。对话框是用户和计算机程序之间通信的重要手段。

我们可以使用预定义的对话框，如消息框、字体或颜色对话框，或者创建自定义对话框。

## 一个简单的消息框

消息框向用户提供简短信息。一个很好的例子是CD刻录应用程序。刻录完CD后，会弹出一个信息框。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

This example shows a simple
message box.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, *args, **kwargs):
        super(Example, self).__init__(*args, **kwargs)

        self.InitUI()

    def InitUI(self):

        wx.CallLater(3000, self.ShowMessage)

        self.SetSize((300, 200))
        self.SetTitle('Message box')
        self.Centre()

    def ShowMessage(self):
        wx.MessageBox('Download completed', 'Info',
            wx.OK | wx.ICON_INFORMATION)


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

此示例显示三秒后的消息框。

```python
wx.CallLater(3000, self.ShowMessage)
```

`wx.CallLater`在三秒后调用一个方法。第一个参数是一个时间值，在该时间值之后调用给定的方法。参数以毫秒为单位。第二个参数是要调用的方法。

```python
def ShowMessage(self):
    wx.MessageBox('Download completed', 'Info', 
        wx.OK | wx.ICON_INFORMATION)
```

`wx.MessageBox`显示一个小对话框窗口。我们提供三个参数：文本消息、标题消息和标志。标志用于显示不同的按钮和图标。在我们的例子中，我们显示了一个OK按钮和Information图标。

![一个消息框](/images/doc/wxpython/messagebox.png)

## 预定义对话框

wxPython有几个预定义的对话框。这些对话框用于常见的编程任务，如显示文本、接收输入、加载和保存文件。

## 消息对话框

消息对话框用于向用户显示消息。它们比我们在前面的示例中看到的简单消息框更灵活。它们是可定制的。我们可以更改将在对话框中显示的图标和按钮。

| 标签                | 意思                     |
| ------------------- | ------------------------ |
| wx.OK               | 显示“确定”按钮         |
| wx.CANCEL           | 显示“取消”按钮         |
| wx.YES_NO           | 显示“是”、“否”按钮   |
| wx.YES_DEFAULT      | 将“是”按钮设为默认按钮 |
| wx.NO_DEFAULT       | 将“否”按钮设为默认按钮 |
| wx.ICON_EXCLAMATION | 显示警报图标             |
| wx.ICON_ERROR       | 显示错误图标             |
| wx.ICON_HAND        | 与wx.ICON_ERROR相同      |
| wx.ICON_INFORMATION | 显示信息图标             |
| wx.ICON_QUESTION    | 显示问题图标             |

这些标志可以与`wx.MessageDialog`类一起使用。

```python
#!/usr/bin/env python

"""
ZetCode wxPython tutorial

This example shows four types of
message dialogs.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
"""

import wx


class Example(wx.Frame):

    def __init__(self, *args, **kwargs):
        super(Example, self).__init__(*args, **kwargs)

        self.InitUI()

    def InitUI(self):

        panel = wx.Panel(self)

        hbox = wx.BoxSizer()
        sizer = wx.GridSizer(2, 2, 2, 2)

        btn1 = wx.Button(panel, label='Info')
        btn2 = wx.Button(panel, label='Error')
        btn3 = wx.Button(panel, label='Question')
        btn4 = wx.Button(panel, label='Alert')

        sizer.AddMany([btn1, btn2, btn3, btn4])

        hbox.Add(sizer, 0, wx.ALL, 15)
        panel.SetSizer(hbox)

        btn1.Bind(wx.EVT_BUTTON, self.ShowMessage1)
        btn2.Bind(wx.EVT_BUTTON, self.ShowMessage2)
        btn3.Bind(wx.EVT_BUTTON, self.ShowMessage3)
        btn4.Bind(wx.EVT_BUTTON, self.ShowMessage4)

        self.SetSize((300, 200))
        self.SetTitle('Messages')
        self.Centre()

    def ShowMessage1(self, event):
        dial = wx.MessageDialog(None, 'Download completed', 'Info', wx.OK)
        dial.ShowModal()

    def ShowMessage2(self, event):
        dial = wx.MessageDialog(None, 'Error loading file', 'Error',
            wx.OK | wx.ICON_ERROR)
        dial.ShowModal()

    def ShowMessage3(self, event):
        dial = wx.MessageDialog(None, 'Are you sure to quit?', 'Question',
            wx.YES_NO | wx.NO_DEFAULT | wx.ICON_QUESTION)
        dial.ShowModal()

    def ShowMessage4(self, event):
        dial = wx.MessageDialog(None, 'Unallowed operation', 'Exclamation',
            wx.OK | wx.ICON_EXCLAMATION)
        dial.ShowModal()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在我们的示例中，我们创建了四个按钮，并将它们放在网格大小器中。这些按钮将显示四个不同的对话框窗口。我们通过指定不同的样式标志来创建它们。

```python
def ShowMessage2(self, event):
    dial = wx.MessageDialog(None, 'Error loading file', 'Error', 
        wx.OK | wx.ICON_ERROR)
    dial.ShowModal()
```

消息对话框的创建非常简单。我们通过提供`None`作为父窗口，将对话框设置为顶级窗口。这两个字符串提供消息文本和对话框标题。我们通过指定`wx.OK`和`wx.ICON_ERROR`标志来显示一个OK按钮和一个错误图标。为了在屏幕上显示对话框，我们调用`ShowModal()`方法。

## “关于”对话框

几乎每个应用程序都有一个典型的关于对话框。它通常位于“帮助”菜单中。此对话框的目的是向用户提供有关应用程序名称和版本的基本信息。在过去，这些对话往往非常简短。如今，这些盒子中的大多数都提供了关于作者的额外信息。他们将学分授予额外的程序员或文档作者。它们还提供有关应用程序许可证的信息。这些框可以显示公司的徽标或应用程序徽标。

为了创建一个关于对话框，我们必须创建两个对象。`wx.adv.AboutDialogInfo`和`wx.adv.AboutBox`。

wxPython可以显示两种“关于”框。这取决于我们使用的平台和调用的方法。它可以是本机对话框，也可以是wxPython通用对话框。Windows原生的关于对话框无法显示自定义图标、许可证文本或URL。如果我们省略这三个字段，wxPython将显示一个原生对话框。否则，它将求助于一个通用的。如果我们想尽可能保持原生状态，建议在单独的菜单项中提供许可证信息。GTK+可以显示所有这些字段。

```python
#!/usr/bin/env python

'''
ZetCode wxPython tutorial

In this example, we create an
about dialog box.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
'''

import wx
import wx.adv


class Example(wx.Frame):

    def __init__(self, *args, **kwargs):
        super(Example, self).__init__(*args, **kwargs)

        self.InitUI()

    def InitUI(self):

        menubar = wx.MenuBar()
        help = wx.Menu()
        help.Append(wx.ID_ANY, '&About')
        help.Bind(wx.EVT_MENU, self.OnAboutBox)

        menubar.Append(help, '&Help')
        self.SetMenuBar(menubar)

        self.SetSize((350, 250))
        self.SetTitle('About dialog box')
        self.Centre()

    def OnAboutBox(self, e):

        description = """File Hunter is an advanced file manager for
the Unix operating system. Features include powerful built-in editor,
advanced search capabilities, powerful batch renaming, file comparison,
extensive archive handling and more.
"""

        licence = """File Hunter is free software; you can redistribute
it and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation; either version 2 of the License,
or (at your option) any later version.

File Hunter is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU General Public License for more details. You should have
received a copy of the GNU General Public License along with File Hunter;
if not, write to the Free Software Foundation, Inc., 59 Temple Place,
Suite 330, Boston, MA  02111-1307  USA"""


        info = wx.adv.AboutDialogInfo()

        info.SetIcon(wx.Icon('hunter.png', wx.BITMAP_TYPE_PNG))
        info.SetName('File Hunter')
        info.SetVersion('1.0')
        info.SetDescription(description)
        info.SetCopyright('(C) 2007 - 2024 Jan Bodnar')
        info.SetWebSite('http://www.zetcode.com')
        info.SetLicence(licence)
        info.AddDeveloper('Jan Bodnar')
        info.AddDocWriter('Jan Bodnar')
        info.AddArtist('The Tango crew')
        info.AddTranslator('Jan Bodnar')

        wx.adv.AboutBox(info)


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

该示例有一个关于菜单项。选择项目后，将显示“关于”框。

```python
        description = """File Hunter is an advanced file manager for 
the Unix operating system. Features include powerful built-in editor, 
advanced search capabilities, powerful batch renaming, file comparison, 
extensive archive handling and more.
"""
```

在应用程序的代码中放入过多的文本不是最好的主意。我们不想让这个例子太复杂，所以我们把所有的文本都放进了代码中。但在现实世界中的程序中，文本应该单独放置在文件中。它帮助我们维护应用程序。例如，如果我们想将应用程序翻译成其他语言。

```python
info = wx.adv.AboutDialogInfo()
```

首先要做的是创建一个`wx.AboutDialogInfo`对象。构造函数为空。它不需要任何参数。

```python
info.SetIcon(wx.Icon('hunter.png', wx.BITMAP_TYPE_PNG))
info.SetName('File Hunter')
info.SetVersion('1.0')
info.SetDescription(description)
info.SetCopyright('(C) 2007  - 2020 Jan Bodnar')
info.SetCopyright('(C) 2007  - 2020 Jan Bodnar')
info.SetWebSite('http://www.zetcode.com')
info.SetLicence(licence)
info.AddDeveloper('Jan Bodnar')
info.AddDocWriter('Jan Bodnar')
info.AddArtist('The Tango crew')
info.AddTranslator('Jan Bodnar')
```

接下来要做的事情是对创建的`wx.AboutDialogInfo`对象调用所有必要的方法。

```python
wx.adv.AboutBox(info)
```

最后，我们创建了一个`wx.adv.AboutBox`小部件。它使用的唯一参数是`wx.adv.AboutDialogInfo`对象。

![关于对话框](/images/doc/wxpython/hunter.png)

## 自定义对话框

在下一个示例中，我们将创建一个自定义对话框。图像编辑应用程序可以更改图片的颜色深度。为了提供这种功能性，我们可以创建一个合适的对话框。

```python
#!/usr/bin/env python

'''
ZetCode wxPython tutorial

In this code example, we create a
custom dialog.

author: Jan Bodnar
website: www.zetcode.com
last modified: July 2020
'''

import wx

class ChangeDepthDialog(wx.Dialog):

    def __init__(self, *args, **kw):
        super(ChangeDepthDialog, self).__init__(*args, **kw)

        self.InitUI()
        self.SetSize((250, 200))
        self.SetTitle("Change Color Depth")


    def InitUI(self):

        pnl = wx.Panel(self)
        vbox = wx.BoxSizer(wx.VERTICAL)

        sb = wx.StaticBox(pnl, label='Colors')
        sbs = wx.StaticBoxSizer(sb, orient=wx.VERTICAL)
        sbs.Add(wx.RadioButton(pnl, label='256 Colors',
            style=wx.RB_GROUP))
        sbs.Add(wx.RadioButton(pnl, label='16 Colors'))
        sbs.Add(wx.RadioButton(pnl, label='2 Colors'))

        hbox1 = wx.BoxSizer(wx.HORIZONTAL)
        hbox1.Add(wx.RadioButton(pnl, label='Custom'))
        hbox1.Add(wx.TextCtrl(pnl), flag=wx.LEFT, border=5)
        sbs.Add(hbox1)

        pnl.SetSizer(sbs)

        hbox2 = wx.BoxSizer(wx.HORIZONTAL)
        okButton = wx.Button(self, label='Ok')
        closeButton = wx.Button(self, label='Close')
        hbox2.Add(okButton)
        hbox2.Add(closeButton, flag=wx.LEFT, border=5)

        vbox.Add(pnl, proportion=1,
            flag=wx.ALL|wx.EXPAND, border=5)
        vbox.Add(hbox2, flag=wx.ALIGN_CENTER|wx.TOP|wx.BOTTOM, border=10)

        self.SetSizer(vbox)

        okButton.Bind(wx.EVT_BUTTON, self.OnClose)
        closeButton.Bind(wx.EVT_BUTTON, self.OnClose)


    def OnClose(self, e):

        self.Destroy()


class Example(wx.Frame):

    def __init__(self, *args, **kw):
        super(Example, self).__init__(*args, **kw)

        self.InitUI()


    def InitUI(self):

        tb = self.CreateToolBar()
        tb.AddTool(toolId=wx.ID_ANY, label='', bitmap=wx.Bitmap('color.png'))

        tb.Realize()

        tb.Bind(wx.EVT_TOOL, self.OnChangeDepth)

        self.SetSize((350, 250))
        self.SetTitle('Custom dialog')
        self.Centre()

    def OnChangeDepth(self, e):

        cdDialog = ChangeDepthDialog(None,
            title='Change Color Depth')
        cdDialog.ShowModal()
        cdDialog.Destroy()


def main():

    app = wx.App()
    ex = Example(None)
    ex.Show()
    app.MainLoop()


if __name__ == '__main__':
    main()
```

在上面的示例中，我们创建了一个自定义对话框。

```python
class ChangeDepthDialog(wx.Dialog):
    
    def __init__(self, *args, **kw):
        super(ChangeDepthDialog, self).__init__(*args, **kw) 
```

在我们的代码示例中，我们创建了一个自定义的`ChangeDepthDialog`对话框。我们继承自一个`wx.Dialog`小部件。

```python
def OnChangeDepth(self, e):

    cdDialog = ChangeDepthDialog(None,
        title='Change Color Depth')
    cdDialog.ShowModal()
    cdDialog.Destroy()
```

我们实例化了一个`ChangeDepthDialog`类。然后我们调用`ShowModal()`方法。稍后，我们必须使用`Destroy()`销毁对话框。注意对话框和顶级窗口之间的视觉差异。下图中的对话框已被激活。在对话框被破坏之前，我们无法使用顶层窗口。窗口的标题栏有明显的区别。

![自定义对话框](/images/doc/wxpython//customdialog.png)

在本章中，我们介绍了对话框。