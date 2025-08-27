---
title: "Mono于FreeBSD上的试用（2）"
date: 2004-07-13 15:05:00
layout: post
categories: FreeBSD dotnet mono
tags: FreeBSD dotnet mono
---

家里买了一个宽带路由器，原来的代理服务器被我格了，配好宽带路由器上的虚拟服务器（NAT端口转发），咱们也来感觉一下在家托管。对了，还有动态域名。前两天看有人问[luyan](http://nluyan.vicp.net)，他的花生壳是怎么装到Linux上去的，有人估计是在Linux上装虚拟机了，咱们不那么搞，咱们找一个支持FreeBSD的免费动态域名就好。首先声明：我不是在做广告——我用的是[科迈](http://www.comexe.cn)的动态域名，感觉还不错，最关键的是免费而且支持FreeBSD。

言归正传：开始安装FreeBSD。

先说我的机器的配置，我的主板是QDI的工作站主板，694x芯片组，集成ATI RageMobile显卡，Intel百兆网卡，和一个双通道160兆的SCSI控制器。我装了一个PIII 766铜矿CPU，256Mb PC133内存，一个雅马哈724声卡，以及一块8139网卡。两块一盘，一块Seagate 18G SCSI硬盘，一块Seagate20G IDE硬盘。由于现在FreeBSD 5 的BootCD有问题，FreeBSD 5的光盘没办法在这个机器上启动，又没有软驱，所以选择装FreeBSD 4.10。

我把18G的SCSI硬盘作为主盘，20G的IDE硬盘作为/ftp挂点，准备将来提供FTP服务之用。我选择的是X+Developer安装，这样会把必要的编译工具和X都安装到机器上面，以便测试Windows App之用。我选的Windows Manager是KDE，没有装中文的环境，上中文的网站字体会比较乱，但是这还不是咱们的主要工作，所以忽略。第一次运行KDE的时候，会提示检测到有声卡（我单插的雅马哈724），但是没有驱动没办法工作，由于和前面同样的理由，也忽略。之后，可以安装cvsup,到cvsup.freebsdchina.org 去升级ports，这样安装操作系统的工作基本完成。

这个时候我们开始检查ports树，在/usr/ports/lang 下面可以找到mono这个目录，阅读里面的说明，可以得知这个ports还是仍然是为mono-0.97制作的。这样我们得自己编译mono-1.0，当然我们自己也可以制作ports，但是这个不是我们这篇文章的目的。mono的源码可以去他的[mono-project](http://www.mono-project.com)网站下载。在正式编译mono之前还要检查一下系统内的几个库是否安装了，比如bison，glib和icu2。由于我们安装了X，以及KDE，这样glib就已经装好了。安装其他的应用或库，可能会依赖bison，所以之前要检查ports记录，可以用pkg_list命令。安装这些可以用ports直接安装，如果你的机器在网上建议直接在ports所在的目录make install，除非没连到互联网的时候再用网站上编译好的packages。bsion、glib、icu2都在/usr/ports/devel目录。

icu是ibm的一个unicode处理的库，我以前也没接触过，仔细观察了它的编译过程，发现里面还带有各个国家和公司的不同字符编码码表，以及到unicode的映射关系表，以方便不同的编码作相互转换。FreeBSD的ports中带有两个icu，一个是icu，一个是icu2。我们使用icu2。icu2的安装需要自己下载源码，这可能是因为ibm的发布许可不允许第三方发布吧！[下载地址](ftp://www-126.ibm.com/pub/icu/2.8/icu-2.8.tgz)

这些mono依赖的部件都安装好之后，我们就可以开始编译了。解压生成mono-1.0这个目录。进入这个目录，根据文档得知，直接使用./configure就可以将代码进行编译前的配置。我们也可以使用./configure -h来查看这个脚本可以带的参数，也可以检查configure默认的设置，其中prefix是默认的安装目录。我们看到prefix的默认值是/usr/local，这个目录正好是FreeBSD里面ports安装的默认路径，所以我们不需要做什么修改，直接使用./configure。在这个脚本结束之后，会显示配置的结果。主要内容好像是虚拟机在单进程内执行，支持JIT，多语言支持使用的是icu2.8。

之后可以直接make，若干分钟以后（我的机器大约是半个小时不到），就可以编译成功。比自己编译JDK快多了。之后可以make check验证一下编译结果，也可以直接make install。我的make install在最后一个生成MONO_PATH的时候停住了，我睡了一觉早上看还是停在那里没有动，估计是有什么问题，早上上班没时间管，晚上再看看吧！

（持续）