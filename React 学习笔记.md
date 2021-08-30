## React.js 相关JS库介绍

- react.js - React 的核心库
- react-dom.js 提供DOM操作的React扩展库
- babel.min.js 解析JSX语法为JS代码

## JSX语法介绍

- react定义的一种类似XML的js扩展语法
- 基本语法规则
  - 遇到 **<** 开头的代码，以标签的语法解析，html同名标签转换成为html同名元素，其它标签需要特别解析
  - 遇到以**{** 开头的代码，以js语法解析，标签中的js表达式必须用**{}** 包含
- 使用jsx需要加上 type="text/babel"声明需要babel来处理

## 简单创建一个React 实例

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React</title>
</head>

<body>
  <div id="container">

  </div>

  <!-- 引入react核心库 -->
  <script type="text/javascript" src="./js/react.development.js"></script>
  <!-- 引入react-dom，用于支持react操作DOM -->
  <script type="text/javascript" src="./js/react-dom.development.js"></script>
  <!-- 引入babel，用于将jsx转为js -->
  <script type="text/javascript" src="./js/babel.min.js"></script>
  <script type="text/babel">
    const VDom = <h1>Hello React</h1>
    ReactDOM.render(VDom,document.getElementById('container'))
  </script>

</body>

</html>
```

## React 组件式开发

- 函数式组件的定义

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
  </head>
  
  <body>
    <div id="container">
  
    </div>
  
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="./js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作DOM -->
    <script type="text/javascript" src="./js/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="./js/babel.min.js"></script>
    <script type="text/babel">
  
      /*定义函数返回组件模板*/
      function MyComponent() {
        return <h1>使用函数定义一个组件</h1>
      }
      // 渲染
      ReactDOM.render(<MyComponent/>,document.getElementById('container'))
    </script>
  
  </body>
  
  </html>
  ```

- 使用类定义一个组件

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
  </head>
  
  <body>
    <div id="container">
  
    </div>
  
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="./js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作DOM -->
    <script type="text/javascript" src="./js/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="./js/babel.min.js"></script>
    <script type="text/babel">
  
      // 定义一个类组件继承自React.Component
      class MyComponent extends React.Component{
        // 通过render函数返回组件结构
        render() {
          return <h1>我是用类定义的组件</h1>
        }
      }
  
      // 渲染
      ReactDOM.render(<MyComponent/>,document.getElementById('container'))
    </script>
  
  </body>
  
  </html>
  ```

## React 三大组件之state

- state 是组件对象最重要属性，是一个对象，保存组件的状态数据

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
  </head>
  
  <body>
    <div id="container">
  
    </div>
  
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="./js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作DOM -->
    <script type="text/javascript" src="./js/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="./js/babel.min.js"></script>
    <script type="text/babel">
  
      // 定义一个天气组件
      class Weather extends React.Component {
        // 状态
        state = {
          isHot:true
        }
        // 渲染
        render() {
          const {isHot} = this.state
          return <h1 onClick={this.changeWeather}>今天天气很 {isHot ? '炎热' : '凉爽'}</h1>
        }
        // 修改状态方法
        changeWeather = ()=>{
          let isHot = this.state.isHot;
          this.setState({
            isHot:!isHot
          })
        }
      }
  
      // 渲染
      ReactDOM.render(<Weather/>,document.getElementById('container'))
    </script>
  
  </body>
  
  </html>
  ```

## React 三大组件之props

- 每个组件都有props属性，通过props从组件外向组件内部传递数据,props中的属性是只读的

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React</title>
  </head>
  
  <body>
    <div id="container">
  
    </div>
  
    <!-- 引入react核心库 -->
    <script type="text/javascript" src="./js/react.development.js"></script>
    <!-- 引入react-dom，用于支持react操作DOM -->
    <script type="text/javascript" src="./js/react-dom.development.js"></script>
    <!-- 引入babel，用于将jsx转为js -->
    <script type="text/javascript" src="./js/babel.min.js"></script>
    <!-- 引入prop-types，用于对组件标签属性进行限制 -->
    <script type="text/javascript" src="./js/prop-types.js"></script>
    <script type="text/babel">
  
      //定义一个Person组件
      class Person extends React.Component {
        constructor(props) {
          super(props)
  
        }
        
        static propTypes = {
          name:PropTypes.string.isRequired, //限制name必传，且为字符串
  				sex:PropTypes.string,//限制sex为字符串
  				age:PropTypes.number,//限制age为数值
        }
  
        static defaultProps = {
          sex:'男',//sex默认值为男
  				age:18 //age默认值为18
        }
  
        render() {
          const {name,age,sex} = this.props
          return (
            <ul>
              <li>名字：{name}</li>
              <li>年龄：{age}</li>
              <li>性别：{sex}</li>
            </ul>
          )
        }
      }
      // 渲染
      ReactDOM.render(<Person name="张三" />,document.getElementById('container'))
    </script>
  
  </body>
  
  </html>
  ```

## React 三大组件之refs

- 通过在主键中定义ref属性来对组件进行标识

- 三种组件的ref标记方式

  - 字符串

    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>React</title>
    </head>
    
    <body>
      <div id="container">
    
      </div>
    
      <!-- 引入react核心库 -->
      <script type="text/javascript" src="./js/react.development.js"></script>
      <!-- 引入react-dom，用于支持react操作DOM -->
      <script type="text/javascript" src="./js/react-dom.development.js"></script>
      <!-- 引入babel，用于将jsx转为js -->
      <script type="text/javascript" src="./js/babel.min.js"></script>
      <!-- 引入prop-types，用于对组件标签属性进行限制 -->
      <script type="text/javascript" src="./js/prop-types.js"></script>
      <script type="text/babel">
    
        //定义一个组件
        class Demo extends React.Component {
    
          render() {
            return (
              <div>
                <input type="text" ref="input" /> &nbsp;
                <button onClick={this.showMsg}>显示信息</button>
              </div>
            ) 
          }
    
          showMsg = ()=>{
            const {input} = this.refs
            alert(input.value)
          }
        }
        // 渲染
        ReactDOM.render(<Demo />,document.getElementById('container'))
      </script>
    
    </body>
    
    </html>
    ```

  - 回调

    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>React</title>
    </head>
    
    <body>
      <div id="container">
    
      </div>
    
      <!-- 引入react核心库 -->
      <script type="text/javascript" src="./js/react.development.js"></script>
      <!-- 引入react-dom，用于支持react操作DOM -->
      <script type="text/javascript" src="./js/react-dom.development.js"></script>
      <!-- 引入babel，用于将jsx转为js -->
      <script type="text/javascript" src="./js/babel.min.js"></script>
      <!-- 引入prop-types，用于对组件标签属性进行限制 -->
      <script type="text/javascript" src="./js/prop-types.js"></script>
      <script type="text/babel">
    
        //定义一个组件
        class Demo extends React.Component {
    
          render() {
            return (
              <div>
                <input type="text" ref={c=>this.input = c} /> &nbsp;
                <button onClick={this.showMsg}>显示信息</button>
              </div>
            ) 
          }
          showMsg = ()=>{
            alert(this.input.value)
          }
        }
        // 渲染
        ReactDOM.render(<Demo />,document.getElementById('container'))
      </script>
    
    </body>
    
    </html>
    ```

  - creatRef创建ref容器

    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>React</title>
    </head>
    
    <body>
      <div id="container">
    
      </div>
    
      <!-- 引入react核心库 -->
      <script type="text/javascript" src="./js/react.development.js"></script>
      <!-- 引入react-dom，用于支持react操作DOM -->
      <script type="text/javascript" src="./js/react-dom.development.js"></script>
      <!-- 引入babel，用于将jsx转为js -->
      <script type="text/javascript" src="./js/babel.min.js"></script>
      <!-- 引入prop-types，用于对组件标签属性进行限制 -->
      <script type="text/javascript" src="./js/prop-types.js"></script>
      <script type="text/babel">
    
        //定义一个组件
        class Demo extends React.Component {
    
          inputRef = React.createRef()
    
          render() {
            return (
              <div>
                <input type="text" ref={this.inputRef} /> &nbsp;
                <button onClick={this.showMsg}>显示信息</button>
              </div>
            ) 
          }
          showMsg = ()=>{
            alert(this.inputRef.current.value)
          }
        }
        // 渲染
        ReactDOM.render(<Demo />,document.getElementById('container'))
      </script>
    
    </body>
    
    </html>
    ```

## React 事件处理

- 通过 onXxx 属性绑定事件处理函数（注意大小写）
  - React 中使用的是自定义事件而不是原生事件
  - React中的事件是通过事件委托处理的（委托给组件的最外层原生）
- 通过event.target 得到发生事件的dom元素对象

## React 生命周期

- 旧版生命周期图

  ![react生命周期(旧)](/Users/zhouqilei/Documents/学习笔记/react生命周期(旧).png)

- 新生命周期图片

  ![react生命周期(新)](/Users/zhouqilei/Documents/学习笔记/react生命周期(新).png)

- 重要的生命周期函数
  - render 初次渲染或更新渲染时调用
  - componentDidMount: 组件挂载完毕 开启监听，发送ajax请求
  - componentWillUnmount: 组件即将卸载，收尾工作

## React 脚手架

- 使用脚手架创建React项目

  - 全局安装脚手架

    ```shell
    npm i -g create-react-app
    ```

  - 在要创建项目的位置开始创建项目

    ```shell
    create-react-app xxxx
    ```

  - 进入到项目根目录

    ```shell
    cd xxx
    ```

  - 运行项目

    ```shell
    npm start
    ```

- 项目结构说明

  ​	public --- 静态资源文件夹

  ​			favicon.icon 网站叶签图标

  ​			index.html 主页面

  ​			logo192.png logo图

  ​			logo512.png  logo图

  ​			manifest.json 应用加壳的配置文件

  ​			robots.txt  爬虫协议文件

  ​	src --- 源码文件夹

  ​			App.css   App组件的样式

  ​			App.js   App组件

  ​			App.test.js   用于给App做测试

  ​			index.css   样式

  ​			index.js   入口文件

  ​			logo.svg   logo图片

  ​			reportWebVitals.js   页面性能分析文件 需要web-vitals库的支持

  ​			setupTests.js   组件单元测试文件 需要jest-dom库的支持

- 脚手架配置代理

  - 在 src/ 下创建代理配置文件 setupProxy.js

  - 编写setupProxy.js配置

    ```js
    const proxy = require('http-proxy-middleware')
       
       module.exports = function(app) {
         app.use(
           proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
             target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
             changeOrigin: true, //控制服务器接收到的请求头中host字段的值
             /*
             	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
             	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
             	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
             */
             pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
           }),
           proxy('/api2', { 
             target: 'http://localhost:5001',
             changeOrigin: true,
             pathRewrite: {'^/api2': ''}
           })
         )
       }
    ```

- 使用pubsub-js 实现消息发送与监听

  - 安装

    ```shell
    npm i pubsub-js
    ```

  - 注册监听

    ```js
    // 引入
    import PubSub from 'pubsub-js'
    // 注册
    this.sub =  PubSub.subscribe('messageName',(_,data)=>{
    	...
    })
    // 销毁
    PubSub.unsubscribe(this.sub)
    ```

  - 发送消息

    ```js
    PubSub.publish('messageName',data)
    ```



## react-router-dom 

- 安装

  ```shell
  npm i react-router-dom
  ```

- 基本使用

  - 在index.js中使用BrowserRouter包裹App组件

    ```js
    //引入react核心库
    import React from 'react'
    //引入ReactDOM
    import ReactDOM from 'react-dom'
    //
    import {BrowserRouter} from 'react-router-dom'
    //引入App
    import App from './App'
    
    ReactDOM.render(
    	<BrowserRouter>
    		<App/>
    	</BrowserRouter>,
    	document.getElementById('root')
    )
    
    ```

  - 在具体页面实现路由

    ```jsx
    import React, { Component } from 'react'
    import {Link,Route} from 'react-router-dom'
    import Home from './components/Home'
    import About from './components/About'
    
    export default class App extends Component {
    	render() {
    		return (
    			<div>
    				<div className="row">
    					<div className="col-xs-offset-2 col-xs-8">
    						<div className="page-header"><h2>React Router Demo</h2></div>
    					</div>
    				</div>
    				<div className="row">
    					<div className="col-xs-2 col-xs-offset-2">
    						<div className="list-group">
    
    							{/* 原生html中，靠<a>跳转不同的页面 */}
    							{/* <a className="list-group-item" href="./about.html">About</a>
    							<a className="list-group-item active" href="./home.html">Home</a> */}
    
    							{/* 在React中靠路由链接实现切换组件--编写路由链接 */}
    							<Link className="list-group-item" to="/about">About</Link>
    							<Link className="list-group-item" to="/home">Home</Link>
    						</div>
    					</div>
    					<div className="col-xs-6">
    						<div className="panel">
    							<div className="panel-body">
    								{/* 注册路由 */}
    								<Route path="/about" component={About}/>
    								<Route path="/home" component={Home}/>
    							</div>
    						</div>
    					</div>
    				</div>
    			</div>
    		)
    	}
    }
    
    ```

- NavLink 组件使用

  ```
  import {NavLink,Route} from 'react-router-dom'
  
  <NavLink activeClassName="menuActived" className="list-group-item" to="/about">About</NavLink>
  <NavLink activeClassName="menuActived" className="list-group-item" to="/home">Home</NavLink>
  ```

- Switch组件可以使被Switch包裹的路由组件匹配成功后不继续向下匹配

  ```
  <Switch>
    <Route path="/about" component={About}/>
    <Route path="/home" component={Home}/>
  </Switch>
  ```

- Redirect 放在路由的最后，如果前面的路由都未成功匹配则匹配Redirect中的路由

  ```
   <Switch>
     <Route path="/about" component={About} />
     <Route path="/home" component={Home} />
     <Redirect to="/home" />
   </Switch>
  ```

- 向路由组件传递params参数

  ```
  // 跳转
  <Link to={`/home/detail/${id}/${title}`}></Link>
  //声明参数的接收
  <Route path="/home/detail/:id/:title" />
  //组件读取参数
  render() {
  	const {id,title} = this.props.match.params
  }
  ```

- 向路由组件传递search参数

  ```
  // 跳转
  <Link to={'/home/detail?id=xx&title=xx'}></Link>
  //路由注册
  <Route path="/home/detail" />
  //组件读取参数
  import qs from 'querystring'
  render() {
  	const {search} = this.props.location
  	const {id,title} = qs.parse(search.slice(1))
  }
  ```

- 向路由组件传递state参数

  ```
  //跳转
  <Link to={{pathname:'/home/detail',state:{id:xxx,title:xxx}}} />
  //路由注册
  <Route path="/home/detail" />
  //组件读取参数
  render() {
  	const {id,title} = this.props.location.state || {}
  }
  ```

- replace 通过在<Link> 上添加属性replace 用于替换当前路由被替换路由在路由栈中不存在历史

  ```
  <Link replace to={{pathname:'/home/detail',state:{id:xxx,title:xxx}}} />
  ```

- 编程式路由

  ```
  // 返回
  this.props.history.goBack()
  // 前进
  this.props.history.goForward()
  // 自由跳转
  this.props.history.go(num)
  // push模式跳转
  this.props.history.push(path,{...state})
  // replace模式跳转
  this.props.history.replace(path,{...state})
  ```

- withRouter 加工一般组件使其具备路由组件的所有API

  ```jsx
  import React, { Component } from 'react'
  import {withRouter} from 'react-router-dom'
  
  class Header extends Component {
  
  	back = ()=>{
  		this.props.history.goBack()
  	}
  
  	forward = ()=>{
  		this.props.history.goForward()
  	}
  
  	go = ()=>{
  		this.props.history.go(-2)
  	}
  
  	render() {
  		console.log('Header组件收到的props是',this.props);
  		return (
  			<div className="page-header">
  				<h2>React Router Demo</h2>
  				<button onClick={this.back}>回退</button>&nbsp;
  				<button onClick={this.forward}>前进</button>&nbsp;
  				<button onClick={this.go}>go</button>
  			</div>
  		)
  	}
  }
  
  export default withRouter(Header)
  
  //withRouter可以加工一般组件，让一般组件具备路由组件所特有的API
  //withRouter的返回值是一个新组件
  
  ```

  

