# vue-history-storage

### What

> 一个vue历史路由持久化的解决方案。

##### 目前功能

1. 持久化用户浏览记录，并在重新进入vue应用时自动恢复原来的路径。
2. 进入vue应用没有历史记录时，自动创建前置历史记录，使应用可以“返回”到上一级页面。
3. 当路由到达根目录时，防止继续后退（因为原来是从其他网站跳转到这个vue应用）而退出vue作用范围。
4. 路由变更时触发前进（router.goforward）、后退（router.goback）、覆盖（router.replace）、到达根目录（router.inroot）事件。

### Why

Vue中使用HTML5 history历史模式时，能通过浏览器进行前进后退操作。但是，当在地址栏直接填写多级路由地址或者从外部链接跳转到Vue应用的多级路由时，会造成历史记录丢失、无法回退上级页面的尴尬情况。本方案则为vue提供历史记录重构和持久化的功能，解决历史记录丢失和无法回退的问题。

如果你的vue应用需要跳转到第三方页面，再跳转回来时，想恢复到原来的历史记录并继续操作，使用本插件是最好的解决方案。

### How

基于localStorage/cookie存储，在Vue实例创建时，先检查本地是否保存这以前的历史记录，如果没有，则把路由路径保存下来，同时通过history.pushState方法，把路由匹配路径注入到浏览器的历史记录中，使浏览器获得回退到上级路由；如果有保存历史记录，则将历史记录注入到浏览器中，使用户重新打开网页时能继续上次的操作。

### Screenshot

![](https://github.com/ElderJames/vue-router-storage/blob/master/screenshot/vue-router-storage-example.gif?raw=true)

## Use Setup

1. 命令行执行npm安装包
``` bash
# install vue-router-storage package
npm install --save vue-router-storage

```
2. 在入口文件加入以下代码
```javascript
import Vue from 'vue'
import RouterStorage from 'vue-router-storage'

Vue.use(RouterStorage);
```

3. 在webpack中加入以下配置
```javascript
    resolve: {
        ...
        alias: {
            'vue-router-storage': 'vue-router-storage/dist/vue-router-storage.esm.js',
        }
    },
```

尽情享用吧！

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
