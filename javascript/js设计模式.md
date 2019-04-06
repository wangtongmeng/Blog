# js 设计模式

## 导学

一名合格工程师必备的条件：前端开发有一定的设计能力

论工程师	的设计能力

- 3年工作经验，面试必考设计能力
- 称为项目技术负责人，设计能力是必要基础
- 从写好代码，到做好设计，设计模式是必经之路

前端学习设计模式的困惑

- 网上的资料都是针对 java 等后端语言的
- 看懂概念，但是不知道怎么用，看完就忘
- 现在的 JS 框架，刀子都用了那些设计模式

课程概述

- 做什么？——讲解 JS 设计模式
- 哪些部分？——面向对象，设计原则，设计模式
- 技术？——面向对象，UML类图，ES6

知识点介绍

- 面向对象
  - ES6 class 语法
  - 三要素
  - UML 类图
- 设计原则
  - 何为设计？
  - 5 大设计原则
  - 从设计到模式
- 设计模式
  - 分优先级讲解
  - 结合核心技术
  - 综合框架应用
- 综合应用
  - 设计方案
  - 代码演示
  - 设计模式对应

课程安排

- 面向对象
  - 使用 webpack 和 babel 搭建 ES6 编译环境
  - ES6 class 面向对象的语法
  - 面向对象三要素：继承、封装、多态
- 设计原则
  - 通过《LINUX/UNIX设计哲学》理解何为设计
  - 5 大设计原则分析和理解，以及代码演示
  - "设计模式" ->从"设计"到"模式"
- 设计模式
  - 概述：创建型、结构型、行为型
  - 常用设计模式，详细讲解，结合经典使用场景
  - 非常用设计模式，理解概念，示例演示
  - 有主有次，掌握重点
- 综合示例
  - 用 jQuery 实现一个简单的购物车
  - 设计分析，画 UML 类图
  - 代码演示
  - 总结使用的 7 种设计模式

课程收获

- 面向对象思想，UML 类图
- 5 大设计原则，23中设计模式
- 能应对前端面试中相关的面试题
- 提升个人设计能力

## **第2章 面向对象**

讲解javascript中的面向对象的概念，包括 ES6 class 语法、UML 类图、以及面向对象三要素

### 搭建开发环境

- 初始化 npm 环境
- 安装 webpack
- 安装 webpack-dev-server
- 安装 babel

**初始化 npm 环境**

```shell
npm init -y
```

**安装 webpack**

在本项目开发环境下安装 webpack，并保存依赖

```shell
npm install webpack webpack-cli --save-dev
```

配置 webpack

根目录创建 webapck.dev.config.js

指定入口文件和出口文件

```js
module.exports = {
  entry: './src/index.js',
  output: {
    path: __dirname, // __dirname 指当前目录
    filename: './release/bundle.js'
  }
}
```

package.json 中指定打包命令行

`npm run dev`时，执行 webpack 命令，配置文件为 webpack.dev.config.js，模式为  development

```shell
"scripts": {
    "dev": "webpack --config ./webpack.dev.config.js --mode development"
  },
```

这时，运行 `npm run dev`，可以完成基本的打包操作。

**安装 webapck-dev-server**

在开发环境下安装 webpack-dev-server 和 html-webpack-plugin，并保存依赖

```shell
npm install webpack-dev-server html-webpack-plugin --save-dev
```

配置 webpack-dev-server

webpack.dev.config.js 添加配置

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  ...,
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html' // 最终渲染模板文件
    })
  ],
  devServer: {
    contentBase: path.join(__dirname, './release'), // 监听目录
    open: true, // 自动打开浏览器
    port: 9000 // 端口
  }
}
```

package.json 脚本命令调整,webpack 改为 webpack-dev-server

```shell
"scripts": {
    "dev": "webpack-dev-server --config ./webpack.dev.config.js --mode development"
  },
```

这时，运行 `npm run dev`，当我们修改js代码，webpack会帮助我们实时修改打包后的文件

**安装 babel**

```shell
npm install babel-core babel-loader@7 babel-polyfill babel-preset-es2015 babel-preset-latest --save-dev 
```

根目录创建 .babelrc 配置文件

```json
// .babelrc
{
  "presets": ["es2015", "latest"],
  "plugins": [] 
}
```

配置 webpack.dev.config.js

```js
module.exports = {
  module: {
    rules: [{
      test: /\.js?$/,
      exclude: /(node_modules)/,
      loader: 'babel-loader'
    }]
  },
}
```

这时，命令行运行`npm run dev`，就可以编译 es6 语法了。

### 面向对象

- 面向对象的概念
- 三要素：继承 封装 多态
  - 继承，子类继承父类
  - 封装，数据的权限和保密
  - 多态，同一接口不同实现
- JS 的应用举例
- 面向对象的意义

**什么是面向对象**

类即模板

```js
// 类，即模板
class People {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  eat() {
    alert(`${this.name}, eat sth`)
  }
  speak() {
    alert(`My name is ${this.name}, age ${this.age}`)
  }
}
```

对象（实例）

```js
// 创建实例
let zhang = new People('zhang', 20)
zhang.eat()
zhang.speak()
// 创建实例
let wang = new People('wang', 21)
wang.eat()
zhang.speak()
```

**面向对象-继承**

People 是父类，公共的，不仅仅服务于 Student

继承可将公共方法抽离出来，提高复用，减少冗余

```js
// 父类
class People {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  eat() {
    alert(`${this.name}, eat sth`)
  }
  speak() {
    alert(`My name is ${this.name}, age ${this.age}`)
  }
}
// 子类继承父类
class Student extends People {
  constructor(name, age, number) {
    super(name, age) // name 和 age 有高级类处理
    this.number = number
  }
  study() {
    alert(`${this.name} study`)
  }
}

