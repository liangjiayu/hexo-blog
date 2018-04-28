---
title: canvas技术需求
categories: canvas
tags:
  - canvas
  - JavaScript
---

### canvas技术需求

#### canvas动效原理

- 不断刷新绘制 如 这一秒小球在左边 下一秒清除画布 绘制小球在右边
- 定时器 `requestAnimationFrame`
- 兼容函数

```javascript
// requestAnimationFrame的向下兼容处理
if (!window.requestAnimationFrame) {
    window.requestAnimationFrame = function(fn) {
        setTimeout(fn, 17);
    };
}
```

- `Ball()` 构造函数 内置属性和方法
- `store` 存放对象
- `draw()` 绘制函数 根据实例属性和方法 定义下一秒的变化
- `render()` 清除画布 `draw()` 通过定时器不断绘制

```javascript
var canvas = document.querySelector('canvas');
var context = canvas.getContext('2d');

// 存储实例
var store = {};

// 实例方法
var Ball = function () {
    // 随机x坐标也就是横坐标，以及变化量moveX，以及半径r
    this.x = Math.random() * canvas.width;
    this.moveX = Math.random();
    this.r = 5 + 5 * Math.random();

    this.draw = function () {
       // 根据此时x位置重新绘制圆圈圈
       // ...
    };
};

// 假设10个圆圈圈
for (var indexBall = 0; indexBall < 10; indexBall += 1) {
    store[indexBall] = new Ball();
}

// 绘制画布上10个圆圈圈
var draw = function () {
    for (var index in store) {
        // 位置变化
        store[index].x += store[index].moveX;
        if (store[index].x > canvas.width) {
            // 移动到画布外部时候从左侧开始继续位移
            store[index].x = -2 * store[index].r;
        }
        // 根据新位置绘制圆圈圈
        store[index].draw();
    }
};

// 画布渲染
var render = function () {
    // 清除画布
    context.clearRect(0, 0, canvas.width, canvas.height);

    // 绘制画布上所有的圆圈圈
    draw();

    // 继续渲染
    requestAnimationFrame(render);
};

render();
```

#### JS基本功

- 遍历、数据存储、多维数组、this等等

#### 动画算法

#### canvas的api

- `重点` 绘图api

#### 常见的曲线函数

- 数学功底