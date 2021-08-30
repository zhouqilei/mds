# 

Vue.js 笔记

## 项目基本结构的搭建

基于 Vite + Vue3 + TypeScript 的前端工程化项目环境的搭建

**使用Vite快速初始化项目的雏形**

```sh
npm init @vitejs/app <project-name> --template vue-ts
cd <project-name>
npm install
npm run dev
```

**修改Vite的配置文件**

项目根目录下存在Vite的配置文件  `vite.config.ts` ,项目启动时会读取

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
// 如果编辑器提示 path 模块找不到，则可以安装一下 @types/node -> npm i @types/node -D
import { resolve } from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src')
    }
  },
  base: './', //打包路径
  server: {
    port: 3000,
    cors: true, //是否跨域
    // 设置代理，根据我们项目实际情况配置
    // proxy: {
    //   '/api': {
    //     target: 'http://xxx.xxx.xxx.xxx:8000',
    //     changeOrigin: true,
    //     secure: false,
    //     rewrite: (path) => path.replace('/api/', '/')
    //   }
    // }
  }
})

```

**使用路由工具Vue Router**

1. 安装支持Vue3的路由工具 vue-router@4

```sh
npm i vue-router@4
```

2. 创建路由的管理文件 src/router/index.ts

```javascript
import {
  createRouter,
  createWebHashHistory,
  RouteRecordRaw
} from 'vue-router'

const routes: Array<RouteRecordRaw> = [
  // {
  //   path: '/',
  //   component:{}
  // }
]

const router = createRouter({
  history: createWebHashHistory(),
  routes
})

export default router
```

3. 在main.ts 文件中挂载路由配置

   ```javascript
   import { createApp } from 'vue'
   import App from './App.vue'
   
   import router from './router/index'
   
   createApp(App).use(router).mount('#app')
   
   ```

**集成UI框架 Element Plus**

1. 安装 element plus

   ```sh
   npm i element-plus
   ```

2. 在 main.ts 中引入

   ```javascript
   import { createApp } from 'vue'
   import App from './App.vue'
   
   import ElementPlus from 'element-plus'
   import 'element-plus/lib/theme-chalk/index.css'
   
   import router from './router/index'
   
   createApp(App).use(router).mount('#app')
   
   ```

   

**集成HTTP工具Axios**

1. 安装 axios

   ```sh
   npm i axios
   ```

2. 在 /utils/ 下创建 axios.ts 文件作为 Axios配置文件

   ```
   import Axios from 'axios'
   
   const baseURL = 'http://127.0.0.1:4000'
   
   const axios = Axios.create({
     baseURL,
     timeout: 100000  //超时时间为10s
   })
   
   // 请求拦截器
   axios.interceptors.request.use(req => {
     return req
   }, error => {
     return Promise.reject(error)
   })
   
   // 响应拦截器
   axios.interceptors.response.use(res => {
     return res
   }, error => {
     return Promise.reject(error)
   })
   
   export default axios
   ```

**集成Css预编译器 Stylus/Sass/Less**

Vite 内部已帮我们集成了相关的 loader，不需要额外配置。

1. 安装

   ```sh
   npm i sass -D
   ```

2. 使用

   ```javascript
   <style lang="scss">
     ...
   </style>
   ```

3. 引用

   ```
   @import url("./style/index.scss");
   ```

   

**集成EditorConfig配置**

EditorConfig 有助于为不同 IDE 编辑器上处理同一项目的多个开发人员维护一致的编码风格。

在项目根目录下增加 .editorconfig文件

VSCode 使用 EditorConfig 需要去插件市场下载插件 **EditorConfig for VS Code** 。

```
# Editor configuration, see http://editorconfig.org

# 表示是最顶层的 EditorConfig 配置文件
root = true

[*] # 表示所有文件适用
charset = utf-8 # 设置文件字符集为 utf-8
indent_style = space # 缩进风格（tab | space）
indent_size = 2 # 缩进大小
end_of_line = lf # 控制换行类型(lf | cr | crlf)
trim_trailing_whitespace = true # 去除行首的任意空白字符
insert_final_newline = true # 始终在文件末尾插入一个新行

[*.md] # 表示仅 md 文件适用以下规则
max_line_length = off
trim_trailing_whitespace = false

```

## Vue-Router 的使用

**在 App.vue 中使用 router-view**

```vue
<template>
  <router-view></router-view>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
});
</script>

<style lang="scss">
@import url("./style/index.scss");
</style>

```

**路由动态引入**

```
const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    redirect: '/login'
  },
  {
    path: '/login',
    component: Login
  }
]
```

**在页面中添加beforeRouteUpdate监听路由的改变**

```javascript
beforeRouteUpdate(to, from, next) {
    const query = to.query;
    console.info(query);
    next();
},
```



## 跨域的实现

1. 在vite.config.js 文件中修改配置

   ```javascript
   import { defineConfig } from 'vite'
   import vue from '@vitejs/plugin-vue'
   // 如果编辑器提示 path 模块找不到，则可以安装一下 @types/node -> npm i @types/node -D
   import { resolve } from 'path'
   
   // https://vitejs.dev/config/
   export default defineConfig({
     plugins: [vue()],
     resolve: {
       alias: {
         '@': resolve(__dirname, 'src')
       }
     },
     base: './', //打包路径
     server: {
       host: '0.0.0.0',
       port: 3000,
       proxy: {
         '/api': {
        		// 接口调用路径   
           target: 'http://localhost:4000/',
           changeOrigin: true,
           ws: true,
           rewrite: (path) => path.replace('/api', '')
         }
       }
     }
   })
   
   ```

   2. 修改 axios请求的baseURL

      ```javascript
      const baseURL = '/api'
      
      const axios = Axios.create({
        baseURL,
        timeout: 100000  //超时时间为10s
      })
      ```

      

## js-cookie 使用

1. 安装 js-cookie

   ```sh
   npm i js-cookie
   ```

   

2. 使用

   ```javascript
   import Cookies from 'js-cookie'
   //设置
   Cookies.set('key',value,{expires:7})
   //获取 
   Cookies.get('key')
   ```

   

3. 注意会出现typescript语言找不到包的类型的报错，可以通过配置tsconfig.json解决

   ```json
       "noImplicitAny": false
   ```

   

## 全局事件监听Bus类的实现

1. 新建一个bus.ts 文件作为全局事件监听处理类

```
class Bus {
  list: { [key: string]: Array<Function> };
  constructor() {
    this.list = {}
  }
  // 订阅
  $on(name: string, fn: Function) {
    this.list[name] = this.list[name] || [];
    this.list[name].push(fn)

  }
  // 发布
  $emit(name: string, data?: any) {
    if (this.list[name]) {
      this.list[name].forEach((fn: Function) => {
        fn(data);
      });
    }
  }
  // 取消
  $off(name: string) {
    if (this.list[name]) {
      delete this.list[name];
    }
  }
}

export default new Bus()
```

2. 具体使用

   ```javascript
   import bus from '../utils/bus'
   
   //订阅
   bus.$on('eventName',(data)=>{});
   //发布
   bus.$emit('eventName',data);
   //取消
   bus.$off('eventName')
   ```

   