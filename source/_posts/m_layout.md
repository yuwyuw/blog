---
title: 基于移动端视口的布局方案
date: 2018-03-26 11:15:33
tags:
---
<!-- more -->
#### 像素（pixel）
- ** 设备像素 ** ：设备屏幕的物理像素。
- ** CSS像素 ** ：是浏览器使用的抽象单位，为Web开发者创造的，用来精确度量网页上的内容。

#### 三个视口
桌面上视口宽度等于浏览器宽度，但在手机上有所不同。
- ** 布局视口 ** ：手机上为了容纳为桌面浏览器设计的网站，默认布局视口宽度远大于屏幕宽度，为了让用户看到网站全貌，它会缩小网站。
- ** 视觉视口 ** ：用户正在看到的网站的区域，与设备屏幕一样宽。
- ** 理想视口 ** ：当网站是为手机准备的时候使用。使用meta声明。

#### viewport
手机浏览器是把页面放在一个虚拟的“窗口”（viewport）中，通常这个虚拟的“窗口”（viewport）比屏幕宽，这样就不用把每个网页挤到很小的窗口中（这样会破坏没有针对手机浏览器优化的网页的布局），用户可以通过平移和缩放来看网页的不同部分。移动版的 Safari 浏览器最新引进了 viewport 这个 meta tag，让网页开发者来控制viewport的大小和缩放，其他手机浏览器也基本支持。一个常用的针对移动网页优化过的页面的viewport meta标签大致如下：
```html
<meta name=”viewport” content=”width=device-width, initial-scale=1, maximum-scale=1″>
```
> `width`：控制 viewport 的大小，可以指定的一个值，如果 750，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
`height`：和 width 相对应，指定高度。
`initial-scale`：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
`maximum-scale`：允许用户缩放到的最大比例。
`minimum-scale`：允许用户缩放到的最小比例。
`user-scalable`：用户是否可以手动缩放
>

#### 长度单位
- ** px ** ：绝对单位，页面按精确像素展示
- ** em ** ：相对单位，基准点为父节点字体的大小，如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。
- ** rem ** ：相对单位，可理解为”root em”, 相对根节点html的字体大小来计算，CSS3新加属性，chrome/firefox/IE9+支持。
- ** vw ** ：viewpoint width，视窗宽度，1vw等于视窗宽度的1%。
- ** vh ** ：viewpoint height，视窗高度，1vh等于视窗高度的1%。

#### 利用视口单位适配页面
###### 做法一：仅使用vw作为CSS单位
- 使用viewport，理想视口为设备宽度
```html
<meta name=”viewport” content=”width=device-width, initial-scale=1, maximum-scale=1″>
```
- 对于设计稿的尺寸转换为vw单位，我们使用Sass函数编译
```scss
// 以iphone6尺寸作为设计稿基准，设计稿的宽度是750。
// 1vw等于视窗宽度的1%
@function vw($px) {
  @return ($px / 750) * 100vw;
}
// 当实际字体小于12px的时候，统一渲染为12px，如果需要小于12px的字体，则采用transform缩小
@function fvw($px) {
  @if ($px <= 24) {
    @return (24 / 750) * 100vw;
  } @else {
    @return ($px / 750) * 100vw;
  }
}
```
- 无论是文本还是布局高宽、间距等都使用 vw 作为 CSS 单位
```scss
.test-component {
  display: flex;
  span {
    background-color: red;
    &.test1 {
      font-size: fvw(12);
      width: vw(688);
      height: vw(180);
    }
    &.test2 {
      font-size: fvw(20);
      width: vw(750);
      height: vw(180);
    }
  }
}
```
- ** 优点 ** 
1.不需要依赖脚本
2.可以控制最小的字体
- ** 缺点 **
1.需要引入scss环境
2.行业样式无法使用定义的vw计算方法
3.实现原理是等比放大或者缩小，不能实现当屏幕更大时，一行看到的字体更多。

