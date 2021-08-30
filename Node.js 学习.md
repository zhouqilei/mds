##  Node.js 介绍

运行在服务端的 JavaScript

基于 Chrome JavaScript 运行时建立的平台

事件驱动I/O服务端JavaScript环境，基于Google V8引擎

## Node.js 安装

使用命令查看是否已经安装 Node:

``` shell
node -v
```

Node安装网站：

https://nodejs.org/en/download/

## 事件循环及EventEmitter类

介绍：Node.js 几乎所有的事件机制都是使用设计模式中的观察者模式

使用Events模块，实例化EventEmitter 类来绑定和监听事件：

```javascript
// 引入event模块
var events = require('events')
// 创建 eventEmitter对象
var eventEmitter = new Event.EventEmitter();
// 绑定监听事件及事件的处理函数
eventEmitter.on('eventName', function () {
  console.log(111);
})

// 触发监听事件
eventEmitter.emit('eventName')
```

## Buffer

介绍：JavaScript语言自身只有字符串数据类型，没有二进制数据类型Buffer库是用于帮助Node.js存储元素数据的方法，可以让Node.js处理二进制数据。

**Buffer与字符编码**

```javascript
const buffer = Buffer.from('runoob', 'ascii');

// 转换成16进制
console.log(buffer.toString('hex'))
// 转换成base64
console.log(buffer.toString('base64'))

```

**创建Buffer类**

通过下列方式来创建Buffer类:

- **Buffer.alloc(size[, fill[, encoding]])：** 返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0
- **Buffer.allocUnsafe(size)：** 返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据
- **Buffer.allocUnsafeSlow(size)**
- **Buffer.from(array)：** 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖）
- **Buffer.from(arrayBuffer[, byteOffset[, length]])：** 返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。
- **Buffer.from(buffer)：** 复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例
- **Buffer.from(string[, encoding])：** 返回一个被 string 的值初始化的新的 Buffer 实例

```javascript
// 创建一个长度为 10、且用 0 填充的 Buffer。
const buf1 = Buffer.alloc(10);
// 创建一个长度为 10、且用 0x1 填充的 Buffer。 
const buf2 = Buffer.alloc(10, 1);
// 创建一个长度为 10、且未初始化的 Buffer。
// 这个方法比调用 Buffer.alloc() 更快，
// 但返回的 Buffer 实例可能包含旧数据，
// 因此需要使用 fill() 或 write() 重写。
const buf3 = Buffer.allocUnsafe(10);
// 创建一个包含 [0x1, 0x2, 0x3] 的 Buffer。
const buf4 = Buffer.from([1, 2, 3]);
// 创建一个包含 UTF-8 字节 [0x74, 0xc3, 0xa9, 0x73, 0x74] 的 Buffer。
const buf5 = Buffer.from('tést');
// 创建一个包含 Latin-1 字节 [0x74, 0xe9, 0x73, 0x74] 的 Buffer。
const buf6 = Buffer.from('tést', 'latin1');

```

**写入缓冲区**

```javascript
/*
	string - 写入缓冲区的字符串
	offset - 缓冲区开始写入的索引值，默认从0开始
	length - 写入的字节数，默认为 buffer.length
	encoding - 使用的编码 默认为 utf-8
	return - 返回实际写入得大小
*/
buf.write(string[, offset[, length]][, encoding])

```

```javascript
const buf = Buffer.alloc(256)
const len = buf.write('www.baidu.com')
console.info('写入的长度:' + len)
```

**从缓冲区读取数据**

```javascript
/**
	encoding - 使用的编码 默认utf-8
	start - 起始位置 默认为0
	end - 结束为止，默认为缓冲区的结尾
	
	return - 解码缓冲区数据并使用指定的编码返回字符串
*/
buf.toString([encoding[, start[, end]]])
```

