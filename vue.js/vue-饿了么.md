# vue 饿了么

## 导学

 **课程目标**

开发体验媲美原生 APP 的饿了么商家页面

内容：商品列表页、评价页面、商家页面、各种组件

技术栈：vue.js 2.5.17、Vue-CLI 3.0、Cube-UI

![vue饿了么-核心技术](C:\Users\wangtongmeng\Desktop\Blog\vue.js\img\vue饿了么-核心技术.png)

**课程安排**：

- 第1章 准备工作
- 第2-6章 实战开发
- 第7章 create-api 原理介绍
- 第8章 项目打包和部署

**课程收获**

- 学会使用 Vue.js 开发 WebApp 应用
- 学会组件化、模块化的方式
- 学会使用第三方组件库辅助我们的开发
- 学会项目的部署构建过程

## 第2章 项目准备工作

### vue-cli 3 创建项目

```shell
vue create vue-sell-cube
```

配置

```shell
? Please pick a preset: Manually select features
? Check the features needed for your project: Babel, CSS Pre-processors, Linter? Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default): Stylus
? Pick a linter / formatter config: Standard
? Pick additional lint features: Lint on save
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? In dedicated config files
? Save this as a preset for future projects? No
? Pick the package manager to use when installing dependencies: NPM
```

进入并启动项目

```shell
cd vue-sell-cube
npm run serve
```

### cube-ui 安装

 vue 的移动端UI框架

安装 vue-cli 

```shell
vue add cube-ui
```

配置

- 使用后编译（减少打包体积）
- 部分引入 type（减少代码体积）
- 自定义主题
- 不适用 rem、vw

```shell
? Use post-compile? Yes
? Import type Partly
? Custom theme? Yes
? Use rem layout? No
? Use vw layout? No
```

### api 接口 mock

项目根目录创建，data.json 用于存储 mock 数据，数据结构如下：

```json
{
    "seller": {},
    "goods": {},
    "ratings": []
}
```

在 vue.config.js 中引入并配置 mock api，使用 webpack 内置的 devServer，设置before()

```json
const appData = require('./data.json')
const seller = appData.seller
const goods = appData.goods
const ratings = appData.ratings

module.exports = {
  ...,
  devServer: {
    before(app) {
      app.get('/api/seller', function (req, res) {
        res.json({
          errno: 0,
          data: seller
        })
      })
      app.get('/api/goods', function (req, res) {
        res.json({
          errno: 0,
          data: goods
        })
      })
      app.get('/api/ratings', function (req, res) {
        res.json({
          errno: 0,
          data: ratings
        })
      })
    }
  }
}
```



