---
layout: post
title: 太阳神三国杀 Mac 版构建指南
description: "构建指南"
tags: [项目文档]
image:
  background: triangular.jpg
  feature: abstract-6.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
author: SE
---
## 构建指南

###写在前面
如果您使用的是一台苹果机，那么您可以忽视这一段文字。  
如果您希望使用一台 Windows 系统的设备编译 OS X 或 iOS 平台下的太阳神三国杀，你可以使用 VMWare 为您的电脑添加一台虚拟机。相关介绍请参考[超详细 VMware Workstation 10 安装 Mac OS X Mavericks](http://wenku.baidu.com/view/0279abe008a1284ac85043d0.html)。

###Mac os X 平台

开始构建前，请尽量保证您的系统不低于 OS X 10.8 Mountain Lion. 您可以在 App Store 中免费升级您的系统。

#####安装 XCode

首先您需要在您的 OS X 系统上安装 XCode。XCode 是苹果公司向开发人员提供的集成开发环境，用于开发 Mac OS X 和 iOS 的应用程序。凭借您的苹果账号，您可以在您系统自带的 App Store 中免费下载。

![](http://i.imgur.com/sPR6Sym.png)

您未曾安装过的话，这里的 open 应该为 get。下载后 XCode 就会出现在您的 LaunchPad 中。
![](http://i.imgur.com/vZhfmYe.jpg)

#####安装Qt
请您到[Qt project 的官方网站下载页面](http://www.qt.io/download/)下载最新版本的 Qt。这里您可以选择完全免费的 Community 版本。下载后，整个安装过程十分简单。

![](http://i.imgur.com/DN4lAe3.jpg)

#####获取源代码
请您从[源码地址](https://github.com/Mogara/QSanguosha)获得最新版本的源代码。您可以使用 git 工具（推荐完全免费的[SourceTree](http://www.sourcetreeapp.com)）。如果您不懂得如何使用 git，您可以直接点击源代码页面右侧的[Clone in Desktop](github-windows://openRepo/https://github.com/Mogara/QSanguosha)或[Download ZIP](https://github.com/Mogara/QSanguosha/archive/master.zip)以获得源代码。当您下载完毕后，请您将其解压到您喜欢的目录。

#####安装swig
您需要下载和安装[swig](http://sourceforge.net/projects/swig/files/swig/)。![](http://i.imgur.com/l96YFxH.png)  
点击一个新版本的文件夹进入后，请确保您下载的版本不低于 3.0.2.您只需下载后缀为 .tar.gz 的文件。  
![](http://i.imgur.com/NzsLtME.jpg)  
下载完成后，解压缩这个压缩包。打开您的terminal，依次输入    
./configure --without-pcre  
make  
sudo make install  
  
如果您看到一大长串，且没有出现error提示，说明您的安装成功了。然后您需要依次输入  
cd swig  
swig -c++ -lua sanguosha.i  
得到sanguosha\_wrap.cxx.  
PS：这里额外说一句，如果您不知道如何使用 terminal，请您先阅读以下有关 terminal 的相关知识。sanguosha.i 文件位于项目根目录下的 swig 文件夹中。整个过程中确保您的每一句指令都是在相应的文件夹下执行的。如果您的神杀文件直接解压缩在您的 user 文件夹下，你可以使用这一串代码。  
cd Downloads/swig-3.0.5/   (这里替换为您的版本）  
./configure --without-pcre  
make  
sudo make install  
cd swig   
swig -c++ -lua ../../../QSanguosha-For-Hegemony/swig/sanguosha.i   

#####开始编译
好了，现在您可以打开您的QtCreator来进行编译了。请您在欢迎界面选择 Open Project, 然后从您的系统中找到 QSanguosha.pro, 然后打开之。这个项目文件位于项目的根目录。![](http://i.imgur.com/a6U1NQB.jpg)   
![](http://i.imgur.com/P1yGKr0.png)  
当您打开项目后，确保您的项目使用 clang 编译，并请把您的 configuration 改为 release。  
![](http://i.imgur.com/IGMZMw1.jpg)  
![](http://i.imgur.com/5yZ0TBU.jpg)  
这样完成后，您就可以顺利地完成构建。建议您把构建完成的文件夹移动到根目录。  

#####连接动态库
这一步比较困难但相当重要。打开您的 terminal，移动到您的构建目录并输入  
otool -L QSanguosha.app/Contents/MacOS/QSanguosha  

您大概会看到  
   QSanguosha.app/Contents/MacOS/QSanguosha:  
   ./libfmodex.dylib (compatibility version 1.0.0, current version 1.0.0)  
   (QtDir)/5.3/clang\_64/lib/QtNetwork.framework/Versions/5/QtNetwork (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtCore.framework/Versions/5/QtCore (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtWidgets.framework/Versions/5/QtWidgets (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtGui.framework/Versions/5/QtGui (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtQml.framework/Versions/5/QtQml (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtQuick.framework/Versions/5/QtQuick (compatibility version 5.3.0, current version 5.3.0)  
   /System/Library/Frameworks/OpenGL.framework/Versions/A/OpenGL (compatibility version 1.0.0, current version 1.0.0)  
   /System/Library/Frameworks/AGL.framework/Versions/A/AGL (compatibility version 1.0.0, current version 1.0.0)  
   /usr/lib/libstdc++.6.dylib (compatibility version 7.0.0, current version 56.0.0)  
   /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 169.3.0)  

请注意 ./libfmodex.dylib 这一行。  
请您使用 install\_name\_tool 来修改这个库文件的绝对路径，如下：    
install\_name\_tool -change ./libfmodex.dylib ~/lib/mac/lib/libfmodex.dylib QSanguosha.app/Contents/MacOS/QSanguosha  
  
再次输入  
otool -L QSanguosha.app/Contents/MacOS/QSanguosha
  
如果您看到所有的路径均变为绝对路径，说明您成功了。（~是您的项目目录）  
   QSanguosha.app/Contents/MacOS/QSanguosha:  
   ~/lib/mac/lib/libfmodex.dylib (compatibility version 1.0.0, current version 1.0.0)  
   (QtDir)/5.3/clang\_64/lib/QtNetwork.framework/Versions/5/QtNetwork (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtCore.framework/Versions/5/QtCore (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtWidgets.framework/Versions/5/QtWidgets (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtGui.framework/Versions/5/QtGui (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtQml.framework/Versions/5/QtQml (compatibility version 5.3.0, current version 5.3.0)  
   (QtDir)/5.3/clang\_64/lib/QtQuick.framework/Versions/5/QtQuick (compatibility version 5.3.0, current version 5.3.0)  
   /System/Library/Frameworks/OpenGL.framework/Versions/A/OpenGL (compatibility version 1.0.0, current version 1.0.0)  
   /System/Library/Frameworks/AGL.framework/Versions/A/AGL (compatibility version 1.0.0, current version 1.0.0)  
   /usr/lib/libstdc++.6.dylib (compatibility version 7.0.0, current version 56.0.0)  
   /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 169.3.0)  

输入  
macdeployqt QSanguosha.app/  

有时您的macdeployqt并不在system directories下，这是您需要去您的Qt文件夹寻找这个文件。（Qt/5.4/clang\_64/bin/）  

输入  
otool -L QSanguosha.app/Contents/MacOS/QSanguosha  

如果您看到所有的非系统库都在@executable\_path中，您应该就完成了。  
   QSanguosha.app/Contents/MacOS/QSanguosha:  
   @executable\_path/../Frameworks/libfmodex.dylib (compatibility version 1.0.0, current version 1.0.0)  
   @executable\_path/../Frameworks/libfreetype.dylib (compatibility version 1.0.0, current version 1.0.0)  
   @executable\_path/../Frameworks/QtNetwork.framework/Versions/5/QtNetwork (compatibility version 5.3.0, current version 5.3.0)  
   @executable\_path/../Frameworks/QtCore.framework/Versions/5/QtCore (compatibility version 5.3.0, current version 5.3.0)  
   @executable\_path/../Frameworks/QtWidgets.framework/Versions/5/QtWidgets (compatibility version 5.3.0, current version 5.3.0)  
   @executable\_path/../Frameworks/QtGui.framework/Versions/5/QtGui (compatibility version 5.3.0, current version 5.3.0)  
   @executable\_path/../Frameworks/QtQml.framework/Versions/5/QtQml (compatibility version 5.3.0, current version 5.3.0)  
   @executable\_path/../Frameworks/QtQuick.framework/Versions/5/QtQuick (compatibility version 5.3.0, current version 5.3.0)  
   /System/Library/Frameworks/OpenGL.framework/Versions/A/OpenGL (compatibility version 1.0.0, current version 1.0.0)  
   /System/Library/Frameworks/AGL.framework/Versions/A/AGL (compatibility version 1.0.0, current version 1.0.0)  
   /usr/lib/libstdc++.6.dylib (compatibility version 7.0.0, current version 56.0.0)  
   /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 169.3.0)  

#####复制resource
将下面的全部文件复制到QSanguosha.app/Contents/MacOS/。这些文件都位于项目的根目录下。  
* ai-selector/  
* audio/  
* developers/  
* diy/  
* font/  
* image/  
* lang/  
* lua/  
* rule/  
* skins/  
* ui-script/  
* qt\_zh\_CN.qm  
* sanguosha.qss  
![](http://i.imgur.com/rzad8im.jpg)  

#####运行
打开您的 .app，这时候您应该就可以运行了。祝您游戏愉快。
![](http://i.imgur.com/hkBWipS.jpg)  