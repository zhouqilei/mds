## 1.项目的创建和文件划分

使用 vue ui 命令打开可视化的项目创建界面

将没有使用的组件和依赖删除，使项目处于纯净状态

在项目根目录下创建 .prettierrc.js 文件控项目的代码格式：

```js
module.exports = {
	semi: false, // 行位是否使用分号，默认为true
	trailingComma: 'none', // 是否使用尾逗号，有三个可选值"<none|es5|all>"
	singleQuote: true, // 字符串是否使用单引号，默认为false，使用双引号
	printWidth: 100, // 一行的字符数，如果超过会进行换行，默认为80
	tabWidth: 4, // 一个tab代表几个空格数
	useTabs: true, // 启用tab缩进
	bracketSpacing: true, // 对象大括号直接是否有空格，默认为true，效果：{ foo: bar }
}
```

在项目的src文件夹下进行文件划分：

```
│─src
  ├─assets 存放公共资源css和图片
    ├─css  全局css
    ├─img  
  ├─common  公共的一些常量
  ├─components 公共组件
  ├─views   路由映射页面
  ├─router  前端路由配置
  ├─service 网络配置和请求
  └─utils   工具函数
```

## 2.处理资源文件

以sass为例，安装相关编译插件:

```shell
 npm install sass-loader node-sass -D
```

注意可能会因为版本过高导致编译报错

在sass中引入图片资源需要在图片资源前面加~，如下：

```scss
.container {
	width: 100vw;
	height: 100vh;
  background: url('~@/assets/img/bg.jpg') no-repeat center;
  background-size: 100% 100%;
}
```

sass文件公共样式引用需要配置vue.config.js文件:

```js
module.exports = {
  css: {
    loaderOptions: {
      sass: {
        prependData: `@import "@/assets/css/common.scss";`
      }
    }
  }
};
```



## 3.vue-router 管理路由

安装：

```shell
npm install vue-router --save
```

在 router文件夹下创建 index.js 文件管理项目中的所有路由

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const Login = () => import('@/views/login/login.vue')

const routes = [{
    path: '/',
    redirect: '/login'
  },
  {
    path: '/login',
    component: Login
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: routes
})

export default router
```

在 main.js文件下引用路由配置：

```js
import router from './router'
new Vue({
  router: router,
  render: h => h(App),
}).$mount('#app')
```

## 4.axios安装与配置

安装：

```shell
npm install axios
```

在 service文件夹下创建文件index.js作为axios的实例配置文件，基本配置如下:

```js
import Vue from 'vue'
import axios from 'axios'

// axios的基本配置
const config = {
  baseURL: 'http://localhost:3000',
  timeout: 60000
}

// 创建axios实例
const _axios = axios.create(config)

// 设置请求过滤器
_axios.interceptors.request.use(request => {
  return request
}, error => {
  console.log(error)
})

// 设置响应过滤器
_axios.interceptors.response.use(response => {
  return response.data
}, error => {
  console.log(error)
})

// 挂载
Vue.prototype.$axios = _axios
```

在main.js中引入:

```js
// 引入 aixos
import '@/service/index'
```



## 5.配置cookie插件

安装:

```shell
npm install vue-cookies --save
```

在main.js 中引入:

```js
import VueCookies from 'vue-cookies'
Vue.use(VueCookies);
```

设置cookie：

```js
this.$cookies.set('key', value)
```

获取cookie:

```js
this.$cookies.get('key')
```

