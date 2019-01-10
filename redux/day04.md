# dva 简介

### 1. 核心概念

- state
- action
- 

### 2. 基本应用

安装dva脚手架

```shell
$ npm install dva-cli -g
```

使用脚手架构建项目

```shell
$ dva new dva-quickstart
$ cd dva-quickstart
$ npm start
```

安装antd以及babel-plugin-import

```shell
$ npm install antd babel-plugin-import --save
```

编辑`.webpackrc`，使 `babel-plugin-import` 插件生效

```javascript
{
  "extraBabelPlugins": [
    ["import", { "libraryName": "antd", "libraryDirectory": "es", "style": "css" }]
  ]
}
```

