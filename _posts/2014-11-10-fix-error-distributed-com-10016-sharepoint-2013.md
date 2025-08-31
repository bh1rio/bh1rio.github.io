---
layout: post
title: SharePoint 2013上的DistributedCOM的10016错误解决
date: 2014-11-10 02:52:34
categories: 技术
tags: SharePoint
---

CLSID{61738644-F196-11D0-9953-00C04FD919C1}很容搜索到，这个是IIS WAMREG admin Service组件。在管理工具的组件服务里面可以找到这个组件，但是无法编辑这个组件。

![](/images/2014/11/image.png)

翻墙google一下，这个问题貌似很多年了，解决办法也简单，在注册表编辑器里面搜索这个CLSID，能搜索到注册表项文件夹，直接在左侧选中文件夹，右键菜单选择选择权限。在权限窗口里面直接点击高级，然后在高级安全设置里面修改所有者。默认的所有者为TrustedInstaller，修改为Domain Admins。

![](/images/2014/11/image1.png)

修改完以后看看Domian Admins的权限有没有开成完全控制，如果开到完全控制，就可以保存退出了。再回到组件服务里面，那个组件就可以编辑激活权限了。
