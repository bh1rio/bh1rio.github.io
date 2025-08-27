---
title: "SharePoint Portal Administration异常事件的处理"
date: 2005-11-03 15:44:00
layout: post
categories: SharePoint
tags: SharePoint
---

一次SharePoint Portal Administration异常事件的处理的过程。

* 场景：

  单服务器，独立的SQL Server。服务器在安装SPS前安装了Win2003的SP1。每次启动的时候会提示一个服务启动不正常，察看系统事件中有两个错误，发现来源于SharePoint Portal Administration服务。实践内容如下：

  1. 等待 SharePoint Portal Administration 服务的连接超时(30000 毫秒)。
  2. 由于下列错误，SharePoint Portal Administration 服务启动失败:服务没有及时响应启动或控制请求。

* 原因分析：

  由于系统安装了Win2003的SP1，怀疑原因是因为安装了这个SP1。故观察了SPS相关的几个服务的可执行文件路径，这几个服务的可执行文件路径都在引号内，和引起SSO服务异常的情景一样，故决定修改注册表，试验一下。

* 具体步骤：

  打开注册表编辑器，定位到\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\。
  下面是SPS服务对应的文件夹的名称：
  * SharePoint Timer Service: SPTimer
  * SharePoint Portal Administration: SPSAdmin
  * Microsoft SharePointPS Search: SharePointPSSearch
  * SharePoint Portal Alert: spsalert
  * Microsoft Single Sign-on Service: ssosrv

  在对应的文件夹下面有一个ImagePath节点，双击打开节点，去掉节点值两端的引号。
重新启动服务器，一切正常。

> 说明：
>
> 由于以上的方法纯属实践得来，没有在各种服务器场环境上进行测试，所以本人不为任何的实验行为带来的后果负责。实验前请做备份。