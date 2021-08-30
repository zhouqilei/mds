## Sass

- 定义变量

  ```scss
  /*定义变量*/
  $mainColor: #ff0000;
  $mainTextSize: 18px;
  
  /*使用变量*/
  h1 {
    color: $mainColor;
    font-size: $mainTextSize;
  }
  ```

- 作用域

  ```scss
  h1 {
  	/*只能在当前作用域中使用外部无法获取*/
  	$mainColor: #ff0000; 
  	color: $mainColor;
  }
  ```

- 声明变量为全局变量

  ```scss
  h1 {
    /*
      被声明后，可以在外部被使用，（变量提升）
      所有的全局变量我们一般定义在同一个文件，如：_globals.scss，然后我们使用 @include 来包含该文件 		*/
  	$mainColor: #ff0000 !global; 
  	color: $mainColor;
  }
  ```

- 嵌套css

  ```scss
  /*
  如下代码的嵌套，
  表示div标签中的p标签蓝色，
  div标签中的a标签红色
  */
  div {
  	p {
  		color:blue;
  	}
  	
  	a {
  		color:red;
  	}
  }
  ```

- 嵌套属性

  ```scss
  /*
  如下代码为h1标签的 font-family font-size font-weight 设置值
  */
  h1 {
  	font:{
  		family:Helvetica, sans-serif;
  		size: 18px;
  		weight: bold;
  	}s
  }
  ```

- @import 引入.scss 文件

  ```scss
  /*全局引入global.scss 并将global.scss中的样式合并到当前scss文件中*/
  @import 'global'
  ```

- @mixin 混入指令允许我们定义一个可以在整个样式表中重复使用的样式,@include指令可以引入定义好的样式

  ```scss
  /*定义一个样式*/
  @mixin normal-text {
  	color:#333333;
  	font-size:18px;
  }
  
  /*使用定义好的样式*/
  h1 {
  	@include normal-text;
  }
  ```

  - @mixin 可以定义参数

    ```scss
    /*定义一个接收三个参数的样式,参数允许有默认值*/
    @mixin bordered($width,$style:solid,$color) {
    	border: $width $style $color;
    }
    /*使用定义好的样式*/
    h1 {
      @include(1px,solid,red);
    }
    ```

  - @mixin 定义可变参数

    ```scss
    /*定义参数可变的样式*/
    @mixin box-shadow($shadows...) {
    	box-shadow:$shadows;
    }
    /*使用*/
    div {
      @include(0px 4px 5px #666, 2px 6px 10px #999)
    }
    ```

- @extends 指令告诉sass一个选择器的样式从另一个选择器中继承

  ```scss
  .father {
  	cursor:point;
  	font-size:15px;
  	text-align:center;
  }
  
  .child {
  	@extends .father;
  	color:red;
  }
  ```

## Less

- 使用**@**符定义变量，使用**:**分配值

  ```less
  @mainColor: red;
  ```

- 嵌套规则

  ```less
  /*定义div标签中的h1标签为红色，a标签为蓝色*/
  div {
  	h1 {
  		color:red;
  	}
  	a {
  		color:blue;
  	}
  }
  ```

- 允许变量进行算术运算

  ```less
  @fontSize: 10px;
  h1 {
  	font-size: @fontSize * 2;
  }
  ```

- 转义**~**动态构建选择器，并使用属性或变量值作为任意字符串

  ```less
  /* ~"red"在less被解析为css是被转义为 red */
  h1 {
  	color: ~"red"
  }
  ```

- @import 用于在less文件中导入其他less文件

  ```less
  @import "path/to/less"
  ```

- 使用 **:extend**在一个选择器重扩展其他选择器样式

  ```less
  .red {
  	color: red;
  }
  h1 {
  	font-size:18px;
  	/*该标签文字为红色*/
  	&:extend(.red)
  }
  
  /*该标签文字为红色*/
  h2:extend(.red) {
    font-size:18px;
  }
  ```

- 混合

  ```less
  .red {
  	color:red;
  }
  h1 {
  	.red;
  	font-size:18px;
  }
  h2 {
  	.red()
  	font-size:18px;
  }
  ```

- 混合参数

  ```less
  .border(@width,@style,@color) {
  	border: @width @style @color;
  }
  
  h1 {
  	.border(1px,solid,red)
  }
  ```

- 带有返回值的混合

  ```less
  .padding(@x;@y) {
  	@padding ((@x + @y) / 2);
  }
  h1 {
  	.padding(80px,120px) // 调用混合
  	padding-left:@padding; //调用混合的返回值
  }
  ```

  