# vue美团

## 项目简介

### 业务内容

- 首页
- 登录/注册
- 产品列表
- 产品详情
- 购物车
- 订单

### 技术内容

![vue-美团-技术内容](./img/vue-美团-技术内容.png)

### 主要内容

![vue-美团-主要内容](./img/vue-美团-主要内容.png)

## vue基础

自定义指令应用场景：一个功能没有复杂到用组件去做，又不是一个表达式能解决的，这时候用自定义指令最合适。

## 第3章 Koa2基础知识
- koa-generator
- async和await语法
- koa2中间件
- koa2路由
- cookie和session
- mongoose基础
- redis基础

### 3-1 Koa-generator

安装

```shell
npm install -g koa-generator
```

创建项目

```shell
koa2 project
```

默认是以jade模板引擎安装的

通过 -e 设置项目模板引擎是 EJS，创建项目，根据提示运行项目，就可以在localhost:3000访问了

```shell
koa2 -e project
```

如果希望改服务端代码自启动，用 `npm run dev`启动项目，对应的dev script脚本中 配置了 nodemon

关于启动脚本

start 和 test，可以直接运行 npm start 启动，而其他脚本命令必须用 npm run ...

### 3-2 Koa异步async

- 异步的概念
- 理解async和await

async 和 await：用同步的方式解决异步的问题。

await 后跟的是 Promise，若不是 Promise 会转换成 Promise

```js
router.get('/testAsync', async (ctx) => {
  global.console.log('start', new Date().getTime()) // time1
  const a = await new Promise((resolve, reject) => {
    setTimeout(function () {
      global.console.log('async a', new Date().getTime())
      resolve('a')
    }, 1000)
  })
  // const b = Promise.resolve(123)
  const b = 123


  ctx.body = {
    a,
    b
  }
  
})
```

### 3-3 Koa中间件

- koa2中间件的原理
- 自定义koa2中间件

![1562057065279](./img/koa2中间件原理.png)

**自定义koa2中间件**

创建一个中间件 middleware/koa-pv.js

```js
function pv(ctx) {
    global.console.log('pv', ctx.path)
}

module.exports = function() {
    return async function(ctx, next) {
        pv(ctx)
        await next() // next() 的作用是继续执行下一个中间件
    }
}
```

并在app.js中使用这个中间件

```js
const Koa = require('koa')
const app = new Koa()
const pv = require('./middleware/koa-pv')

app.use(pv())
```

刷新浏览器，向服务器发送请求，会输出 console.log的结果，证明中间件执行了

**koa2中间件的原理**

代码的顺序从上到下，引用的顺序可以不一样，但是都会运行到。

定义三个中间件，m1 m2 m3

```js
function m1(ctx) {
    global.console.log('m1') // m2 m3
}

module.exports = function() {
    return async function(ctx, next) {
        global.console.log('m1 start') // m2 start m3 start
        m1(ctx)
        await next()
        global.console.log('m1 end') // m2 end m3 end
    }
}
```

在app.js 中使用

```js
const Koa = require('koa')
const app = new Koa()
const pv = require('./middleware/koa-pv')

app.use(pv())
app.use(m1())
app.use(m2())
app.use(m3())
...其他中间件
```

刷新页面，服务端会打印出如下内容，运行顺序符合洋葱模型，最开始的中间件运行后，最后还是可以会运行，形成一个闭环。

![1562059619857](./img/koa洋葱模型demo结果.png)

###  3-4 koa路由和cookie

- 路由的写法
- 接口举例
- cookie 和session的定义
- cookie和session的作用

<https://github.com/ZijianHe/koa-router>

通过 `ctx.cookies.set()` 和 `ctx.cookies.get()` 方法设置和获取cookie，访问 `/` 接口时在application的cookies选项中可以看到我们设定的cookie，当访问`/json` 接口时，返回数据中有cookie，说明读取到了。

```js
router.get('/', async (ctx, next) => {
  global.console.log('index2')
  ctx.cookies.set('pvid', Math.random())
  await ctx.render('index', {
    title: 'Hello Koa 2!'
  })
})

router.get('/string', async (ctx, next) => {
  ctx.body = 'koa2 string'
})

router.get('/json', async (ctx, next) => {
  ctx.body = {
    title: 'koa2 json',
    cookie: ctx.cookies.get('pvid')
  }
})
```

## 第4章 Mongoose和Redis基础

