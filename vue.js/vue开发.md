# vue 开发

## css 作用域

### 深度作用选择器(vue-loader编译)

如果你希望 `scoped` 样式中的一个选择器能够作用得“更深”，例如影响子组件，你可以使用 `>>>` 操作符：

```html
<style scoped>
.a >>> .b { /* ... */ }
</style>
```

上述代码将会编译成：

```css
.a[data-v-f3f3eg9] .b { /* ... */ }
```

有些像 Sass 之类的预处理器无法正确解析 `>>>`。这种情况下你可以使用 `/deep/` 操作符取而代之——这是一个 `>>>` 的别名，同样可以正常工作。

参考：https://vue-loader-v14.vuejs.org/zh-cn/features/scoped-css.html

## 实现全局 loading

### 封装 axios 调用 api 自动全局 loading、错误提示

https://juejin.im/post/5bfb63e86fb9a049c30ae96d

### 通过 plugin

### 通过组件

## 使用 echarts

x 轴 为 time 时，https://www.cnblogs.com/vipstone/p/5318615.html

[时间为横坐标的柱状图超出x坐标了](https://github.com/apache/incubator-echarts/issues/5651)

## mock数据

[你是如何构建 Web 前端 Mock Server 的？](https://www.zhihu.com/question/35436669)

## vue 使用 echarts 遇到的问题

### ehart 切换显示宽度不正确

 nextick 解决

- [Vue解决echart在element的tab切换时显示不正确](https://blog.csdn.net/SanJiK/article/details/79764429)

- [Vue.nextTick 的原理和用途](https://segmentfault.com/a/1190000012861862)
- https://juejin.im/post/5a6fdb846fb9a01cc0268618