```javascript
const buf = Buffer.alloc(26);
for (var i = 0 ; i < 26 ; i++) {
  buf[i] = i + 97;
}
console.log( buf.toString('ascii'));       // 输出: abcdefghijklmnopqrstuvwxyz
console.log( buf.toString('ascii',0,5));   //使用 'ascii' 编码, 并输出: abcde
console.log( buf.toString('utf8',0,5));    // 使用 'utf8' 编码, 并输出: abcde
console.log( buf.toString(undefined,0,5)); // 使用默认的 'utf8' 编码, 并输出: abcde
```

**将Buffer转换成Json对象**

```javascript
buf.toJson()
```

**缓冲区合并**

```javascript
/*
list - 用于合并的Buffer对象数组列表
totalLength - 指定合并后的Buffer对象总长度
return - 返回一个合并了多个成员的新Buffer对象
*/
Buffer.concat(list[,totalLength])
```

```javascript
var buf1 = Buffer.from('buf1')
var buf2 = Buffer.from('buf2')
var buf3 = Buffer.concat([buf1,buf2])
console.log(buf3.toString())
```

**缓冲区比较**

```javascript
/*
otherBuffer - 与buf对象进行比较的另外一个Buffer对象
return - 表示buf在otherBuffer 之前，之后，相同
*/
buf.compare(otherBuffer)
```

```javascript
var buffer1 = Buffer.from('ABC');
var buffer2 = Buffer.from('ABCD');
var result = buffer1.compare(buffer2);

if(result < 0) {
   console.log(buffer1 + " 在 " + buffer2 + "之前");
}else if(result == 0){
   console.log(buffer1 + " 与 " + buffer2 + "相同");
}else {
   console.log(buffer1 + " 在 " + buffer2 + "之后");
}
```

**拷贝缓冲区**

```javascript
/*
targetBuffer - 要拷贝的对象
targetStart - 数字，可选，默认0
sourceStart - 数字，可选，默认0
sourceEnd - 数字，可选，默认buffer.length
*/
buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])
```

```javascript
var buf1 = Buffer.from('abcdefghijkl');
var buf2 = Buffer.from('RUNOOB');

//将 buf2 插入到 buf1 指定位置上
buf2.copy(buf1, 2);

console.log(buf1.toString());
```

**缓冲区裁剪**

```javascript
/*
start - 起始位置，可选，默认0
end - 结束为止，可选，默认buffer.length
return - 返回一个新的缓冲区，它和旧的缓冲区指向同一块内存
*/
buf.slice([start[,end]])
```

```javascript
var buf1 = Buffer.from('Hello World')

var buf2 = buf1.slice(0, 5)
console.log(buf2.toString())
```

**缓冲区的长度**

```javascript
/*
return - 返回对象所占的内存长度
*/
buf.length
```

## Stream

介绍：Stream是Node.js中的一个抽象接口，有四种流类型，Readable(可读操作)，Writable(可写操作)，Duplex(可读可写操作)，Transform(操作被写入数据，然后读出结果)

**从流中读取数据**

```javascript
var fs = require('fs')
var data = ''

// 创建可读流
var readerStream = fs.createReadStream('input.txt')

// 设置编码 utf8
readerStream.setEncoding('utf-8')

// 处理流事件 data, end, error,
readerStream.on('data', function (chunk) {
  data += chunk
})

readerStream.on('end', function () {
  console.log(data)
})

readerStream.on('error', function (err) {
  console.log(err.stack)
})
```

**写入流**

```javascript
var fs = require('fs')
var data = '你好，我叫小明'

// 创建一个可以写入的流，写入到文件out.txt 文件中
var writeStream = fs.createWriteStream('out.txt')
// 使用编码
writeStream.write(data, 'utf-8')
// 标记文件末尾
writeStream.end()
// 处理流事件
writeStream.on('finish', function () {
  console.log('写入完成')
})

writeStream.on('error', function (err) {
  console.log(err.stack)
})
```

**管道流**
管道流提供了一个输出流到输入流的机制，通常用于从一个流中获取数据并将数据传递到另外一个流中

```javascript
var fs = require('fs')

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt')
// 创建一个可写流
var writerStream = fs.createWriteStream('out.txt')

// 管道读写操作
// 将可读流中的内容复制到可写流中
readerStream.pipe(writerStream)

```

