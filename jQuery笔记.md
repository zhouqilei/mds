## jQuery 安装 

- 使用CND

  ```html
  <head>
  <script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js">
  </script>
  </head>
  ```

- 下载后本地引入

  ```html
  /* 下载链接 https://jquery.com/download/ */
  <head>
  <script src="jquery-1.10.2.min.js"></script>
  </head>
  ```

- 文档就绪事件

  ```javascript
  // 复杂写法
  $(document).ready(function() {
  	// 开始写jQuery	
  })
  // 简洁写法
  $(function(){
    // 开始写jQuery
  })
  ```

## jQuery选择器

- 元素选择器

  ```javascript
  // 选择页面中所有p元素
  $("p")
  
  ```

- id选择器

  ```javascript
  //选择指定id的元素
  $("#test")
  ```

- class 选择器

  ```javascript
  // 选择指定类名的元素
  $(".className")
  ```

## JQuery事件

```javascript
//点击事件
$("p").click(function(){})
//双击事件
$("p").dbclick(function(){})
// 鼠标进入
$("p").mouseenter(function(){})
// 鼠标离开
$("p").mouseleave(function(){})
// 鼠标移动到元素上方并按下鼠标按键
$("p").mousedown(function(){})
// 在元素上方松开鼠标按钮
$("p").mouseup(function(){})
// 模拟光标悬停事件
$("p").hover(function(){
  // 鼠标进入元素
},function(){
  //鼠标离开元素
})
//元素获得焦点
$("input").focus(function(){
  
})
// 元素失去焦点
$("input").blur(function(){
  
})

```

## 元素的隐藏于显示

```javascript
//显示
$("p").show()
// 隐藏
$("p").hide()
// 自动 speed 可取 slow fast 毫秒
$("p").toggle(speed,function(){
  
})
```

## 元素的淡入淡出

```javascript
// 淡入 speed 可取 slow fast 毫秒
$("p").fadeIn(speed,function(){})
// 淡出  speed 可取 slow fast 毫秒
$("p").fadeOut(speed,function(){})
// 自动 speed 可取 slow fast 毫秒
$("p").fadeToggle(speed,function(){})
// 渐变元素的透明度到一定值 speed 可取 slow fast 毫秒 opacity 0~1
$("p").fadeTo(speed,opacity,function(){})
```

## 元素的滑动

```javascript
// 元素向下滑动
$("p").slideDown(speed,function(){})
// 元素向上滑动
$("p").slideUp(speed,function(){})
// 自动
$("p").slideToggle(speed,function(){})
```

## jQuery动画

- 语法

  ```
  $(selector).animate({params},speed,callback)
  ```

- 操作多个属性

  ```javascript
  $('#div').animate({
  	left:'100px',
    opacity: '0.8',
    width:'100px',
    height:'100px'
  })
  ```

- 使用相对值

  ```javascript
  $("#div").animate({
  	width:'-=40px',
  	height:'+=40px'
  })
  ```

- 队列功能

  ```javascript
   var div=$("div");
   div.animate({height:'300px',opacity:'0.4'},"slow");
   div.animate({width:'300px',opacity:'0.8'},"slow");
   div.animate({height:'100px',opacity:'0.4'},"slow");
   div.animate({width:'100px',opacity:'0.8'},"slow");
  ```

- 停止动画

  ```
  // stopAll 表示是否停止动画队列，默认false
  // goToEnd 表示是否立即停止当前动画
  $(selector).stop(stopAll,goToEnd)
  
  ```

  

## JQuery捕获

- 获取/设置元素内容

  ```
  // 设置或获取元素的文本内容
  $(selector).text() 
  // 设置或获取所选元素的内容
  $(selector).html()
  // 设置或获取表单字段的值
  $(selector).val()
  ```

- 获取/设置属性

  ```
  //获取元素的属性
  $(selector).attr('href')
  // 设置元素的属性
  $(selector).attr('href','value')
  // 同时设置多个属性
  $(selector).attr({
  	'href':'value1',
  	'title':'value2'
  })
  ```

## jQuery 添加元素

```
// 在被选元素之后加入内容，仍在元素内部
$(selector).append(content)
// 在被选元素之前加入内容，仍在元素内部
$(selector).prepend(content)
// 在被选元素之前加入内容，元素之外
$(selector).before(content)
// 在被选元素之后加入内容，元素之外
$(selector).after(content)
```

## jQuery 删除元素

```
//删除被选元素及子元素
$(selector).remove()
//删除被选元素的子元素
$(selector).empty()
// 过滤被删除的元素 例如删除所有类名为test的p元素
$("p").remove(".test")
```

## jQuery CSS类及方法

```
// 被选元素添加类名
$(selector).addClass(className)
// 被选元素删除类名
$(selector).removeClass(className)
// 被选元素删除或添加类名
$(selector).toggleClass(className)
// 返回第一个所选元素的css样式值
$(selector).css(propertyName)
//设置所选元素的css样式
$(selector).css(propertyName,propertyValue)
// 设置所选元素的多个css样式
$(selector).css({
	propertyName1:propertyValue1,
	...
})
```

## jQuery 尺寸

![jQuery Dimensions](https://www.runoob.com/images/img_jquerydim.gif)

```
// 设置或返回元素的宽度（不包括内边距、边框或外边距）
$(selector).width()
// 设置或返回元素的高度（不包括内边距、边框或外边距）
$(selector).height()
// 返回元素的宽度（包括内边距）
$(selector).innerWidth
// 返回元素的高度（包括内边距）
$(selector).innerHeight
// 返回元素的宽度（包括内边距和边框）
$(selector).outerWidth
// 返回元素的高度（包括内边距和边框）
$(selector).outerHeight

```

## JQuery 遍历

- 祖先

  ```
  // 获取所选元素的直接父元素
  $(selector).parent()
  // 获取所选元素的所有祖先元素，直到根节点（<html>
  $(selector).parents('过滤条件')
  // 获取所选元素到给定元素直接的所有祖先元素
  $(selector).parentsUntil('条件元素')
  ```

- 后代

  ```
  // 获取所选元素的直接子元素
  $(selector).children('过滤')
  // 获取所选元素的所有后代元素
  $(selector).find('过滤')
  ```

- 同胞

  ```
  // 获取所选元素的所有同胞元素
  $(selector).siblings()
  // 获取所选元素的下一个同胞元素
  $(selector).next()
  // 获取所选元素的所有跟随同胞元素
  $(selector).nextAll()
  // 获取所选元素的直到给定元素之间的同胞元素
  $(selector).nextUntil('给定元素')
  // 对应next
  $(selector) prev(), prevAll() & prevUntil() 方法
  ```

- 过滤

  ```
  // 符合条件的元素的第一个元素
  $(selector).first()
  // 符合条件的元素的最后一个元素
  $(selector).last()
  // 符合元素的相应下标的元素
  $(selector).eq(index)
  // 过滤条件
  $(selector).filter('过滤')
  $(selector).not('过滤'）
  ```

## Ajax

- get

  ```
  $.get(url,function(data,status) {
  	
  })
  ```

- post

  ```
  $.post(url,body,function(data,status) {
  
  })
  ```

  