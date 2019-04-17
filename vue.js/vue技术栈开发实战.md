#  vue 技术栈开发实战

课程源码：https://github.com/lison16/vue-cource

## 使用 vue-cli3创建项目

- 使用 Vue UI 创建、管理项目
- 项目结构目录整理
- 初始文件添加
- 基本配置
- 跨域配置

### 使用 Vue UI 创建、管理项目

命令行打开 vue ui

```shell
vue ui
```

- 创建项目
  - 选择项目文件夹
  - 包管理器：npm
  - 下一步
- 预设
  - 选择手动
  - 下一步
- 功能
  - babel，勾选
  - vue-router，勾选
  - vuex，勾选
  - css预处理器，勾选
  - linter / formatter，勾选
  - 使用配置文件，勾选
  - 下一步
- 配置
  - 预处理器，选 less
  - linter / formatter 配置，选 eslint + standard config
  - lint on save，先关掉
  - 点击创建项目
- 是否保存预设
  - 不需要

### 项目结构目录整理

![1555312334007](./img/项目目录.png)

### 初始文件添加

**配置 .editorconfig**

```shell
root = true /# 使其生效 #/
[*] /# 对所有文件都有效 #/
charset = utf-8 /# 编码 utf-8 #/
indent_style = tab /# 缩进选择 tab，空格是 space #/
indent_size = 2 /# 缩进尺寸 #/

```

vscode 需要安装插件 EditorConfig for VS Code，安装后配置文件才会生效。

**添加 api 目录**

创建 /src/api/ 文件夹，作为请求文件的目录。

**整理 assets 目录**

添加 /assets/img/ 文件夹，存放图片。

添加 /assets/font/ 文件夹，存放图标字体。

**添加 config 目录**

创建 /src/config/ 文件夹，项目的配置文件，存放在 config文件夹中。

创建 /src/config/index.js 文件，并导出一个对象。

```js
export default {}
```

通过 import from '相对路径'，在其他文件中引入。

**添加 directive 目录**

创建 /src/directive/ 文件夹，用于存放自定义指令。

创建 /src/directive/index.js 文件。

**添加 lib 目录**

创建 /src/lib/ 文件夹。

创建 /lib/util.js 文件，用于存放与业务结合的工具函数。

创建 /lib/tools.js 文件，存放与业务无关的工具函数。

**添加 router 目录**

创建 /src/router/ 文件夹。

创建 /router/index.js 文件

将 router.js 移入文件夹。

拆分代码

```js
// index.js，存放路由实例，以及路由拦截等
import Vue from 'vue'
import Router from 'vue-router'
import routes from './router'

Vue.use(Router)

export default new Router({
  routes
})
// router.js，存放路由列表
import Home from './views/Home.vue'

export default [
	{
		path: '/',
		name: 'home',
		component: Home
	},
	{
		path: '/about',
		name: 'about',
		// route level code-splitting
		// this generates a separate chunk (about.[hash].js) for this route
		// which is lazy-loaded when the route is visited.
		component: () => import(/* webpackChunkName: "about" */ './views/About.vue')
	}
]
```

**添加 store 目录**

创建 /src/store/ 文件夹。将 store.js 移入文件夹。

创建根级别文件 /store/state.js 文件，/store/mutations 文件，/store/actions.js 文件。

创建模块级别文件 /store/module/user.js 文件，存放模块级别的 state、mutations、actions

将 store.js 改名为 index.js。

将各文件导入 index.js

```js
// index.js
import Vue from 'vue'
import Vuex from 'vuex'
import state from './state'
import mutations from './mutations'
import actions from './actions'
import user from './module/user'


Vue.use(Vuex)

export default new Vuex.Store({
  state,
  mutations,
	actions,
	modules: {
		user
	}
})
// module/user.js
const state = {
	//
}

const mutations = {
	//
}

const actions = {
	//
}

export default {
	state,
	mutations,
	actions
}
```

**添加 mock 目录**

创建 /src/mock/ 文件夹，用于模拟返回数据。
创建 /src/index.js 文件

安装 mockjs， `-D`作为开发依赖。

```shell
npm install mockjs -D
```
引入 mockjs
```js
import Mock from 'mockjs'

// 具体 mock 操作

export default Mock
```

**修改入口文件 main.js**

查看文件引入路径，保证路径正确。

### 基本配置与跨域配置

**配置 vue.config.js**

配置基础路径、目录别名、SourceMap、devServer 代理跨域。

