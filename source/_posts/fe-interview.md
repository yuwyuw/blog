---
title: 前端知识点
date: 2018-01-29 14:04:09
tags:
---
有关前端一些常见的知识点。
<!-- more -->
##### JS
###### 什么是闭包，以及闭包的应用。
由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

###### 同步、异步、回调之间的执行顺序以及Javascript异步编程的4种方法。
执行顺序：
- 同步 => 异步 => 回调。

异步编程：
- 回调函数。
- 事件监听。
- 发布信号。
- Promises对象。
 
###### 什么是跨域？以及跨域的解决方式。
- 什么是跨域？
一个域名下请求另外一个域名的资源。
- 解决方式。
1.「jsonp」。
2.「CORS 」Cross-Origin Resource Sharing(跨域资源共享)是一种允许当前域（origin）的资源（比如html/js/web service）被其他域（origin）的脚本请求访问的机制。当使用XMLHttpRequest发送请求时，浏览器如果发现违反了同源策略就会自动加上一个请求头:origin,后端在接受到请求后确定响应后会在Response Headers中加入一个属性:Access-Control-Allow-Origin,值就是发起请求的源地址，浏览器得到响应会进行判断Access-Control-Allow-Origin的值是否和当前的地址相同，只有匹配成功后才进行响应处理。
3.「服务器跨域 」在前后端分离的项目中可以借助服务器实现跨域，具体做法是：前端向本地服务器发送请求，本地服务器代替前端再向api服务器接口发送请求进行服务器间通信，本地服务器其实就是个中转站的角色，再将响应的数据返回给前端。
4.「postmessage跨域 」、在HTML5中新增了postMessage方法，postMessage可以实现跨文档消息传输（Cross Document Messaging），Internet Explorer 8, Firefox 3, Opera 9, Chrome 3和 Safari 4都支持postMessage。该方法可以通过绑定window的message事件来监听发送跨文档消息传输内容。 
- 弊端。
jsonp只能发送get请求、cors会忽略cookie、服务器跨域需要另起服务器。

###### JSON 和 JSONP的区别。
- JSON是一种基于文本的数据交换方式。跨平台传递极其简单，后台语言几乎全部支持。方便使用。
- JSONP是一种非正式传输协议，该协议的一个要点就是允许用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹住JSON数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。

###### Canvas 和SVG的区别。
- Canvas。
1.通过 JavaScript 来绘制 2D 图形。
2.是逐像素进行渲染的。
3.一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。
- SVG。
1.是一种使用 XML 描述 2D 图形的语言。
2.基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。
3.每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。
- 比较。
1.Canvas依赖分辨率、不支持事件处理器、能够以 .png 或 .jpg 格式保存结果图像、最适合图像密集型的游戏。
2.SVG不依赖分辨率、支持事件处理器、不适合游戏应用。

###### JS数据类型。
- 6种原始数据类型。
1. Boolean。
2. Null。
3. Undefined。
4. Number。
5. String。
6. Symbol(ES6新定义)。
-  Object。
  
###### 判断是否为字符串。
```js
function isString(stringToCheck) {
    return typeof stringToCheck === 'string' || stringToCheck instanceof String
}
```
###### 判断是否为数字。
```js
function isNumber (numberToCheck) {
    return typeof numberToCheck === 'number' || numberToCheck instanceof Number
}
```
###### 判断是否为数组。
```js
function isArray (arrayToCheck) {
    return Array.isArray(arrayToCheck)
}
```
###### 判断是否为对象。
```js
function isObject (objectToCheck) {
    if (!!objectToCheck) {
        return objectToCheck.constructor === Object
    }
}
```
###### 判断是否为空对象。(对象不为空返回false，null,array等返回true)
```js
function isEmptyObj (objectToCheck) {
    let boolean = true
    if (!!objectToCheck) {
        boolen =  !(objectToCheck.constructor === Object && !!Object.keys(objectToCheck).length)
    }
    return boolean;
}
```
###### React和Vue的优缺点。
- Vue。
1. 核心架构是MVVM（model,view,viewModel），特点是数据双向绑定。
2. 轻量级，对于简单页面、小型应用，vue开发则非常高效。
3. vue源码相对简单，容易上手。
4. 后期维护成本高。
5. 不适用于大型项目。
- React。
1. react是真正能把复杂问题拆分成独立的模块的。
2. 后期维护成本低。
3. 适用于大型的项目。
4. 有大量的社区。
5. React的双向绑定的使用没有Vue便捷。
6. 对使用者有技术要求，学习成本高。

