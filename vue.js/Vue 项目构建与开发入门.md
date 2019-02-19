# [Vue 项目构建与开发入门](https://juejin.im/book/5b23a5aef265da59716fda09)

## 第一章 Vue CLI 3 项目构建基础

### 依赖工具

在构建一个 Vue 项目前，确保本地安装了 `Node` 环境以及包管理工具 `npm`

检查版本

```shell
# 查看 node 版本
node -v

# 查看 npm 版本
npm -v
```

### 脚手架

安装完 node 后便可以开始进行后续的构建工作了，这里通过最便捷的脚手架构建。

#### 什么是脚手架

它在生活中的含义是为了保证各施工过程顺利进行而搭设的工作平台。因此作为一个工作平台，前端的脚手架可以理解为能够帮助我们快速构建前端项目的一个工具或平台。

#### vue-cli

`vue-cli` 是 Vue 的脚手架工具。

**1.安装**

```shell
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

检查其版本是否正确 (3.x)：

```shell
vue --version
```

**2.构建**

安装完 vue-cli 后，我们在你想要创建的项目目录地址下执行构建命令：

```shell
# my-project 是你的项目名称
vue create my-project
```

![img](https://user-gold-cdn.xitu.io/2018/6/18/16412343fab2e351?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

如果你只想构建一个基础的 Vue 项目，那么使用 `Babel`、`Router`、`Vuex`、`CSS Pre-processors` 就足够了，最后选择你喜欢的包管理工具 npm or yarn。

**3.启动**

等待构建完成后你便可以运行命令来启动你的 Vue 项目：

```shell
# 打开项目目录
cd vue-project

# 启动项目
yarn serve

# or
npm run serve
```

成功后打开浏览器地址：http:/localhost:8080/

**4.目录结构**

最后脚手架生成的目录结构如下：

```shell
├── node_modules     # 项目依赖包目录
├── public
│   ├── favicon.ico  # ico图标
│   └── index.html   # 首页模板
├── src 
│   ├── assets       # 样式图片目录
│   ├── components   # 组件目录
│   ├── views        # 页面目录
│   ├── App.vue      # 父组件
│   ├── main.js      # 入口文件
│   ├── router.js    # 路由配置文件
│   └── store.js     # vuex状态管理文件
├── .gitignore       # git忽略文件
├── .postcssrc.js    # postcss配置文件
├── babel.config.js  # babel配置文件
├── package.json     # 包管理文件
└── yarn.lock        # yarn依赖信息文件
```

安装时选择的依赖不同，最后生成的目录结构也会有所差异。

#### 可视化界面

除了使用上述命令行构建外，`vue-cli 3.x` 还提供了可视化的操作界面，在项目目录下我们运行如下命令开启图形化界面：

```shell
vue ui
```

之后浏览器会自动打开本地 `8000` 端口

如果你还没有任何项目，那么可以点击创建或者直接导入现有的项目。创建项目和我们使用命令行的步骤基本相同，完全可视化操作，一定程度上降低了构建和使用的难度。项目创建或导入成功后你便可以进入项目进行可视化管理了。

在整个管理界面中，我们可以为自己的项目安装 CLI 提供的插件，比如安装 `@vue/cli-plugin-babel`插件，同时我们也可以配置相应插件的配置项，进行代码的编译、热更新、检查等。

## 第2章 构建基础篇 1：你需要了解的包管理工具与配置项

















