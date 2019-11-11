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

**布尔数据类型**

只有两个值 true/false

**转布尔**

只有 0、NaN、''、null、undefined 五个值转换成false，其余都转换为true。

- Boolean([val])
- !/!!
- 条件判断

```js
Boolean(0) // false
Boolean('') // false
Boolean(' ') // true
Boolean(null) // false
Boolean(undefined) // false
Boolean([]) // true
Boolean([1, 2]) // true
Boolean(-1) // true

// !:取反（先转为布尔，然后取反）
// !!：取反再取反，相当于转换为布尔 <=> Boolean
!1 // false
!!1 // true

// 如果条件只是一个值，不是 ==/===/!=/>= 等这些比较，是要把这个值先转换为布尔类型，然后验证真假
if(1) {} // true
if('3px' + 3){} // true,'3px3'=> true
 if('3px' - 3){} // false，NaN - 3 => NaN => false
```

**null / undefined**

null和undefined都代表是没有

null：意料之中（一般都是开始不知道值，我们手动先设置为null，后期再给赋予值操作）

```js
let num = null // let num = 0 一般最好用null作为初始空值，因为零不是空值，它在栈内存中有自己的存储空间（占了位置）
num = 12
```

undefined：意料之外（不是我能决定的）

```js
let num; // 创建一个变量没有赋值，默认值是undefined
num = 12;
```

**object对象数据类型-普通对象**

> {[key]:[value],...} 任何一个对象都是由零到多组键值对（属性名：属性值）组成的（且属性名不能重复）

  ```js
let person = {
  name: 'xxx',
  age: 10,
  height: '185CM',
  weight: '80KG',
  1: 100
}
// 获取属性名对应的属性值
// =>对象.属性名
// =>对象[属性名] 属性名是数字或字符串格式的
// =>如果当前属性名不存在，默认的属性值是undefined
// =>如果属性名是数字，则不能使用点的方式获取属性值
person.name
person['age']
person.sex //=>undefined
person[1]
person.1 //=>SyntaxError:语法错误
// 设置属性名属性值
// =>属性名不能重复，如果属性名已经存在，不属于新增属于修改属性值
person.GF = 'yyy'
person['GF'] // 'yyy'
person.name = 'zzz'
// 删除属性
// =>真删除：把属性彻底干掉
delete person[1]
// =>假删除：属性还在，值为空
person.weight = null
console.log(person)


  ```

> 数组是特殊的对象数据类型

```js
/*
	数组是特殊的对象
	1. 我们中括号中设置的属性值，它的属性名是默认生成的数字，从零开始递增，而且这个数字代表每一项的位置，我们把其称为“索引”=>从零开始，连续递增，代表每一项位置的数字属性名
	2. 天生默认一个属性名 lenfth，存储数组的长度
*/
let ary = [12, '哈哈', true, 13]
console.log(ary)
ary.length
ary['length']
ary[1]
// 第一项索引0 最后一项索引 ary.length -1
ary[0]
ary[ary.length - 1]
// 向数组末尾追加内容
ary[ary.length] = 100
```

**JS中数据类型检测**

> 有且只有4中方法

- typeof [val]：：用来检测数据类型的运算符
- instanceof：用来检测当前实例是否隶属于某个类
- constructor：基于构造函数检测数据类型（也是基于类的方式）
- Object.prototype.toString.call()：检测数据类型最好的方法

```js
/*
	基于typeof检测出来的结果
	1. 首先是一个字符串
	2. 字符串中包含对应的类型
	局限性
	1. typeof null => "object" 但是null并不是对象
	2. 基于typeof无法细分出当前值是普通对象还是数组对象等，因为只要是对象数据类型，返回的结果都是"object"
*/
typeof 1 // 'number'
typeof NaN // =>'number'
typeof '12' // 'string'
typeof true // 'boolean'
typeof null // "object"
typeof undefined // "undefined"
typeof {} // "object"
typeof [] // "object"
typeof /^/ // "object"
typeof function(){} // "function"
// 面试题
console.log(typeof typeof typeof []) // 从右到左计算，"string"，因为typeof检测的结果都是字符串，所以只要两个及以上同时检测，最后结果必然是"string"
```

## 堆栈内存（stack & heap）

- 浏览器渲染JS的机制
- 数据类型之间的区别
- 经典面试题联系
- 数据类型的检测

```js
let a = 12
let b = a
b  = 13
console.log(a) // 12

let n = {
  name: 'xxx'
}
let m = n
m.name= 'yyy'
console.log(n.name) // 'yyy'
```

浏览器想要执行JS代码：

1.从电脑内存中分配出一块内存，用来执行代码（栈内存=>Stack）

2.分配一个主线程用来自上而下执行JS代码

栈内存：包含变量存储空间、值存储空间、主线程

![1573439415468](./img/浏览器运行机制-堆栈内存.png)

```js
let n = [10, 20]
let m = n 
let x = m
m[0] = 100
x = [30, 40]
x[0] = 200
m = x
m[1] = 300
n[2] = 400
// 画图
console.log(n, m, x) // n=>[100,20,400] m=x=>[200,300]
```

![1573441034355](./img/浏览器运行机制-堆栈内存-练习1.png)

写出下面结果输出的答案（阿里面试题）

```js
let a = {
  n: 1
}
let b = a
a.x = a = {
  n: 2
}
console.log(a.x)
console.log(b)
```

![1573442065044](./img/浏览器运行机制-堆栈内存-练习2.png)

 ## JS中的操作语句：判断、循环

