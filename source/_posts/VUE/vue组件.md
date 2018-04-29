---
title: vue组件
categories: VUE
tags:
  - VUE
---



## vue组件 [vue](https://cn.vuejs.org/v2/guide/components.html)

### 未完成

- slot 作用域插槽
- 动态组件
- 杂项
- 自定义 表单 子组件通讯
- prop验证

### 使用组件

#### 全局注册和局部注册

```html
<div id="app">
  <my-component></my-component>
  <app-component></app-component>
</div>
```

```javascript
// 全局注册
Vue.component('my-component',{
  template:'<div>this is my component</div>'
});
var vm = new Vue({
  el:'#app',
  // 局部注册
  components:{
    'app-component':{
      template:'<div>this is app-component</div>'
    }
  }
});
```

#### dom解析限制

- 比如`table`、`ul`、`ol`、 `select` 限制包围的元素可以通过 `is` 来变通

```html
<ul id="app">
  <li is="my-component"></li>
  <li is="app-component"></li>
</ul>
```

#### 组件的data必须是函数

- 每个组件的作用域都是独立的

```javascript
// 全局注册
Vue.component('my-component',{
  template:'<div>{{msg}}</div>',
  data:function () {
    return {
      msg: 'hello world vue'
    };
  }
});
var vm = new Vue({
  el:'#app',
  // 局部注册
  components:{
    'app-component':{
      template:'<div>{{msg}}</div>',
      data:function () {
        return {
          msg: 'hello world app'
        };
      }
    }
  }
});
```

#### 父元素和子元素通讯

- props 父到子
- event 子到父

### Prop

#### 基本用法

```html
<div id="app">
  <!--父模板传入数据  -->
  <my-component v-bind:child="child"></my-component>
</div>
```

```javascript
Vue.component('my-component',{
  template:'<div>{{child +" "+msg}}</div>',
  data:function () {
    return {
      msg: 'hello world vue'
    };
  },
  // 声明输入接口
  // 这个接口可以调用父模板数据
  props:['child']
});
var vm = new Vue({
  el:'#app',
  data:{
    child:"this is parent message"
  }
});
```

#### 父模板传入数据

- 字面量语法
- 传入一个字符串

```html
<div id="app">
  <my-component child="child"></my-component>
</div>
```

- 动态语法
- 绑定一条JavaScript语句

```html
<div id="app">
  <my-component v-bind:child="child"></my-component>
</div>
```

#### 单向数据流

- 父模板流进子组件 子组件不会传回给父模板
- 可以用data放置props的数据 或者计算属性 computed

```javascript
Vue.component('my-component',{
  template:'<div>{{childData}}</div>',
  props:['child'],
  data:function () {
    return {
      childData: this.child
    };
  }
});
```

### 自定义事件

```html
<div id="app">
  <p>{{total}}</p>
  <!--父模板监听子组件的自定义事件  -->
  <my-component v-on:increment="incrementTotal"></my-component>
  <my-component v-on:increment="incrementTotal"></my-component>
</div>
```

```javascript
Vue.component('my-component',{
  template:'<button v-on:click="increment">{{count}}</button>',
  data:function () {
    return {
      count:0
    };
  },
  methods:{
    increment:function () {
      this.count += 1;
      // 当子组件触发事件后 触发对应实例的自定义事件
      this.$emit('increment');
    }
  }
});
var vm = new Vue({
  el:'#app',
  data:{
    total:0
  },
  methods:{
    incrementTotal:function () {
      this.total += 1;
    }
  }
});
```

- 子组件和父模板作用域都是独立的，子组件通过自定义事件告诉父模板
- 父模板监听自定义事件，子组件完成事件后触发实例的自定义事件 `this.$emit('increment')`

### slot分发内容

#### 编译作用域

- 父模板编译的数据来自 实例
- 子组件编译的数据来自 自身的数据

#### 单个slot

- slot的定义 备用内容 父模板的中子组件的内容将会在子组件slot下编译

```html
<div id="app">
  <my-component>
    <p>slot的内容</p>
    <p>slot的内容</p>
  </my-component>
</div>
```

```javascript
Vue.component('my-component',{
  template:'<div><h2>子组件模板</h2><slot>没用内容显示我</slot></div>',
});
var vm = new Vue({
  el:'#app',
});
```

#### 具名slot

- `<slot>` 元素可以用一个特殊的属性 `name` 来配置如何分发内容

```html
<div id="app">
  <my-component>
    <h2 slot="header">这是头部内容</h2>
    <div>
      <p>这是主要内容</p>
      <p>这是主要内容</p>
      <p>这是主要内容</p>
    </div>
    <h2 slot="footer">这是底部内容</h2>
  </my-component>
</div>
```

```javascript
Vue.component('my-component',{
  template: '\
  <div class="container">\
    <header>\
      <slot name="header"></slot>\
    </header>\
    <main>\
      <slot></slot>\
    </main>\
    <footer>\
      <slot name="footer"></slot>\
    </footer>\
  </div>\
  ',
});
var vm = new Vue({
  el:'#app',
});
```



