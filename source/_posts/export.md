---
title: 一篇文章带你看懂export、export default 命令差异
date: 2020-01-09 11:19:50
tags:
---
ES6的精髓之一就是它的模块（module）体系，在使用 module 时,我们总会和 export 以及 exports 打交道，本文将给大家介绍这2点的差异点，以供大家学习。
<!-- more -->
##### 1.exports default 后面不能跟变量声明语句, export 后面可以跟变量申明语句。
本质上，export default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字。正是因为export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句。接下来，我们可以实践下。

- 首先看看 `export` 的执行情况：

	```js
	export let test1 = 'test1';
	```

	```js
	import {test1} from "./index";
	console.log(test1);
	````


	上述代码的执行结果如下：

	```js
	// test1 
	```

-  接下来，我们来看看`export default` 的执行情况

	```js
	export default let test1 = 'test1'
	```
	```js
	import test1 from "./index";
	console.log(test1);
	```
	上述代码的执行结果如下：
	```js
	// 报错。
	```


##### 2.使用export， import 需要加大括号(* 除外), export default 则不需要。
##### 3.export default 在一个模块里只能有一个，但是export可以有多个
- 首先看看 `export` 的执行情况：
```js
	let test1 = 'test1'
	let test2 = 'test2'
	export {
		test1,
		test2
	}

	```

	```js
	import {test1, test2}  from "./index";
	console.log(test1, test2);
	```
	上述代码的执行结果如下：
	```js
	// test1 test2
	```
- 接下来看看export default 的执行情况
	```js
	let test1 = 'test1'
	let test2 = 'test2'
	export default test1
	export default test2

	```

	```js
	import test1, test2 from "./index";
	console.log(test1, test2);
	```

	上述代码的执行结果如下：

	```js
	// 报错
	```

##### 4.通过export导出的属性或者方法可以修改，通过export default 导出的基本类型不可修改
- 首先看看 `export` 的执行情况：
	```js
	let test1 = 'test1'
	let test2 = {
		a: '1'
	}
	export  {
		test1,
		test2
	}
	test1 = 'test1 modify'
	test2.a = '1 modify'

```

	```js
	import {test1, test2} from "./index";
	console.log(test1, test2);
	```

	上述代码的执行结果如下：

	```js
	test1 modify {a: "1 modify"}
	```

- 接下来看看export default 的执行情况

	```js
	let test1 = 'test1'
	export default test1
	test1 = 'test1 modify'
	```

	```js
	import test1  from "./index";
	console.log(test1);
	```
	上述代码的执行结果如下：
	```js
	// test1
	```
	> 上述代码证明export导出的属性或者方法可以修改，无论是基本类型，还是引用类型。

	```js
	let test1 = {
		a: 'test1'
	}
	export default test1
	test1.a = 'test1 modify'

	```

	```js
	import test1  from "./index";
	console.log(test1);
	```

	上述代码的执行结果如下：
	```
	{a: "test1 modify"}
	```
	> 上述代码证明export default导出的属性或者方法部分可以修改，其中，基本类型无法修改