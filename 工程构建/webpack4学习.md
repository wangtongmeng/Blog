# webpack 4 学习

课程目标

- 彻底学会 Webpack 的配置
- 理解 Webpack 的作用及原理
- 上手项目的打包过程配置
- 拥有工程化的前端思维
- 步入高级前端工程师行里

## webpack 是什么

模块打包工具

- 模块相关阅读

  - documentation-concepts-modules
  - documentation-api-modules

## 安装 webapck

### webapck 环境搭建

安装 Node 和 npm

node 版本越新，webpack 越快，webpack 会调用 node 的一些新特性加快 webpack 打包性能。

安装后，查看 node 和 npm

```shell
node -v
npm -v
```

### webapck 全局安装

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

### webapck 局部安装

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

