---
title: select自定义样式
categories: CSS
tags:
  - CSS
---



## select自定义样式

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-tap-highlight-color: transparent;
}

.con {
  width: 500px;
  margin: 50px auto;
}

.select-wrap {
  position: relative;
  display: block;
  width: 300px;
  background-color: #fff;
}

.select {
  /*层级*/
  position: relative;
  z-index: 1;
  width: 100%;
  height: 45px;
  padding: 0 30px 0 15px;
  line-height: 45px;
  outline: 0;
  border: 1px solid #000;
  font-size: 17px;
  /*透明显示底层的icon*/
  background-color: transparent;
  /*去除默认样式*/
  -moz-appearance: none;
  -webkit-appearance: none;
  -ms-appearance: none;
}

select::-ms-expand {
  /*id默认样式 支持ie10*/
  display: none;
}

.select-icon {
  position: absolute;
  top: 50%;
  right: 15px;
  width: 15px;
  height: 15px;
  margin-top: -7.5px;
  background-color: #ccc;
}
```


```html
<div class="con">
  <div class="select-wrap">
    <select class="select">
      <option value="">名字</option>
      <option value="">小明</option>
      <option value="">小红</option>
      <option value="">小方</option>
    </select>
    <div class="select-icon"></div>
  </div>
</div>
```