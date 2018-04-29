---
title: node学习笔记
categories: node
tags:
  - node
  - JavaScript
---



## node学习笔记

### 简介

#### 异步操作

- JavaScript是`单线程`运行 `node`采用大量的异步操作
- 异步就像发短信,发完短信要等别人回复我,回复后我做出响应,等待中我可以继续打电话(同步)
- 回调函数 默认参数一为 错误对象

#### 全局变量和方法

- `global` 全局环境
- `console` 打印
- `process` 当前进程
- setTimeout() clearTimeout() setInterval() clearInterval()
- `require()` 加载模块
- `Buffer()` 操作二进制数据

### 模块化

- `require()` 加载模块 默认路径扩展名 `.js`

#### 核心模块

- `http` 提供HTTP服务器功能
- `url` 解析URL
- `fs` 与文件系统交互
- `querystring` 解析URL的查询字符串
- `child_process` 新建子进程
- `util` 提供一系列实用小工具
- `path` 处理文件路径
- `crypto` 提供加密和解密功能，基本上是对OpenSSL的包装

#### 自定义模板

- 输出模块再通过`require`使用
- `module.exports` = foo;
- `exports.foo` = foo;

### 异常处理

#### 回调函数

- 回调函数 第一个参数默认为错误对象

```javascript
fs.readFile('/foo.txt', function(err, data) {
  if (err !== null) throw err;
  console.log(data);
});
```

- `'/foo.tet'` 是异步操作 通过回调函数来捕获异常

```javascript
//定义async2 异步操作并抛出异常信息
function async2(continuation) {
  setTimeout(function() {
    try {
      var res = 42;
      if (true)
        throw new Error("woops!");
      else
        continuation(null, res); // pass 'null' for error
    } catch(e) {
      continuation(e, null);
    }
  }, 2000);
}
//通过回调函数 处理异常信息
async2(function(err, res) {
  if (err)
    console.log("Error: (cps) failed:", err);
  else
    console.log("(cps) received:", res);
});
// Error: (cps) failed: woops!
```

------

## CommonJS

### 概述

- `node.js` 采用`commonjs`模块规范 每一个文件就是一个模块 有自己的作用域
- `require()` 加载模块
- `module.exports`.*** 输出模块

#### 特点

- 所有代码都运行在模块作用域，不会污染全局作用域。
- 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存
- 模块加载的顺序，按照其在代码中出现的顺序

### module对象

- `node`每个模板内置一个`modul`对象 有几个属性

#### modul.exports

- 定义 表示模块的输出 一个模块(文件)只有一个出口
- `node`为每一个模块内置`exports`变量 指向`module.exports`

```javascript
var exports = module.exports;
```

- 可以只用`module.exports`来输出函数

### require命令

- 基本用法 `var foo = require('foo.js');`

#### 目录加载

- 目录中放置`package.json` `require()`会根据`main` 加载文件目录

```javascript
{
  "name" : "some-library",
  "main" : "./lib/some-library.js"
}
```