# edu-boss-fed

### 项目地址：http://117.50.13.207:8090/

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### 打包后本地预览
```
yarn preview
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).



1. 说说 application/json 和 application/x-www-form-urlencoded 二者之间的区别。

   - application/json 提交的数据是序列化后的 JSON 字符串
   - application/x-www-form-urlencoded提交的数据按照 key1=val1&key2=val2 的方式进行编码

2. 说一说在前端这块，角色管理你是如何设计的。

   - 可以主动新增角色
   - 可以为每个角色分配菜单权限
   - 可以为每个角色分配资源权限
   - 每个用户可以有多个角色来管理不同页面

3. @vue/cli 跟 vue-cli 相比，@vue/cli 的优势在哪？

   - 抽离cli service层
   - 一个运行时依赖 (@vue/cli-service)，该依赖：
     - 可升级；
     - 基于 webpack 构建，并带有合理的默认配置；
     - 可以通过项目内的配置文件进行配置；
     - 可以通过插件进行扩展。
   - 一个丰富的官方插件集合，集成了前端生态中最好的工具。
   - 一套完全图形化的创建和管理 Vue.js 项目的用户界面。