mongoose是mongodb的对象模型管理工具，使用mongoose可以更简单的操作mongodb数据库，通过可视化工具的robo 3t的介绍，任何数据库操作都可以直观的感受到，非常利于数据库操作的学习。redis是服务端开发必备的工具之一，通过本章的学习可以快速掌握常用redis命令以及在node中的应用。

- mongodb的概念&安装
- mongodb可视化工具RoBo 3T安装及应用
- mongoose的作用
- mongoose的应用

**mongodb的概念&安装**

mongodb是非关系型数据库。

安装 mongodb

配置mongodb环境变量，<https://www.youtube.com/watch?v=sBdaRlgb4N8&feature=youtu.be&t=120>

验证安装成功 打开git bash，which mongod，显示 mongod 所在路径，证明安装成功。

再输入 mongod，启动数据库

<https://stackoverflow.com/questions/41420466/mongodb-shuts-down-with-code-100>

**mongodb可视化工具RoBo 3T安装及应用**

### 4-1 mongoose（1）

**安装 mongoose**

```shell
npm i mongoose
```

**创建数据表**

创建 dbs/，用来创建和数据库配置相关的文件。

创建dbs/config.js，用来生命数据库的配置选项。

```json
module.exports = {
    dbs: 'mongodb://127.0.0.1:27017/dbs' // 在27017端口的mongodb服务下，新创建 dbs数据库
}
```

创建 dbs/models/person.js

创建collection数据表的描述 Schema 并和模型 model 关联，并导出

注意dbs/models/person.js，这个文件名 person 就是数据表collection的名字，文件内部是表的数据。

```js
// dbs/models/person.js
const mongoose = require('mongoose') 

let personSchema = new mongoose.Schema({
    name: String,
    age: Number
})

module.exports =  mongoose.model('Person', personSchema)
```

**和数据库连接**

```js
// app.js
const mongoose = require('mongoose')
const dbConfig = require('./dbs/config')

mongoose.connect(dbConfig.dbs, {
  useNewUrlParser: true
})
```

### 4-2 mongoose（2）

数据库中的表（colection），对应 person.js 文件。

表的描述，对应 mongoose.Schema 的实例

mongoose.model相当于表和描述之间的桥梁。 

通过模型model的实例去操作数据库。

```js
// person.js
const mongoose = require('mongoose') 

let personSchema = new mongoose.Schema({
    name: String,
    age: Number
})

module.exports =  mongoose.model('Person', personSchema)
```
这里完成了数据库的一个**写操作**。
```js
// user.js
const router = require('koa-router')()
const Person = require('../dbs/models/person')

router.prefix('/users')

router.post('/addPerson', async function(ctx) {
  const person = new Person({
    name: ctx.request.body.name,
    age: ctx.request.body.age
  })
  let code
  try {
    await person.save()
    code = 0
  } catch (e) {
    code = -1
  }

  ctx.body = {
    code: code
  }

})

module.exports = router
```

测试post接口

linux命令 curl ，-d 表示 post，数据项，请求地址

```shell
 curl -d 'name=lilei&age=27' http://localhost:3000/addPerson
```

**读数据库**

这里不考虑错误的情况

这里用的是 Person 的静态方法，没用使用模型的实例。	

```js
// user.js
const router = require('koa-router')()
const Person = require('../dbs/models/person')

router.prefix('/users')

router.post('/getPerson', async function(ctx) {
  const result = await Person.findOne({name: ctx.request.body.name}) // 找到一个
  const results = await Person.find({name: ctx.request.body.name}) // 找到多个
  ctx.body = {
    code: 0,
    result,
    results
  }
})

module.exports = router
```

测试post接口

```shell
 curl -d 'name=meimei' http://localhost:3000/getPerson
```

**更新数据库**

```js
// user.js
router.post('/updatePerson', async function(ctx) {
  const result = await Person.where({
    name: ctx.request.body.name
  }).update({
    age: ctx.request.body.age
  })
  ctx.body = {
    code: 0
  }
})
```

测试post接口

```shell
curl -d 'name=meimei&age=17' http://localhost:3000/users/updatePerson
```

**删除数据库**

真正写业务是严禁删除的

```js
// user.js
router.post('/removePerson', async function(ctx) {
  const result = await Person.where({
    name: ctx.request.body.name
  }).remove()
  ctx.body = {
    code: 0
  }
})
```

测试post接口

