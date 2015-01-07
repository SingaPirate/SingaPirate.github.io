---
layout: post
title: 太阳神三国杀构建指南
description: "构建指南"
tags: [项目文档]
image:
  background: triangular.png
  feature: abstract-4.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

#构建指南

##构建前的准备工作

###GPL 协议

太阳神三国杀是一个遵循 GPLv3 协议的开源项目，在编译和使用时应当完全遵守 GPLv3 协议。
具体地，可以参考源码目录下的 LICENSE 文件，以获得更多有关 GPLv3 的信息。
对于因违反协议而引发的法律问题，Mogara 开发组（以下简称开发组）不承担任何责任，所以请在阅读本文档之前认真阅读 GPLv3 协议。

###你的身份

如果你是一名开发者，请留意本文档中**明显强调**的内容，这些内容将有助于你对整个过程的理解，同时，这些内容也会给你提供一些更加高级的信息。（将有利于你的代码工作）
如果你是一名玩家，你也可以留意这些内容。

###源码地址

目前的源码地址有这样几个：
太阳神三国杀-主线项目：https://github.com/MogaraOrg/QSanguosha （目前正处于开发状态）
太阳神三国杀-国战项目：https://github.com/MogaraOrg/QSanguosha-For-Hegemony
你可以任选一个进行编译，当然，我们建议你选择国战，因为主线还没有彻底完成。
注意，这些网站都是外国网站，有时候会非常慢。

###构建工具

####编译器

目前，以 Windows 为例，我们可以用这样两种编译器可供选择：

*MinGW

这种编译器环境配置简单，适合非开发者使用。
这种编译器包含在 Qt 的安装包里。

*MSVC

所谓的 MSVC 就是微软的 Visual Studio 所提供的编译器，你可以使用 VS2010 或者 VS2013 进行编译。
