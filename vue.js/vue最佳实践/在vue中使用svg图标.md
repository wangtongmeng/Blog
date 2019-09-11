# 在 vue 中使用 svg 图标

在后台管理项目等兼容性要求不高的项目中可使用此方案，便于维护。

## 安装依赖
 安装依赖 `svg-sprite-loader`
```shell
npm i svg-sprite-loader -D
```

## 下载 svg 图标
[下载 svg 图标](<https://www.iconfont.cn>)，存入 src/icons/svg 中 
## 修改规则和新增规则
修改规则和新增规则，vue.config.js 
```js
const path = require('path')
// resolve定义一个绝对路径获取函数
function resolve (dir) { 
  return path.join(__dirname, dir)
}
//...
chainWebpack (config) {
    // 配置svg规则排除icons目录中svg文件处理
    config.module
      .rule("svg")
      .exclude.add(resolve("src/icons"))
      .end();
    // 新增icons规则，设置svg-sprite-loader处理icons目录中的svg
    config.module
      .rule("icons")
      .test(/\.svg$/)
      .include.add(resolve("src/icons"))
      .end()
      .use("svg-sprite-loader")
      .loader("svg-sprite-loader")
      .options({ symbolId: "icon-[name]" }) 
      .end();
  }
```

## 图标自动导入
```js
// icons/index.js
const req = require.context('./svg', false, /\.svg$/) // false 文件夹从不会再嵌套子文件夹了
req.keys().map(req);
// main.js
import './icons'
```

## 创建SvgIcon组件
创建SvgIcon组件，./components/SvgIcon.vue 
```vue
<template>
  <svg :class="svgClass" aria-hidden="true" v-on="$listeners">
    <use :xlink:href="iconName" />
  </svg>
</template>

<script>
export default {
  name: 'SvgIcon',
  props: {
    iconClass: {
      type: String,
      required: true
    },
    className: {
      type: String,
      default: ''
    }
  },
  computed: {
    iconName () {
      return `#icon-${this.iconClass}`
    },
    svgClass () {
      if (this.className) {
        return 'svg-icon ' + this.className
      } else {
        return 'svg-icon'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.svg-icon {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
```

## 组件全局注册
注册，icons/index.js 
```js
import Vue from 'vue'
import SvgIcon from '@/components/SvgIcon.vue'
// 全局引入 SvgIcon 组件
Vue.component('svg-icon', SvgIcon)
```
## 在组件中使用 SvgIcon 组件
在组件中使用 SvgIcon 组件，App.vue 

```vue
<svg-icon icon-class="qq"></svg-icon>
```

参考

<https://www.cnblogs.com/shenyf/p/10370949.html>

<https://juejin.im/post/59bb864b5188257e7a427c09>