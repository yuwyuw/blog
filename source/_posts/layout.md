---
title: layout
date: 2017-03-16 14:32:11
tags:
---
有关布局的一些demo
### demo
[在线调试环境](https://jsfiddle.net/)
#### 容器内左右布局（换行时，不用限制高度）
```css
    .main {
        display: inline-block;
        width: 1100px; 
        border:1px solid red; 
    }
    .main div { 
        margin-left: 95px;
        padding-bottom: 20px;
    }
    label {
        float: left;
        width: 85px;
        margin-left: -95px;
        background-color: red;
        text-align: right;
    }
    span {
        display: inline-block;
         padding-left: 30px;
        }
```
```html
    <div class="main">
        <div>
            <label>云硬盘名称</label>
            <span class="text">所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们我们所以，我们所以，我们所以，我们所以，我们我们所以，我们所以，我们所以，我们所以，我们我们所以，我们所以，我们所以，我们所以，我们我们所以，我们所以，我们所以，我们所以，我们</span>
        </div>
        <div>
            <label>购买数量</label>
            <span class="text">所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们</span>
        </div>
        <div>
            <label>类型</label>
            <span class="text">所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们所以，我们</span>
        </div>
    </div>
```
### React 和普通js相比，优点在哪里
```html
1. 前端界面是由组件和数据渲染组成的，组件固定，根据数据渲染可以减少dom的操作。React可以组件化管理，组件的相互嵌套。而普通的js的实现就会比较复杂。比如组件的相互嵌套就很难实现。
2. 事件绑定，针对某个组件特定的事件绑定，普通js容易造成全局绑定，或者影响到其他地方，有隐患。而React，可以很好的规避到这一点。
3. 方便测试。
```