**链式流**
链式是通过连接输出流到另外一个流并创建多个流操作的机制

如使用管道和链式流实现压缩和解压文件

```javascript
var fs = require('fs')
var zlib = require('zlib')

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
```

## 模块系统

Node.js 提供 exports 和 require 两个对象作为模块的公开接口和引入接口

创建并公开 hello.js 文件

```javascript
exports.world = function() {
  console.log('hello world')
}
```

如果想要将一个对象封装到模块中:

```javascript
function Hello() {
	var name;
	this.setName = function(theName) {
    name = theName;
  }
  this.sayHello = function(){
    console.log('hello '+ name)
  }
}

module.exports = Hello
```

## 路由

我们要为路由提供请求的URL和其它需要的GET或POST参数，随后路由需要根据这些数据来执行相应的代码

创建 server.js

```javascript
var http = require('http')
var url = require('url')

function start(route) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    route(pathname)
    response.writeHead(200, {
      "Content-type": "text/plain"
    })
    response.write("Hello World")
    response.end()
  }

  http.createServer(onRequest).listen(8888)
  console.log('server is running!')
}

exports.start = start
```

创建 router.js

```javascript
function route(pathname) {
  console.log("About to route a request for " + pathname);
}

exports.route = route
```

创建 index.js

```javascript
var server = require('./server')
var router = require('./router')
server.start(router.route)
```

命令行输入：node index.js 启动服务

## 全局对象

JavaScript 中的特殊对象，称为全局对象，它及其所有属性可以在程序的任何地方访问，即全局变量。

**__filename**
表示当前执行脚本的文件名，输出文件所在位置的绝对路径

**__dirname**
表示当前执行脚本的所在目录

**setTimeout(cb,ms)**

表示在指定的毫秒后执行cb，只执行一次

**clearTimeout(t)**

停止一个 setTimeout，其中t是setTimeout(cb,ms)返回的

**setInterval(cb,ms)**

表示没隔一定毫秒执行一次cb

**console**

打印操作

**process**

表示描述当前Node.js进程状态的对象,提供了一个与操作系统相关的简单接口

exit

当进程准备推出是触发

beforeExit

当 node 清空事件循环，并且没有其他安排时触发这个事件。通常来说，当没有进程安排时 node 退出，但是 'beforeExit' 的监听器可以异步调用，这样 node 就会继续执行。

uncaughtException

当一个异常冒泡回到事件循环，触发这个事件。如果给异常添加了监视器，默认的操作（打印堆栈跟踪信息并退出）就不会发生。

Signal 事件

当进程接收到信号时就触发。信号列表详见标准的 POSIX 信号名，如 SIGINT、SIGUSR1 等。

示例：

```javascript
process.on('exit', function (code) {
  console.log('退出码为：' + code)
})
```

## 文件系统

**引入**:

```javascript
var fs = require('fs')
```

**异步和同步**

Node.js文件系统模块中的方法均有异步和同步版本

```javascript
var fs = require('fs')

// 异步读取
fs.readFile('input.txt', function (err, data) {
  if (err) {
    return console.error(err)
  }
  console.log('异步读取：' + data.toString())
})

// 同步读取
const data = fs.readFileSync('input.txt')
console.log('同步读取：' + data.toString())
```

**打开文件**

```javascript
var fs = require('fs')

// 异步读取
fs.readFile('input.txt', function (err, data) {
  if (err) {
    return console.error(err)
  }
  console.log('异步读取：' + data.toString())
})

// 同步读取
const data = fs.readFileSync('input.txt')
console.log('同步读取：' + data.toString())
```

**获取文件信息**

```javascript
/*
path - 文件路径
callback - 回调函数 (err,stats)=>{} stats 是 fs.Stats对象
*/
fs.stat(path,callback)
```

```javascript
var fs = require('fs')
fs.stat('/tmp/file.js',function(err,data){
	cosnole.log(stats.isFile())
})
```

**写入文件**