```js
// vue.config.js
const path = require('path')

const resolve = dir => path.join(__dirname, dir)

const BASE_URL = process.env.NODE_ENV === 'production' ? '/iview-admin' : '/'

module.exports = {
	lintOnSave: false,
	baseUrl: BASE_URL,
	chainWebpack: config => {
		config.resolve.alias
			.set('@', resolve('src'))
			.set('_c', resolve('src/components'))
	},
	// 打包时不生成.map文件，减少体积，加快打包速度 
	productionSourceMap: false,
	devServer: {
		proxy: 'http://localhost:4000'
	}
}

```

## 路由基础篇

- router-link 和 router-view 组件
- 路由配置
  - 动态路由
  - 嵌套路由
  - 命名路由
  - 命名视图
- JS 操作路由
- 重定向和别名

### router-link 和 router-view 组件

点击 `router-link`组件，发生路由跳转，跳转路径由属性 to 决定。路由内容通过 `router-view`组件渲染到页面。

```html
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
```

### 动态路由

优点：组件复用、在同一组件处理不同逻辑

**路由列表中定义动态路由**

```js
// router.js
[
  {
		path: '/argu/:name',
		component: () => import('@/views/argu.vue')
  }
]
```
**页面组件处理不同逻辑**

当访问 /argu/动态值 时，可以根据路由参数的不同，处理不同的逻辑；相当于用同一个组件显示不同路由下的页面，实现了组件复用。

```html
<--页面组件-->
<template>
	<div>
		{{ $route.params.name }}
	</div>
</template>
```

### 嵌套路由

**路由列表中定义动态路由**

```js
// router.js
[
  {
		path: '/parent',
		component: () => import('@/views/parent.vue'),
		children: [
			{
				path: 'child',
				component: () => import('@/views/child.vue')
			}
		]
	}
]
```

**父级组件中使用 `<router-view />`**

```html
<template>
	<div>
		parent
		<router-view /> <--子组件在此显示-->
	</div>
</template>
<script>
```

当访问路径 /parent/child 时，就会显示 parent.vue 和 child.vue 结合的内容了。

### 命名路由

**路由列表中给路由项添加 name 属性**

```js
[{
		path: '/',
		name: 'home',
		component: Home
	},
	{
		path: '/about',
		name: 'about',
		component: () => import(/* webpackChunkName: "about" */ '@/views/About.vue')
	}]
```

**`<router-link>的 to 属性中使用 name 属性跳转`**

```html
<--正常情况-->
<router-link to="/">Home</router-link> |
<router-link to="/about">About</router-link>
<--使用命名路由时-->
<router-link :to="{ name: 'home' }">Home</router-link> |
<router-link :to="{ name: 'about' }">About</router-link>
```

### 命名视图

在一个页面显示多个视图(由`<router-view>`渲染出来的视图)。

**在页面组件中添加多个带名字的`<router-view>`**

```html
<-- 页面组件 -->
<template>
  <div id="app">
    <router-view />
      <router-view />
      <router-view name='email' />
      <router-view name='tel' />
  </div>
</template>
```

**路由列表中配置具有多个命名视图的路由**

```js
// router.js
[
    {
		path: '/named_view',
		components: {
			default: () => import('@/views/child.vue'),
			email: () => import('@/views/email.vue'),
			tel: () => import('@/views/tel.vue')
		}
	}
]
```


> 注意，components 需要加 s。

### 重定向

**路由列表中通过 redirect 重定向**

当访问 /main 路由时，重定向到首页。

```js
// router.js
// 1. 给 redirect 传入一个字符串路由
[
    {
		path: '/main',
		redirect: '/'
	}
]
// 2. 给 redirect 传入一个对象，通过 name 来重定向到响应名字的路由
[
    {
        {
		path: '/main',
		redirect: {
			name: 'home'
		}
	}
    }
]
// 3. 给 redirect 传入一个函数，根据 to对象 中的参数，灵活的重定向
[
    {
		path: '/main',
		redirect: to => { name: 'home' }
	}
]
```

### 别名

当访问路由别名时，就相当于访问这个路由。

**路由列表中通过 alias 给路由设置别名**

当我们访问 /home_page 时，显示的也是 home 页面。

```js
// router.js
[
    {
		path: '/',
		alias: '/home_page',
		name: 'home',
		component: Home
	},
]
```

### 编程式导航

通过 JS 来控制路由的跳转和返回。

通过 `$router` 实施路由跳转，`$router` 是在 new Vue({ router }) 注册的。

**回退 1**

`this.$router.go(-1)`

`this.$router.back()`

**向前 1**

`this.$router.go(1)`

**跳转指定路由**

