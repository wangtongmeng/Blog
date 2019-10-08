# iview Message(全局提示)与Notice(通知提醒)全局配置方法

在使用iview 的Message与Notice组件时，可以对提示框的显示位置与显示时长进行配置。

iview提供了两个配置属性。分别是：

- top 提示组件距离顶端的距离，单位像素。
- duration 默认自动关闭的延时，单位秒。

可以对这两个组件进行全局配置:

```js
//在某个组件中全局配置，只需要在mouted()钩子函数中写入
mounted() {
    this.$Message.config({
      top: 100,
      duration: 3
  });
    this.$Notice.config({
      top: 100,
      duration: 3
    });
}
//在整个项目中全局配置，需要在main.js中写入

Vue.prototype.$Message.config({
    top: 100,
    duration: 3
});
Vue.prototype.$Notice.config({
    top: 50,
    duration: 3
});
```

