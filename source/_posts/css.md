---
title: css3的一些Demo
date: 2017-03-15 11:32:14
tags:
author: lemon
---
有关css3的一些demo

### demo
#### 1.map site（地图节点）[在线调试环境](https://jsfiddle.net/lemon_yw/pydoxmyz/)     

```css
    @keyframes map-pulse { 
        0% {
            opacity: .85; 
            filter: alpha(opacity= 85);
            transform: scale(0); 
        } 
        100% {
            opacity: 0;
            filter: alpha(opacity= 0);
            transform: scale(1); 
        }
    }
```
#### 2.鼠标hover（边框向两边展开）[在线调试环境](https://jsfiddle.net/lemon_yw/9sqmh7so/)
```css
    .button .check {
       position: absolute;
       top: 0;
       left: 50%;
       margin-left: -50%;
       width: 50%;
       height: 100%;
       border-top: 1px solid red;
       border-bottom: 1px solid red;
       transform-origin: 0;
       transform: scaleX(2);
       transition: 0.3S ease-in-out
    }
```
#### 3.消息框（下方三角形带背景和边框）[在线调试环境](https://jsfiddle.net/lemon_yw/t1bk9zvg/)
```css
    .triangle {
      position:absolute;
      left:50%;
      margin-left:-10px;
      width:0px;
      height:0px;
      border-width:10px;
      border-style:solid dashed dashed dashed
    }
    .border {
      border-color:#C6CCDC transparent  transparent transparent;
      bottom: -20px;  
    }
    .bg {
      border-color:#fff transparent  transparent transparent;
      bottom: -19px;  
    }
```
#### 4. 图片hover效果（边框显示&消失）[在线调试环境](https://jsfiddle.net/lemon_yw/18c6pcnz/)
```css
     .main {
        display: inline-block;
        background-color: gray;
        width: 250px;
        height: 250px;
        margin: 0 auto;
        position: relative;
    }
    .border {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
    }
    .border:before {
        position: absolute;
        top: 30px;
        right: 30px;
        bottom: 30px;
        left: 30px;
        content: '';
        border-top: 1px solid red;
        border-bottom: 1px solid red;
        transform: scale(0,1);
        transition: opacity 0.35s, transform 0.35s
    }
    .border:after {
        position: absolute;
        top: 30px;
        right: 30px;
        bottom: 30px;
        left: 30px;
        content: '';
        border-left: 1px solid red;
        border-right: 1px solid red;
        transform: scale(1,0);
        transition: opacity 0.35s, transform 0.35s
    }
    .main:hover .border:before ,  .main:hover .border:after{
        transform: scale(1);
    } 
```
#### 5.图片hover效果-局部放大效果
```css
    .main {
        display: inline-block;
        width: 250px;
        height: 250px;
        margin: 0 auto;
        position: relative;
        border:1px solid red;
        overflow: hidden;
        }
    .main img {
        width: calc(100% + 10px);
        opacity: 1;
        transition: opacity 0.35s, transform 0.35s;
        transform: translate3d(-30px,0,0) scale(1.12);
        }
    .main:hover img {
        opacity: 0.5;
        transform: translate3d(0,0,0) scale(1)
        }
```
