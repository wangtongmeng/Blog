# vue轮子

科学上网 vpn vps vultr.com

## 环境搭建

私有仓库：github收费版、gitlab、brackets

### 初始化项目

```shell
npm init
```

### 集成第三方库

**安装 vue**

```js
npm installl vue
```

**安装 parcel**

局部安装

```shell
npm install -D parcel-bundler
```

重构项目，使用vue单文件组件

创建src/button.vue

```vue
<template>
    <button class="m-button">按钮</button>
</template>
<script>
    export default {

    }
</script>
<style lang="scss">
    .m-button {
        font-size: var(--font-size);
        height: var(--button-height);
        padding: 0 1em;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        &:hover {
            border-color: var(--border-color-hover);
        }
        &:active {
            background-color: var(--button-active-bg);
        }
        &:focus {
            outline: none;
        }
    }

</style>
```

在app.js 入口文件中引入button.vue

```js
import Vue from 'vue'
import Button from './button'

Vue.component('m-button', Button)

new Vue({
    el: '#app'
})
```

在主模板文件中，引入app.js入口文件

```html
<body>
<div id="app">
    <m-button></m-button>
</div>
<script src="src/app.js"></script>
</body>
```

根据vue文档-安装，搜索parcel，在package.json中配置parcel

```json
"alias": {
  "vue" : "./node_modules/vue/dist/vue.common.js" // 使用 vue 完整版
}
```

执行 执行parcel 命令

```shell
parcel index.html
parcel index.html --no-cache # 不要用之前的缓存
# 或者使用 npx
npx parcel index.html [--no-cache] # 如果报错加不使用缓存，或者删掉之前的缓存文件
```

**安装 git-open**

```shell
npm i -g git-open
# 使用，在项目目录下使用
git open
```



### 开发工具

webstorm

> 最重要的两个快捷键 shift + shift 任意搜索 / 点击设置

操作git，搜索 vcs(version control system)

添加 .gitignore 文件，忽略 node_modules 和 idea文件夹

```shell
node_modules/
.idea/
```

勾选 Allow unsigned requests，设置搜索 unsign，勾选

关闭 WebStorm 的 Safe Write 功能，设置搜索 safe write ，取消勾选 `Use "safe write..."`

emmet设置及使用

- 设置=>搜索 emmet =>选择 css，勾选 `Enable fuzzy search ...`
- 使用，如 ali:c=>align-items:center

## button组件

### 使用css变量

使用 css 变量使用户可以改变组件样式

```css
/*css 变量*/
html { /*:root*/
  --button-height: 32px;
  --font-size: 14px;
  --button-bg: white;
  --button-active-bg: #eee;
  --border-radius: 4px;
  --color: #333;
  --border-color: #999;
  --border-color-hover: #666;
}
/*组件样式中使用*/
.m-button {
  font-size: var(--font-size);
  height: var(--button-height);
  padding: 0 1em;
  border-radius: var(--border-radius);
  border: 1px solid var(--border-color);
  background: var(--button-bg);
}
.m-button:hover {
  border-color: var(--border-color-hover);
}
.m-button:active {
  background-color: var(--button-active-bg);
}
.m-button:focus {
  outline: none;
}
```

### iconfont的使用及设置

添加图标至购物车，并创建项目vue-compoents

- 编辑项目
  - FontClass/Symbol前缀  `icon-` 改为 `i`
  - Font Family `iconfont` 改为`m-icon`
- 编辑字体
  - 修改姓名，如，`i-shezhi`改为`i-settings`
  - 修改字体大小及位置，字体大小保持一致，位置居中对称
  - 对称图像生成，可以使用sketch、ps、在线svg编辑器生成对称图形，再上传到iconfont
- 批量去色
  - 批量操作=>全选=>批量去色
- 生成 Symbol
  - 点击Symbol=>生成在线链接
- 在项目中使用
  - 

## 工具知识

xxx.log => console.log(xxx)