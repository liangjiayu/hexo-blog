---
title: mui框架
categories: JavaScript
tags:
  - mui
  - JavaScript
---



## mui框架

### 概述

- 工具 `HBuilder` 内置mui语法提示 打包 真机检测
- `HTML5 plus` 是规范 常用的api [HTML5+](http://www.html5plus.org/doc/h5p.html)
- `Native.js` 通过js映射原生的api
- `mui` 一套css的ui框架

### 窗口管理

#### 页面初始化

- `mui.plusReady()` 放置html5+的api
- `mui.init()` 初始化参数
- `mui.ready()` dom加载完 运行函数

#### 子页面

- 在主页面下创建一个子页面 webview

```javascript
mui.init({
    subpages:[{
      url:'list.html',
      id:'list.html',
      styles:{
        top:'45px',//mui标题栏默认高度为45px；
        bottom:'0px'//默认为0px，可不定义；
      }
    }]
  });
```

#### 打开新页面

- 通过webview加载dom 动画调用原生

```javascript
mui.openWindow({
    url:'new-page-url',
    id:'new-page-id',
    styles:{
      top:
      bottom:
      width:
      height:
    },
    extras:{},
    createNew:false,//是否重复创建同样id的webview，默认为false:不重复创建，直接显示
    show:{
      autoShow:true,//自动显示
      aniShow:animationType,//动画类型
      duration:animationTime,//动画持续时间
    },
    waiting:{
      autoShow:true,//是否显示等待框
      title:'正在加载...',//等待文字
    }
})
plus.nativeUI.closeWaiting(); //关闭等待框
```

- 打开带原生导航栏的新页面
  `mui.openWindowWithTitle()`

#### 关闭页面 mui.back()

- 若当前`webview`为预加载页面，则hide当前webview；
  否则，close当前webview；
- 触发`mui.back()`情况
- 点击包含`.mui-action-back`类的控件
- 在屏幕内，向右快速滑动
- Android手机按下back按键

#### 预加载

### utils

- init() 创建子页面、关闭页面、手势事件配置、预加载、下拉刷新、上拉加载、设置系统状态栏背景颜色。
- mui() 像jquery
- each()循环 extend()合并对象 later()延迟函数 scrollTo() os 环境属性

## 页面传值

### 本地存储

```javascript
//读取本地存储
var foo = plus.storage.getItem(key);
//存储在本地存储
plus.storage.setItem(key,value);
//删除本地存储
plus.storage.removeItem(key);
```

- 原理把数据存储在本地中
- 在新页面通过key读取出来
- 适用场景打开新页面

### 打开新页面

```javascript
//打开新页面
mui.openWindow({
  url:url,
  id:id,
  //传递的值
  extras:{
    targetId:targetId
  }
})
```

```javascript
//新页面读取数据
var self = plus.webview.currentWebview();
var targetId = self.targetId;
```

- 适用场景 在列表页跳转到详情页

### 自定义事件

```javascript
//填写页面
//触发的页面
ws = plus.webview.getWebviewById('back');
//触发事件 目标 自定义事件名称 传递值
mui.fire('ws','updata',{
  id:id
});
```

```javascript
//返回页面
//添加自定义事件监听
window.addEventListener('updata',function(event){
  var id = event.detail.id;
});
```

- 适用场景页面已经创建
- 从填写页面 更新内容到 目标页面 并且页面需要更新内容

### 页面显示监听

```javascript
var ws=plus.webview.currentWebview();
ws.addEventListener("show", function(e){
    console.log( "Webview Showed" );
}, false );
```

