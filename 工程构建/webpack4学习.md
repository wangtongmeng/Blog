# webpack 4 学习

课程目标

- 彻底学会 Webpack 的配置
- 理解 Webpack 的作用及原理
- 上手项目的打包过程配置
- 拥有工程化的前端思维
- 步入高级前端工程师行里

## 第 2 章 webpack 初探

### webpack 是什么

模块打包工具

- 模块相关阅读

  - documentation-concepts-modules
  - documentation-api-modules

### 安装 webapck

#### webapck 环境搭建

安装 Node 和 npm

node 版本越新，webpack 越快，webpack 会调用 node 的一些新特性加快 webpack 打包性能。

安装后，查看 node 和 npm

```shell
node -v
npm -v
```

#### webapck 全局安装

**安装 webpack**

```shel
npm install webpack webpack-cli -g
```

**查看 webpack 版本号**

查看版本号，确定安装成功

```shell
webpack -v
```

**卸载全局 webpack**

```shell
npm uninstall webpack webpack-cli -g
```

此时，通过 `webpack -v`就无法查看了

>  全局安装的坏处：若两个项目一个是 webpack 4 一个是 webpack 3，那么在全局安装 webpack 4 的情况下，3 的项目就无法运行了。

#### webapck 局部安装

进入项目目录

```shell
npm install webapck webpack --save-dev
// 或
npm install webapck webpack -D
```

安装后，确定版本号 `webpack -v`无法查看版本号，因为此命令会去全局环境下找 webpack 命令，而我们没有安装全局 webpack

查看项目中的 webpack 版本

```shell
npx webpack -v
```

查看 wbepack 历史版本

```shell
npm info webpack
```

安装老版本 webpack

```shell
npm install webpack@4.16.5 webpack-cli -D
```

### 使用Webpack的配置文件

项目根目录创建 webpack.config.js

```js
// webpack.config.js
const path = require('path')

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    // 改变输出路径需要使用 绝对路径，利用 node 的 path 模块的 resolve 方法，第一个参数 __dirname 指的是 index.js 所在目录 和 dist 结合，形成绝对路径。
    path: path.resolve(__dirname, 'dist')
  }
}
```

运行 `npx webpack` 即可。运行此命令，webpack 并不知道要如何打包，它回去找默认文件 `webpack.config.js` 获取配置信息。

**打包时，不使用默认配置文件**

```shell
npx webpack --config webpackconfig.js
```

## 第 3 章 Webpack 的核心概念

### 3-1 什么是loader