let xiaoming = new Student('xiaoming', 10, 'A1')
xiaoming.study()
alert(xiaoming.number)
xiaoming.eat()

let xiaohong = new Student('xiaohong', 11, 'A2')
xiaohong.study()
```

**面向对象-封装**

- public 完全开放
- protected 对子类开放
- private 对自己开放
- (ES6 尚不支持，可用 typescript 演示)，在线ts代码运行,http://www.typescriptlang.org/play/

特点

- 减少耦合，不该外露的不外露
- 利用数据、接口的权限管理
- ES6 目前不支持，一般认为 _ 开头的属性是 private

```typescript
class People {
    name
    age
    protected weight // 受保护的属性，只有自己或子类可以访问
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  eat() {
    alert(`${this.name}, eat sth`)
  }
  speak() {
    alert(`My name is ${this.name}, age ${this.age}`)
  }
}
// 子类继承父类
class Student extends People {
    number
    private girlfriend
  constructor(name, age, number) {
    super(name, age) // name 和 age 有高级类处理
      this.number = number
      this.girlfriend = 'xiaoli'
  }
  study() {
    alert(`${this.name} study`)
    }
    getWeight() {
      alert(`weight ${this.weight}`)
  }
}

let xiaoming = new Student('xiaoming', 10, 'A1')
xiaoming.getWeight()
// alert(xiaoming.weight) // 报错，weight是protected，只能在类及子类中访问
// alert(xiaoming.girlfriend) // 报错，girlfriend是私有属性，只能在类内访问
```

**面向对象-多态**

- 同一个接口，不同表现
- JS 应用极少
- 需要结合 java 等语言的接口、重写、重载等功能

特点

- 保持子类的开放性和灵活性
- 面向接口编程
- (JS 引用极少，了解即可)

```js
class People {
  constructor(name) {
    this.name = name
  }
  saysomething() {

  }
}

class A extends People {
  constructor(name) {
    super(name)
  }
  saysomething() {
    alert('I am A')
  }
}

class B extends People {
  constructor(name) {
    super(name)
  }
  saysomething() {
    alert('I am B')
  }
}

let a = new A('a')
a.saysomething()
let b = new B('b')
b.saysomething()
```

**JS 应用类型**

- jQuery 是一个 class
- $('p') 是 jQuery 的一个实例

```js
class jQuery {
  constructor (selector) {
    let slice = Array.prototype.slice
    let dom = slice.call(document.querySelectorAll(selector))
    let len = dom ? dom.length: 0
    for (let i = 0; i < len; i++) {
      this[i] = dom[i]
    }
    this.length = len
    this.selector = selector || ''
  }
  append (node) {

  }
  addClass (name) {

  }
  html (data) {

  }
  // 此处省略 N 个 API
}

window.$ = function (selector) {
  return new jQuery(selector)
}
// 由于加载顺序的问题，暂时写在一个文件中
let $p = $('p')
console.log($p)
console.log($p.addClass)
```

**为何使用面向对象？**

- 程序执行：顺序、判断、循环——结构化
- 面向对象——数据结构化
- 对于计算机，结构化才是最简单的
- 编程应该 简单 & 抽象

### UML 类图

- Unified Modeling Language 统一建模语言
- 类图，UML 包含很多种图，和本课相关的是类图
- 关系，主要讲解泛化和关联

**画图工具**

- MS Office visio
- https://www.processon.com/

**类图**

![uml类图](./img/uml类图.png)

```js
// 类，即模板
class People {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  eat() {
    alert(`${this.name}, eat sth`)
  }
  speak() {
    alert(`My name is ${this.name}, age ${this.age}`)
  }
}
```

![people-uml类图](./img/people-uml类图.png)

 **关系**

- 泛化，表示继承
- 关联，表示引用

```js
class People {
  constructor (name, house) {
    this.name = name
    this.house = house
  }
  saySomething () {
    
  }
}
class A extends People {
  constructor (name, house) {
    super(name, house)
  }
  saySomethin () {
    alert('I am A')
  }
}
class B extends People {
  constructor (name, house) {
    super(name, house)
  }
  saySomething () {
    alert('I am B')
  }
}
class House {
  constructor (city) {
    this.city = city
  }
  showCity () {
    alert(`house in ${this.city}`)
  }
}
let aHouse = new House('beijing')
let a = new A('a', aHouse)
let b = new B('b')
b.saySomething()
```

A 和 B 继承了 People，用空心箭头表示；People 引用了 House，用实心箭头表示。

![uml类图-关系](./img/uml类图-关系.png)

### 总结

- 搭建开发环境： npm init、webpack、babel
- 面向对象：概念、三要素、应用举例、意义
- UML类图：类图、关系、示例