###### 事件捕获与冒泡。
```html
<div id="outer">
    <p id="inner">Click me!</p>
</div>
```
事件捕获：`document -> html -> body -> div -> p`。
事件冒泡：`p -> div -> body -> html -> document`。
W3C：采用折中的方式,先捕获再冒泡。 
##### CSS
###### CSS的书写顺序。
1. 位置属性。(`position, top, right, z-index, display, float`等)
2. 大小。(`width, height, padding, margin`)
3. 文字系列。(`font, line-height, letter-spacing, color- text-align`等)
4. 背景。(`background, border`等)
5. 其他。(`animation, transition`等)

###### 清除浮动的方法。
- 给最后一个浮动元素添加一个兄弟元素、应用 `clear：both`。
- 浮动元素的父级元素定义`overflow: auto`。
- 浮动元素的父级元素定义宽高。
- 给浮动元素的父级添加`:after`方法。
```scss
.clearfix {
  &:after {
    content: '.';
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
    }
}
```

###### 什么是BFC？
块格式化上下文（Block Formatting Context，BFC） 是Web页面的可视化CSS渲染的部分，是块级盒布局发生的区域，也是浮动元素与其他元素交互的区域。
BFC的使用。
- `float` 除了`none`以外的值。
- `overflow` 除了`visible` 以外的值。（`hidden，auto，scroll` ）
- `display`。 (`table-cell，table-caption，inline-block, flex, inline-flex`)
- `position`。值为（`absolute，fixed`）

BFC的应用场景。
- 解决margin叠加问题。
```html
<p class="demo1">hello</p>
<p class="demo2">hello</p>
```
  ```css
.demo1 {
    width: 100px;
    height: 100px;
    margin: 50px;
    line-height:  100px;
    text-align: center;
    background-color: red;
  }
```
  `2个P标签`的`margin`是`50px`，而不是`100px`,因为发生了`margin`叠加。如果想要`2个P标签`的值是`100px`，需要运动到BFC。给需要`margin`不叠加的一个元素添加一个父元素，设置`overflow: hidden`属性。
    ```html
    <div class="warp">
        <p class="demo1">hello</p>
    </div>
    <p class="demo1">hello</p>
    ```
    ```css
    .warp {
        overflow: hidden;
      }
```
- 清除浮动。
    ```html
    <p class="demo1">hello</p>
    <p class="demo2">hello</p>
    ```
    ```css
    .demo1 {
        float: left;
        width: 100px;
        height: 100px;
        line-height:  100px;
        text-align: center;
        background-color: red;
      }
    .demo2 {
        height: 200px;
        background-color: blue;
      }
    ```
    这2个标签会重合，如果想要不重合，实现2栏布局需要运动到BFC。给浮动后的一个未浮动的元素添加`overflow:hidden`属性。
    ```css
    .demo2 {
        height: 200px;
        background-color: blue;
        overflow: hidden;
      }
    ```