`this.$router.push('/parent')`，push 传入路由字符串

`this.$router.push({ name: 'parent'})`，通过命名路由跳转

**替换到指定路由**

`this.$router.push({ name: 'parent'})`

**replace 和 push 的区别**

- push 跳转路由，会添加到路由跳转记录中。
- replace 是替换路由，也就是把当前路由的跳转记录替换掉。

**跳转路由传参的 3 种写法**

1.name 和 query 

查询参数传参，跳转后`http://localhost:8080/#/parent?name=lison`

```js
this.$router.push({
    name: 'parent',
    query: {
        name: 'lison'
    }
})
```

2.name 和 params

动态路由传参，跳转后 `http://localhost:8080/#/argu/lison`

```js
this.$router.push({
    name: 'argu',
    params: {
        name: 'lison'
    }
})
```

3.path

动态路由传参，结合模板字符串的写法，跳转后 `http://localhost:8080/#/argu/lison`

```js
const name = 'lison'
this.$router.push({
    path: `/argu/${name}`
})
```

> 注意，path 不能喝 params一起使用，无效。

## 路由进阶篇

- 路由组件传参
- HTML5 History 模式
- 导航守卫
- 路由元信息
- 过渡效果

### 路由组件传参

通过 `$route`接收参数，使页面组件和路由高度耦合。可以通过路由组件传参来解决，路由组件传参有 3 种模式。

**1.布尔模式**

路由列表中设置路由 props 为 true

```js
// router.js
[
    {
		path: '/argu/:name',
		name: 'argu',
		component: () => import('@/views/argu.vue'),
		props: true
	}
]
```

组件内通过 props 接收参数

```html
<--组件-->
<template>
	<div>{{ name }}</div>
</template>
<script>
export default {
	props: {
		name: {
			type:String,
			default: 'lison'
		}
	}
}
</script>
```

**2.对象模式**

路由列表中设置路由 props 为一个对象，不同路由可以设置传入不同参数

```js
// router.js
[
    {
		path: '/about',
		name: 'about',
		component: () => import('@/views/About.vue'),
		props: {
			food: 'banana'
		}
	}
]
```

组件内通过 props 接收参数，同上

**3.函数模式**

路由列表中设置路由 props 为一个函数，通过函数参数 route对象拿到参数值

```js
// router.js
[
    {
		path: '/',
		alias: '/home_page',
		name: 'home',
		component: Home,
		props: route => ({
			food: route.query.food
		})
	}
]
```

组件内通过 props 接收参数，同上

### HTML5 History 模式

router 构造函数除了传入路由列表还可以传入 mode 选项

history 模式是利用浏览器 history api 做页面无刷新跳转。但需要后端配合。

当 url 匹配不到静态资源时，默认显示 index.html

当 url 匹配不到静态资源并且前端路由也匹配不到组件的话，就会有问题，所以需要统一显示404页面。

**在路由列表的末尾添加404页面路由**

注意一定要在末尾，因为路由优先级前面的高。`path: '*'`表示匹配任意路由，当前面路由都匹配不到时，匹配404页面。

```js
// router.js 
[
    {
		path: '*',
		component: () => import('@/views/error_404.vue')
	}
]
```

### 导航守卫

路由发生跳转到导航结束期间，做一些相应的逻辑处理；如跳转到某个页面时，判断用户是否登录，若没登录就跳转到登录页面；如权限控制，若页面用户没有权限，做一些相应的处理。

**全局守卫**

在 router 实例上进行全局守卫设置

1.全局前置守卫

通过全局前置守卫`beforeEach`处理用户是否登录。逻辑如下：

- 若跳转页面不是登录页
  - 已登录就跳转
  - 否则跳转到登录页
- 若跳转页面时登录页
  - 已登录就跳转到首页
  - 否则跳转到登录页

```js
const HAS_LOGINED = true
// to from 都是路由对象，to 跳转后页面的路由对象，from，跳转前的路由对象，next 函数控制页面跳转。
router.beforeEach((to, from, next) => {
	if (to.name !== 'login') {
		if (HAS_LOGINED) next()
		else next({ name: 'login'})
	} else {
		if (HAS_LOGINED) next({ name: 'home'})
		else next()
	}
})
```

2.全局后置钩子

也为页面已发生跳转，所以不能叫守卫。

可以用来关闭 login 动画。

```js
router.afterEach((to, from) => {
	// logining = false
})
```

3.全局解析守卫

`router.beforeResolve` 注册一个全局守卫。这和 `router.beforeEach` 类似，区别是在导航被确认之前，**同时在所有组件内守卫和异步路由组件被解析之后**，解析守卫就被调用。

