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

本章讲解 Webpack 中的一些核心概念，从 Loader 与 Plugin 开始，带你学明白 Webpack 的运行机制，然后逐步深入，扩展衍生出 SoureMap， HMR， WDS 等常见概念。本章课程学习过程中，额外增加了对 Webpack 官方文档的查阅方式讲解，帮助大家学会查阅文档。...

### 3-1 什么是loader

webpack 是什么？模块打包工具

模块是什么？不只是js、css和图片等其他任何内容。

webpack配置文件的作用是什么？答案在前面

使用 file-loader 做 jpg 文件的打包

打包流程：

- 命令行 `npm run bundle`，执行 package.json  中的 script ，运行 bundle 命令，实际上是运行 webpack。
- webpack 找它的配置，根据配置打包。
  - 遇到 js文件，默认可以处理 js文件。
  - 当遇到 jpg 图片文件，webpack 默认不知道如何打包，会去配置中找相应规则

### 3-2 使用 Loader 打包静态资源（图片篇）







