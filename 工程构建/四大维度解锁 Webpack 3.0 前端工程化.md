# 四大维度解锁 Webpack 3.0 前端工程化

## 学习准备

### 模块化

#### JS模块化

- 命名空间
- commonJS
- amd/cmd/umd
- es 6 module

#### webpack 支持

AMD（RequireJS）

ES Modules(推荐)

CommonJS

#### css模块化

- CSS 设计模式
  - OOCSS
  - SMACSS
  - Atomic CSS
  - MCSS
  - AMCSS
  - BEM

### 环境准备

- 命令行工具
  - mac下
    - Terminal
      - iTerm2: http://www.iterm2.com/
      - Zsh:http://ohmyz.sh/
      - 知乎：mac下有哪些好用的命令行工具？
- Node + Npm
- Webpack

### webpack 简介

- Webpack 概述
- Webpack 的版本更迭
- Webpack 的功能进化

#### Webapck 概述

![webpack概述](C:\Users\wangtongmeng\Desktop\Blog\img\webpack概述.png)

官网：https://webpack.js.org/

Version:

Github:https://github.com/webpack/webpack

中国官网：https://doc.webpack-china.org/

#### Webpack 版本更迭

https://github.com/webpack/webpack/releases

#### 大版本变化

Webpack v1.0.0 --- 2014.2.20

Webpack v2.20 --- 2017.1.18

Webpack v3.30 --- 2017.6.19

Webpack v4.0.0 beta ?

#### 功能进化

**Webapck V1**

- 编译、打包
- HMR(模块热更新)
- 代码分割
- 文件处理

**Webpack V2**

- Tree Shaking
- ES module
- 动态 Import
- 新的文档

**Webapck V3**

- Scope Hoisting (作用域提升)
- Magic Comments (配合动态 import 使用)

#### 版本迁移

V1 -> V2

迁移指南 https://webpack.js.org/guides/migrating/

中文版 https://webpack-china.org/guides/migrating/

V2 - V3

#### 参与社区投票

Vote: https://webpack.js.org/vote/

### 核心概念

- Entry
- Output
- Loaders
- Plugins

#### Entry

代码的入口

打包的入口

单个或多个

#### Output

打包成的文件（bundle）

一个或多个

自定义规则

#### Loaders

处理文件

转化为模块

##### 常用 Loader

编译相关：babel-loader、ts-loader

样式相关：style-loader、css-loader、less-loader、postcss-loader

文件相关：file-loader、url-loader

#### Plugins

参与打包整个过程

打包优化和压缩

配置编译时的变量

##### 常用 Plugins

优化相关

​	CommonsChunkPlugin

​	UglifyjsaWebpackPlugin

功能相关

​	ExtractTextWebpackPlugin

​	HtmlWebpackPlugin

​	HotModuleReplacementPlugin

​	CopyWebpackPlugin

#### 名词

Chunk

Bundle

Module










