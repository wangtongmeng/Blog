# 10天webpack

课程目标

- webpack常见配置
- webpack高级配置
- webpack优化配置
- ast抽象语法树
- webapck中的Tapable
- 掌握webpack流程，手写webapck
- 手写webpack中常见的plugin

## 安装

安装本地的webpack

- yarn add webpack webpack-cli -D

## 使用

```shell
npx webpack
```

## 基础配置

默认配置文件 webpack.config.js（在项目根目录创建）

```javascript
// webpack.config.js
let path = require('path')

module.exports = {
  mode: 'development', // 模式， production/development
  entry: './src/index.js', // 入口
  output: {
    filename: 'bundle.js', // 打包后的文件名
    path: path.resolve(__dirname, 'dist') // 路径必须是绝对路径，通过 node 的核心模块 path 解析
  }
}
```

这个不够详细，先不学



