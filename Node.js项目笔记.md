

## 一般项目结构搭建

```
BLOG_SERVER
	--config 存放项目配置相关文件夹
	--controller 业务逻辑处理文件夹
	--models 数据模型
	--mongodb mongodb数据库连接
	--public 暴露给外界的文件
	--routes 路由配置
	--app.js 项目启动页面
```

## nodemon 的使用

**介绍**

当项目文件发生改变是，自动重新启动项目

**安装**

```shell
npm install nodemon -g
```

**使用**

```shell
nodemon app.js
```

## mongoose的使用

**介绍**

Mongoose为模型提供了一种直接的，基于scheme结构去定义你的数据模型。它内置数据验证， 查询构建，业务逻辑钩子等，开箱即用。

**网址**
http://www.mongoosejs.net/

**使用mongoose连接数据库**

```javascript
const mongoose = require('mongoose')
const config = require('../config/index')

mongoose.connect(config.DB_PATH, {
  autoReconnect: true
})

const db = mongoose.connection;

db.once('open', () => {
  console.log('连接数据库成功')
})

db.on('error', (err) => {
  console.error('数据库发生错误' + error)
})

db.on('close', () => {
  console.log('数据库关闭了')
})

module.exports = db
```

**模型文件创建实例**

```javascript
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const userSchema = new Schema({
  account: String,
  password: String,
  avatar: {
    type: String,
    default: ''
  }
}, {
  timestamps: {
    createdAt: 'createdTime',
    updatedAt: 'updatedTime'
  }
})

const User = mongoose.model('User', userSchema)

module.exports = User
```

**插入一条数据**

```javascript
 const newUser = await new User(req.body).save()
```

**查询一条数据**

```javascript
 const user = await User.findOne({account})
```

**根据id查询并更新数据**

```javascript
// 返回的是旧的数据，使用该函数需要对mongoose进行配置  useFindAndModify: false
let user = await User.findByIdAndUpdate(body._id, req.body)

```





## express路由的使用

在项目的routes文件夹中创建处理用户路由的user.js文件

```javascript
const express = require('express')
//userHandler 为controller层的具体的业务处理
const userHandler = require('../controller/user')
const router = express.Router();
//userHandler.login (req,res)=>{}
router.post('/user/login', userHandler.login)

module.exports = router;
```

在项目的routes文件夹中创建处理所有路由文件的index.js

```javascript
const userRoute = require('./user')
//暴露出去
exports.init = app => {
  app.use('/core', userRoute)
}

```

在启动文件app.js中使用路由

```javascript
// 引入express框架
const express = require('express')
// 引入配置文件
const config = require('./config/index')
// 引入路由
const router = require('./routes/index')

// 开启数据库连接
require('./mongodb/index')
// 创建express实例
const app = express()

// 暴露公共文件夹
app.use(express.static('public'))

// 解析rquest
app.use(express.urlencoded({
  extended: false
}))
app.use(express.json({}))


// 挂载路由
router.init(app)

// 监听端口
app.listen(config.port, () => {
  console.log('服务启动成功')
})
```

