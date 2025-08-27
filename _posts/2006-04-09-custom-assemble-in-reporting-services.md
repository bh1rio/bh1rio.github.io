---
layout: post
title: 在报表服务当中使用定制程序集
date: 2006-04-09 15:05:00
categories: SQLServer
tags: ReportingServices SQLServer
---
报表服务允许在报表当中内嵌代码，也允许报表引用定制的程序集。内嵌代码要求是VB.NET编写的代码，而引用的定制程序集没有限制，在codeproject上面甚至看到有人调用包装了COM的定制程序集。

本文的注意力不在内嵌代码上，因为内嵌代码相对引用定制程序集简单，功能也要弱一些。我们的注意力着重在报表如何引用定制程序集，以及这样的报表如何部署。

### 在报表中如何引用定制程序集

![RSAddition1](/images/2010/08/RSAddition1.jpg)

在报表的数据或者布局视图点击“报表”菜单->“报表属性”项会出现如下的窗口：

![RSAddition2](/images/2010/08/RSAddition2.jpg)

在点击“...”按键选择要应用的程序集。如果使用对象的静态成员，可以应用以后直接使用。如果对象需要实例化以后才能使用，则需要在窗口下半部分的添加类名和准备使用的实例名。静态成员可以直接以`myNameSpace.myClass.myFunction()`的方式来执行，如果不是静态成员，则要以`Code.myObject.myFunction()`方式来执行。其中myClass是类名，myObject是实例化以后的实例名。

### 部署引用的定制程序集

部署应用的定制程序集有三个步骤：

  1. 将引用的dll添加到报表设计器和报表服务器的bin目录，具体来讲就是报表设计器的`C:\Program Files\Microsoft SQL Server\80\Tools\Report Designer`和报表服务器的`C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin`。
  2. 编辑`C:\Program Files\Microsoft SQL Server\80\Tools\Report Designer`目录下的`rspreviewpolicy.config`文件和`C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer`目录下的`rssrvpolicy.config`文件。在`<CodeGroup>`节点下添加相应的`<CodeGroup>节点：  

```xml
<CodeGroup class="UnionCodeGroup"  
  version="1"  
  PermissionSetName="FullTrust"  
  Name="MyCodeGroup"  
  Description="Code group for my data processing extension">  
  <IMembershipCondition class="UrlMembershipCondition"  
    version="1"  
    Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\RSAddition.dll"  
  />
```
  3. 编辑`C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer`下的`web.config`文件。修改`<system.web>`节点内的`<trust>`节点为`<trust level="Full" originUrl="" />`。

此方法适用于SQL Server 2000 Reporting Service SP2和SQL Server 2005 Reporting Service。但是不适用于没有安装过ServicePack的SQL Server 2000 Reporting Service。

### 在报表当中使用引用的定制程序集

#### 在数据视图中使用

数据视图当中的对象主要是`DataSet`。要如何在DataSet当中使用应用的定制程序集呢？首先我们可以在`DataSet`当中使用参数，这个参数不是报表参数而是`DataSet`参数，之后我们在`DataSet`属性的参数页当中设置参数调用应用的定制程序集。

![RSAddition3](/images/2010/08/RSAddition3.jpg)

#### 在设计视图中使用

在设计视图中使用相对比较简单，我们只需要在相应的表达始终按照“**在报表中如何引用定制程序集** ”一节中说明的使用方法就可以了。