```javascript
/*
file - 文件名
data - 写入文件的数据，字符串或者Buffer对象
options - {encoding,mode,flag} 默认为 utf8, 0666, w
callback - 回调函数 
*/
fs.writeFile(file,data[, options],callback)
```

```javascript
var fs = require("fs");

console.log("准备写入文件");
fs.writeFile('input.txt', '我是通 过fs.writeFile 写入文件的内容',  function(err) {
   if (err) {
       return console.error(err);
   }
   console.log("数据写入成功！");
   console.log("--------我是分割线-------------")
   console.log("读取写入的数据！");
   fs.readFile('input.txt', function (err, data) {
      if (err) {
         return console.error(err);
      }
      console.log("异步读取文件数据: " + data.toString());
   });
});
```

**读取文件**

```javascript
/*
fd - 通过fs.open() 方法返回的文件描述符
buffer - 数据写入的缓冲区
offset - 缓冲区写入的写入偏移量
length - 要从文件中读取的字节数
position - 文件的读取的起始位置
callback - 回调函数 (err,bytesRead,buffer) bytesRead 表示读取的字节数，buffer 为缓冲区对象。''
*/
fs.read(fd,buffer,offset,length,position,callback)
```

```javascript
var fs = require('fs')

const buf = new Buffer.alloc(1024)

fs.open('input.txt', 'r+', function (err, fd) {
  if (err) {
    return console.error(err)
  }
  fs.read(fd, buf, 0, buf.length, 0, function (err, bytes) {
    console.log(bytes + '字节被读取')
    if (bytes > 0) {
      console.log(buf.slice(0, bytes).toString())
    }
  })
})
```

**关闭文件**

```
fs.close(fd,callback)
```

**截取文件**

```javascript
/*
fd - 通过fs.open() 方法返回的文件描述符
len - 文件内容截取的长度

*/
fs.ftruncate(fd,len,callback)
```

**删除文件**

```javascript
/*
path - 文件路径
callback - 回调函数，没有参数
*/
fs.unlink(path,callback)
```

**创建目录**

```javascript
/*
path - 文件路径
options - 包含recursive: 是否以递归的方式创建目录，默认false
						  mode: 目录权限 默认777
callback - 回调函数，没有参数
*/
fs.mkdir(path[,options],callback)
```

**读取目录**

```javascript
/*
path - 文件路径
callback - (err,files) files为目录下的文件数组列表
*/
fs.readdir(path,callback)
```

**删除目录**

```javascript
/*
path - 文件路径
callback - 没有参数
*/
fs.rmdir(path,callback)
```

## GET/POST 请求

```javascript
var http = require('http')
var url = require('url')
var util = require('util')

http.createServer(function (request, response) {
  response.writeHead(200, {
    'Content-Type': 'text/plain; charset=utf-8'
  });
  // 解析 url 参数
  var params = url.parse(request.url, true).query;
  response.write("网站名：" + params.name);
  response.write("\n");
  response.write("网站 URL：" + params.url);
  response.end();
}).listen('3000')
```

**获取POST请求内容**

```javascript
var http = require('http')
var querystring = require('querystring')
var util = require('util')

http.createServer(function (req, res) {
  // 定义了一个post变量，用于暂存请求体的信息
  var post = '';

  // 通过req的data事件监听函数，每当接受到请求体的数据，就累加到post变量中
  req.on('data', function (chunk) {
    post += chunk;
  });

  // 在end事件触发后，通过querystring.parse将post解析为真正的POST请求格式，然后向客户端返回。
  req.on('end', function () {
    post = querystring.parse(post);
    res.end(util.inspect(post));
  });
}).listen('3000')
```

## Express 框架

一个简单灵活的Node.js Web应用框架，可以设置中间件来响应HTTP请求，定义了路由表用于执行不同的HTTP请求动作，可以通过向模板传递参数来动态渲染HTML页面

**安装**

express 安装

```shell
npm install express --save
```

body-parser 安装 - node.js中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。

cookie-parser 安装 - 一个解析Cookie的工具，通过req.cookies可以取到传过来的cookie，并把它们转成对象。

