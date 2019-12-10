---
title: Vue 中 $router 和 $route 的区别
date: 2019-12-10 11:10:00
tags:
---
在前端开发中，我们一直和Vue开发打交道，我们有时会运用 $router ，有时会运用 $route 你能说出其中缘由吗？
<!-- more -->
##### 什么是$route
- route 它是一条路由信息
```js
{
  name: 'scroll_index',
  path: 'scroll_behavior',
  component: () => import('@/pages/ScrollBehavior'),
  meta: {
    keepAlive: true
  }
}
```
- route 是一个局部的对象，可以获取当前对应的路由信息，比如path，query，params，meta，name等信息。
![route](/images/vue/route.jpg)

##### 什么是$router
- router 它是一组路由
```js
let routeLists = [
  {
    path: '/',
    component: () => import('@/App'),
    children: [
      {
        name: 'scroll_index',
        path: 'scroll_behavior',
        component: () => import('@/pages/ScrollBehavior'),
        meta: {
          keepAlive: true
        }
      },
      {
        name: 'scroll_catalogue',
        path: 'scroll_behavior1',
        component: () => import('@/pages/TestScrollBehavior')
      },
      {
        name: 'scroll_detail',
        path: 'scroll_behavior2',
        component: () => import('@/pages/TestScrollBehavior1')
      }
    ]
  }
]
```
- Router 可以理解为一个容器，容器里面包含了所有的 Route，也就是说 Router 是所有 Route的集合，也管理了所有的Route。
![router](/images/vue/router.jpg)
- 我们可以运用Router来实现页面的跳转以及参数传递。

```html
<router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>
```

```js
this.$router.push({ name: 'user', params: { userId: 123 }})
```