```js
// router.beforeResolve
```

4.路由独享的守卫

在路由配置上直接定义 `beforeEnter` 守卫：

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
        next() // 注意，一定要调用 next 不然无法跳转
      }
    }
  ]
})
```

5.组件内的守卫

- `beforeRouteEnter`
- `beforeRouteUpdate`
- `beforeRouteLeave`

```js
// 页面路由组件中
beforeRouteEnter (to, from, next) {
    // this，虽然进入了组件内钩子，但此时页面还没有渲染，所以没有 this
    next(vm => {
        // 如果要使用组件实例，可以在 next 中使用
        // console.log(vm)
    })
},
beforeRouteLeave (to, from, next) {
    // 例如，用户一个页面编辑，突然点击跳转页面，这时需要提醒用户还未保存编辑
    // 组件已经渲染好了，可以使用 this
    const leave = confirm('您确认要离开吗？')
    if (leave) next()
    else next(false)
},
beforeRouteUpdate (to, from ,next) {
    // 路由发生变化，组件被复用时调用
    // 由于组件已经渲染过了，所以可以使用 this
    console.log(to.name, from.name)
},
```

6.完整的导航流程

1. 导航被触发
2. 在失活的组件 (即将离开的页面组件) 里调用离开守卫 beforeRouteLeave
3. 调用全局的前置守卫 beforeEach
4. 在重用的组件里调用 beforeRouteUpdate
5. 调用路由独享的守卫 beforeEnter
6. 解析异步路由组件
7. 在被激活的组件 (即将进入的页面组件) 里调用 beforeRouteEnter
8. 调用全局的解析守卫 beforeResolve
9. 导航被确认
10. 调用全局的后置守卫 afterEach
11. 触发 DOM 更新
12. 用创建好的实例调用 beforeRouterEnter 守卫里传给 next 的回调函数

### 路由元信息

在路由列表中，每个路由对象可以配置一个 meta 字段，存放自定义的信息。

例如页面权限，之后在路由前置路由中做处理。

demo: 动态设置路由页面的 title 值

```js
// 1. 在路由列表的路由对象中，配置 meta 字段，添加 title 值
//  router.js
[
    {
		path: '/about',
		name: 'about',
		component: () => import('@/views/About.vue'),
		meta: {
			title: '关于'
		}
	},
]
// 2. 在全局前置守卫处理
//  /router/index.js
import { setTitle } from '@/lib/util'
router.beforeEach((to, from, next) => {
	to.meta && setTitle(to.meta.title)
})

//  util.js 和业务有关的工具函数
export const setTitle = (title) => {
	window.document.title = title || 'admin'
}
```

### 路由切换动效

包住多个组件用 `<transition-group>`，单个组件用`<transition>`

为  `<transition-group>` 中的每一个组件设置一个 key，给`<transition-group>`设置一个 name，通过类名的方式设置，路由切换时，组件的隐藏和显示。

```html
<-- App.vue 根组件中 --> 
<template>
  <div id="app">
      <transition-group name='router'>
          <router-view key='default' />
          <router-view key='email' name='email' />
          <router-view key='tel' name='tel' />
      </transition-group>
  </div>
</template>

<style lang="less">
// 页面进入
//   进入路由前
.router-enter {
	opacity: 0;
}
//   路由页面从无到有的过程
.router-enter-active {
	transition: opacity 1s ease;
}
//   路由页面完全显示时
.router-enter-to {
	opacity: 1;
}
// 页面注销/离开
//   离开路由前
.router-leave {
	opacity: 1;
}
//   路由页面从有到无的过程
.router-leave-active {
	transition: opacity 1s ease;
}
//   路由页面完全消失时
.router-leave-to {
	opacity: 0;
}
</style>

```

若为某个页面设置特定的路由切换过渡效果，可以动态设置`<transtion-group>`的 name 属性。我们可以在访问特定路由时传递一个参数，比如通过 query 传一个参数，通过监听 `$route` 变化拿到参数，并根据参数设置特定路由页面的过渡效果。当路由切换携带对应参数时`http://localhost:8080/#/about?transitionName=router`，页面就可以显示指定过渡效果了。

```html
<template>
  <div id="app">
		<transition-group :name='routerTransition'>
		</transition-group>
  </div>
</template>
<script>
export default {
	data () {
		return {
			routerTransition: ''
		}
	},
	watch: {
		'$route' (to) {
			to.query && to.query.transitionName && (this.routerTransition = to.query.transitionName)
		}
	}
}
</script>
```

