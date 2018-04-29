---
title: vue表单控件
categories: VUE
tags:
  - VUE
---



### 基本用法

#### 文本

```html
<div id="app">
  <input type="text" v-model="msg">
  <p>{{msg}}</p>
</div>
```

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    msg:''
  },
});
```

#### 复选框

- 绑定字符串 表示 `逻辑`

```html
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```

- 绑定数组 表示 `value`

```html
<div id="app">
  <input type="checkbox" v-model="checkName" value="input-1">
  <input type="checkbox" v-model="checkName" value="input-2">
  <input type="checkbox" v-model="checkName" value="input-3">
  <p>{{checkName}}</p>
</div>
```

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    checkName:[]
  },
});
```

#### 单选

- 绑定是value

```html
<div id="app">
  <label for="">one</label>
  <input type="radio" v-model="picker" value="one">
  <label for="">two</label>
  <input type="radio" v-model="picker" value="two">
  <p>{{picker}}</p>
</div>
```

```javascript
var vw = new Vue({
  el:'#app',
  data:{
    picker:''
  },
});
```

### 绑定value

```html
<input type="radio" v-model="pick" v-bind:value="a">
```

- 当选中时，`value`等于数值 `vm.a`

### 修饰符

- `.lazy` 同步数据
- `.number` 转为数字
- `.trim` 去除空格