```shell
curl -d 'name=meimei' http://localhost:3000/users/removePerson
```

### 4-3 4-4 Redis

- redis 的概念&安装
- redis 的应用场景
- redis 的用法

**cookie 与 session 的关系**

服务端的程序如何识别客户端的状态，http是没有状态的，服务器通过session识别不同的用户，session就是用来存储用户信息的，也就是服务端用session保持用户的状态，客户端用cookie保存session,服务器端把session种植在cookie中，在下次访问时，cookie会带着session给服务端，进而达到身份认证的过程。

那么，session 存储在哪里呢？redis 是一个快速读写的存储数据库，使用简单，可以用来存放session。session也可以存放在内存当中，但当数据量庞大时，内存会不够。

**redis 的概念&安装**

<https://www.runoob.com/redis/redis-install.html>

配置好redis的环境变量

**启动redis**，`redis-server`

**连接redis**，需要两个中间件

- koa-redis，使用koa-redis连接redis
- koa-generic-session，用来处理session

安装这两个中间件

```shell
npm install koa-generic-session koa-redis
```

连接redis

```js
// app.js
const Koa = require('koa')
const app = new Koa()
const session = require('koa-generic-session')
const Redis = require('koa-redis')

app.keys = ['keys', 'keyskeys']
app.use(session({ // 配置项默认是session保存在内存中的，这里需要配置保存在redis中
  store: new Redis() 
}))


module.exports = app
```

在其中一个中间件内添加，每次经过这个中间件，session的count加1

```js
ctx.session.count++
```

这里操作的session对象，并没有直接操作redis，是通过中间件操作的。

刷新页面访问，在application中就可以看到存放有session的cookie了

更改cookie的key和前缀

```js
app.use(session({
  key: 'mt',   // 自定义 key
  prefix: 'mtpr', // 自定义前缀
  store: new Redis()
}))
```

**查看存储在redis中session**

命令行 `redis-cli`，打开服务

输入 `keys *`

可以看到我们之前配置过前缀是 mtpr的session

![1562145431967](/img/redis-查看session.png)



通过 get sessionkey 可以查看对应session的value值。

之前设置经过一个中间件时，session.count++，再次请求时count+2,是因为浏览器请求了两个文件，都经过了这个中间件。

![1562145956742](./img/redis-cli查看数据.png)

**不通过中间件，直接操作redis**

不经过session读写redis

通过中间件`koa-redis` 创建redis的客户端，通过客户端直接操作redis

```js
const router = require('koa-router')()
const Redis = require('koa-redis')
const Person = require('../dbs/models/person')

// 新建 redis 客户端
const Store = new Redis().client

router.prefix('/users')

router.get('/fix', async function(ctx) {
  const st = await Store.hset('fix', 'name', Math.random())
  ctx.body = {
    code: 0
  }
})

module.exports = router
```

通过curl发送一个get请求

```shell
curl http://localhost:3000/users/fix
```

在 redis-cli 中，输入命令

`key *` 可以查看所有key，发现有fix

通过 `hget fix name` 查看value值

![1562203948176](./img/redis直接操作.png)

所以redis有两种使用场景

- 结合 session 使用
- 只是为了存储数据，保证高速读写，也可以用redis

具体redis的操作命令可以参考，redis 菜鸟 文档

## 第5章 Nuxt.js基础知识

Nuxt是Vue实现SSR最好的方案，我们整个项目都是基于Nuxt框架来实现的，我们需要了解如何通过脚手架快速初始化一个工程项目，熟悉每个目录的含义，知道如何配置各个页面的视图、模板、异步获取数据等。

### Nuxt.js 概述

基于 vue2 包含了 vue-router，可以支持 vuex 、Vue Server Render、vue-meta。

### Nust.js 工作流

![1562204744128](./img/nuxtjs工作流.png)

### Nuxt.js 安装

```shell
vue init nuxt-community/koa-template
```

使用这个模板，需要把nuxt版本降级到1.4.2

npm 切换依赖包安装源

```shell
nrm use npm 选择 npm 作为安装源
nrm ls 查看安装源
```

- 路由&示例
- 页面模板&示例
- 异步数据&示例&SSR剖析
- Vuex应用&示例

mac下eslint会提示有错误，需要更新 eslint-plugin-html，`npm i eslint-plugin-html@^3`，安装主版本是3的以上版本。

这里没有提示，暂时用主版本是2的版本。

