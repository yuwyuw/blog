---
title: Mac下常见Nginx使用命令（未完待续...）
date: 2019-11-29 14:34:31
tags:
author: lemon
---
有关Nginx常见命令
##### 常见查看Nginx信息命令

###### 查看版本信息
```
nginx -v
```
###### 查看编译器版本和配置参数
```
nginx -V
```
###### 检测配置(也可用于查找文件目录)
```
nginx -t
```
###### 查看进程
```
ps -ef |grep nginx
```
###### 重新打开日志文件
```
nginx -s reopen
```
##### 常见操作Nginx信息命令

######  启动nginx
```
nginx
或者
brew services start nginx
```
###### 重新启用
```
nginx -s reload
或者
brew services restart nginx 
```
###### 快速关闭
```
nginx -s stop
```
###### 优雅关闭(进程如果还在服务中，那么就不会关闭该进程，直到进程完成服务为止)
```
nginx -s quit
```
> 当运行nginx -s quit时，Nginx 会等待工作进程处理完成当前请求，然后将其关闭。当你修改配置文件后，并不会立即生效，而是等待重启或者收到nginx -s reload信号。
当 Nginx 收到 nginx -s reload 信号后，首先检查配置文件的语法。语法正确后，主线程会开启新的工作线程并向旧的工作线程发送关闭信号，如果语法不正确，则主线程回滚变化并继续使用旧的配置。当工作进程收到主进程的关闭信号后，会在处理完当前请求之后退出。