---
layout: post
title: 太阳神三国杀构建指南
description: "构建指南"
tags: [项目文档]
image:
  background: triangular.jpg
  feature: abstract-4.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
author: 数字
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
太阳神三国杀-新框架：[https://github.com/Mogara/QSanguosha](https://github.com/Mogara/QSanguosha) （目前正处于开发状态）  
太阳神三国杀-国战：[https://github.com/Mogara/QSanguosha-For-Hegemony](https://github.com/Mogara/QSanguosha-For-Hegemony)  
太阳神三国杀-V2：[https://github.com/Mogara/QSanguosha-v2](https://github.com/Mogara/QSanguosha-v2)  
你可以任选一个进行编译，当然，我们建议你选择国战和V2，因为新框架还没有完成。  
注意，这些网站都是外国网站，有时候会非常慢。  
大家可以在国内的镜像网站下Clone，如果镜像不全，也可以从Github上pull更新。  
太阳神三国杀-新框架（国内镜像）：[https://git.oschina.net/Fsu0413/QSanguosha](https://git.oschina.net/Fsu0413/QSanguosha)  
太阳神三国杀-国战（国内镜像）：[https://git.oschina.net/Fsu0413/QSanguosha-For-Hegemony](https://git.oschina.net/Fsu0413/QSanguosha-For-Hegemony)  
太阳神三国杀-V2（国内镜像）:[https://git.oschina.net/Fsu0413/QSanguosha-v2](https://git.oschina.net/Fsu0413/QSanguosha-v2)  
  
###构建工具

####编译器

目前，以 Windows 为例，我们可以用这样两种编译器可供选择：

* MinGW

这种编译器环境配置简单，适合非开发者使用。  
这种编译器包含在 Qt 的安装包里。

* MSVC

所谓的 MSVC 就是微软的 Visual Studio 所提供的编译器，你可以使用 VS2010 或者 VS2013 进行编译。

####Qt

Qt 是一个运行库。因为太阳神三国杀（以下简称为神杀）使用了 Qt 框架，所以需要下载相应的 Qt 运行库来配置开发环境。  
本文档使用 Qt5.4.0 的 Library 。  
对于下载地址，需要根据你的编译器版本来选择，这里暂不放出。 

####SWIG

SWIG 用于处理 Lua 的接口，是一个非常重要的工具。  
本文档使用 SWIG 的 3.0.2 版本。  
下载地址：[http://sourceforge.net/projects/swig/files/swigwin/](http://sourceforge.net/projects/swig/files/swigwin/) （3.0.2版本）

###处理源码

你可以选择上面源码地址中的一个进行下载。打开连接后，在网页的右边又一个 Download Zip 的按钮，点击一下，源码就会以Zip的压缩文件的形式下载下来。  
**明显强调：这不是单一的下载源码的方法，你也可以使用git Extensions来下载源码。相对于 Download Zip而言，使用git可以随时检查源码的更新状态。[（git Extensions的使用方法介绍页）]({{ site.url }}/git-extensions-tutorial)git Extensions的使用方法介绍页。**  
下载完源码之后，解压开，（如果你使用git Extensions就不必解压）你会得到这样的一个文件夹：（以国战为例）

![]({{ site.url }}/images/hegemony.jpg)

####Windows 或 Android

打开之，然后在里面创建一个 tools 文件夹，然后把你下载的 swig 解压开，将文件放进去，经过适当的改名之后，要确保 tools\swig\swig.exe 存在：

![]({{ site.url }}/images/path.jpg)

这个目录下，确保图示文件在正确的位置

![]({{ site.url }}/images/swig.jpg)

####OS X 或 Linux

打开一个终端在 swig 的解压目录，然后输入这样的几条命令：

./configure --without-pcre  
   make  
   sudo make install 

至此，编译前的准备工作完成。 

##开始编译

###明确编译目标平台

由于 Qt 的跨平台特性，我们需要选择目标平台，目测有这样几种平台可供我们选择：

####桌面平台

* Windows
* OS X
* Linux

####移动平台

* Android （开发中）
* iOS （需要开发者帐号）
* Window8 RT  （处于调试阶段）
* Windows Phone （处于调试阶段）

选择好你需要的平台，我们开始行动。

###下载 Qt 库

选择好平台后，我们需要下载Qt。  
Qt官方下载页面：[http://www.qt.io/download-open-source/](http://www.qt.io/download-open-source/)

![]({{ site.url }}/images/downloads.jpg)

打开 View All Downloads：  
然后根据你的平台选择响应的安装包。比如说如果你是 Win64+VS2013，则应该选择

![]({{ site.url }}/images/win64vs13.jpg)

这两个中的一个，其余的以此类推。  
注意：  
1.如果你希望同时编译 Windows 和 Android 版本，你应该选择 Android 版本，

![]({{ site.url }}/images/android.jpg)

这种情况同时也发生在 OS X 和 iOS（或者Android或者二者都有）

![]({{ site.url }}/images/osx.jpg)

以及 Linux 和 Android 上。

![]({{ site.url }}/images/linux-android.jpg)

**2.如果你使用的是 MSVC 类的编译器并且你是一位开发者，还需要下载下面的 QtVSAddIn 的插件。**

![]({{ site.url }}/images/addin.jpg)

###构建

对于不同的平台，我们有不同的编译说明。你可以选择适合你的平台的教程。

####Windows 平台

如果你的开发平台是 Windows 并且你的目标平台是 Windows 或者 Android ，你可以按照你的编译器类型来选择教程。

- MinGW 编译器类 

这类教程是使用 MinGW 作为编译器的教程，在 Windows 平台来说，也就是非 MSVC 编译器……

	1. 安装Qt

运行你下载的 QtLibrary 的安装文件，这里我们以 Android 为例：

![]({{ site.url }}/images/x86android.jpg)

运行之，应该会有这样的界面：

![]({{ site.url }}/images/setup1.jpg)

然后下一步：

![]({{ site.url }}/images/setup2.jpg)

这里的安装目录你可以改一改，因为放在C盘实在是太坑爹了……  
选好目录后，点下一步：

![]({{ site.url }}/images/setup3.jpg)

对于只想编译 Windows 版的可以直接点下一步。  
而对于 Android 版的来说，则需要稍微配置一下，点开 Qt5.4 这一项前面的小三角：

![]({{ site.url }}/images/setup4.jpg)

首先，![]({{ site.url }}/images/setup5.jpg) 这一项是必要的。而

![]({{ site.url }}/images/setup6.jpg)

这三项，则需要根据你的 Android 设备的 CPU 型号来决定了。具体地，你可以到网络上查询你的 Android 设备的型号，再查询其 CPU 型号，看看相关的信息。  
最后一项 Source Components 是源码，可以不装。当然，装了基本没用……  
选择好了以后，你就可以下一步了。

![]({{ site.url }}/images/setup7.jpg)

这个也就不用说了，当然得同意吧，然后下一步：

![]({{ site.url }}/images/setup8.jpg)

下一步……

![]({{ site.url }}/images/setup9.jpg)

然后你就可以点安装了。  
在安装完之后，有一个运行 QtCreator 的选项，建议先将其去掉……然后退出安装程序即可。

	2. 安装Android SDK   Android NDK   JDK   Ant等

这4个东西都是编译Android平台所需要的。  
下载下来后请将其解压到一个位置。  
Android SDK ：[http://wear.techbrood.com/sdk/index.html](http://wear.techbrood.com/sdk/index.html)  
打开后先点击VIEW ALL DOWNLOADS AND SIZES，然后再选择与你匹配的版本。  
Android NDK ：[http://wear.techbrood.com/tools/sdk/ndk/index.html](http://wear.techbrood.com/tools/sdk/ndk/index.html)  
直接选择与你匹配版本即可。  
JDK:[http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)  
首先要点击许可协议：（选择左边的那个） 

![]({{ site.url }}/images/setup10.jpg)

然后直接选择与你匹配版本即可。  
Ant：[http://mirrors.hust.edu.cn/apache//ant/binaries/apache-ant-1.9.4-bin.zip](http://mirrors.hust.edu.cn/apache//ant/binaries/apache-ant-1.9.4-bin.zip)  
下载后解压即可。  
接下来需要配置 QtCreator 。  
运行 QtCreator ，打开工具→选项→Android：

![]({{ site.url }}/images/setup11.jpg)

这里是已经配置好了的，点击浏览，参照上图选择文件夹……（这里的Android SDK放在D:\Android_Deployment\Android_SDK文件夹，NDK放在D:\Android_Deployment\Android_NDK 文件夹）  
配置完成后，点击下面的OK，然后关掉QtCreator。 

	3. SWIG小插曲

在确保正确配置 SWIG 的情况下，打开swig文件夹，运行其目录下的cxx-creator批处理。  
在运行完成之后，你应该会看到目录下多了一个sanguosha_wrap.cxx文件，代表这一步完成了。

	4. 运行 QtCreator

打开源码目录下的 QSanguosha.pro 文件：

![]({{ site.url }}/images/setup12.jpg)

打开后 QtCreator 会提示你配置项目：

![]({{ site.url }}/images/setup13.jpg)

选择你需要的编译目标。第一个电脑形状的就是 Windows 平台的，其他的是 Android 平台。（你可能没有这么多的选项，当然，选择你需要的就行了……）  
在配置完成后，会出现这样的界面：

![]({{ site.url }}/images/setup14.jpg)

接下来，对于Windows和Android的不同平台，我们要分开叙述了……

#####部署在Windows平台

调整左下脚![]({{ site.url }}/images/setup15.jpg)上方的那个电脑或者安卓按钮，将其调整为电脑的 Release 状态：

![]({{ site.url }}/images/setup16.jpg)

然后等QtCreator分析一会，就可以点那个锤子![]({{ site.url }}/images/setup17.jpg)了，然后它就会自己编译。  
正常情况下编译是不会有错误的，如果有错误，请及时到项目主页反馈给开发组。

等它编译完之后，转到生成目录：  
Tips：如果你不知道生成目录，你可以点击QtCreator左边的项目，点构建和运行，应该是个这样的界面：

![]({{ site.url }}/images/setup18.jpg)

然后你就看到构建目录了。  
打开构建目录下的 Release 文件夹，从里面找到 QSanguosha.exe，然后把其复制到源码目录下。  
先不要着急运行，从你的Qt安装目录下5.4\ mingw491_32（或者64？）\bin下找出下列几个 dll 复制到源码目录：
 
* icudt53.dll
* icuin53.dll
* icuuc53.dll
* libgcc_s_dw2-1.dl
* libstdc++-6.dll
* libwinpthread-1.dll
* Qt5Core.dll
* Qt5Declarative.dll
* Qt5Gui.dll
* Qt5Network.dll
* Qt5Script.dll
* Qt5Sql.dll
* Qt5Widgets.dll
* Qt5XmlPatterns.dll

然后双击运行游戏。（如果还提示缺少 dll 的话继续在 bin 目录下找就可以了）

![]({{ site.url }}/images/setup19.jpg)

至此，编译过程完成了。

当然，如果一直玩英文版的肯定是不爽啊，我们需要用 Qt 来生成翻译文件。  
点击上面的工具→外部→Qt语言家→发布翻译：

![]({{ site.url }}/images/setup20.jpg)

然后翻译文件 sanguosha.qm 就在源码目录下 build 文件夹里生成了，将其复制到源码目录即可。   
至此，Windows 平台编译过程结束。

#####部署在Android平台：

调整左下脚![]({{ site.url }}/images/setup15.jpg)上方的那个电脑或者安卓按钮，将其调整为安卓的 Release 状态：

![]({{ site.url }}/images/setup21.jpg)

然后等QtCreator分析一会，就可以点那个锤子![]({{ site.url }}/images/setup17.jpg)了，然后它就会自己编译。

正常情况下编译是不会有错误的，如果有错误，请及时到项目主页反馈给开发组。  
在它编译完成后，转到生成目录下的 android-build\bin 文件夹，找到里面的 QtApp-debug.apk ，将其安装到你的Android设备上。  
图省略（……）  
然后将下面几个文件夹复制到你的 Android 设备的 SD 卡或者内存（即你安装的位置）下的 /Android/data/org.qsgsrara.qsanguosha 目录： 

* ai-selector
* audio
* diy
* font
* hero-skin
* image
* lang
* lua
* rule
* skins
* style-sheet
* ui-script

如果需要的话，你可以生成翻译文件，并将 sanguosha.qm 和源码目录下的 qt_zh_CN.qm 文件一起复制到刚才的目录。

至此，Android 平台的编译过程告一段落。

- MSVC类

首先，确保你的 VS2010 或者 VS2013 不是所谓的体验版的（Express），否则无法进行正常的编译。

**注意：使用 MSVC 无法生成 Android 平台的 apk 文件。如果实在需要的话，请参考上面有关 Android 平台的配置过程。**

你可以选择用 QtCreator 来作为编辑器，当然，如果你有自信，你也可以使用 VS 自带的编辑器。对于 QtCreator 作为编辑器的来说，你可以参考上一章的正式的编译过程。我们这里重点介绍使用 VS 自带的编辑器的编译过程。

	1. 安装Qt

安装Qt的过程基本和使用MinGW的过程类似，你可以参考其相关章节。

	2. 安装QtVSAddIn

使用 VS 的编辑器必须要安装 Qt 的 VSAddIn，这里我们截取了《用 VS2010 来编译 QsgsV2》的部分内容来补充说明。

下载完成后，你应该会看到这样的文件。（其实，相应的版本应该不是这个，这个是为 Qt4 服务的，所以就将就着看吧……）

![]({{ site.url }}/images/setup22.jpg)

打开它，  
（解压数据的部分略过）

![]({{ site.url }}/images/setup23.jpg)

还是老套路，Next

![]({{ site.url }}/images/setup24.jpg)

还是老套路同意并Next

![]({{ site.url }}/images/setup25.jpg)

对于这一步，鸟语不好的人可以直接Next了（比如笔者）

![]({{ site.url }}/images/setup26.jpg)

安装目录？还是老话，找个瞅着顺眼的地方装

![]({{ site.url }}/images/setup27.jpg)

然后就可以点 Install 了  
安装步骤，点 Show details 可以显示详情。

![]({{ site.url }}/images/setup28.jpg)

这个过程比较短……

![]({{ site.url }}/images/setup29.jpg)

安装完了，点Next

![]({{ site.url }}/images/setup30.jpg)

然后Finish就行了。

	3. 开始编译（这里以VS2010为例）

打开 builds 目录，根据你的 VS 版本打开相应的文件夹，（比如说是 VS2010 ，那就打开 VS2010 的文件夹……）然后打开里面的 Qsanguosha.sln……

![]({{ site.url }}/images/setup31.jpg)这是VS2010的，当然VS2013应该也差不多……

打开后，把上方的生成方案由![]({{ site.url }}/images/setup32.jpg)转换为![]({{ site.url }}/images/setup33.jpg)  
然后就可以直接 Ctrl+Shift+B 编译了。

![]({{ site.url }}/images/setup34.jpg)

在编译过程中应该是不会出现问题的。如果出现了 Qt 库没有找到的问题，请检查 QT5→QtOptions 中 Qt 的目录设置。在编译完成后：

![]({{ site.url }}/images/setup35.jpg)

打开源码目录下的 Bin 文件夹，将生成的 QSanguosha.exe 复制到源码目录下。  
别着急运行，我们还需要复制这样几个 dll：（从 Qt 的安装目录下 5.4/msvc**/bin 中） 

* icudt53.dll
* icuin53.dll
* icuuc53.dll
* Qt5Core.dll
* Qt5Declarative.dll
* Qt5Gui.dll
* Qt5Network.dll
* Qt5Script.dll
* Qt5Sql.dll
* Qt5Widgets.dll
* Qt5XmlPatterns.dll

如果你用的是VS2010，则需要复制这两个文件： 

* msvcp100.dll
* msvcr100.dll

如果是VS2013，则： 

* msvcp120.dll
* msvcr120.dll

然后就可以运行了。如果提示缺少什么文件的话，继续到刚才的目录里面找……

找到最上面的 QT5 的菜单，点击 Launch Linguist：

![]({{ site.url }}/images/setup36.jpg)

应该会弹出一个 Qt 语言家，然后点击文件→打开……

![]({{ site.url }}/images/setup37.jpg)

打开源码目录下的 builds 文件夹里面的 sanguosha.ts 文件：  
然后点击文件→发布。于是翻译文件 sanguosha.qm 就在 builds 文件夹里生成了。请将其复制到源码目录下。  
然后你就可以开始游戏了。

####Linux平台

####OS X平台

	（这部分文档等待更新）

