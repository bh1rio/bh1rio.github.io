---
title: "Mono于FreeBSD上的试用（5）"
date: 2004-11-15 15:33:00
layout: post
categories: FreeBSD dotnet mono
tags: FreeBSD dotnet mono
---

FreeBSD 5.3发布了，可以在新的平台上测试mono了。于是就把原来的文章续出来了一个（5）。

这次让我比较兴奋前面都成功了。mono通过ports就可以编译，xsp也可以编译了。
只不过需要gmake替代make就可以了。

```bash
./configure –prefix=/usr
gmake
gmake install
```

测试静态页面还是没有问题的。
但是测试它的名为test的ASP.NET应用就出了问题。前一段时间听说是因为线程库的问题，看来是真的了。

```bash
fd53# mono /usr/local/bin/xsp.exe –port 80
Adding applications ‘/:.’…
Registering application:
Host: any
Port: any
Virtual path: /
Physical path: /root/xsp-1.0
Listening on port: 80
Listening on address: 0.0.0.0
Root directory: /root/xsp-1.0
Hit Return to stop the server.
Segmentation fault (core dumped)
Nov 15 15:17:57 fd53 kernel: pid 44678 (mono), uid 0: exited on signal 11 (core dumped)
Nov 15 15:24:33 fd53 kernel: pid 44701 (mono), uid 0: exited on signal 11 (core dumped)
Unhandled Exception: System.IO.FileNotFoundException: Could not find file "[Unkown]" in <0x00076> System.IO.FileStream:WriteInternal (byte[],int,int)
in <0x00073> (wrapper remoting-invoke-with-check)System.IO.FileStream:WriteIntrnal (byte[],int,int)
in <0x00198> System.IO.FileStream:Write (byte[],int,int)
in <0x0006c> System.IO.StreamWriter:FlushBytes ()
in <0x0004f> (wrapper remoting-invoke-with-check) System.IO.StreamWriter:FlushB
tes ()
in <0x00055> System.IO.StreamWriter:Flush ()
in <0x00088> System.IO.StreamWriter:Write(string)
in <0x00032> System.IO.SynchronizedWriter:Write (string)
in <0x00012> System.Console:Write (string)
in <0x0004c> Mono.CSharp.Driver:Main (string[])
```