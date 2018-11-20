---
title: Vue如何实现双向绑定(上)
date: 2018-11-15 10:52:29
tags:
---
Vue的双向绑定特性一直广受人们欢迎，但是大家知道实现双向绑定的原理吗？这篇文章将给大家介绍实现双向绑定的原理。
<!-- more -->
##### 为什么会出现MVVM
###### 什么是MVC
![](/images/vue/mvc.png)

MVC即Model-View-Controller的缩写，就是模型-视图-控制器 , 也就是说一个标准的Web 应用程序是由这三部分组成的。

> Model：管理数据。
> View：UI布局，展示数据。
> Controller：响应用户操作，并将Model更新到 View 上。

###### MVC的缺点
这种MVC架构模式对于简单的应用来看起是OK的，也符合软件架构的分层思想。 但实际上，随着H5 的不断发展，人们更希望使用H5开发的应用能和Native媲美，或者接近于原生App的体验效果，于是前端应用的复杂程度已不同往日，今非昔比。这时前端开发就暴露出了三个痛点问题：
* 开发者在代码中大量调用相同的DOM API, 处理繁琐 ，操作冗余，使得代码难以维护。
* 大量的DOM操作使页面渲染性能降低，加载速度变慢，影响用户体验。
* 当Model频繁发生变化，开发者需要主动更新到View。当用户的操作导致Model发生变化，开发者同样需要将变化的数据同步到Model中，这样的工作不仅繁琐，而且很难维护复杂多变的数据状态。

###### 什么是MVVM
![](/images/vue/mvvm.png)
MVVM即Model-View-ViewModel的缩写，就是模型-视图-视图模型，也就是说一个标准的Web 应用程序是由这三部分组成的。

> Model：代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。
> View：代表UI组件，它负责将数据模型转化成UI 展现出来。
> ViewModel：是一个同步View 和 Model的对象。

###### MVVM的优点
在MVVM架构下，View和Model之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel通过双向数据绑定把View层和Model层连接了起来，而View和Model之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM,不需要关注数据状态的同步问题，复杂的数据状态维护完全由MVVM来统一管理。
##### 双向绑定
![](/images/vue/bind.png)
###### [如何理解双向绑定](https://jsfiddle.net/lemon_yw/9a67Lx13/)
简单来说就是用户更新了视图，Model也随之更新就称为双向绑定。再说细点，就是在单向绑定的基础上给可输入元素（input、textare等）添加了change(input)事件,(change事件触发，View的状态就被更新了)来动态修改model。
###### 双向绑定原理
> Observer: 数据监听器，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者，内部采用Object.defineProperty的getter和setter来实现。
> Dep: 消息订阅器，内部维护了一个数组，用来收集订阅者（Watcher），数据变动触发notify 函数，再调用订阅者的 update 方法。
> Watcher: 订阅者,作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数。
> Compile: 指令解析器，它的作用对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数。





