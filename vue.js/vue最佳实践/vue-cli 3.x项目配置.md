# vue-cli 3.x项目配置 

vue-cli项目基于 webpack 构建，并带有合理的默认配置；可以通过项目内的配置文件进行配置；可以通过插件进
行扩展。 

- webpack相关配置，请在根目录创建vue.config.js 

```js
// vue.config.js
const port = 7070;
const title = "vue项目最佳实践";
module.exports = {
  publicPath: '/best-practice', // 部署应用包时的基本 URL
  devServer: {
 		port: port,
  },
  configureWebpack: {
    // 向index.html注入标题
    name: title
  }
};
// public/index.html
<title><%= webpackConfig.name %></title>
```

>  注意：以上配置要求vue-cli-service版本>=3.5

通过命令查看配置结果：

```shell
vue inspect 全部配置
vue inspect --rules 查看全部规则
vue inspect --rule vue 查看指定规则
vue inspect --plugins 查看全部插件
vue inspect --plugin vue-plugin 查看指定插件
vue inspect --mode development 指定模式
```
通过ui查看配置结果：
```shell
vue ui 
```



