---
title: Node版本管理器-NVM
date: 2019-01-07 15:17:14
tags:
---
###### 介绍
总所周知，在项目开发中，不同的项目可能会用到不同的Node版本。鉴于此景，Node版本管理器变应运而生。今天给大家推荐一款好用的Node版本管理器-NVM。它可以灵活的切换不同的Node版本，简单，好用。有兴趣的朋友可以访问[nvm官网](https://github.com/creationix/nvm)
###### 安装（MAC）
>安装命令
```
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

>检测
```
 nvm 
```

>若出现 `Node Version Manager` 安装成功

###### 使用
```
    nvm install stable  #安装当前最新的稳定版
    nvm install 0.12.4  #安装指定版本
    nvm ls #查看node的所有安装版本
    nvm use 0.12.4 #默认使用某个版本
    nvm uninstall 0.12.4 #删除某个版本
```
###### 遇到的问题
>设置默认Node版本后，切换窗口查看Node版本依旧没有变化？

采用nvm use xx版本修改默认版本的方式，只是修改了当前环境下的Node默认版本,并不是修改了系统默认的Node版本，若想修改系统默认的版本，可采用以下方法。
```
    nvm alias default 0.12.4
```
>切换版本以后，其他开发环境缺失?比如cnpm vue

cnpm , vue是基于当前使用的Node环境安装，当切换不同的Node环境时，新的Node环境并没有安装cnpm，vue等。此时，需要重新安装这些环境或者在项目中删除node_modules执行npm install 即可。