---
title: vue基础
categories: VUE
tags:
  - VUE
---



## vue实例 [官方文档](https://cn.vuejs.org/v2/guide/)

### vue构造器

```javascript
var vm = new Vue({
  //选项
});
```

### 属性与方法

```javascript
var vm = new Vue({
  el:'#app',
  data:{
    a:1,
    b:2
  }
});
vm.$watch(); //实例方法
vm.$el //实例属性
```

### 生命周期钩子函数

- `beforeCreate` 实例新建完调用
- `created` 初始化data、方法 调用
- `beforeMount` 模板el编译前 调用
- `mounted` 模板el编译后调用
- `beforeUpdate` 组件数据更新前调用
- `updated` 组件数据更新后调用
- `beforeDestroy` 组件销毁前调用
- `destroy` 组件销毁后调用

### 用途

- `beforeCreate` 可以添加 loading 事件
- `created` 在模板编译之前 做一些初始化
- `mounted` 向后台请求，获取数据
- `beforeDestroy` 删除组件调用函数

## 模板语法

### 插值

- `v-text` 插入文本 双大括号
- `v-html` 插入html
- `v-bind` 绑定属性
- 可以使用`JavaScript`表达式

```html
<div >{{msg+1}}</div>
<div >{{ok?'yes':'no'}}</div>
<span v-bind:id="'java-'+ id"></span>
```

### 指令

- `v-bind`: 参数. 修饰符 = “javascript表达式”
- 缩写 `:` === `v-bind` `@` === `v-on`

### 过滤器 filters

- 可以在 双括号 和 `v-bind` 中使用

```html
<span>{{msg | filtersFun}}</span>
<span v-bind:id="msg | filtersFun"></span>
```

- filters 函数第一参数的值为 msg

```javascript
var vm = new Vue({
  filters:{
    filtersFun:function (value,arg1,agr2) {
      value = value.toString();
      return value;
    }
  }
});
```

## 计算属性

### 基础例子

```javascript
var vm = new Vue({
  el:'app',
  data:{
    msg:'hello world'
  },
  computed:{
    reverseMsg:function () {
      return this.msg.split('').revers().join('');
    }
  }
});
```

- reverseMsg 的值是根据msg响应的 msg是它的依赖

### 计算属性和method

- 计算属性是根据msg做响应 有缓存的
- method 是重新渲染 调用函数

### watch

- 定义 当某个数据变化时引起其他数据一起变化

```javascript
var vm = new Vue({
  el:'app',
  data:{
    firstName:'123',
    lastName:'456',
    fullName:'123 456'
  },
  computed:{
    fullName:function () {
      return  this.firstName+' '+this.lastName;
    } //使用计算属性更简洁
  },
  watch:{
    firstName:function (value) {
      this.fullName = value +' '+this.lastName;
    },
    lastName:function (value) {
      this.fullName = this.firstName+' '+value;
    }
  }
});
```

- 当数据变化后需要调用异步请求要使用watch

```javascript
var vm = new Vue({
  el:'app',
  data:{
    question:'',
    answar:'123'
  },
  watch:{
    question:function () {
      this.answar = 'question is change';
      this.getAnswar(); //异步请求数据
    }
  },
  methods:{
    getAnswar:function () {
      var self = this;
      axios.get('url') //axios一个异步请求插件
        .then(function (response) {
          self.answar = response.data.answar;
        })
        .catch(function (error) {
          self.answar = 'Error '+error;
        })
    }
  }
```

