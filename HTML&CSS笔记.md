```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>
 
<h1>我的第一个标题</h1>
 
<p>我的第一个段落。</p>
 
</body>
</html>
```



![img](https://www.runoob.com/wp-content/uploads/2013/06/02A7DD95-22B4-4FB9-B994-DDB5393F7F03.jpg)

## HTML头部 <meta> 标签的使用实例

- 为搜索引擎定义搜索关键字

  ```html
  <meta name="keywords" content="HTML CSS JavaScript"></meta>
  ```

- 为网页定义描述内容

  ```html
  <meta name="description" content="这是一个网页"></meta>
  ```

- 定义网页的作者

  

  ```html
  <meta name="author" content="30"></meta>
  ```
  
- 设置viewport

  ```html
  <meta name="viewport"content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
  ```

## 块级元素和行内元素

  块级元素会在显示的时候以新的一行来开始，行内元素通常不会以新行开始

- 常见的块级元素

  div、p、h1~h6、ul、ol、dl、li、dd、table、hr、blockquote、address、table、menu、pre、header、section、aside、footer

- 常见的行内元素

  span、img、a、input、textarea、select、strong、lable、button、abbr、em、cite、i、q、small、big、sub、sup、u

- 将块级元素变成行内元素

  ```css
  display:inline-block
  ```

- 将行内元素变成块级元素

  ```css
  display:block
  ```


## CSS选择器

- Id选择器

  ```css
  #id{
  	color:red;
  }
  ```

- class选择器

  ```css
  .class {
  	color:blue;
  }
  ```

- 标签选择器

  ```css
  tagName {
  	color:green;
  }
  ```

- 后代选择器 使用空格  分隔

- 子元素选择器 使用 > 号分隔

- 相邻兄弟选择器 使用 + 号分隔

- 后续兄弟选择器 使用 ~ 号分隔

## background的简写顺序

- background-color 背景色
- background-image 背景图片
- background-repeat 图片重复
- background-attachment 背景图片随滚动轴的移动方式
- background-position 图片位置

## Text 设置

- text-decoration 文字的横线装饰
- text-transform 文字的大小写转换
- text-indent 文字缩进
- letter-spacing 文字的间距
- line-height 文字的行距
- word-spacing 单词的间距
- white-space 元素中空白的处理方式

## em的使用

为了避免Internet Explorer 中无法调整文本的问题，许多开发者使用 em 单位代替像素。

em的尺寸单位由W3C建议。

1em和当前字体大小相等。在浏览器中默认的文字大小是16px。

因此，1em的默认大小是16px。可以通过下面这个公式将像素转换为em：**px/16=em**

不幸的是，仍然是IE浏览器的问题。调整文本的大小时，会比正常的尺寸更大或更小,解决方法如下

```
body {font-size:100%;}
h1 {font-size:2.5em;}
h2 {font-size:1.875em;}
p {font-size:0.875em;}
```

## a链接的样式

- a:link - 正常未访问过的链接
- a:visited - 用户已经访问过的链接
- a:hover - 鼠标放在链接上面时 必须放在前两个之后
- a:active - 链接被点击时 必须放在 a:hover 之后

## 列表

- list-style-type 设置列表项标记的类型
- list-style-image 设置列表项标记的图片

## CSS盒子

- 元素的总宽度 总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距
- 元素的总高度 总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距

- 使用 box-sizing 来修改这一原则
  - cntent-box 宽度和高度分别应用到元素的内容框。在宽度和高度之外绘制元素的内边距和边框。
  - border-box 为元素设定的宽度和高度决定了元素的边框盒。为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制
  - inherit 规定应从父元素继承 box-sizing 属性的值。



## CSS伪类

- :first-child 获取父元素的第一个子元素

  ```css
  /*
  匹配作为任何元素的第一个子元素的 p元素
  */
  p:first-child {
  	color:red;
  }
  ```

- 匹配所有<p> 元素中的第一个子元素 <i> 元素

  ```css
  p > i:first-child {
  	color: red;
  }
  ```

- 匹配所有作为第一个子元素的 <p> 元素中的所有 <i> 元素

  ```css
  p:first-child i {
  	color: red;
  }
  ```

## CSS伪元素

- :first-line 向文本的首行添加样式，只可以用于块级元素
- :first-letter 向文本的首字母添加样式，只可以用于块级元素
- :brefore 向元素的内容前面插入新内容
- :after 向元素的内容后面插入新内容

## CSS属性选择器

- [title]   包含属性title的元素

  ```css
  [title] {
  	color: red;
  }
  ```

- [title=red] 属性title的值为red的元素

  ```css
  [title=red] {
  	color:red;
  }
  ```

- [title~=red] 属性title的值包含red的元素

  ```css
  [title~=red] {
  	color:red;
  }
  ```

  

## CSS2D转换

- matrix(n,n,n,n,n,n) 使用6个值的矩阵
- translate(x, y) 沿着x轴和y轴移动元素
- translateX(n) 沿着x轴移动
- translateY(n) 沿着y轴移动
- scale(x,y) 沿着x轴和y轴缩放
- scaleX(n) 缩放宽度
- scaleY(n) 缩放高度
- rotate(angle) 选择一定角度
- skew(x-angle,y-angle) 沿着x轴和y轴倾斜
- skewX(angle) 沿着x轴倾斜
- skewY(angle) 沿着y轴倾斜

## CSS3D转换

- matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n) 使用16个值的 4*4 矩阵
- translate3d(x,y,z) 定义3D转化
- translateX(n) 3D转化 x轴
- translateY(n) 3D转化 y轴
- translateZ(n) 3D转化 z轴
- scale3d(x,y,z) 3D缩放
- scaleX(n) 3D x缩放
- scaleY(n) 3D y缩放

- scaleZ(n) 3D z缩放
- rotate3d(x,y,z,angle) 定义 3d旋转
- rotateX(n) x轴旋转
- rotateY(n) y轴旋转
- rotateZ(n) z轴旋转
- perspective(*n*) 3D转换视图的透视视图

## CSS过渡

- transition 简写属性 用于在一个属性中设置四个过渡属性
- transition-property 过渡属性的名称
- transition-duration 过渡的时间花费
- transition-timing-function 过渡的时间曲线
- transiton-delay 过渡的延时

## CSS动画

- 使用@keyframes 定义动画

  ```css
  @keyframes myAnimation {
  	from {background:red;}
  	to {background:yellow}
  }
  /*使用*/
  div {
  	animation:myAnimation 5s;
  }
  ```

  