---
title: 你会如何处理这样的需求
date: 2018-01-10 14:32:14
tags:
author: lemon
---
当你遇到“函数有一个参数n，返回值是一个数组，数据随机不重复，返回n个整数取值范围是2-32”，你会如何处理。
<!-- more -->
这个题目很简单，却有很多的小细节需要考虑到。
1.参数n一定存在嘛？如果不存在会怎样？
2.参数n的数据格式一定正确嘛？如果是n是负数、0、浮点数、String类型的数字会怎样？
3.有验证返回的数据随机不重复嘛？
4.随机数的取值范围是2-32嘛？
5.如果修改随机数的取值范围，你的函数需要大幅度修改嘛？
以下是我的代码
```js
    function random (n) {
      let numberlist = [],min = 2, max = 32;
      if (!checkParameter(n)) return numberlist;
      for (let i = 0; i < n; i++) {
        let random = getRand(min,max)
        checkInArr(numberlist,random) ? i-- : numberlist.push(random);
      }
      return numberlist;
    }
    function checkParameter(n) {
      let boolean  = !! (n && typeof Number(n) === 'number')
      return boolean
    }
    function getRand (min,max) {
      return Math.floor(Math.random()*(max-min+1)+min);
    }
    function checkInArr (arr, random) {
      return arr.includes(random)
    }
    random(6);
```
其实写代码本身是简单的，但是涉及以下几个方面，可能就没有那么简单了。
「安全」指代码执行性，我们写出的代码首先需要保证可以执行，一旦缺少这个前提，其他都是无用功。
「可用」指满足需求性，我们写出的代码需要满足需求，这样才是一段及格的代码。
「健壮」指处理多元性，我们写代码的时候需要去处理不同的场景，如兼容处理、边界处理、用户验证处理、异常处理、隐藏逻辑处理等。
「宽容」指角色包容性，我们写代码需要对需求宽容、对用户宽容、对维护者宽容、对调用者宽容。
若我们能做到这些，才是一名有钱途的开发者。