# Node.js 从零开发web server博客项目

## 第3章 项目介绍

课程是通过案例的形式来学习 nodejs ，本章先来介绍这个案例，即个人博客项目。包括需求分析、原型图设计、以及 server 端的技术方案设计。有了详细的设计方案，才能指导后续的实际开发。

### 3-1 项目需求分析

- 目标
  - 开发一个博客系统，具有博客的基本功能
  - 只开发 server 端，不关心前端
- 需求
  - 首页，作者主页，博客详情页
  - 登录页
  - 管理中心，新建页，编辑页
- 技术方案

总结

- 需求一定要明确，需求指导开发
- 不要纠结于简单的页面样式，并不影响 server 端的复杂度

###  3-2 技术方案

- 数据如何存储
- 如何与前端对接，即接口设计

数据存储

- 博客
- 用户

存储博客

| id   | title | content | createtime    | author   |
| ---- | ----- | ------- | ------------- | -------- |
| 1    | 标题1 | 内容1   | 1567757639968 | zhangsan |
| 2    | 标题2 | 内容2   | 1567757665307 | lisi     |

存储用户

| id   | username | password | realname |
| ---- | -------- | -------- | -------- |
| 1    | zhangsan | 123      | 张三     |
| 2    | lisi     | 123      | 李四     |

接口设计

| 描述               | 接口             | 方法 | url参数                         | 备注                           |
| ------------------ | ---------------- | ---- | ------------------------------- | :----------------------------- |
| 获取博客列表       | /api/blog/list   | get  | author 作者，keyword 搜索关键字 | 参数为空的话，则不进行查询过滤 |
| 获取一篇博客的内容 | /api/blog/detail | get  | id                              |                                |
| 新增一篇博客       | /api/blog/new    | post |                                 | post 中有新增的信息            |
| 更新一篇博客       | /api/blog/update | post | id                              | postData 中有更新的内容        |
| 删除一篇博客       | /api/blog/del    | post | id                              |                                |
| 登录               | /api/user/login  | post |                                 | postData 中有用户名和密码      |

关于登录

- 业界有统一的解决方案，一般不用再重新设计
- 实现起来比较复杂，课程后面会讲解

总结

- 明白“存储”和“接口的概念和用途”

## 第4章 开发博客项目之接口

要开发一个博客项目的 server 端，首先要实现技术方案设计中的各个 API 。本章主要讲解如何使用原生 nodejs 处理的 http 请求，包括路由分析和数据返回，然后代码演示各个 API 的开发 。但是本章尚未连接数据库，因此 API 返回的都是假数据。

- nodejs 处理 http 接口
- 搭建开发环境
- 开发接口（暂不连接数据库，暂不考虑登录）

### 4-1 http-概述

- DNS 解析，建立 TCP 连接，发送 http 请求
- server 接收到 http 请求，处理，并返回
- 客户端接收到返回数据，处理数据（如渲染页面，执行 js ）

4-2 至 4-4 nodejs 处理 http请求

- get 请求和 querystring
- post 请求和 postdata
- 路由

简单示例
```js
const http = require('http')

const server = http.createServer((req, res) => {
	res.end('hello world')
})

server.listen(8000)
// 然后浏览器访问 http://localhost:8000/
```

### 4-2 处理get请求**试看**

- get 请求，即客户端要向 server 端获取数据，如查询博客列表
- 通过 querystring 来传递数据，如 a.html?a=100&b=200
- 浏览器直接访问，就发送 get 请求

新建 http-test/

`npm init -y`，初始化 npm

打开 package.json，设置入口文件为 app.js `"main": "app.js"`

新建 app.js

```js
const http = require('http')
const querystring = require('querystring')

const server = http.createServer((req, res) => {
  console.log('method: ', req.method)
  const url = req.url
  console.log('url: ', url)
  req.query = querystring.parse(url.split('?')[1])
  console.log('query: ', req.query)
  res.end(
    JSON.stringify(req.query)
  )
})
server.listen(8000)
console.log('server is running on 8000')
```

运行，`node app.js`

浏览器输入`http://localhost:8000/api/blog/list?author=zhangsan&keyword=A`

服务端控制台

```shell
method:  GET
url:  /
query:  [Object: null prototype] {}
method:  GET
url:  /api/blog/list?author=zhangsan&keyword=A
query:  [Object: null prototype] { author: 'zhangsan', keyword: 'A' }
```

页面显示

```js
{
  "author": "zhangsan",
  "keyword": "A"
}
```

### 4-3 处理post请求

- post 请求，即客户端向服务端传递数据，如新建博客
- 通过 post data 传递数据，后面会演示
- 浏览器无法直接模拟，需要手写 js，或者使用 postman

```js
const http = require('http')

const server = http.createServer((req, res) => {
  if (req.method === 'POST') {
    // req 数据格式
    console.log('req content-type', req.headers['content-type'])
    // 接收数据
    let postData = ''
    req.on('data', chunk => {
      postData += chunk.toString()
    })
    req.on('end', () => {
      console.log('postData: ', postData)
      res.end('hello world!')
    })
  }
})

server.listen(8000)
console.log('server is running on 8000')
```

重新运行，`node app.js`

postman`http://localhost:8000/`，选择 post，body，raw，JSON(application/json)

请求数据为

```json
{
	"name": "张三",
	"age": 25
}
```

服务端控制台

```shell
req content-type application/json
postData:  {
        "name": "张三",
        "age": 25
}
```

响应 body 显示

```js
hello world!
```

### nodejs 处理路由

路由是哪一部分

| url地址                         | 路由          |
| ------------------------------- | ------------- |
| https://github.com/             | /             |
| https://github.com/username     | /username     |
| https://github.com/username/xxx | /username/xxx |

处理路由

```js
const http = require('http')

const server = http.createServer((req, res) => {
  const url = req.url
  const path = url.split('?')[0]
  res.end(path) // 返回路由
})
server.listen(8000)
```



### 4-4 处理http请求的综合示例

### 4-5 搭建开发环境
### 4-6 初始化路由
### 4-7 开发路由（博客列表路由）_1
### 4-8 开发路由（博客详情路由）
### 4-9 开发路由（处理 POSTData）
### 4-10 开发路由（新建和更新博客路由）
### 4-11 开发路由（删除博客路由和登录路由）
### 4-12 补充：路由和API