###### 做法二：将视口宽度设置为750px。
- 使用viewport，理想视口为750
```html
<meta name=”viewport” content=”width=750, initial-scale=1, maximum-scale=1″>
```
- 直接使用设计稿所定义的长度。不需要转换。
```scss
.test-component {
  display: flex;
  span {
    background-color: red;
    &.test1 {
      font-size: 24px;
      width: 688px;
      height: 180px;
    }
    &.test2 {
      font-size: 20px;
      width: 750px;
      height: 180px;
    }
  }
}
```
- ** 优点 **
1.不需要依赖scss环境
2.不需要进行单位转换，直接使用设计稿中的长度大小即可。
- ** 缺点 **
1.浏览器调试的时候可能会出现问题，实际情况以真机为准。
2.实现原理是等比放大或者缩小，不能实现当屏幕更大时，一行看到的字体更多。

###### 做法三：使用rem布局(网易做法)
无需自己手动引入viewport
- 计算rem,在页面中引入js
```js
    (function(doc, win) {
        var docEl = doc.documentElement,
            isIOS = navigator.userAgent.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/),
            dpr = isIOS ? Math.min(win.devicePixelRatio, 3) : 1,
            dpr = window.top === window.self ? dpr : 1, //被iframe引用时，禁止缩放
            dpr = 1,
            scale = 1 / dpr,
            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
        docEl.dataset.dpr = dpr;
        var metaEl = doc.createElement('meta');
        metaEl.name = 'viewport';
        metaEl.content = 'initial-scale=' + scale + ',maximum-scale=' + scale + ', minimum-scale=' + scale;
        docEl.firstElementChild.appendChild(metaEl);
        var recalc = function() {
            var width = docEl.clientWidth;
            if (width / dpr > 750) {
                width = 750 * dpr;
            }
            // 乘以100，px : rem = 100 : 1
            docEl.style.fontSize = 100 * (width / 750) + 'px';
        };
        recalc()
        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
    })(document, window);
```
- 使用
```scss
.test-component {
  display: flex;
  span {
    background-color: red;
    &.test1 {
      width: 6.88rem;
      height: 1.8rem;
    }
  }
}
```
- ** 优点 **
1.不依赖于scss
2.可实现自适应布局，当屏幕更大时，可实现一行看到的字体更多。
3.当屏幕变小时，看到的字体更大，屏幕变大时，看到的字体更多
- ** 缺点 **
1.无法控制最小字体。

###### 做法四：使用vw和rem布局方式
- 使用viewport，理想视口为设备宽度
```html
<meta name=”viewport” content=”width=device-width, initial-scale=1, maximum-scale=1″>
```
- 对于设计稿的尺寸转换为rem 以及vw单位，我们使用Sass函数编译
```scss
$vw_fontsize: 75; // 以iPhone 6尺寸根元素大小作为基准值
$vw_design: 750; // 以设计稿宽度750作为基准值
@function rem($px) {
  @return ($px / $vw_fontsize ) * 1rem;
}
@function fvw($px) {
  @if ($px <= 24) {
    @return (24 / 750) * 100vw;
  } @else {
    @return ($px / 750) * 100vw;
  }
}
html {
  font-size: ($vw_fontsize / ($vw_design)) * 100vw;
  // 同时，通过Media Queries 限制根元素最大最小值
  @media screen and (max-width: 320px) {
    font-size: 64px;
  }
  @media screen and (min-width: 540px) {
    font-size: 108px;
  }
}
```
- 无论是文本还是布局高宽、间距等都使用 vw 作为 CSS 单位
```scss
.test-component {
  display: flex;
  span {
    background-color: red;
    &.test1 {
      font-size: fvw(58);
      width: rem(688);
      height: rem(180);
    }
  }
}
```
- ** 优点 **
1.不需要依赖脚本
2.可以控制最小字体
3.可实现自适应布局，当屏幕更大时，可实现一行看到的字体更多。
- ** 缺点 **
1.依赖scss环境
2.行内样式无法采用rem以及vw计算方式