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

####Qt

Qt 是一个运行库。因为太阳神三国杀（以下简称为神杀）使用了 Qt 框架，所以需要下载相应的 Qt 运行库来配置开发环境。
本文档使用 Qt5.4.0 的 Library 。
对于下载地址，需要根据你的编译器版本来选择，这里暂不放出。

####SWIG

SWIG 用于处理 Lua 的接口，是一个非常重要的工具。
本文档使用 SWIG 的 3.0.2 版本。
下载地址：http://sourceforge.net/projects/swig/files/swigwin/ （3.0.2版本）

###处理源码

你可以选择上面源码地址中的一个进行下载。打开连接后，在网页的右边又一个 Download Zip 的按钮，点击一下，源码就会以Zip的压缩文件的形式下载下来。
**明显强调：这不是单一的下载源码的方法，你也可以使用git Extensions来下载源码。相对于 Download Zip而言，使用git可以随时检查源码的更新状态。[点击进入]({{ site.url }}/git-extensions-tutorial)git Extensions的使用方法介绍页。**
下载完源码之后，解压开，（如果你使用git Extensions就不必解压）你会得到这样的一个文件夹：（以国战为例）

![]({{ site.url }}/images/hegemony.png)

####Windows 或 Android

打开之，然后在里面创建一个tools文件夹，然后把你下载的swig解压开，将文件放进去，经过适当的改名之后，要确保 tools\swig\swig.exe存在：

![]({{ site.url }}/images/path.png)

这个目录下，确保图示文件在正确的位置

![]({{ site.url }}/images/swig.png)

####OS X 或 Linux

打开一个终端在swig的解压目录，然后输入这样的几条命令：

{% highlight shell %}
./configure --without-pcre
   make
   sudo make install
{% endhighlight %}

至此，编译前的准备工作完成。

##开始编译

###明确编译目标平台

由于 Qt 的跨平台特性，我们需要选择目标平台，目测有这样几种平台可供我们选择：

####桌面平台

*Windows
*OS X
*Linux

