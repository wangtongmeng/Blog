# Bootstrap

## 概念

Bootstrap 是最受欢迎的 HTML、CSS 和JS框架，用于开发响应式布局、移动设备优先的WEB 项目。它将常见的CSS布局小组件和JS插件进行了封装，提高了效率，在某种程度上规范前端团队编写CSS和JS的规范。  

- 一套丰富的预定义样式表
- 一组基于JQuery的JS插件集
- 移动设备优先
- 灵活的响应式栅格系统（自适应pc、平板、手机设备）

![bootstrap概念图](./img/bootstrap概念图.png)

## 下载地址

官方地址： http://getbootstrap.com   中文地址：www.bootcss.com

- 下载用于生产环境的文件
- 下载用于编译CSS的Less源码及插件的js源文件
- 下载用于编译CSS的Sass源码ji插件的js源文件
- 用CDN直接引入

## html 标准模板

1. HTML 文档结构
2. 移动设备优先
3. Bootstrap css 引入
4. JQuery 引入
5. Bootstrap js 引入

   [hml 模板示例](https://v3.bootcss.com/getting-started/#template)

## 栅格系统布局

### 概念

- 响应式设计
  - 自适应pc、平板、手机设备等。
- 栅格实现原理
- [媒体查询](https://v3.bootcss.com/css/#grid-media-queries)

### 用法

- [布局容器](https://v3.bootcss.com/css/#overview-container)
- 列组合 `.col-md-*`
- 列偏移 `.col-md-offset-*`
- 列嵌套
- 列排序 `.col-md-push-*`  `.col-md-pull`

### 栅格参数

- 跨设备组合定义
- 清浮动 `clearfix visible-xs`

## 排版

### 标题

- h1-h6
- .h1-.h6
- `<small>` 65% 75%

### 页面主体

body 和 p: 字体 14px，行高 1.428

p：0.5 行高的 margin-bottom

中心内容： `.lead` 段落突显。

### 内联文本元素

- 高亮，`<mark>内容</mark>`
- 删除的文本，`<del>内容</del>`
- 无用文本，`<s>内容</s>`
- 插入文本，`<ins>内容</ins>`
- 带下划线的文本，`<u>内容</u>`
- 小号文本，`<small>内容</small>`或`<span class="small">内容</span>`
- 着重，`<strong>内容</strong>`
- 斜体，`<em>内容</em>`







