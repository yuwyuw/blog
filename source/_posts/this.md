---
title: 对Javascript中this的理解
date: 2017-12-28 14:12:44
tags:
---
与其他语言相比，函数的 this 关键字在 JavaScript中的表现略有不同，此外，在严格模式和非严格模式之间也会有一些差别。本文介绍this在不同使用场景的指向问题。
1、this 并不是在编写的时候绑定的，而是在运行时绑定的。它的上下文取决于函数调用时的各种条件。
2、this 的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式。当一个函数被调用时，会创建一个「执行上下文」，这个上下文会包含函数在哪里被调用（调用栈）、函数的调用方式、传入的参数等信息。this 就是这个记录的一个属性，会在函数执行的过程中用到。
<!-- more -->
###### 情况一、全局性调用，this代表全局对象Global 
这是函数的最通常的用法，请看下面这段代码，无论在函数里执行，还是函数外执行，它的运行结果都是2。
```js
    function test () {
        this.x = 2;
        alert(this.x);
    }
    test(); //2
    console.log(this.x) //2
```
为了证明this代表全局对象Global，我对代码作一定的修改，请看下面这段代码，它的运行结果是1。
```js
    this.x = 1;
    function test () {
        alert(this.x)
    }
    text(); //1
```
this代表全局对象，多次申明表示重新定义，请看下面这段代码，它的运行结果是2。
```js
    this.x = 1;
    funtcion text () {
        this.x = 2;
        alert(this.x);
    }
    text(); //2
```
######  情况二、作为对象方法的调用
函数还可以作为某个对象的方法调用，这时this就指这个上级对象。
```js
    function test () {
       alert(this.x); 
    }
    var o = {};
    o.x = 1;
    o.m = text;
    o.m(); //1
```
######  情况三、作为构造函数调用
this指向构造函数，this不再是全局变量
```js
    this.x = 2;
    function text () {
        this.x = 1;
        alert(this.x) //1
    }
    let newText = new text();
    alert(newText.x) //1
    alert(x) // 2
```
###### 情况四、使用 Function.prototype 中的三个方法 call(), apply(), bind()
这三个函数，都可以改变函数的 this 指向到指定的对象，不同之处在于，call() 和 apply() 是立即执行函数，并且接受的参数的形式不同call(this, arg1, arg2, ...)，apply(this, [arg1, arg2, ...])，bind() 则是创建一个新的包装函数，并且返回，而不是立刻执行，bind(this, arg1, arg2, ...)，apply() 接收参数的形式，有助于函数嵌套函数的时候，把 arguments 变量传递到下一层函数中。
上面代码中， foo() 内部的 this 遵循默认绑定规则，绑定到全局变量中。
而 bar() 在调用的时候，调用了 apply() 函数，把 this 绑定到了一个新的对象中 {a: 2}，而且原封不动的接收 foo() 接收的函数。
```js
    function foo() {
      console.log(this.a);  // 输出 1
      bar.apply({a: 2}, arguments);
    }
    function bar(b) {
      console.log(this.a);  // 输出 2
    }
    var a = 1;
    foo(3);
```