###### 如何画一个三角形。
```html
<p class="demo1 demo"></p> //直角在左上方
<p class="demo2 demo"></p> //直角在右下方
<p class="demo3 demo"></p> //直角在左下方
<p class="demo4 demo"></p> //直角在右上方
```
- 画一个直角在左上方的三角形。
规律：希望直角在上方或者下方，就设置`border-top`或者`border-bottom`,希望左边或者右边透明就设置`border-left`或者`border-right`透明。
```css
.demo {
    display: inline-block;
    margin: 5px;
  }
//直角在左上方
.demo1 {
    width: 0px;
    left: 0px;
    border-top: 100px solid red;
    border-right: 100px solid transparent;
  }
//直角在右下方
.demo2 {
    width: 0px;
    left: 0px;
    border-bottom: 100px solid red;
    border-left: 100px solid transparent;
  }
//直角在左下方  
.demo3 {
    width: 0px;
    left: 0px;
    border-bottom: 100px solid red;
    border-right: 100px solid transparent;
  }
//直角在右上方  
.demo4 {
    width: 0px;
    left: 0px;
    border-top: 100px solid red;
    border-left: 100px solid transparent;
  }
```
##### 安全

##### 性能

###### 前端可以从哪些方面优化？
一、页面级优化
1.减少 HTTP请求数。
- 「从设计实现层面简化页面。」保持页面简洁、减少资源的使用。
- 「合理设置 HTTP缓存。」恰当的缓存设置可以大大的减少 HTTP请求。
- 「资源合并与压缩。」CSS、Javascript、Image都可以用相应的工具进行压缩，压缩后往往能省下不少空间。 
- 雪碧图。
- 懒加载。

2.「将外部脚本置底。」如果外部脚本出现问题，至少可以加载完静态页面。
3.「异步执行」。 保证脚本在页面内容后面加载。
4.按需加载。
5.将 CSS放在 HEAD中。
6.异步请求。
7.减少不必要的 HTTP跳转。
8.避免重复的资源请求。
二、代码级优化
1.优化JS，函数命名简洁易读,代码干练，减少DOM。
2.选择合理的CSS选择符以及层级。
3.Image压缩

###### [网页性能管理详解。](http://www.ruanyifeng.com/blog/2015/09/web-page-performance-in-depth.html)
>文章涉及网页生成的过程、重排和重绘、对于性能的影响等。
>重构：页面任何的变化都可以称为页面重构：完全重构、细节调整。
>重排（回流）：重新排版，为渲染树需要重新计算。（DOM元素的几何属性变化、DOM树的结构变化、获取某些属性、其他）
>重绘是重新描绘,如改变`visibility`、`outline`、`background-color`等
重排是DOM节点发生了变化，重绘是样式发生了变化。所以重排一定会重绘，但是重绘不一定会重排。


##### 普文
###### 为什么页面需要加上DOCTYPE。
它的目的是要告诉标准通用标记语言解析器，它应该使用什么样的文档类型定义（DTD）来解析文档。目前有3种解析方式：
- 非怪异（标准）模式。
- 怪异模式。
- 部分怪异（近乎标准）模式。

>在“标准模式”(standards mode) 页面按照 HTML 与 CSS 的定义渲染，而在“怪异模式(quirks mode) 模式”中则尝试模拟更旧的浏览器的行为。 一些浏览器（例如，那些基于 Mozilla 的 Gecko 渲染引擎的，或者 Internet Explorer 8 在 strict mode 下）也使用一种尝试于这两者之间妥协的“近乎标准”(almost standards) 模式，实施了一种表单元格尺寸的怪异行为，除此之外符合标准定义。
一个不含任何`DOCTYPE`的网页将会以 怪异(quirks) 模式渲染。
HTML5提供的<DOCTYPE html>是标准模式，向后兼容的, 等同于开启了标准模式，那么浏览器就得老老实实的按照W3C的 标准解析渲染页面，这样一来，你的页面在所有的浏览器里显示的就都是一个样子了。

###### IE盒子模型和标准盒子模型有什么重要区别？
盒子模型是由`margin`、`border`、`padding`、`content`组成。
两者的区别在于`content`的不同，IE盒模型的`content`包括`border`、`padding`。
###### [什么是viewport](http://www.css88.com/archives/5975)。