multer 安装 - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

```
npm install body-parser --save
npm install cookie-parser --save
npm install install multer --save
```

**创建express框架实例**

```javascript
const express = require('express')
const app = express()

app.get('/', function (req, res) {
  res.send('Hello World')
})

const server = app.listen(3000, function () {
  const host = server.address().host
  const port = server.address().port

  console.log("应用实例，访问地址为 http://%s:%s", host, port)
})
```

**路由**

```javascript
const express = require('express')
const app = express()

// 响应主页get
app.get('/', function (req, res) {
  res.send('Hello GET')
})

// 响应主页post
app.post('/', function (req, res) {
  res.send('Hello POST')
})

// 对页面 abcd, abxcd, ab123cd, 等响应 GET 请求
app.get('/ab*cd', function (req, res) {
  res.send('正则匹配')
})


const server = app.listen(3000, function () {
  console.log("服务启动了")
})
```

**静态资源**

```javascript
// 使用express.static中间件来设置静态资源的路径
app.use('/public', express.static('public'))
```

**POST请求**

创建表单提交html

```html
<html>
<body>
<form action="http://127.0.0.1:3000/process_post" method="POST">
First Name: <input type="text" name="first_name">  <br>
 
Last Name: <input type="text" name="last_name">
<input type="submit" value="Submit">
</form>
</body>
</html>
```

请求接收处理

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
 
// 创建 application/x-www-form-urlencoded 编码解析
var urlencodedParser = bodyParser.urlencoded({ extended: false })
 
app.use('/public', express.static('public'));
 
app.get('/index.html', function (req, res) {
   res.sendFile( __dirname + "/" + "index.html" );
})
 
app.post('/process_post', urlencodedParser, function (req, res) {
 
   // 输出 JSON 格式
   var response = {
       "first_name":req.body.first_name,
       "last_name":req.body.last_name
   };
   console.log(response);
   res.end(JSON.stringify(response));
})
 
var server = app.listen(3000, function () {
})
```

**文件上传**
创建文件上传html

```html
<html>
<head>
<title>文件上传表单</title>
</head>
<body>
<h3>文件上传：</h3>
选择一个文件上传: <br />
<form action="/file_upload" method="post" enctype="multipart/form-data">
<input type="file" name="image" size="50" />
<br />
<input type="submit" value="上传文件" />
</form>
</body>
</html>
```

处理文件上传

```javascript
var express = require('express');
var app = express();
var fs = require("fs");
 
var bodyParser = require('body-parser');
var multer  = require('multer');
 
app.use('/public', express.static('public'));
app.use(bodyParser.urlencoded({ extended: false }));
app.use(multer({ dest: '/tmp/'}).array('image'));
 
app.get('/index.html', function (req, res) {
   res.sendFile( __dirname + "/" + "index.html" );
})
 
app.post('/file_upload', function (req, res) {
 
   console.log(req.files[0]);  // 上传的文件信息
 
   var des_file = __dirname + "/" + req.files[0].originalname;
   fs.readFile( req.files[0].path, function (err, data) {
        fs.writeFile(des_file, data, function (err) {
         if( err ){
              console.log( err );
         }else{
               response = {
                   message:'File uploaded successfully', 
                   filename:req.files[0].originalname
              };
          }
          console.log( response );
          res.end( JSON.stringify( response ) );
       });
   });
})
 
var server = app.listen(3000, function () {
 
})
```

**Cookie管理**

```javascript
// express_cookie.js 文件
var express      = require('express')
var cookieParser = require('cookie-parser')
var util = require('util');
 
var app = express()
app.use(cookieParser())
 
app.get('/', function(req, res) {
    console.log("Cookies: " + util.inspect(req.cookies));
})
 
