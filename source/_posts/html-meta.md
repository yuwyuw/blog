---
title: html_meta
date: 2017-09-26 14:02:31
tags:
---
[有关HTML<meta>标签的使用](http://www.w3school.com.cn/tags/tag_meta.asp)
[meta http-equiv大全](http://www.cnblogs.com/jerryshi/archive/2008/10/14/1310611.html)
```html
推荐使用：
<meta charset="utf-8"/>
<meta name="renderer" content="webkit"/>
<meta http-equiv="X-UA-Compatible" content="IE=edge"/>
涉及到后端项目
<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
禁止浏览器从本地机的缓存中调阅页面内容，网页不保存在缓存中，每次访问都刷新页面。这样设定，访问者将无法脱机浏览。
<meta http-equiv="Pragma" content="no-cache" />
说明：指定网页在缓存中的过期时间，一旦网页过期，必须到服务器上重新调阅。
<meta http-equiv="Expires" content="0" />
```
### meta renderer
```html
我们可以使用标签来指定适合自己网站的渲染内核名称，当双核浏览器访问本网页时，
就会根据我们的指示，选择我们指定的渲染内核来处理网页。
若页面需默认用极速核，增加标签：
<meta name="renderer" content="webkit">

若页面需默认用ie兼容内核，增加标签：
<meta name="renderer" content="ie-comp">

若页面需默认用ie标准内核，增加标签：
<meta name="renderer" content="ie-stand">

我们只需在网站的head标签中添加上面的代码，即可以相对应的模式来渲染网站。
同时我们也可以同时指定多个内核名称，之间以符号”|”进行分隔，如下代码：
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```
### X-UA-Compatible
```html
X-UA-Compatible是针对IE8新加的一个设置，对于IE8之外的浏览器是不识别的，这个区别与content="IE=7"在无论页面是否包含<!DOCTYPE>指令，都像是使用了Windows Internet Explorer 7的标准模式。而content="IE=EmulateIE7"模式遵循<!DOCTYPE>指令。对于多数网站来说，它是首选的兼容性模式。

为了避免制作出的页面在IE8下面出现错误，建议直接将IE8使用IE7进行渲染。也就是直接在页面的header的meta标签中加入如下代码：
<meta http-equiv="X-UA-Compatible" content="IE=7" /> 

 X-UA-Compatible 是针对 IE8 版本的一个特殊文件头标记，用于为 IE8 指定不同的页面渲染模式。由于当下 IE6 和 IE7 使用率依然较高，综合考虑，启用 IE8 版本的 X-UA-Compatible 兼容模式显得相当重要。

 各种兼容模式代码示例如下：
 1.<meta http-equiv="X-UA-Compatible" content="IE=5" />
像是使用了 Windows Internet Explorer 7 的 Quirks 模式，这与 Windows Internet Explorer 5 显示内容的方式很相似。

2.<meta http-equiv="X-UA-Compatible" content="IE=7" />
无论页面是否包含 <!DOCTYPE> 指令，均使用 Windows Internet Explorer 7 的标准渲染模式。

3.<meta http-equiv="X-UA-Compatible" content="IE=8" />
开启 IE8 的标准渲染模式，但由于本身 X-UA-Compatible 文件头仅支持 IE8 以上版本，因此等同于冗余代码。

4.<meta http-equiv="X-UA-Compatible" content="edge" />
Edge 模式通知 Windows Internet Explorer 以最高级别的可用模式显示内容，这实际上破坏了“锁定”模式。即如果你有IE9的话说明你有IE789，那么就调用高版本的那个也就是IE9。

5.<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1" >
如果IE有安装Google Chrome Frame，那么就走安装的组件，如果没有就和<meta http-equiv="X-UA-Compatible" content="edge" />一样。
说明：针对IE 6，7，8等版本的浏览器插件Google Chrome Frame，可以让用户的浏览器外观依然是IE的菜单和界面，但用户在浏览网页时，实际上使用的是Google Chrome浏览器内核。

6.<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7" />
EmulateIE7 模式通知 Windows Internet Explorer 使用 <!DOCTYPE> 指令确定如何呈现内容。标准模式指令以Windows Internet Explorer 7 标准模式显示，而 Quirks 模式指令以 IE5 模式显示。与 IE7 模式不同，EmulateIE7 模式遵循 <!DOCTYPE> 指令。对于多数网站来说，它是首选的兼容性模式。
```