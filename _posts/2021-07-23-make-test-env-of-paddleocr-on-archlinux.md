---
layout: post
title: 关于Archlinux下搭建百度PaddleOCR的测试环境
date: 2021-07-23 10:02:10 
categories: Linux
tags: Archlinux OCR python
---

[原文](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.1/doc/doc_ch/installation.md)推荐使用Dockers镜像，但是我觉得没意思，于是在虚机里面找了一个干净的Archlinux来搞，需要提前给arch里面安装：base-devel，python，python-pip，cython，wget，libglvnd。

在第2步安装PaddlePaddle的时候，如果提示版本找不到的话，可以考虑去掉版本，安装最新版。

在第3步从github获取PaddleOCR的代码，在github连不上的时候，可以改用gitee，延迟几天无所谓，反正同步过来的应该都是可用版。

在第4步安装requirements.txt的时候，建议加上 -i https://mirror.baidu.com/pypi/simple 。百度的这个pypi的镜像网站，比清华的那个快，而且稳定。另外，建议加上环境变量MAKEFLAGS开启make的多job支持，在安装scikit-image的时候，还需要编译一些内容，不开多job支持，还是挺慢的。

使用[快速使用文档](https://github.com/PaddlePaddle/PaddleOCR/blob/release/2.1/doc/doc_ch/quickstart.md)中的命令行，测试通过。
