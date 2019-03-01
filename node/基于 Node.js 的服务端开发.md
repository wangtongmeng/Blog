# 基于 Node.js 的服务端开发

## Node.js介绍

### 为什么要学习 Node.js

- 企业需求
  - 具有服务端开发经验更好，可以做后端的 Java、PHP、Python、Ruby、.Net、node.js 等。
  - 全栈工程师
  - 基本的网站开发能力
    - 服务端
    - 前端
    - 运维部署

### Node.js 是什么

官网：nodejs.org

Node.js 不是一门语言、库、框架，它是一个 JS 运行时环境，简单说就是 Node.js 可以解析和执行 JS 代码，也就是说现在的 JS 可以脱离浏览器运行。

**浏览器中的 JS**

- EcmaScript
- BOM
- DOM

**Node.js 中的 JS**

- 没有 BOM、DOM
- EcmaScript
- 在 Node 这个 JS 执行环境中为 JS 提供了一些服务器级别的操作 API
  - 文件读写
  - 网络服务的构建
  - 网络通信
  - http 服务器等

**Node.js 的特点**

- event-driven 事件驱动
- non-blocking I/O model 非阻塞 IO 模型（异步）
- lightweight and efficient 轻量和高效

**Node.js 的生态系统**

npm 是世界上最大的开源库生态系统

绝大多数 JS 相关包都存放在了 npm 上，这样做的目的是为了让开发人员更方便的去下载使用。

**构建于 Chrome 的 V8 引擎之上**

- 代码只是特定格式的字符串而已
- 引擎可以认识它，引擎可以帮你去解析和执行
- Google Chrome 的 V8 引擎是目前公认的解析执行 JS 代码最快的
- Node.js 作者把 Google Chrome 中的 V8 引擎移植了过来，开发了一个独立的 JS运行时环境。

### Node.js 能做什么

- Web 服务器后台
- 命令行工具
  - npm（node）
  - git （c 语言）
  - hexo（node）
  - 。。。
- 对于前端工程师来说，接触 node 最多的是它的命令行工具。
  - 自己写的很少，主要是使用第三方的
  - webpack
  - gulp
  - npm

### 学习资源

- 《深入浅出Node.js》
  - 偏理论，几乎没有实战性内容
  - 对理解底层有帮助
- 《Node.js权威指南》
  - API 讲解
  - 没有业务和实战
- Node 入门：http://www.nodebeginner.org/index-zh-cn.html
- 官方 API 文档：https:nodejs.org/
- CNODE社区：http://cnodejs.org
- CNODE-新手入门：http://cnodejs.org/getstart

### 课程收获

- B/S 编程模型
  - Browser / Server
  - back-end
  - 任何服务端技术这种B/S 编程模型都是一样的，和语言无关
  - Node 只是学习 B/S 编程模型的一个工具
- 模块化编程
- Node 常用 API
- 异步编程
  - 回调函数
  - Promise
  - async
  - generator
- Express Web 开发框架
- es6

## 起步

###  安装 Node 环境

- 查看当前 Node 环境版本号（命令行 node --version或 node -v）
- 下载：https://nodejs.org/en/download/
- 安装
  - 已经安装过的，重新安装会升级
- 确认 Node 环境是否安装成功
  - 打开命令行，输入 `node --version`
  - 或 `node -v`
- 环境变量

### hello world

1. 创建编写 js 脚本文件
2. 打开终端，定位到脚本文件所属目录
3. 输入`node 文件名`执行对的文件

> 注意：文件名不要使用 `node.js`来命名，尽量不要使用中文命名。

### 最简单的 http 服务器

```javascript
// 使用 Node 构建一个 Web 服务器
// 在 Node 中专门提供了一个核心模块： http
// http 的职责就是创建编写服务器

// 1. 加载 http 核心模块
var http = require('http')

// 2. 使用 http.createServer() 方法创建一个服务器
//    返回一个 Server 实例
var server = http.createServer()

// 3.服务器做的事情，提供对数据的服务
//     包括接收请求、处理请求、发送响应

// 注册 request 请求事件
// 当客户端请求过来，就会自动触发服务器的 request 请求事件，然后执行第二个参数：回调函数
server.on('request', function () {
  console.log('收到客户端请求了')
})

// 4. 绑定端口号，启动服务器
server.listen(3000, function () {
  console.log('服务器启动成功，可通过 http://127.0.0.1:3000/ 来进行访问')
})
```

## Node 中的 JavaScript

- EcmaScript
- 核心模块
- 第三方模块
- 用户自定义模块

### 核心模块

Node 为 JavaScript 提供了很多服务器级别的 API， 这些 APi 绝大多数被包装到了一个具名的核心模块中了。

如，文件操作的 `fs` 核心模块，http服务构建的 `http`模块，`path`路径操作模块、`os`操作系统信息模块等。



要使用核心模块，就必须先引入它：

```javascript
var fs = require('fs')
var http = require('http')
```



## Node 中的模块系统



## 参考

[基于 Node.js 的服务端开发](https://nodejs.lipengzhou.com/)

 













