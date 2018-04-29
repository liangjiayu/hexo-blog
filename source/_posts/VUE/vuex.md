---
title: vuex
categories: VUE
tags:
  - VUE
---



### [vuex](https://vuex.vuejs.org/zh-cn/)

- vuex是状态管理工具
- vuex的核心是store(仓库)
- 只能通过commit的方法 改变store中的state(状态)

## api概述

### vuex.store

```javascript
import Vuex from 'vuex'
const store = new Vuex.Store({ ...options })

// 注册仓库
export default new Vuex.Store({
  state,
  mutations,
});
```

### stare 状态

#### 定义

```javascript
const state = {
  count: 1
};
```

#### 组件获得stare的方法

```javascript
//方法一 计算属性 保存
computed: {
  count(){
    return this.$store.state.count;
  }
},
// 方法二 mapStare 辅助函数
import { mapState } from 'vuex';
computed: {
  ...mapState(['count'])
}
```

### mutations 改变

- 定义 改变仓库的状态的方法

#### 定义

```javascript
const mutations = {
  // 第一参数默认为state,n为参数
  add(state,n) {
    state.count+=n;
  },
  reduce(state) {
    state.count--;
  }
};
```

#### 使用

```javascript
//第一种方法
methods: {
  add(n) {
    this.$store.commit('add', n);
  }
}
//第二种通过辅助函数
import { mapMutations } from 'vuex';
methods: {
  ...mapMutations(['add', 'reduce'])
}
```

### Getters 计算属性

#### 定义

```javascript
const getters = {
  todo:(state) => {
    return state.count += 50;
  }
};
```

#### 使用

```javascript
//第一种
todo() {
  return this.$store.getters.todo
}
//第二种
import { mapGetters } from 'vuex';
computed: {
  ...mapGetters(['todo'])
}
```

