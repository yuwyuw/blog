---
title: Vue 实现前进刷新，后退缓存处理，保留上次浏览位置
date: 2019-12-10 10:19:12
tags:
---
有这样一个需求。从A页面访问B页面，B页面需要刷新加载，从B页面返回A页面，A页面缓存处理。你会怎么处理？
场景：列表页访问详情页面后，从详情页面返回列表页面时，列表页面滚动到上次浏览的位置。方便用户继续浏览。
<!-- more -->
##### 需求分析
1.如果想要A页面停留在上次浏览的位置，必须记录离开A页面前的浏览位置。 
2.如何区分是否缓存处理？
3.A页面如何滚动到上次浏览的位置？

##### 如何Coding？
- 如何记录离开A页面前的浏览位置？
我们可以利用Vue Router 来处理, Vue Router中提供了一个名为beforeRouteLeave方法，可以处理离开页面前的一些操作。
我们可以在A页面中加入这样的一个方法，来记录当前的页面浏览位置。并保存到meta中。
```js
// A页面
beforeRouteLeave (to, from, next) {
	let position = document.documentElement.scrollTop || document.body.scrollTop
	from.meta.savedPosition = position
	next()
}
```
- 如何区分是否缓存处理？
我们依旧可以利用 Vue 的 keep-alive 组件 和 Vue 的 Router 共同处理，在根组件（以App.vue为例）中，加入下面代码。

```js
// 在Vue router中标记是否需要缓存处理
{
  name: 'A',
  path: '/a',
  component: () => import('@/pages/A'),
  meta: {
    keepAlive: true
    // keepAlive为 true表示缓存处理
  }
},

```

```html
<!-- App.vue -->
<!-- 如果路由里面的meta存在keepAlive，就缓存处理 -->
<keep-alive>
  <router-view v-if="$route.meta.keepAlive"></router-view>
</keep-alive>
<router-view v-if="!$route.meta.keepAlive"></router-view>
```

- 如何加载到上次浏览位置？
我们可以利用Vue Router中提供的一个名为[scrollBehavior](https://router.vuejs.org/zh/guide/advanced/scroll-behavior.html)的方法。
```js
scrollBehavior (to, from, savedPosition) {
  if (savedPosition) {
    return savedPosition
  } else {
    if (to.meta.savedPosition) {
    	// 如果meta信息中存在savedPosition，页面就滚动到上次浏览的位置（savedPosition）
      return { x: 0, y: to.meta.savedPosition}
    }
    return { x: 0, y: 0 }
  }
}
```