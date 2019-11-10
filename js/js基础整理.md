# js 基础整理

## 前端发展史

### WEB1.0时代：静态网页

### WEB2.0时代：动态网页的崛起（服务端渲染时代 ）

- 问题1：服务器压力过大
- 问题2：同步非异步刷新，页面中某一个数据想要更改，只能重新刷新整个页面（全局刷新）
- 问题3：不利于团队协作开发

### ajax时代：前后端分离的雏形，异步渲染大显神通（客户端渲染时代）

- 导致后期，跨域策略请求方案（JSONP、IFRAME、CORS、DOMAIN、POXY、SCOKET..）以及FETCH等新通信方案的不断崛起。

![1573314189412](./img/前端发展史-客户端时代.png)

### node 崛起：JS 成为最为热门全栈开发技术

前端侵占移动端APP市场

- 原生APP（Native App）
  - 优势：
    - 性能好
    - 功能强大（可以调用手机软件硬件）
  - 弊端：
    - 不能跨平台、成本大
    - 不能同步
- Web App（H5页面）==>响应式布局开发
  - 优势：
    - 跨平台
    - 及时更新
  - 弊端：
    - 性能相对不好
    - 功能没有那么强大
- 混合开发

前端未来发展预估

- 小程序是企业产品的重要组成部分
- iOS和安卓开发逐步被淘汰
- VR/AI最终转为B端（JS，尤其是webGL、canvas、three.js等是3D虚拟交互的主要实现技术） 
- H5游戏/小游戏的热度会提高（白鹭JS引擎 ）
- NODE.js还会迎来下一个高潮

## 需要的技术栈

当下前端开发的技术体系

1.HTML5+CSS3。

2.JS 包括E6核心原理

JS堆栈内存、闭包作用域、浏览器词法解析（V8渲染机制原理） 、面向对象和this处理（主要是独立封装组件和插件，研究常用类库的源码）

ES6基础语法（包括class类的继承封装和多态） 、ES6中的Promise(及 Promise A+规范)、Generator生成器函数等深入用法

同步异步编程（包括运行机制和微任务、宏任务，以及实战应用）

常用的编程思想和设计模式：函数的防抖和节流、柯理化函数、惰性函数、单例设计模式、发布订阅模式、Promise 设计模式等

DOM性能优化（重排和重绘的优化）、DOM事件

前端编程常规算法：去重、冒泡排序、插入排序、快速排序、递归等

3.ajax和http

技术要点：ajax原理、ajax异步解决方案（promise）、axios(包括自己封装promise版ajax库)、fetch及封装处理、jquery中的ajax操作和库的封装等

跨域解决方案及实现原理：jsonp、cors、webpack proxy(socket.io)、document.domain、window.name+iframe、postMessage等

HTTP报文（常用的响应请求头实战应用技巧）、HTTP（TCP）传输流程（包括三次握手四次挥手及TCP底层协议）、HTTP1和HTTP2的区别、HTTP和HTTPS的区别等

 HTTP相关优化手段是性能提高的重要方法（如：304缓存、DNS缓存、减少HTTP传输次数和大小、HTTPS的加密等 ） 

4.框架开发

vue全家桶：vue(MVVM实现的原理以及一些语法实现的原理)、vue-router(HASH路由实现的原理)、vuex(掌握原理)、axios、vue-cli(需要能够修改脚手架的webpack配置项)、iview/vux/vue element 等常用框架的使用

react全家桶：create-react-app（能够修改webapck的配置项）、react(掌握虚拟DOM渲染原理，掌握DOM-DIFF原理，掌握iNDEX索引对比机制，掌握MVC实现的原理)、react-dom/react-native、react-router、react-redux/dva/mobx（掌握原理，自己可以基于原生JS写一套类似的插件、发现里面的一些不足点）、antd(最好可以自己封装一些基础的组件)等

5.辅助技能

webapck:掌握常用的脚手架使用和修改，会一些基础的webpack搭建

Git

Node：掌握基础的API、掌握express/koa/egg等框架、可以编写伪API，可以基于node做跨域处理等

Canvas：可视化，需掌握canvas/webGL/d3等，对数学结构、算法有要求 

## 浏览器的内核和控制台

浏览器内核分类：

webkit/gecko/presto/trident

常用的浏览器

- webkit内核（V8引擎）
  - 谷歌Chrome
  - Safari
  - Opera >=V14
  - 国产浏览器
  - 手机浏览器
  - ...
- Gecko
  - 火狐FireFox
- Presto
  - Opera < V14
- Trident
  - IE
  - IE EDGE 开始使用双内核（其中包含 chrome迷你）

谷歌浏览器的控制台（F12/Fn+F12）

