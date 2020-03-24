---
title: 什么是JavaScript，由哪些部分组成？
date: 2019-12-02 17:46:57
tags:
author: lemon
---
作为一名前端开发工程师，每天 coding JS，那你知道什么是 JS ，又由哪些部分组成吗？
##### JavaScript 的起源
JavaScript 诞生于1995年，主要目的是为了处理以前由服务器端语言负责的一些输入验证的操作。在 JavaScript 诞生以前，必须把表单数据发送给服务器端才能确定用户是否可以填写数据，是否输入无效的值。由于拨号上网速度太慢，对用户上网产生十分严重的影响。当时走在技术前沿的 Netscape 公司决定开发一种客户端语言，用于处理这种简单的验证。
当时就职于 Netscape 公司的 布兰登 · 艾奇 （Brendan Eich）用时10天开发出一种名为 LiveScript 的脚本语言。 Netscape 公司为了搭上媒体热炒 Java 的顺风车，临时把 LiveScript 改名为 JavaScript, 而实际上， JavaScript 和 Java一点关系也没有。

##### JavaScript是什么
随着时间的推移，JavaScript 也日益强大，JavaScript 逐渐成为浏览器必备的一项特色功能。JavaScript 也不在局限于表单验证，而是具备了与浏览器窗口以及内容的交互能力。JavaScript 成为一门功能全面的编程语言， 能够处理复杂的计算和交互，拥有了闭包、匿名 甚至元编程等特性。

- 浏览器中的 JavaScript 能做什么

``` 
Atwood's Law: Any application that can be written in JavaScript, will eventually be written in JavaScript ```

> 翻译过来就是凡是可以被JavaScript写出来的，最终都会用JavaScript写出来。（ 定律原始出处[The Principle of Least Power](https://blog.codinghorror.com/the-principle-of-least-power/)）


1. 浏览器中的 JavaScript 可以做与网页操作、用户交互和 Web 服务器相关的所有事情, 例如：
	- 在网页中插入新的 HTML，修改现有的网页内容和网页的样式
	- 响应用户的行为，响应鼠标的点击或移动
	- 向远程服务器发送网络请求，下载或上传文件
	- 获取或修改 cookie，向访问者提出问题、发送消息。
	- 记住客户端的数据（本地存储）

- 浏览器中的 JavaScript 不能做什么

1. 为了用户的（信息）安全，在浏览器中的 JavaScript 的能力是有限的。这样主要是为了阻止邪恶的网站获得或修改用户的私人数据。这些限制的例子有：
	- 网页中的 JavaScript 不能读、写、复制及执行用户磁盘上的文件或程序。
	- 浏览器的同源策略会影响JS的访问（[浏览器的同源策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)），比如你访问的是 ```https:www.baidu.com``` , JavaScript 肯定不能访问 ```https:www.jd.com```的内容。在比方说你在页面里面嵌入了百度地图,是无法直接修改百度地图任何信息，只能通过官方提供的接口进行修改。因为不同源，JS无法执行。

##### JavaScript由哪些部分组成
JavaScript 由三大部分组件，分别为核心（ECMA Script）、文档对象模型（DOM）、浏览器对象模型（BOM）

![alt JavaScript组成](/images/javascript1.jpeg)

- [什么是 核心（ECMAScript)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Language_Resources)
ECMAScript 是一种标准，标准化了脚本语言。
- [什么是文档对象模型（DOM）](https://baike.baidu.com/item/%E6%96%87%E6%A1%A3%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B/1033822?fromtitle=DOM&fromid=50288)
文档对象模型（DOM, Document Object Model） 是针对XML但经过扩展用于HTML的应用程序编程接口。DOM把整个页面映射为一个多层节点结构，每一个节点可视为一个对象，这些对象依照层级关系形成一颗树，这颗树就命名为DOM树。
有了对象，编程就方便多了，只要一层层拿到对象就可以优雅地改变对象的属性进而动态地改变HTML等文档的展示。
- [什么是浏览器对象模型BOM](https://baike.baidu.com/item/BOM/1801)
浏览器对象模型（BOM, Browser Object Model）从根本上来看，BOM只处理浏览器窗口和框架，支持以下功能（部分列举）
	- 弹出新浏览区功能
	- 移动、缩放、关闭浏览器等功能
	- 提供浏览器详细信息 navigato r对象
	- 提供浏览器加载页面的详细信息 location对象
	- 对cookies的支持

##### 小结
JavaScript是一种专为与网页交互而设计的脚本语言，由下列3个部分组成：
- ECMAScript 提供核心语言功能，是一种标准
- 文档对象模型（DOM），提供访问和操作网页内容的方法和接口
- 浏览器对象模型（BOM）提供与浏览器交互的方法和接口

###### tips
以上部分内容节选红宝石书《JavaScript高级程序设计》。有兴趣的朋友可阅读原著。