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