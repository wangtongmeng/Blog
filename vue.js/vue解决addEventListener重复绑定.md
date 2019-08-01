# vue解决addEventListener重复绑定

在组件里用addEventListener绑定了一个滚动事件

```js
mounted(){
    window.addEventListener('scroll', this.scrollListener,false)
}
```

在mounted中解绑无用，因为vue组件不同，导致this.scrollListener不同

```js
mounted(){
    window.removeEventListener('scroll',this.scrollListener,false)
    window.addEventListener('scroll', this.scrollListener,false)
}
```

应该在组件销毁时，解绑监听函数，保证事件处理程序相同

```js
mounted(){
   window.addEventListener('scroll', this.scrollListener,false)
},
destroyed(){
    window.removeEventListener('scroll',this.scrollListener,false)
}
```

