---
title: vue
date: 2017-06-07 11:57:00
tags:
author: lemon
---
有关vue的一些语法
## 缩写
#### v-bind缩写
```html
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
<!-- 完整语法 -->
<button v-bind:disabled="someDynamicCondition">Button</button>
<!-- 缩写 -->
<button :disabled="someDynamicCondition">Button</button>
```
#### v-on缩写
```html
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```
## 组件通信
#### 父组件通信子组件

```html
父组件
<radios :radiosData="radiosData" />
export default {
  components: {
    About,
    Radios
  },
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      radiosData: [
        {'id': 'man', 'text': '男'},
        {'id': 'woman', 'text': '女'}
      ]
    }
  },
  methods: {
    showChild: function (data) {
    }
  }
}
```
```html
子组件
<script>
  export default {
    props: ['radiosData', 'defaultID'],
    data: function () {
      return {
        checkClass: 'check',
        checkedClass: 'checked',
        id: this.defaultID
      }
    },
    methods: {
      onRadioClick: function (item) {
      }
    }
  }
</script>
```
#### 子组件通信父组件
```html
子组件：
methods: {
      onRadioClick: function (item) {
        this.id = item
        this.$emit('listenToChildEvent', this.id)
      }
    }
```
```html
父组件：
<radios :radiosData="radiosData" defaultID='man' v-on:listenToChildEvent="showChild"/>
methods: {
    showChild: function (data) {
      console.log(11)
      console.log(data)
    }
  }
```