- Elements: 查看结构样式，可以修改这些内容
- Console：查看输出结果和报错信息，是JS调试的利器
- Sources：查看项目源码
- Network：查看当前网站所有资源的请求信息（包括和服务器传输的HTTP报文信息）、加载时间等（根据加载时间进行项目优化）
- Application：查看当前网站的数据存储和资源文件（可以盗图）

## js看书顺序

js高程->阮一峰es6->你不知道的js->js权威指南

### js组成

JavaScript 是有三部分组成：

- ECMAScript（ES）：描述了改语言的语法和基本对象
- DOM：文档对象模型，描述处理网页内容的方法和接口
- BOM，浏览器对象模型，描述与浏览器进行交互的方法和接口 

## JavaScript中的变量和数据类型

**创建变量的几种方式**：var、let、const、声明函数function、创建类class、ES6模块导入import、Symbol创建唯一值

```js
let n = Symbol(100)
let m = Symbol(100)
```

**命名规范**：

- 严格区分大小写
- 使用数字、字母、下划线、$、数字不能作为开头
- 使用驼峰命名法
- 常用的缩写：add/insert/create/new（新增）、update(修改)、delete/del/remove/rm(删除)、sel/select/query/get（查询）、info（信息）...
- 不能使用关键字和保留字

**数据类型分类：**

- 基本数据类型：
  - 数字number：常规数字和NaN
  - 字符串string：所有用单引号、双引号、反引号包起来都是字符串
  - 布尔boolean：true/false
  - 空对象指针null、未定义undefined

引用数据类型：

- 对象数据类型object：{}普通对象、[] 数组对象、/.../ 正则对象、Math数学函数对象、日期对象...
- 函数数据类型function

**数字**

数字：正常数字和NaN

Nav和任何值（包括自己）都不相等：NaN!=NaN。

判断一个值是否为非有效数字：isNaN([val])

> 在使用isNaN进行检测时，首先会验证检测的值是否为数字类型，若不是，先基于Number()，把值转换为数字类型，然后再检测

```js
isNaN(10) //false
isNaN('AA') // true
isNaN('10') // false 注意 Number('10')=>10 isNaN(10)=>false
```

**转换为数字类型**

- Number([val])
- parseInt/parseFloat([val],[进制])，对于字符串来说，它是从左到右依次查找有效数字字符，直到遇到非有效数字字符，停止查找（不管后面是否还有数字），把找到的当作数字返回。
- == 进行比较时，可能要出现把其他类型值转换为数字

```js
// 字符串转数字，Number() 把字符串转换为数字，只要字符串中包含任意一个非有效数字字符（第一个点除外）结果都是NaN，空字符串会变为数字零。
Number('12.5') // 12.5
Number('12.5px') // NaN
Number('12.5.5') // NaN
Number(' ') // 0
// 布尔转数字
Number(true) // 1
Number(false) // 0
isNaN(false) // false
// null->0 undefined->NaN
Number(null) // 0
Number(undefined) // NaN
// 把引用类型转换为数字，是先把他基于toString方法转换为字符串，然后再转换为数字
Number({name: '10'}) // NaN
Number({}) // NaN，()/{xxx:'xxx'}.toString()=>'[object Object]'=>NaN
Number([]) // 0，[].toStirng()=>''
Number([12]) // 12，[12].toStirng()=>'12'
Number([12, 23]) // NaN，[12,23].toString()=>'12,23'

let str = '12.5px'
Number(str) // NaN
parseInt(str) // 12
parseFloat(str) // 12.5
parseFloat('width:12.5px') // NaN
parseFloat(true) // NaN，非数字类型转字符串，再根据查找规则，'true'=>NaN
```

**string字符串数据类型**

所有用单引号、双引号、反引号（撇 ES6模板字符串）包起来的都是字符串

**转字符串**

- [val].toString()
- 字符串拼接

```js
let a = 12
a.toString() // '12'
(NaN).toStirng() // 'NaN'

// null和undefined是禁止直接toString的
// (null).toString // 报错
// 但是和undefined一样转换为字符串的结果就是 'null' 'undefined'

// 普通对象.toString()的结果是 “[object Object]” => Object.prototype.toString方法不是转换为字符串的，而是用来检测数据类型的

// 字符串拼接
// 四则运算法则中，除加法外，其余都是数学计算，只有加法可能存在字符串拼接（一旦遇到字符串，则不是数学运算，而是字符串拼接）
'10' + 10 // '1010'
'10' - 10 // 0
'10px' - 10 // NaN

let a = 10 + null + true + [] + undefined + '啦啦' + null + [] + 10 + false
/*
	10 + null -> 10 + 0 10
	10 + true -> 10 + 1 -> 11
	11 + [] -> 11 + '' -> '11' 空数组变为数字，先要经历变为空字符串，遇到字符串，直接变为字符串拼接
	...
	'11undefined啦啦null10false'
*/
console.log(a) '11undefined啦啦null10false'
```

