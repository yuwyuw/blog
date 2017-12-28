---
title: 常见布局说明
date: 2017-03-16 14:32:11
tags:
author: lemon
---
#### 容器内左右布局（换行时，不用限制高度）[在线调试环境](https://jsfiddle.net/)
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