Vue SSR 工作原理

- SSR 概述
  - 用来解决 SEO 的问题
  - 使结果快速展现
- SSR 实现原理
  - 
- Vue SSR 的渲染流程

## 第6章 实战准备

工程搭建使用Nuxt脚手架快速搭建工程，这块是通用的，所有学员都可以直接应用到自己的项目。

- 环境准备
- 项目安装
- 辅助工具安装
- 配置改装

### 6-1 环境准备与项目安装

环境准备

- node，8.12.0
- vue，2.5.17
- npm，6.4.1
- webpack，4.19.1
- nuxt，2.0.0

项目安装

1. npm install -g npx
2. npx create-nuxt-app project-name

![1562219845446](./img/create-nuxt-app配置选项.png)

###  6-2 辅助工具安装与配置改装

#### 辅助工具安装

- MongoDB
- redis
- TObo 3T

#### 配置改装

- 支持es6/7，例如 import/export
- 使用 sass
- 修改 build配置

**不识别es module语法，通过 babel 解决，顺便解决es6编译问题**

1. 修改脚本命令
2. 添加babel配置文件
3. 安装babel所需插件

1.修改脚本命令

改dev和start添加`--exec babel-node`

```json
  "scripts": {
    "dev": "cross-env NODE_ENV=development nodemon server/index.js --watch server --exec babel-node",
    "start": "cross-env NODE_ENV=production node server/index.js --exec babel-node",
  },
```

2.添加babel配置文件

在根目录创建 `.babelrc` 文件，添加如下配置

```json
{
  "presets": ["es2015", "stage-0"]
}
```

3.安装babel所需插件

先全局安装 babel-cli babel-core，否则会报内部没有 babel-node 命令

```shell
npm i babel-cli babel-core -g
```

项目安装

```shell
npm i babel-cli   // 这是babel解释器的客户端主程序 
npm i babel-core   // babel的核心文件,好像默认会自动安装
npm i babel-preset-es2015 // 把代码转换成ES6
npm i babel-preset-stage-0 // 把代码转换成ES7
```

**使用 sass**

当我们在vue文件中，使用scss语法会出错 `<style lang="scss">`

需要安装sass对应loader

```shell
npm install --save-dev node-sass sass-loader
```

重启项目生效。

**修改 build配置**

修改 nuxt.config.js

1.配置文件

添加 reset.css 和 main.css，main.css 后面会创建，这里先注释掉

```json
css: [
    'element-ui/lib/theme-chalk/reset.css',
    'element-ui/lib/theme-chalk/index.css'
    // '~assets/css/main.css'
  ],
```

2.添加缓存，增加编译速度

在build配置选项中，添加 cache: true

```json
build: {
    transpile: [/^element-ui/],
    /*
    ** You can extend webpack config here
    */
    extend(config, ctx) {
    },
    cache: true
  }
```

## 第7章 开发美团网首页

从需求分析到设计思路讲述再通过手把手的引导实现首页设计，在功能上包括城市定位服务，头部引导导航，搜索等。

### 7-1 需求分析

需求分析

- 模板设计
- 组件设计
- 数据结构设计
- 接口设计

模板设计

大多数页面可分为三大板块 header、body、footer，可作为默认模板。而像登录注册明显板式不同的可以单独出来。然后再根据具体内容，根据功能或内容等不同分类，抽象成组件。

![1562227328021](./img/美团-需求分析-模板设计.png)

组件设计

城市服务组件

![1562229150547](./img/美团-需求分析-组件设计-city.png)

用户数据&状态

![1562229408315](C:\Users\Administrator\Desktop\Blog\vue.js\img\美团-需求分析-组件设计-用户数据和状态.png)

导航标签

![1562229714544](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1562229714544.png)

这里完全可以写死

需要考虑的是

- 如何节省网络请求？
- 如何语义化？
- DOM最简化？

...

### 7-2 首页Header开发-城市定位服务设计

### 7-3 首页Header开发-头部引导导航设计

报document错误的时候，解决方案是把 nuxt.config.js 的cache设为false，cache:false

<https://github.com/nuxt/nuxt.js/issues/3804>

### 7-4 首页Header开发-搜索界面设计

### 7-5 Bug修复

### 7-6 首页搜索

### 7-7 首页菜单（1）

### 7-8 首页菜单（2）

### 7-9 章节小结

### 7-10 Footer补充