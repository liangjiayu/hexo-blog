---
title: rem
categories: CSS
tags:
  - CSS
---



### rem

- rem单位是根据html的font-size的大小定义的

### 不同设备的font-size

```javascript
// 根据设备的宽度设置htm的font-size
(function(win) {
  var winHtml = win.document.documentElement;
  var width = winHtml.getBoundingClientRect().width;
  if (width >= 640) {
    width = 640
  }
  var rem = width / 10;
  winHtml.style.fontSize = rem + 'px';
})(window)
```

### 利用sass 便利转化rem

```scss
@charset "UTF-8";
// 设计稿的分辨率
$baseDevice: 640;
// 前端切图移动端默认正常显示尺寸320
$device: 320;
// 默认html font-size
$baseFontSize: 32px;
// scss function
@function px2rem($px, $base-font-size: $baseDevice / $device * $baseFontSize) {
  @if (unitless($px)) {
    @warn "Assuming #{$px} to be in pixels, attempting to convert it into pixels for you";
    @return px2rem($px + 0px); // That may fail.
  }
  @else if (unit($px)==rem) {
    @return $px;
  }
  @return ($px / $base-font-size) * 1rem;
}
```