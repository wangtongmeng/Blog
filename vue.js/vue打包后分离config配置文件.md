# vue打包后分离config配置文件

需求：项目打包后，更改服务器需要重新配置接口地址，若不分离需要修改接口地址后重新打包。

解决方案：利用static中静态文件不被webpack打包的原理，创建 serverConfig.js文件用于存放和服务器相关的配置信息。

1.在static文件下创建serverConfig.js 文件

```js
window.serverConfig = {
    /** 
     * domain1 基础域名
     * domain2 第三方域名
     */
    baseUrl: { // api请求基础url
        domain1: '协议://主机名:端口',
        domain2: '协议://主机名:端口',
    }
}
```

2.在index.html入口文件中引入配置文件

```html
<script type="text/javascript" src="/static/serverConfig.js"></script>
```

3.在需要的地方通过window对象获取

```js
var urls = window.serverConfig.baseUrl
// 创建axios实例
const service = axios.create({
  baseURL: urls.domain1,
  timeout: 5000
})
```

4.最后在打包成功之后，serverConfig,js文件不会被打包，需要修改时通过开发工具或记事本打开修改地址即可。

其他方案

[vue打包后分离config配置文件](https://blog.csdn.net/benben0729/article/details/88545790)

[基于Vue-Cli 打包自动生成/抽离相关配置文件](https://juejin.im/post/5c0b8d89e51d454f7e2b9a7b)

[如何做到webpack打包vue项目后，可以修改配置文件](https://www.cnblogs.com/caimuqing/p/7094364.html)

[vue 接口请求地址前缀本地开发和线上开发设置](https://blog.csdn.net/wuyan1001/article/details/84840703)

