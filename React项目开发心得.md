## 1.项目创建

 使用react脚手架创建react-app

```shell
creact-react-app music_pro
cd music_pro
npm start
```

## 2.项目文件划分

文件目录结构的划分

```
│─src
  ├─assets 存放公共资源css和图片
    ├─css  全局css
    ├─img  
  ├─common  公共的一些常量
  ├─components 公共组件
  ├─pages   路由映射组件
  ├─router  前端路由配置
  ├─service 网络配置和请求
  └─store   全局的store配置
  └─utils   工具函数
  └─hooks   自定义hook
```

## 3.项目的样式选择

使用normalize.css使不同浏览器在渲染网页元素时保持样式的统一

```shell
yarn add normalize.css
```

创建一个reset.css用于全局样式的初始化,该初始化对应的自己的项目中可能用到的通用样式

```css
/* reset.css (自定义的css) */
@import '~normalize.css';
@import '~antd/dist/antd.css';

/* 样式的重置 */
body, html, h1, h2, h3, h4, h5, h6, ul, ol, li, dl, dt, dd, header, menu, section, p, input, td, th, ins {
  padding: 0;
  margin: 0;
}

ul, ol, li {
  list-style: none;
}

a {
  text-decoration: none;
  color: #666;
}

a:hover {
  color: #666;
  text-decoration: underline;
}

i, em {
  font-style: normal;
}

input, textarea, button, select, a {
  outline: none;
  border: none;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

img {
  border: none;
  vertical-align: middle;
}

/* 全局样式 */
body, textarea, select, input, button {
  font-size: 12px;
  color: #333;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #f5f5f5;
}

.text-nowrap {
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}

.w1100 {
  width: 1100px;
  margin: 0 auto;
}

.w980 {
  width: 980px;
  margin: 0 auto;
}

.text-indent {
  text-indent: -9999px;
}

.inline-block {
  display: inline-block;
}

.sprite_01 {
  background: url(../img/sprite_01.png) no-repeat 0 9999px;
}

.sprite_02 {
  background: url(../img/sprite_02.png) no-repeat 0 9999px;
}

.sprite_cover {
  background: url(../img/sprite_cover.png) no-repeat 0 9999px;
}

.sprite_icon {
  background: url(../img/sprite_icon.png) no-repeat 0 9999px;
}

.sprite_icon2 {
  background: url(../img/sprite_icon2.png) no-repeat 0 9999px;
}

.sprite_button {
  background: url(../img/sprite_button.png) no-repeat 0 9999px;
}

.sprite_button2 {
  background: url(../img/sprite_button2.png) no-repeat 0 9999px;
}

.sprite_table {
  background: url(../img/sprite_table.png) no-repeat 0 9999px;
}

.my_music {
  background: url(../img/mymusic.png) no-repeat 0 9999px;
}

.not-login {
  background: url(../img/notlogin.jpg) no-repeat 0 9999px;
}

.image_cover {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  text-indent: -9999px;
  background: url(../img/sprite_cover.png) no-repeat -145px -57px;
}

.sprite_player {
  background: url(../img/playbar_sprite.png) no-repeat 0 9999px;
}

.lyric-css .ant-message-notice-content {
  position: fixed;
  left: 50%;
  bottom: 50px;
  transform: translateX(-50%);
  background-color: rgba(0,0,0,.5);
  color: #f5f5f5;
}

.wrap-bg2 {
  background: url(../img/wrap3.png) repeat-y center 0;;
}

```

使用styled-components来防止react项目中的组件间的样式冲突问题：

```shell
yarn add styled-components
```



## 4.配置路由别名

安装：

```shell
yarn add @craco/craco
```

修改package.json文件：

```json
"scripts": {
-"start": "react-scripts start",
-"build": "react-scripts build",
-"test": "react-scripts test",

\+ "start": "craco start",
\+ "build": "craco build",
\+ "test": "craco test",
}

```

在项目根目录下创建craco.config.js文件进行路由别名配置：

```js
// 根路径 -> craco.config.js
const path = require('path')
const resolve = dir => path.resolve(__dirname, dir)

module.exports = {
  webpack: {
    alias: {
       // @映射src路径
      '@': resolve('src'),
      'components': resolve('src/components')
    }
  }
}
```

## 5.页面路由相关配置

安装router:

```shell
yarn add react-router-dom
```

安装react-router-config集中式配置路由映射：

```shell
yarn add react-router-config
```

在router/文件夹下创建index.js文件对路由映射进行集中管理：

```js
// 配置项目中的路由映射

import Discover from '@/pages/discover'
import Mine from '@/pages/mine'
import Friend from '@/pages/friend'

const routes = [
  {
    path: '/',
    exact: true,
    render: () => < Redirect to = "/discover" / >
  },
  {
    path: "/discover",
    component: Discover
  },
  {
    path: "/mine",
    component: Mine
  },
  {
    path: "/friend",
    component: Friend
  }
]
export default routes
```

在App.js文件中对路由进行配置：

```js

import { BrowserRouter } from 'react-router-dom'
import { renderRoutes } from 'react-router-config'
import routes from './router/index'

import AppHeader from 'components/app-header'
import AppFooter from 'components/app-footer'

function App() {
  return (
    <BrowserRouter>
      <AppHeader/>
      {renderRoutes(routes)}
      <AppFooter/>
    </BrowserRouter>
  );
}

export default App;

```

## 6.使用axios进行网络请求

安装axios

```shell
yarn add axios
```

在 src文件加下新建service文件,用于网络请求相关的文件

## 7.使用redux管理状态

安装redux:

```shell
yarn add redux react-redux redux-thunk
```

在store文件加下创建index.js和reducer.js

在reducer.js文件中进行多个reducer合并：

```js
import { combineReducers } from "redux";
// 将多个reducer合并
const cRducer = combineReducers({
   //具体的reducer
})
export default cRducer

```

在index.js中配置store：

```js
import { createStore, applyMiddleware, compose } from "redux";
// 引入thunk中间件(可以让派发的action可以是一个函数)
import thunk from 'redux-thunk'
// 引入合并后的reducer
import cRducer from "./reducer";
// redux-devtools -> 浏览器插件
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
// 创建store并传递: 1.reducer(纯函数) 2.StoreEnhancer
const store = createStore(cRducer, composeEnhancers(
  applyMiddleware(thunk)
))

export default store

```

在App.js文件中配置react-redux:

```jsx
// 在App.js组件中使用react-redux
import { Provider } from 'react-redux'
import { renderRoutes } from 'react-router-config'
import store from './store'
function App() {
  return (
    <Provider store={store}>
      {/*...*/}
    </Provider>
  );
}

export default App;

```

