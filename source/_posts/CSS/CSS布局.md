---
title: CSS布局
categories: CSS
tags:
  - CSS
---



## CSS布局

### 单页面布局

```css
/*背景*/
.container {
  background-color: #000;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
/*内容*/
.con__middle {
  background-color: #fff;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  width: 100px;
  height: 100px;
}
```

- 适合用于简单的单页面布局
- 场景 h5简单推广页 只用于手机端
- container 表示单页面的背景
- 内容需要固定宽度和高度居中
- 单位vw、vh、rem做响应式单位

### inline-block 两端布局

```css
/*列表容器*/
.container {
  width: 650px;
  margin: auto;
  text-align: justify;
  font-size: 0;
}
/*列表元素*/
.item {
  display: inline-block;
  width: 150px;
  height: 100px;
  margin-bottom: 20px;
  background-color: #000;
}
/*最后一行 让上面变为两端对齐*/
.justify_fix {
  display: inline-block;
  width: 100%;
  height: 0;
  overflow: hidden;
}
/*让最好一行向左对齐 */
.left_fix {
  display: inline-block;
  height: 0;
  margin: 0;
  overflow: hidden;
}
```

```html
<div class="container">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <!--最后一行两端对齐-->
  <span class="justify_fix"></span>
</div>
```

```html
<div class="container">
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <div class="item"></div>
  <!--最后一行左对齐-->
  <span class="item left_fix">&nbsp;</span>
  <span class="item left_fix">&nbsp;</span>
</div>
```

- `justify` 表示一行的内联元素两端对齐
- 这一行要填满一行，所以未行不会对齐

### 图片自适应

```css
.wrap {
  float: left;
  overflow: hidden;
  width: 50%;
}

.box {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
/*添加一个子元素 通内边距撑开父元素的盒子模型*/
.box::before {
  content: '';
  padding-top: 100%;
  display: block;
}
/*内容通过绝对定位来放置*/
.img-item {
  position: absolute;
  top: 0;
  max-width: 100%;
  max-height: 100%;
}
<div class="wrap">
  <div class="box">
    <img src="./head-img.jpg" alt="" class="img-item">
  </div>
</div>
```

- 原理通过子元素撑开父元素盒子
- 适用于不同大小的图片的自适应 做响应式