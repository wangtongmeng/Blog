# 在 vue 中使用 svg 图标

<https://www.cnblogs.com/shenyf/p/10370949.html>

<https://juejin.im/post/59bb864b5188257e7a427c09>

<https://blog.csdn.net/weixin_42204698/article/details/93751906>比较全

svg兼容性问题

vue组件中

```vue
<template>
	<svg>
  	<use xlink:href='#icon-qq'></use>
  </svg>
</template>
<script>
	import '@/icons/svg/qq.svg'
</script>
```

为了更方便的使用，还需要做两件事：

- 图标自动导入：利用 require.context
- 封装 SvgIcon 组件，使用方便，样式好控制

