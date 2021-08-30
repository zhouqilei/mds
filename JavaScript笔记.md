## JS方法注释规范

```js
/**
* demo1
* @param {number} 参数1
* @return {void}
*/
function demo1() {
	console.log(1)
}
```

规范列表

- @api  提供给第三方使用的接口
- @author  标明作者
- @param 参数
- @return 返回值
- @todo 待办
- @version 版本号
- @inheritdoc 文档继承
- @property 类属性
- @property-read 只读属性
- @property-write 只写属性
- @const 常理
- @deprecated 过期方法
- @example 示例
- @final 标识类式终态，禁止派生
- @global 指明引用的全局变量
- @static 标识类、方法、属性是静态
- @ignore 忽略
- @internal 限内部使用
- @license 协议
- @link 链接，引用文档等
- @see 与link类似，可以访问内部方法或类
- @method 方法
- @package 命名空间
- @since 从指定版本开始的变动
- @throws 抛出异常
- @users 使用
- @var 变量
- @copyright 版权声明

## 字符串的常用方法总结

- charAt() 返回指定索引位置的字符
- charCodeAt() 返回指定索引位置的字符的Unicode值
- concat() 连接两个或多个字符串，返回连接后的字符串
- indexOf() 返回字符串中的指定字符最后一次出现的位置
- match() 找到一个或多个正则表达式的匹配
- replace() 替换与正则表达式匹配的子串
- search() 检索与正则表达式匹配的值
- slice() 提取字符串的片段，并在新的字符串中返回被提取的部分
- split() 将字符串分割为子字符串数组
- substr() 从起始索引提取字符串中指定数目的子字符串
- substring() 提取字符串中两个指定索引号之间的子串
- trim() 移除字符串首尾空白
- valueOf() 返回字符串对象的原始值

## 数组的遍历总结

- for语句 标准的for循环，可以使用 break，continue，如果在遍历中删除元素，被删除的元素不会被遍历到

  ```javascript
  for (let i=0; i < arr.length; i++) {
  	console.log(arr[i])
  }
  ```

- forEach 语句，对数组的每个元素执行一次CALLBACK函数，不能使用break，continue，如果在遍历中对数组使用push添加元素，添加的元素不会被遍历,如果在遍历中执行删除未遍历的元素，被删除的元素将不会被遍历

  ```javascript
  arr.forEach(item=>{
  	console.log(item)
  })
  ```

- for-in 语句 一般使用for-in 来遍历对象的属性，属性需要 emumerable才能被读取到,遍历中可以使用break，continue,如果在遍历中对数组使用push添加元素，添加的元素不会被遍历,如果在遍历中执行删除未遍历的元素，被删除的元素将不会被遍历

  ```javascript
  let arr = [1,2,3,4,5]
  for(let i in arr) {
  	console.log(arr[i])
  }
  ```

- for-of 语句可以遍历实现iterable的对象，可以使用 break 和 continue,如果在遍历中对数组使用push添加元素，添加的元素可以被遍历，如果在遍历中执行删除未遍历的元素，被删除的元素将不会被遍历

- map 方法，不会改变原数组，对原数组中的每个元素按顺序调用callback函数，函数执行完毕后返回的值组成一个新的数组,不可以使用break，continue

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  
  let newArr = arr.map(num => {
    return num + 1
  })
  
  console.log(newArr)
  ```

- reduce 方法，让数组中的前项和后项做某种计算，并累计最终值,不可使用break，continue

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  
  let total = arr.reduce((total, num, index, arr) => {
    return total + num
  })
  
  console.log(total)
  ```

- filter 方法，不改变原数组，为数组中的每个元素调用callback，并根据callback函数返回true或等价于true的值得元素创建一个新数组（即根据条件筛选）

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  
  let newArr = arr.filter(num => {
    if (num > 3) return true
  })
  
  console.log(newArr)
  ```

- every 方法，数组中的每个元素执行一次callback函数，如果有一次函数返回false，every方法返回false，否则返回true，（即判定数组中的所有元素是否满足条件）

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  
  let result = arr.every(num => {
    if (num > 5) return false
  })
  
  console.log(result)
  ```