app.listen(3000)
```

## RESTful API

**介绍**

表述性状态转移是一组架构约束条件和原则。满足这些约束条件和原则的应用程序或设计就是RESTful，主要用于使用接口操作数据表的增删改查。

GET - 用于获取数据

PUT - 更新或添加数据

DELETE - 删除数据

POST - 添加数据

## 多进程

**介绍**

我们都知道 Node.js 是以单线程的模式运行的，但它使用的是事件驱动来处理并发，这样有助于我们在多核 cpu 的系统上创建多个子进程，从而提高性能。

每个子进程总是带有三个流对象：child.stdin, child.stdout 和child.stderr。他们可能会共享父进程的 stdio 流，或者也可以是独立的被导流的流对象。

Node 提供了 child_process 模块来创建子进程，方法有：

- **exec** - child_process.exec 使用子进程执行命令，缓存子进程的输出，并将子进程的输出以回调函数参数的形式返回。
- **spawn** - child_process.spawn 使用指定的命令行参数创建新进程。
- **fork** - child_process.fork 是 spawn()的特殊形式，用于在子进程中运行的模块，如 fork('./son.js') 相当于 spawn('node', ['./son.js']) 。与spawn方法不同的是，fork会在父进程与子进程之间，建立一个通信管道，用于进程之间的通信。

**exec()方法**

```javascript
/*
command - 字符串， 将要运行的命令，参数使用空格隔开
options - 对象 ：
								cwd ，字符串，子进程的当前工作目录
								env，对象 环境变量键值对
								encoding ，字符串，字符编码（默认： 'utf8'）
								shell ，字符串，将要执行命令的 Shell（默认: 在 UNIX 中为/bin/sh， 在 Windows 中为cmd.exe，Shell应										当能识别 -c开关在 UNIX 中，或 /s /c 在 Windows 中。 在Windows 中，命令行解析应当能兼容cmd.exe）
								timeout，数字，超时时间（默认： 0）
								maxBuffer，数字， 在 stdout 或 stderr 中允许存在的最大缓冲（二进制），如果超出那么子进程将会被杀死 （默									认: 200*1024）
								killSignal ，字符串，结束信号（默认：'SIGTERM'）
								uid，数字，设置用户进程的 ID
								gid，数字，设置进程组的 ID
callback - (err,stdout,stderr)=>{}
return 方法返回最大的缓冲区，并等待进程结束，一次性返回缓冲区的内容。
*/
child_process.exec(command[, options], callback)
```

创建两个 js 文件 support.js 和 master.js

support.js:

```javascript
console.log("进程 " + process.argv[2] + " 执行。" );
```

 master.js:

```javascript
const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
    var workerProcess = child_process.exec('node support.js '+i, function (error, stdout, stderr) {
        if (error) {
            console.log(error.stack);
            console.log('Error code: '+error.code);
            console.log('Signal received: '+error.signal);
        }
        console.log('stdout: ' + stdout);
        console.log('stderr: ' + stderr);
    });
 
    workerProcess.on('exit', function (code) {
        console.log('子进程已退出，退出码 '+code);
    });
}
```

执行:

```shell
node master.js
```

**spawn()方法**

```javascript
/*
command - 要运行的命令
args - 字符串参数数组
options - 
					cwd String 子进程的当前工作目录
					env Object 环境变量键值对
					stdio Array|String 子进程的 stdio 配置
					detached Boolean 这个子进程将会变成进程组的领导
					uid Number 设置用户进程的 ID
					gid Number 设置进程组的 ID
return - 方法返回流 (stdout & stderr)，在进程返回大量数据时使用。进程一旦开始执行时 spawn() 就开始接收响应。
*/
child_process.spawn(command[, args][, options])
```

修改master.js

```javascript
const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
   var workerProcess = child_process.spawn('node', ['support.js', i]);
 
   workerProcess.stdout.on('data', function (data) {
      console.log('stdout: ' + data);
   });
 
   workerProcess.stderr.on('data', function (data) {
      console.log('stderr: ' + data);
   });
 
   workerProcess.on('close', function (code) {
      console.log('子进程已退出，退出码 '+code);
   });
}
```

**fork()方法**

```javascript
/*
modulePath - String，将要在子进程中运行的模块
args - Array 字符串参数数组
options - 
					cwd String 子进程的当前工作目录
					env Object 环境变量键值对
					execPath String 创建子进程的可执行文件
					execArgv Array 子进程的可执行文件的字符串参数数组（默认： process.execArgv）
					silent Boolean 如果为true，子进程的stdin，stdout和stderr将会被关联至父进程，否则，它们将会从父进程中继承。（默认为：false）
					uid Number 设置用户进程的 ID
					gid Number 设置进程组的 ID
return - 返回的对象除了拥有ChildProcess实例的所有方法，还有一个内建的通信信道。
*/
child_process.fork(modulePath[, args][, options])
```

修改master.js

```
const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
   var worker_process = child_process.fork("support.js", [i]);    
 
   worker_process.on('close', function (code) {
      console.log('子进程已退出，退出码 ' + code);
   });
}
```

## MongoDB

**介绍**

MongoDB 是一个基于分布式文件存储的数据库。由 C++ 语言编写。旨在为 WEB 应用提供可扩展的高性能数据存储解决方案。

MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。

**安装**

https://www.runoob.com/mongodb/mongodb-osx-install.html

**Node.js 安装MongoDB驱动**

```shell
npm install mongodb --save
```

**创建并连接数据库**

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/test'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');
  db.close();
})
```

