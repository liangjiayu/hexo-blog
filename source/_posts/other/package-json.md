---
title: package.json学习笔记
categories: other
tags:
  - other
---



### package.json学习笔记

```json
{
  "name": "demo",
  "version": "1.0.0", //版本
  "description": "this is demo",
  "main": "index.js",
  //npm run 命令
  "scripts": {
    "start": "webpack"
  },
  "repository": {
    "type": "git",
    "url": "liangjiayu.github.com"
  },
  "keywords": [
    "demo"
  ],
  "author": "ljy",
  "license": "ISC",
  //项目运行依赖
  // ^不改变大版本
  // 大版本 次版本 小版本
  // ~不改变小版本
  "dependencies": {
    "autoprefixer": "^6.7.7",
    "css-loader": "^0.27.3",
    "html-webpack-plugin": "^2.28.0",
    "json-loader": "^0.5.4",
    "postcss-loader": "^1.3.3",
    "style-loader": "^0.16.1",
    "webpack": "^2.3.2"
  },
  //项目开发依赖
  "devDependencies": {
    "browserify": "~13.0.0",
    "karma-browserify": "~5.0.1"
  }
}
```

### npm学习笔记

- `npm install` (packageName) [`-g` 全局]
- `npm init` 初始化项目
- `npm update`(packageName) 更新模板
- `npm uninstall` 卸载模板
- `npm instal` 安装 `package.json` 对应的依赖
- `npm run` *** 运行 `package.json` 对应的脚本指令

