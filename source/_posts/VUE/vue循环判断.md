---
title: vue循环判断
categories: VUE
tags:
  - VUE
---



### 条件渲染

- `v-if`
- `v-else`
- `v-else-if`
- `<template></template>` 条件渲染一组
- `key` 声明这个元素是完全独立的
- `v-show` 控制 `display`的值

### 列表循环

#### 基本用法

```html
<div id="app">
  <template v-for="(item, index) in items">
    <h4>中国四大名著</h4>
    <p>{{index}}-{{item.book}}</p>
  </template>
</div>
```

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    items:[
      {book:'西游记'},
      {book:'红楼梦'},
      {book:'水浒传'},
      {book:'三国志'},
    ]
  }
});
```

- `template` 标签渲染多组元素

#### 对象循环

```html
<div id="app">
  <template v-for="(item,key,index) in object">
    <h4>中国四大名著</h4>
    <p>{{item}}-{{key}}-{{index}}</p>
  </template>
</div>
```

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    object:{
      book1:'西游记',
      book2:'红楼梦',
      book3:'水浒传',
      book4:'三国志',
    }
  }
});
```

#### key

- 使用循环 `v-for` 提供 `key` 需要用 `v-bind` 绑定

#### 数组更新

- 变异方法
- `push()` `pop()` `shift()` `unshift()` `splice()` `sort()` `reverse()`
- 重构数组
- `oldArray = oldArray.filter()`;

#### 显示过滤/排序结果

- 可以通过 `computed` 来创建过滤或排序后的数组

```html
<div id="app">
  <div v-for="item in evenNums">{{item}}</div>
</div>
```


```javascript
var vw = new Vue({
  el:'#app',
  data:{
    nums:[1,2,3,4,5,6,7,8,9]
  },
  computed:{
    evenNums:function () {
      return this.nums.filter(function (num) {
        return num%2 ===0;
      });
    }
  }
});
```



