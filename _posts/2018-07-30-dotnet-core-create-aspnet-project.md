---
layout: post
title: dotnet core点滴:创建asp.net core项目
date: 2018-07-30 09:56:22
categories: dotnet
tags: dotnet
---

1. `dotnet new webapp –o aspnetcoreapp`

新建webapp类型的项目到aspnetcoreaspp文件夹

2. `cd aspnetcoreapp`

3. `dotnet dev-certs https –trust`

为项目创建https的证书，并信任这个证书

4. `dotnet run`

5. 浏览 https://localhost:5001
