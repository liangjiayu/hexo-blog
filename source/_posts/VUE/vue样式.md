---
title: vue样式
categories: VUE
tags:
  - VUE
---



## vue样式绑定

- class和style强化 数组和对象

### class对象语法

```html
<div v-bind:class="{active:isActive,error:isError}" class="box"></div>
```

```javascript
var vm = new Vue({
  el:'app',
  data:{
    isActive:true,
    isError:true
  }
});
```

```html
<div  class="box active error"></div>
```

- 可以通过强大的计算属性 返回一个对象 绑定 `class`

```javascript
var vm = new Vue({
  data:{
    isActive:true,
    isError:true  
  },
  computed:{
    classObj:function () {
      return {
        active:this.isActive,
        error:this.isError
      }
    }
  }
})
```

### class数组语法

```html
<div v-bind:class="[{active:isActive},errorClass]"></div>
```

```javascript
var vm = new Vue({
  data:{
    activeClass:'active',
    errorClass:'error'
  }
})
```

### style对象语法

```html
<div v-bind:style="styleObj"></div>
```

```javascript
data:{
  styleObj:{
    color:'red',
    fontSize:'16px'
  }
}
```

### style数组语法

```html
<div v-bind:style=[styleObj,baseObj]></div>
```





