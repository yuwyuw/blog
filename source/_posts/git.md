---
title: 'git使用指南'
date: 2017-03-22 15:11:35
tags:
author: lemon
---
#### 一、本地项目放入github（https） 
###### 登录github，创建一个仓库，复制仓库地址,打开命令行终端，进入项目所在的本地目录，将目录初始化为一个 Git 项目
```base
    git init
```
###### 将代码放入git 暂存区
```base
    git add .
```
###### 讲代码提交到工作区
```base
    git ci -m "commit"
```
###### 回到命令行终端界面，将本地仓库关联到远程仓库
```base
    git remote add origin https://github.com/superRaytin/alipay-app-ui.git
```
###### 提交代码到 GitHub 仓库
``` base
    git push origin master
```
#### 二、git reset 和git git revert的区别
``` base
 git reset a->b->c ,想去掉c的commit，git reset 到b的commit，--hard不保留修改到工作区。
 git revert a->b->c,想去掉B，把B的commitID revert，这样就把B的+-改为-+，恢复到修改之前。
 git cherry-pick commitID，把某一次提交拿到该分支里面，commitID是针对git 全局，和某个分支无关。
```
