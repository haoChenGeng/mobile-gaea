  1.0.0 是业务代码版本上线文件夹，lib/vendor.js 是静态文件第三库，不会随着业务代码更改而变化的。
3. webpack.config.js 是开发和编译项目的配置文件
4. webpack.dll.config.js 是编译抽离第三方库的配置文件
5. static/vendor.dll.js 和 static/vendor-manifest.json 是 npm run dll 生成的第三方库静态文件和索引文件

## Other Features

### 图片压缩篇
采用TinyPNG node.js API 进行在线压缩图片，并且转换Webp格式文件，需要去[官网](https://tinypng.com/developers)注册KEY，填入`package.json`文件
`tinypngkey`字段。每个账号每个月有500次的免费上传压缩限制。

### 路由篇
文件router.js 配置了脚手架的相关路由信息，推荐使用【history】路由。脚手架支持history路由和hash路由。在 router.js 中默认是history路由。它是真实的路由地址，所以需要后台那帮你配置重定向。

比如首页的路由是 http://telink.jd.com/index。那么你的路由的首页也是/index 。
比如搜索页/search 是不存在后端服务器上的。所以需要你让后端把其余的单页面的路由都重定指向首页的vm。

对于carefree，上传到测试服务器page.jd.com 默认是hash路由，方便大家进行测试
```bash
const router = new VueRouter({
    mode:carefree?'hash':'history',
    routes
});
```

### 骨架屏篇
脚手架提供了vue的骨架屏注入方案，在命令行工具选择骨架屏，就会下载骨架屏相对应的模板。

src/skeleton 就是基于[vue-server-renderer](https://github.com/vuejs/vue/tree/dev/packages/vue-server-renderer)服务端渲染，抽取手写骨架屏的css 和 html 注入到 打包的html中。

src/skeleton/skeleton.vue 文件就是手写的骨架屏组件，推荐只渲染入口页首屏骨架
npm run skeleton 就会将src/skeleton/index.html  生成到外层src/index.html
注入完成后，就可以后续正常开发

### SMOCK篇
smock 是开发阶段基于swagger的自动化mock假数据工具，需要配置参数如下：
修改package.json 中字段，具体可以[参看](https://smock.jd.com/)

```bash
"smock": {
      "host": "",
      "domain": "",
      "projectName": ""
}
```

## Note
* 上线逻辑，前后端分离上线，lib/vendor.js 属于第三方库会发生变动机会比较小，所以在后续迭代可以不需要上线，只需要上线1.0.0/或者1.0.1/版本的文件
* 如果是覆盖上线，需要统一一次刷新cdn所有静态资源路径，因为整个build包是一个整体。如果是流量较高的业务，建议新增版本上线，覆盖版本上线有小风险。
* 使用carefree时候，注意自己的cmd等是黑色背景主体，不然二维码是反的。

## Plan
[开发计划](https://github.com/jdf2e/Gaea4/blob/master/PLANS.md)

## Change Log
[更新日志](https://github.com/jdf2e/Gaea4/blob/master/CHANGELOG.md)

## License
MIT License - [LICENSE](./LICENSE)

