---
title: vue响应式原理
categories: VUE
tags:
  - VUE
---



## vue响应式原理 [vuejs](https://cn.vuejs.org/v2/guide/reactivity.html)

### 原理

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    message:'123'
  }
});
```

- 先把`data`封装 可以`getter`、`setter`
- 通过`watch`观察数据变化 告诉 `renderFun()` 改变 `dom`
- `dom` => `touch` => `data` => `watch` => `renderFun` => `dom`

### 声明响应式属性

- vue不允许动态添加根级响应式属性

- 可以通过set(this.someObj,key,value) 给根级响应式属性 添加属性

- 添加一些属性

  ```javascript
  this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })
  ```

### 异步更新队伍

- `oldvalue` => `newvalue` => `异步(promise.then)(去除重复)` => `更新dom`
- `nextTick()` 数据更新 dom更新完成 调用回调函数