- some 方法，为数组中的每一个元素执行一次callback函数，直到有一次callback函数返回true，否则返回false （即判定数组中是否存在复核条件的元素）

  ```javascript
  let arr = [1, 2, 3, 4, 5]
  
  let result = arr.some(num => {
    if (num == 5) return true
  })
  
  console.log(result)
  ```

  

## HTML DOM

**通过id查找元素**

```javascript
const x = document.getElementById("id")
```

**通过标签名查找HTML元素**

```javascript
const p = document.getElementByTagName("p")
```

**通过类名找HTML元素**

```javascript
const x = document.getElementByClassName('className')
```

**改变HTML内容**

```
document.getElementById(id).innerHTML = '新的HTML'
```

**改变HTML属性**

```javascript
document.getElementById(id).attributeName = '属性值'
```

**改变HTML样式**

```javascript
document.getElementById(id).style.property = '新样式'
```

**使用DOM分配事件**

```javascript
document.getElementById(id).onclick = function(){}
```

**DOM事件监听**

```javascript
document.getElementById(id).addEventListener("click",function(){})
```

**Window对象添加事件监听**

```javascript
window.addEventListener('resize',function(){})
```

**移除事件监听**

```javascript
element.removeEventListener('eventName',function(){})
```

**创建新的HTML元素并添加到DOM中**

```javascript
const para = document.createElement('p')
const node = document.createTextNode("这是一段文字")
//在结尾处插入
para.appendChild(node)
// 在开头处插入
para.insertBefore(node)
```

**移除已经存在的节点**

```javascript
const para = document.getElementById('para')
const child = document.getElementById('child')
para.removeChild(child)
```

**替换元素**

```javascript
paraent.replaceChild(newNode,oldNode)
```



## Window 对象

**Window尺寸**

- window.innerHeight 浏览器的窗口的内部高度(包含滚动条)
- window.innerWidth 浏览器的窗口的内部宽度(包含滚动条)

```javascript
//覆盖所有浏览器的方案
var w=window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;

var h=window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;
```

- window.open() 打开新的窗口
- window.close() 关闭当前窗口
- window.moveTo() 移动当前窗口
- Window.resizeTo() 调整当前窗口的尺寸

## Window Screen对象

**获取屏幕的可用宽高**

- screen.availableWidth 
- screen.availableHeight

## Windwo Location对象

- location.hostname 返回web主机域名
- location.pathname 返回当前页面的路径和文件名
- location.port 返回web主机的端口号
- location.protocol 返回web主机的协议 （http: 或 https)
- location.href 返回当前页面的整个URL

## Window History对象

- history.back() 后退
- history.forward() 前进
- history.go() +为前进 - 为后退 0为刷新

## Window Navigator 对象

- navigator.appCodeName 浏览器代号
- navigator.appName 浏览器名称
- navigator.appVersion 浏览器版本
- navigator.cookieEnable 是否启用cookies
- navigator.platform 硬件平台
- navigator.userAgent 用户代理
- navigator.language 用户代理语言

## Cookie

**设置cookie值的函数**

```javascript
function setCookie(name,value,expireDays) {
  let d = new Date()
  d.setTime(d.getTime()+(expireDays * 24 * 3600 * 1000))
  let expires = "expires="+d.goGMTString()
  document.cookie = name+"="+value+"; "+expires
}
```

**获取cookie值的函数**

```javascript
function getCookie(name) {
	let name = name + "="
  let ca = document.cookies.split(';')
  for (let i=0;i<ca.length;i++){
    let c = ca[i].trim();
    if(c.indexOf(name) == 0) {
      return c.substring(name.length,c.length)
    }
  }
  return ""
}
```

## JavaScript 存储对象

- localStorage 本地存储 用于长久保存整个网站数据，保存的数据没有过期时间，直到手动去除
- sessionStorage 用于临时保存同一窗口的数据，在关闭窗口之后数据会被删除

```
getItem(keyname) 获取指定键的值
setItem(keyname,value) 添加或更新指定键的值
remove(keyname) 删除键
clear() 清空所有键
```

