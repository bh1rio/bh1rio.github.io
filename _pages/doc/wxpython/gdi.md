---
layout: framework
title: wxPython图形
permalink: /doc/wxpython/gdi.html
---

# wxPython图形

GDI（图形设备接口）是用于处理图形的接口。它用于与显示器、打印机或文件等图形设备进行交互。GDI允许程序员在屏幕或打印机上显示数据，而不必关心特定设备的细节。GDI将程序员与硬件隔离开来。

从程序员的角度来看，GDI是一组用于处理图形的类和方法。GDI由2D矢量图形、字体和图像组成。

![GDI结构](/images/doc/wxpython/gdi2.png)

要开始绘制图形，我们必须创建一个设备上下文（DC）对象。在wxPython中，设备上下文被称为wx。DC。文档定义了wx。DC作为设备上下文，可以在其上绘制图形和文本。它以通用的方式表示设备的数量。同一段代码可以写入不同类型的设备。无论是屏幕还是打印机。wx。DC不打算直接使用。相反，程序员应该选择一个派生类。每个派生类都打算在特定条件下使用。

## 派生`wx.DC`等级

* wxBufferedDC
* wxBufferedPaintDC
* wxPostScriptDC
* wxMemoryDC
* wxPrinterDC
* wxScreenDC
* wxClientDC
* wxPaintDC
* wxWindowDC

wx.ScreenDC用于在屏幕上的任何位置绘制。wx。如果我们想在整个窗口上绘制，则使用WindowDC（仅限Windows）。这包括窗户装饰。wx.ClientDC用于绘制窗口的客户端区域。客户端区域是没有装饰（标题和边框）的窗口区域。wx。PaintDC也用于在客户端区域绘制。但wx之间有一个区别。PaintDC和wx。ClientDC。wx。PaintDC只能从wx中使用。PaintEvent。wx。不应从wx使用ClientDC。PaintEvent。wx。MemoryDC用于在位图上绘制图形。wx。PostScriptDC用于在任何平台上写入PostScript文件。wx。PrinterDC用于访问打印机（仅限Windows）。