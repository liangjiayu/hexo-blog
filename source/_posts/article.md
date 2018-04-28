---
title: 模板
categories: CSS
tags:
  - CSS
  - HTML
---



## 这是一个模板



```javascript
/* global hexo */

var merge = require('./merge');

/**
 * Merge configs in _data/next.yml into hexo.theme.config.
 * Note: configs in _data/next.yml will override configs in hexo.theme.config.
 */
hexo.on('generateBefore', function () {
  if (hexo.locals.get) {
    var data = hexo.locals.get('data');
    data && data.next && merge(hexo.theme.config, data.next);
  }
});
```

<!-- more -->