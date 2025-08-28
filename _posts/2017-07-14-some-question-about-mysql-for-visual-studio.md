---
layout: post
title: 使用MySQL for Visual Studio创建EF模型的注意事项
date: 2017-07-14 07:23:28
categories: dotnet MySQL VisualStudio
tags: MySQL VisualStudio
---

几个注意事项。

1. 安装的MySQL for Visual Studio之前需要先安装MySQL的Connector/NET
2. Connector/NET和MySQL for Visual Studio建议都安装release的版本。
3. 在项目中创建MySQL的EF模型前，项目里面需要先用Nuget安装MySQL.Data.Entity，同样建议安装release版本。
4. 更新EnityFramework到最新的版本。

因为：

* 如果没有按照1、2和3的顺序来做的话，会出现创建连接的时候没有mysql的驱动。
* 不都是用统一的release版本的话，可能在创建完成数据连接以后，选择表之前，窗口闪退。闪退的情况在Visual Studio 2015和2017中都会发生。互联网上还有2013同类问题的报告。
* EntityFramework不升级到最新版的话，会有提示问题你是否生产EF5的实体模型……