**创建集合**

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  dbase.createCollection('site', function (err, res) {
    if (err) throw err
    console.log('集合site创建成功')
    db.close
  })
})
```

**插入数据**
插入一条数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  const item = {
    name: '百度',
    url: 'www.baidu.com'
  }
  dbase.collection('site').insertOne(item, function (err, res) {
    if (err) throw err
    console.log('文档插入成功')
    db.close()
  })
})
```

插入多条数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  const items = [{
    name: '淘宝',
    url: 'www.taobao.com'
  }, {
    name: '知乎',
    url: 'www.zhihu.com'
  }]
  dbase.collection('site').insertMany(items, function (err, res) {
    if (err) throw err
    console.log('文档插入成功,数量为：' + res.insertedCount)
    db.close()
  })
})
```

**查询数据	**

find()

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  dbase.collection('site').find({}).toArray(function (err, res) {
    if (err) throw err
    console.log(res)
    db.close()
  })
})
```

查询指定条件的数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  dbase.collection('site').find({
    name: '百度'
  }).toArray(function (err, res) {
    if (err) throw err
    console.log(res)
    db.close()
  })
})
```

**更新数据	**
更新一条数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')
  var whereStr = {
    name: '百度'
  }
  var updateStr = {
    $set: {
      url: 'https://www.baidu.com'
    }
  }
  dbase.collection('site').updateOne(whereStr, updateStr, function (err, res) {
    if (err) throw err;
    console.log('更新成功')
    db.close()
  })
})
```

更新多条数据使用updateMany

**删除数据**

删除一条数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')
  var whereStr = {
    name: '百度'
  }
  dbase.collection('site').deleteOne(whereStr, function (err, obj) {
    if (err) throw err
    console.log('删除成功')
  })
})
```

删除多条数据使用deleteMany

**排序**

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  // 根据name升序 -1 为降序 1 为升序
  dbase.collection('site').find().sort({
    name: 1
  }).toArray(function (err, res) {
    if (err) throw err
    console.log(res)
    db.close()
  })
})
```

**查询分页**
limit() 限制每页数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  // 限制每页1条数据
  dbase.collection('site').find().limit(1).toArray(function (err, res) {
    if (err) throw err
    console.log(res)
    db.close()
  })
})
```

skip() 跳过数据

```javascript
// 创建并连接数据库
const MongoClient = require('mongodb').MongoClient
// 数据库地址 如果数据库test不存在，创建该数据库
const url = 'mongodb://localhost:27017/'
// 连接
MongoClient.connect(url, function (err, db) {
  if (err) throw err;
  console.log('数据库连接/创建成功');

  const dbase = db.db('test')

  // 跳过前面1条数据 限制每页1条数据,
  dbase.collection('site').find().skip(1).limit(1).toArray(function (err, res) {
    if (err) throw err
    console.log(res)
    db.close()
  })
})
```

