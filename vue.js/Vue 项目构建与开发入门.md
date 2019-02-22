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

## 第2章 构建基础:包管理工具与配置项

任何一个项目的构建离不开工具和统一的管理标准，在项目开发和维护过程中，我们需要了解安装包的相应工具和配置文件，以此来有效的进行项目的迭代和版本的更新，为项目提供基本的运行环境。本文将详细介绍构建 Vue.js 项目相关的依赖包安装工具和相应的配置文件，为大家提供参考。

###  npm 与 package.json

包管理工具的使用一定不会陌生，毕竟它已经成为前端项目中必不可少的一部分。

npm 是 Node Package Manager 的简称，顾名思义，它是 node 的包管理工具，也是目前世界上最大的开源库生态系统。官方地址为：[www.npmjs.com/](https://link.juejin.im/?target=https%3A%2F%2Fwww.npmjs.com%2F)，你可以在里面找到数以万计的开源包。

使用 npm 包下载量统计工具，比如 [npm-start](https://link.juejin.im/?target=https%3A%2F%2Fnpm-stat.com%2F)，我们可以查看相应包在一定时间范围内的下载量数据。

使用 vue-cli 来构建自己的项目，并生成了相应的目录结构，而在最外层目录中，我们可以看到有 `package.json` 这一文件，该文件便是我们需要了解的包管理文件。

我们先来看一下该文件里面的内容：

```javascript
{
    "name": "my-project", 
    "version": "0.1.0", 
    "private": true, 
    "scripts": {
        "serve": "vue-cli-service serve",
        "build": "vue-cli-service build",
        "lint": "vue-cli-service lint"
    },
    "dependencies": {
        "vue": "^2.5.16",
        "vue-router": "^3.0.1",
        "vuex": "^3.0.1"
    },
    "devDependencies": {
        "@vue/cli-plugin-babel": "^3.0.0-beta.15",
        "@vue/cli-service": "^3.0.0-beta.15",
        "less": "^3.0.4",
        "less-loader": "^4.1.0",
        "vue-template-compiler": "^2.5.16"
    },
    "browserslist": [
        "> 1%",
        "last 2 versions",
        "not ie <= 8"
    ]
}
```

可以看到该文件是由一系列键值对构成的 JSON 对象，每一个键值对都有其相应的作用，比如 scripts 脚本命令的配置，我们在终端启动项目运行的 `npm run serve` 命令其实便是执行了 scripts 配置下的 serve 项命令 `vue-cli-service serve` ，我们可以在 scripts 下自己修改或添加相应的项目命令。

而 dependencies 和 devDependencies 分别为项目生产环境和开发环境的依赖包配置，也就是说像 `@vue/cli-service` 这样只用于项目开发时的包我们可以放在 devDependencies 下，但像 `vue-router` 这样结合在项目上线代码中的包应该放在 dependencies 下。

详细的package.json文件配置项介绍可以参考：[package.json](https://link.juejin.im/?target=https%3A%2F%2Fdocs.npmjs.com%2Ffiles%2Fpackage.json)

### 常用命令

包管理工具的常用命令，一般在项目的构建和开发阶段，我们常用的 npm 命令有：

```shell
# 生成 package.json 文件（需要手动选择配置）
npm init

# 生成 package.json 文件（使用默认配置）
npm init -y

# 一键安装 package.json 下的依赖包
npm i

# 在项目中安装包名为 xxx 的依赖包（配置在 dependencies 下）
npm i xxx

# 在项目中安装包名为 xxx 的依赖包（配置在 dependencies 下）
npm i xxx --save

# 在项目中安装包名为 xxx 的依赖包（配置在 devDependencies 下）
npm i xxx --save-dev

# 全局安装包名为 xxx 的依赖包
npm i -g xxx

# 运行 package.json 中 scripts 下的命令
npm run xxx
```

比较陌生但实用的有：

```shell
# 打开 xxx 包的主页
npm home xxx

# 打开 xxx 包的代码仓库
npm repo xxx

# 将当前模块发布到 npmjs.com，需要先登录
npm publish
```

相比 npm，[yarn](https://link.juejin.im/?target=https%3A%2F%2Fyarnpkg.com%2Fzh-Hans%2F) 相信大家也不会陌生，它是由 facebook 推出并开源的包管理工具，具有速度快，安全性高，可靠性强等主要优势，它的常用命令如下：

```shell
# 生成 package.json 文件（需要手动选择配置）
yarn init

# 生成 package.json 文件（使用默认配置）
yarn init -y

# 一键安装 package.json 下的依赖包
yarn

# 在项目中安装包名为 xxx 的依赖包（配置在 dependencies 下）,同时 yarn.lock 也会被更新
yarn add xxx

# 在项目中安装包名为 xxx 的依赖包（配置在配置在 devDependencies 下）,同时 yarn.lock 也会被更新
yarn add xxx --dev

# 全局安装包名为 xxx 的依
yarn global add xxx

# 运行 package.json 中 scripts 下的命令
yarn xxx
```

比较陌生但实用的有：

```shell
# 列出 xxx 包的版本信息
yarn outdated xxx

# 验证当前项目 package.json 里的依赖版本和 yarn 的 lock 文件是否匹配
yarn check

# 将当前模块发布到 npmjs.com，需要先登录
yarn publish
```

### 第三方插件配置

在上方的 package.json 文件中我们可以看到有 browserslist 这一配置项，那么该配置项便是这里所说的第三方插件配置，该配置的主要作用是用于在不同的前端工具之间共享目标浏览器和 Node.js 的版本：

```javascript
"browserslist": [
    "> 1%", // 表示包含所有使用率 > 1% 的浏览器
    "last 2 versions", // 表示包含浏览器最新的两个版本
    "not ie <= 8" // 表示不包含 ie8 及以下版本
]
```

比如像 [autoprefixer](https://link.juejin.im/?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Fautoprefixer) 这样的插件需要把你写的 css 样式适配不同的浏览器，那么这里要针对哪些浏览器呢，就是上面配置中所包含的。

而如果写在 autoprefixer 的配置中，那么会存在一个问题，万一其他第三方插件也需要浏览器的包含范围用于实现其特定的功能，那么就又得在其配置中设置一遍，这样就无法得以共用。所以在 package.json 中配置 browserslist 的属性使得所有工具都会自动找到目标浏览器。

当然，你也可以单独写在 .browserslistrc 的文件中：

```shell
# Browsers that we support 

> 1%
last 2 versions
not ie <= 8
```

至于它是如何去衡量浏览器的使用率和版本的，数据都是来源于 [Can I Use](https://link.juejin.im/?target=https%3A%2F%2Fcaniuse.com%2F)。你也可以访问 [browserl.ist/](https://link.juejin.im/?target=http%3A%2F%2Fbrowserl.ist%2F) 去搜索配置项所包含的浏览器列表，比如搜索 `last 2 versions` 会得到你想要的结果，或者在项目终端运行如下命令查看：

```javascript
npx browserslist
```

除了上述插件的配置，项目中常用的插件还有：babel、postcss 等，有兴趣的同学可以访问其官网进行了解。

### vue-cli 包安装

在上述的教程中，我们使用 npm 或 yarn 进行了包的安装和配置，除了以上两种方法，vue-cli 3.x 还提供了其专属的 `vue add` 命令，但是需要注意的是该命令安装的包是以 @vue/cli-plugin 或者 vue-cli-plugin 开头，即只能安装 Vue 集成的包。

比如运行：

```shell
vue add jquery
```

其会安装 `vue-cli-plugin-jquery`，很显然这个插件不存在便会安装失败。又或者你运行：

```shell
vue add @vue/eslint
```

其会解析为完整的包名 `@vue/cli-plugin-eslint`，因为该包存在所以会安装成功。

同时，不同于 npm 或 yarn 的安装， `vue add` 不仅会将包安装到你的项目中，其还会改变项目的代码或文件结构，所以安装前最好提交你的代码至仓库。

另外 vue add 中还有两个特例，如下：

```shell
# 安装 vue-router
vue add router

# 安装 vuex
vue add vuex
```

这两个命令会直接安装 vue-router 和 vuex 并改变你的代码结构，使你的项目集成这两个配置，并不会去安装添加 vue-cli-plugin 或 @vue/cli-plugin 前缀的包。

## 第3章 构建基础：webpack 在 CLI 3 中的应用

webpack 作为目前最流行的项目打包工具，被广泛使用于项目的构建和开发过程中，其实说它是打包工具有点大材小用了，我个人认为它是一个集前端自动化、模块化、组件化于一体的可拓展系统，你可以根据自己的需要来进行一系列的配置和安装，最终实现你需要的功能并进行打包输出。

而在 Vue 的项目中，webpack 同样充当着举足轻重的作用，比如打包压缩、异步加载、模块化管理等等。

### webpack 的使用

####  1. 与 vue-cli 2.x 的差异

 vue-cli 2.x，那么你应该了解其构建出的目录会包含相应的 webpack 配置文件。

在 vue-cli 3.x 中你却见不到一份关于 webpack 的配置文件，3.x 提供了一种开箱即用的模式，即你无需配置 webpack 就可以运行项目，并且它提供了一个 vue.config.js 文件来满足开发者对其封装的 webpack 默认配置的修改。如图：

![vue-cli-webpack](C:\Users\Administrator\Desktop\Blog\vue.js\img\vue-cli-webpack.png)

#### 2. vue.config.js 的配置

通过上方新老版本的对比，我们可以清晰的看出 vue.config.js 的配置项结构，如果你构建的项目中没有该文件，那么你需要在根目录手动创建它。下面我们就来介绍一下其常用配置项的功能和用途：

**baseurl**

在第一节《Vue CLI 3 项目构建基础》中我们通过 vue-cli 3.x 成功构建并在浏览器中打开 `http://localhost:8080/` 展示了项目首页。如果现在你想要将项目地址加一个二级目录，比如：`http://localhost:8080/vue/`，那么我们需要在 vue.config.js 里配置 baseurl 这一项：

```javascript
// vue.config.js
module.exports = {
    ...
    
    baseUrl: 'vue',
    
    ...
}
```

其改变的其实是 webpack 配置文件中 output 的 `publicPath` 项，这时候你重启终端再次打开页面的时候我们首页的 url 就会变成带二级目录的形式。

**outputDir**

如果你想将构建好的文件打包输出到 output 文件夹下（默认是 dist 文件夹），你可以配置：

```javascript
// vue.config.js
module.exports = {
    ...
    
    outputDir: 'output',
    
    ...
}
```

然后运行命令 `yarn build` 进行打包输出，你会发现项目跟目录会创建 output 文件夹， 这其实改变了 webpack 配置中 output 下的 `path` 项，修改了文件的输出路径。

**productionSourceMap**

该配置项用于设置是否为生产环境构建生成 source map，一般在生产环境下为了快速定位错误信息，我们都会开启 source map：

```javascript
// vue.config.js
module.exports = {
    ...
    
    productionSourceMap: true,
    
    ...
}
```

该配置会修改 webpack 中 `devtool` 项的值为 `source-map`。

开启 source map 后，我们打包输出的文件中会包含 js 对应的 .map 文件，其用途可以参考：[JavaScript Source Map 详解](https://link.juejin.im/?target=http%3A%2F%2Fwww.ruanyifeng.com%2Fblog%2F2013%2F01%2Fjavascript_source_map.html)

**chainWebpack**

chainWebpack 配置项允许我们更细粒度的控制 webpack 的内部配置，其集成的是 [webpack-chain](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fmozilla-neutrino%2Fwebpack-chain)这一插件，该插件可以让我们能够使用链式操作来修改配置，比如：

```javascript
// 用于做相应的合并处理
const merge = require('webpack-merge');

module.exports = {
    ...
    
    // config 参数为已经解析好的 webpack 配置
    chainWebpack: config => {
        config.module
            .rule('images')
            .use('url-loader')
            .tap(options =>
                merge(options, {
                  limit: 5120,
                })
            )
    }
    
    ...
}
```

以上操作我们可以成功修改 webpack 中 module 项里配置 rules 规则为图片下的 url-loader 值，将其 limit 限制改为 5M，修改后的 webpack 配置代码如下：

```javascript
{
    ...
    
    module: {
        rules: [
            {   
                /* config.module.rule('images') */
                test: /\.(png|jpe?g|gif|webp)(\?.*)?$/,
                use: [
                    /* config.module.rule('images').use('url-loader') */
                    {
                        loader: 'url-loader',
                        options: {
                            limit: 5120,
                            name: 'img/[name].[hash:8].[ext]'
                        }
                    }
                ]
            }
        ]
    }
    
    ...
}
```

这里需要注意的是我们使用了 webpack-merge 这一插件，该插件用于做 webpack 配置的合并处理，这样 options 下面的其他值就不会被覆盖或改变。

关于 webpack-chain 的使用可以参考其 github 官方地址：[github.com/mozilla-neu…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fmozilla-neutrino%2Fwebpack-chain)，它提供了操作类似 JavaScript Set 和 Map 的方式，以及一系列速记方法。

![webpack-chain](C:\Users\Administrator\Desktop\Blog\vue.js\img\webpack-chain.png)

**configureWebpack**

除了上述使用 chainWebpack 来改变 webpack 内部配置外，我们还可以使用 configureWebpack 来进行修改，两者的不同点在于 chainWebpack 是链式修改，而 configureWebpack 更倾向于整体替换和修改。示例代码如下：

```javascript
// vue.config.js
module.exports = {
    ...
    
    // config 参数为已经解析好的 webpack 配置
    configureWebpack: config => {
        // config.plugins = []; // 这样会直接将 plugins 置空
        
        // 使用 return 一个对象会通过 webpack-merge 进行合并，plugins 不会置空
        return {
            plugins: []
        }
    }
    
    ...
}
```

configureWebpack 可以直接是一个对象，也可以是一个函数，如果是对象它会直接使用 webpack-merge 对其进行合并处理，如果是函数，你可以直接使用其 config 参数来修改 webpack 中的配置，或者返回一个对象来进行 merge 处理。

你可以在项目目录下运行 `vue inspect` 来查看你修改后的 webpack 完整配置，当然你也可以缩小审查范围，比如：

```shell
# 只查看 plugins 的内容
vue inspect plugins
```

**devServer**

vue.config.js 还提供了 devServer 项用于配置 webpack-dev-server 的行为，使得我们可以对本地服务器进行相应配置，我们在命令行中运行的 `yarn serve` 对应的命令 `vue-cli-service serve` 其实便是基于 webpack-dev-server 开启的一个本地服务器，其常用配置参数如下：

```javascript
// vue.config.js
module.exports = {
    ...
    
    devServer: {
        open: true, // 是否自动打开浏览器页面
        host: '0.0.0.0', // 指定使用一个 host。默认是 localhost
        port: 8080, // 端口地址
        https: false, // 使用https提供服务
        proxy: null, // string | Object 代理设置
        
        // 提供在服务器内部的其他中间件之前执行自定义中间件的能力
        before: app => {
          // `app` 是一个 express 实例
        }
    }
    
    ...
}
```

当然除了以上参数，其支持所有的 webpack-dev-server 中的选项，比如 `historyApiFallback` 用于重写路由（会在后续的多页应用配置中讲解）、progress 将运行进度输出到控制台等，具体可参考：[devServer](https://link.juejin.im/?target=https%3A%2F%2Fwww.webpackjs.com%2Fconfiguration%2Fdev-server%2F)

以上讲解了 vue.config.js 中一些常用的配置项功能，具体的配置实现需要结合实际项目进行，完整的配置项可以查看：[vue.config.js](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fvue-cli%2Fblob%2Fce3e2d475d63895cbb40f62425bb6b3237469bcd%2Fdocs%2Fzh%2Fconfig%2FREADME.md)

#### 3. 默认插件简介

通过对 vue.config.js 的了解，我们知道了 vue-cli 3.x 为我们默认封装了项目运行的常用 webpack 配置，那么它给我们提供了哪些默认插件，每一个 plugin 又有着怎样的用途呢？除了使用 `vue inspect plugins` 我们还可以通过运行 `vue ui` 进入可视化页面查看，步骤如下：

- 打开可视化页面，点击对应项目进入管理页面（如果没有对应项目，需要导入或新建）
- 点击侧边栏 Tasks 选项，再点击二级栏 inspect 选项
- 点击 Run task 按钮执行审查命令

最后我们从输出的内容中找到 plugins 数组，其包含了如下插件（配置项已经省略，增加了定义插件的代码）：

```javascript
// vue-loader是 webpack 的加载器，允许你以单文件组件的格式编写 Vue 组件
const VueLoaderPlugin = require('vue-loader/lib/plugin');

// webpack 内置插件，用于创建在编译时可以配置的全局常量
const { DefinePlugin } = require('webpack');

// 用于强制所有模块的完整路径必需与磁盘上实际路径的确切大小写相匹配
const CaseSensitivePathsPlugin = require('case-sensitive-paths-webpack-plugin');

// 识别某些类型的 webpack 错误并整理，以提供开发人员更好的体验。
const FriendlyErrorsPlugin = require('friendly-errors-webpack-plugin');

// 将 CSS 提取到单独的文件中，为每个包含 CSS 的 JS 文件创建一个 CSS 文件
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

// 用于在 webpack 构建期间优化、最小化 CSS文件
const OptimizeCssnanoPlugin = require('optimize-css-assets-webpack-plugin');

// webpack 内置插件，用于根据模块的相对路径生成 hash 作为模块 id, 一般用于生产环境
const { HashedModuleIdsPlugin } = require('webpack');

// 用于根据模板或使用加载器生成 HTML 文件
const HtmlWebpackPlugin = require('html-webpack-plugin');

// 用于在使用 html-webpack-plugin 生成的 html 中添加 <link rel ='preload'> 或 <link rel ='prefetch'>，有助于异步加载
const PreloadPlugin = require('preload-webpack-plugin');

// 用于将单个文件或整个目录复制到构建目录
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
    plugins: [
        /* config.plugin('vue-loader') */
        new VueLoaderPlugin(), 
        
        /* config.plugin('define') */
        new DefinePlugin(),
        
        /* config.plugin('case-sensitive-paths') */
        new CaseSensitivePathsPlugin(),
        
        /* config.plugin('friendly-errors') */
        new FriendlyErrorsWebpackPlugin(),
        
        /* config.plugin('extract-css') */
        new MiniCssExtractPlugin(),
        
        /* config.plugin('optimize-css') */
        new OptimizeCssnanoPlugin(),
        
        /* config.plugin('hash-module-ids') */
        new HashedModuleIdsPlugin(),
        
        /* config.plugin('html') */
        new HtmlWebpackPlugin(),
        
        /* config.plugin('preload') */
        new PreloadPlugin(),
        
        /* config.plugin('copy') */
        new CopyWebpackPlugin()
    ]
}
```

我们可以看到每个插件上方都添加了使用 chainWebpack 访问的方式，同时我也添加了每个插件相应的用途注释，需要注意的是要区分 webpack 内置插件和第三方插件的区别，如果是内置插件则无需安装下载，而外部插件大家可以直接访问：[www.npmjs.com/](https://link.juejin.im/?target=https%3A%2F%2Fwww.npmjs.com%2F) 搜索对应的插件，了解其详细的 api 设置。

## 第4章 构建基础篇:env 文件与环境设置



























