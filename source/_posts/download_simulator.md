---
title: mac xcode 下载 ios指定版本的模拟器
date: 2018-18-28 11:32:14
tags:
author: lemon
---
mac xcode 下载ios指定版本的模拟器
<!-- more -->
+ 打开终端，输入命令
```
sudo /Applications/Xcode.app/Contents/MacOS/Xcode
```
+ 打开xcode， 选择需要下载的模拟器版本，点击下载，开始下载以后，点击取消
+ 回到终端，复制下载地址,开始下载
+ 安装 等待下载完成, 进入下面地路径
```
    ~/Library/Caches
```
+ 找到 com.apple.dt.Xcode 文件<类似于应用程序的文件>, 打开方式：选择显示包内容
+ 进入 Downloads 目录 (如果没有, 则手动创建一个 Downloads 目录)将下载好的文件移动到 Downloads 目录 (最好不要改动文件名)
+ 重新打开xcode, 再次打开references中下载相对应的simulator,选择之前的下载版本。
+ 下载完成之前，重新打开xcode即可
 