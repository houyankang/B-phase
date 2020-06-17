# CSS相关知识

### 一、CSS介绍

------

#### 1.1什么是CSS

> 指层叠样式表
>
> cascading(层叠) style(样式) sheets(表格)

#### 1.2作用

> 通过css可以定义html元素如何显示。
> html相当于毛坯房,很多效果达不到，css相当于是在毛坯基础上做精装修.

#### 1.3优点

> 通过css可以大大提高工作效率，可以让我们将html代码与样式代码分离

#### 1.4书写规范

> 格式：选择器 {属性:属性值;属性:属性值}
> 	选择器：确定当前css修饰的是哪一个元素

###  二、CSS和HTML三种结合方式

#### 2.1内联结合

> 实现：
>
> [在标签中使用style属性,格式如下：
> 			style="属性名1: 属性值1;属性名2: 属性值2"]()
>
> ```html
> <div style="font‐size: 20px;color: red;">这是一个div</div>
> ```
>
> 优缺点：
>
> ​	优点:简单方便，对少数的特定的元素进行单独设置！
> ​	缺点:复用性差
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>CSS和html结合之内联结合</title>
		
		<!--
			使用font标签来改变文本的字体大小和字体颜色
			font标签设置字体大小，最大只能设定为7.
			css内联代码:所有的符号必须是在英文半角模式下！！！
			在标签中使用style属性,格式如下：
			style="属性名1: 属性值1;属性名2: 属性值2"
			颜色取值：颜色英文单词/颜色16进制
			
		-->
	</head>
	<body>
		
		<div>
			<font style="font-size: 600px;color: #008000;">这是一个div</font>
			
		</div>
		
	</body>
</html>
```

#### 2.2内部结合

> 实现：
>
> [           1，需要在head标签中，使用style标签
> 				2，使用选择器选中元素(后面详细讲)
> 				3，编写css代码
> 				格式：
> 					选择器 {
> 						属性名1:属性值1;
> 						属性名2:属性值2;
> 					}]()
>
> ```html
> <head>
>   <title>内部结合</title>
>   <style type="text/css">
>     
>     div {
>       font‐size: 20px;
>       color: red;
>     }
>   </style>
> </head>
> <body>
>   <div>这是一个div</div>
>   <div>这是一个div</div>
> </body>
> ```
>
> 优缺点：
>
> ​	优点：可以对多个标签进行统一样式设置
> ​	缺点：只能作用于当前页面，复用性不高！css代码和html代码分离不彻底！

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>内部结合</title>
		<style>
			font{
				font-size: 200px;
				color: green;
			}
		</style>
	</head>
	<body>
		<div>
			<!--字体大小为:200px,字体颜色:绿色-->
			<font >这是一个font1</font><br />
			<!--字体大小为:200px,字体颜色:绿色-->
			<font >这是一个font2</font><br />
			<!--字体大小为:200px,字体颜色:红色-->
			<font style="color: red;">这是一个font3</font><br />
		</div>
	</body>
</html>

```

#### 2.3外部结合

> 实现：
>
> [			  1，新建一个css样式文件
> 				2，编写css代码
> 				3，在html文件中引入css外部文件 ,使用link标签引入]()
>
> 优点：复用性高，简单

```html
<!--css文件-->
font{
	font-size: 200px;
	color: greenyellow;
}
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>CSS和html结合之外部结合</title>
	
		<link rel="stylesheet" href="css/css01.css" />

	</head>
	<body>
		
		<div>
			<!--字体大小为:200px,字体颜色:绿色-->
			<font >这是一个font1</font><br />
			<!--字体大小为:200px,字体颜色:绿色-->
			<font >这是一个font2</font><br />
			<!--字体大小为:200px,字体颜色:红色-->
			<font >这是一个font3</font><br />
		</div>
		
	</body>
</html>

```

[注意：以上三种结合方式都有用，外部结合方式，使用html中的相对路径]()

### 三、CSS选择器

#### 3.1id选择器

> 概念：它使用#引入，引用的是元素的id属性值。
>
> 实现：
>
> [id选择器：引用的是id属性值
> 					#id属性值{
> 						属性名:属性值;
> 					}]()
>
> ```html
> <head>
>     <style type="text/css">
>       
>       #div1 {
>         font‐size: 20px;
>         color: red;
>       }
>       #div2 {
>         font‐size: 10px;
>         color: blue;
>       }
>     </style>
> </head>
> <body>
>     <div id="div1">这是一个div</div>
>     <div id="div2">这是一个div</div>
> </body>
> ```
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>id选择器</title>
		<style>
			#one{
				color:green;
			}
			#two{
				color:red;
			}
			#three{
				color:orange;
			}
		</style>
	</head>
	<body>
		<!--字体颜色：绿-->
		<font id="one">this is font one</font><br />
		<!--字体颜色：虹-->
		<font id="two">this is font two</font><br />
		<!--字体颜色：橙-->
		<font id="three">this is font three</font><br />
	</body>
</html>

```

#### 3.2类选择器

> 概念：使用”.”来描述，引用的的是元素上的class属性值。
>
> [类选择器:引用的是class属性值
> 			格式：
> 				.class属性值{
> 					属性名:属性值;
> 				}
> 			处理多个元素有相同样式效果的！！！]()
>
> 实现：
>
> ```html
> <head>
>   <title></title>
>   <style >
>     
>     .div1 {
>       font‐size: 20px;
>       color: red;
>     }
>   </style>
> </head>
> <body>
>   <div class="div1">这是一个div</div>
>   <div class="div1">这是一个div</div>
> </body>
> ```
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>类选择器</title>
		<style>
			.one{
				color: greenyellow;
			}
			.two{
				color: lightseagreen;
			}
			.three{
				color: darkgreen;
			}
		</style>
	</head>
	<body>
			<!--字体颜色：淡绿-->
		<font class="one">this is font one</font><br />
		<font class="one">this is font two</font><br />
		<!--字体颜色：中绿-->
		<font class="two">this is font three</font><br />
		<font class="two">this is font one</font><br />
		<!--字体颜色：深绿-->
		<font class="three">this is font three</font><br />
		<font class="three">this is font two</font><br />
	</body>
</html>
```

#### 3.3标签选择器

> 概念：对页面上的标签进行统一的设置，引用的就是标签的名称.
>
> [格式：
> 				标签名{
> 					属性名:属性值;
> 				}]()
>
> 实现：
>
> ```html
> <head>
>   <title></title>
>   <style >
>     
>     div {
>       font‐size: 20px;
>       color: red;
>     }
>   </style>
> </head>
> <body>
>   <div >这是一个div</div>
>   <div >这是一个div</div>
> </body>
> ```
>
> 

```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>标签选择器</title>
		<!--
        	
        	将font标签中的文本颜色修改为红色
			将span标签中的文本颜色修改为蓝色
			将div标签中的文本颜色修改为绿色
			所有的文本大小都为100px
        -->
        <style>
        	body{
        		font-size: 100px;
        	}
        	font{
        		color: red;
        	}
        	span{
        		color: blue;
        	}
        	div{
        		color: green;
        	}
        </style>

	</head>
	<body>
		<font>this is a font</font><br />
		<span>this is a span</span><br />
		<font>this is a font</font><br />
		<div>this is a div</div><br />
		<span>this is a span</span><br />
		<font>this is a font</font><br />
		<div>this is a div</div><br />
	</body>
</html>

```

#### 3.4分组选择器

> 概念：多个选择器使用同一段css,那么就可以使用分组。选择器之间使用逗号分开.
>
> [格式：
> 				id选择器,class选择,元素选择器{
> 					属性名:属性值;
> 				}]()
>
> 实现：
>
> ```html
> <head>
>   <title></title>
>   <style >
>     
>     #div1,.c1 {
>       font‐size: 20px;
>       color: red;
>     }
>   </style>
> </head>
> <body>
>   <div id="div1">这是一个div</div>
>   <span class="c1">这是一个span</span>
> </body>
> ```
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>分组选择器</title>
		<!--
        	font/span/div中的文本内容字体大小为200px,字体颜色为绿色
        -->
       <style>
       	#f1,.s1,div{
       		font-size: 200px;
       		color: green;
       	}
       </style>
	</head>
	<body>
		<font id="f1">this is a font</font><br />
		<span class="s1">this is a span</span><br />
		<div>this is a div</div><br />
	</body>
</html>

```

#### 3.5派生（衍生）选择器

> 概念：通过依据元素在其位置的上下文关系来定义，可以使标记更加简洁。也称为上下文选择器.
>
> [格式：
> 				父选择器 子选择器{
> 					属性名:属性值;
> 				}]()
>
> [注意：父选择器：可以是id选择器、class选择器、元素选择器
> 				子选择器：可以是id选择器、class选择器、元素选择器]()
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>派生选择器</title>
		<!--
        	需求：设置span中的font中内容样式。不准用id选择器、内联、class选择器
			先找到span,再找到font
        -->
        <style>
        	span font{
        		font-size: 50px;
        		color: red
        	}
        </style>
	</head>
	<body>
		<span>
			<font>这是一个font</font>
		</span>
		<div>
			<font>这是一个font</font>
		</div>
	</body>
</html>

```

#### 3.6总结：选择器的优先级

> [内联结合方式 > ID选择器 > 类选择器 > 元素选择器]()
>
> [ 规律：作用范围越小，优先级越大！！]()

### 四、CSS伪类

> 实现：
>
> [a:link {color: #FF0000} /* 未访问的链接 */
> a:visited {color: #00FF00} /* 已访问的链接 */
> a:hover {color: #FF00FF}  /* 鼠标移动到链接上 */
> a:active {color: #0000FF}  /* 选定的链接 */]()
>
> [注意：a:hover 必须被置于 a:link 和 a:visited 之后
> 				a:active 必须被置于 a:hover 之后]()

```html
<!DOCTYPE html>
<html>

	<head>
		<meta charset="UTF-8">
		<title>css伪类</title>

		<!--
			a:link {color: #FF0000}	/* 未访问的链接 */
			a:visited {color: #00FF00}	/* 已访问的链接 */
			a:hover {color: #FF00FF}	/* 鼠标移动到链接上 */
			a:active {color: #0000FF}	/* 选定的链接 */
			注意事项：
		-->
		<style>
			
			a:link {
				/* 未访问的链接 */
				color: cornflowerblue;
			}
			
			a:visited {
				/* 已访问的链接 */
				color: red;
			}

			a:hover {
				/* 鼠标移动到链接上 */
				color: orange;
			}
			a:active {
				/* 选定的链接 */
				color: green;
			}
			
			font:hover{
				color: green;
				font-size: 100px;
			}
			
			button{
				background-color: orange;
			}
			
			button:hover{
				background-color: orangered;
			}
			
			

		</style>
	</head>

	<body>

		<a href="index.html">this i a super link</a><br />
		<font>this is a font element</font><br />
		<button>按钮</button><br />
	</body>

</html>
```

### 五、CSS相关属性

#### 5.1字体属性

> 概念：CSS 字体属性允许设置字体系列 (font-family) 和字体加粗 (font-weight)，您还可以设置
> 字体的大小、字体风格（如斜体）和字体变形（如小型大写字母）。
>
> 常用属性：
>
> | [font](pr_font_font.asp.htm)                         | 简写属性。作用是把所有针对字体的属性设置在一个声明中。       |
> | ---------------------------------------------------- | ------------------------------------------------------------ |
> | [font-family](pr_font_font-family.asp.htm)           | 设置字体系列。                                               |
> | [font-size](pr_font_font-size.asp.htm)               | 设置字体的尺寸。                                             |
> | [font-size-adjust](pr_font_font-size-adjust.asp.htm) | 当首选字体不可用时，对替换字体进行智能缩放。（CSS2.1 已删除该属性。） |
> | [font-stretch](pr_font_font-stretch.asp.htm)         | 对字体进行水平拉伸。（CSS2.1 已删除该属性。）                |
> | [font-style](pr_font_font-style.asp.htm)             | 设置字体风格。                                               |
> | [font-variant](pr_font_font-variant.asp.htm)         | 以小型大写字体或者正常字体显示文本。                         |
> | [font-weight](pr_font_weight.asp.htm)                | 设置字体的粗细。                                             |
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>css中的字体属性</title>
		
		<!--
			
			font-family:
				微软雅黑、楷体、宋体、仿宋。如果浏览器不支持字体系列，就会使用默认的字体系列(微软雅黑!)，比如：草书
			font-size:
				字体大小
			font-style:
				字体倾斜度
			font-weight:
				字体的粗细
		-->
		<style>
			
			span{
				font-family: "草书";
				font-size: 100px;
				font-style: oblique;
				font-weight: bolder;
			}
	
		</style>
	</head>
	<body>
		
		<span>这是一个span标签</span>
		
	</body>
</html>

```

#### 5.2文本属性

> 概念：可以改变文本的颜色、字符间距，对齐文本，装饰文本，对文本进行缩进，等等。
>
> 常用属性：
>
> | [color](pr_text_color.asp.htm)                     | 设置文本颜色                                                |
> | -------------------------------------------------- | ----------------------------------------------------------- |
> | [direction](pr_text_direction.asp.htm)             | 设置文本方向。                                              |
> | [line-height](pr_dim_line-height.asp.htm)          | 设置行高。                                                  |
> | [letter-spacing](pr_text_letter-spacing.asp.htm)   | 设置字符间距。                                              |
> | [text-align](pr_text_text-align.asp.htm)           | 对齐元素中的文本。                                          |
> | [text-decoration](pr_text_text-decoration.asp.htm) | 向文本添加修饰。                                            |
> | [text-indent](pr_text_text-indent.asp.htm)         | 缩进元素中文本的首行。                                      |
> | text-shadow                                        | 设置文本阴影。CSS2 包含该属性，但是 CSS2.1 没有保留该属性。 |
> | [text-transform](pr_text_text-transform.asp.htm)   | 控制元素中的字母。                                          |
> | unicode-bidi                                       | 设置文本方向。                                              |
> | [white-space](pr_text_white-space.asp.htm)         | 设置元素中空白的处理方式。                                  |
> | [word-spacing](pr_text_word-spacing.asp.htm)       | 设置字间距。                                                |
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>css文本属性</title>
		<style>
			
			/*
			 	css文本属性
			 	direction:
			 		ltr: left to right
			 		rtl: right to left
			 	line-height:
			 		行高
			 	text-align:
			 		文本的对齐方式
			 	text-decoration
			 		文本装饰  underline none line-through
			 		
			 	letter-spacing
			 		字符间距,字符与字符之间的间距
			 	word-spacing:
			 		单词间距,单词与单词之间的间距
			 		
			  
			 */
			
			div{
				font-size: 50px;
				color: gray;
				direction: ltr;
				text-align: left;
				text-decoration: none;
			}
			
			a{
				font-size: 50px;
				text-decoration: none;
			}
			
		</style>
	</head>
	<body>
		
		<div>
			这是一个div
		</div>
		
		<a href="index.html">超链接</a>
		
	</body>
</html>


```



> 文本属性及字体属性综合练习
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
> 		<meta charset="UTF-8">
> 		<title>文本属性及文字属性综合练习</title>
> 		<!--
> 			标题：字号3em，颜色红色，居中，楷体。
> 			内容：字号1.2em，颜色黑色，居左，宋体，首行缩进2em，行高2em,字符间距0.1em。
> 		-->
> 		
> 		<style>
> 			body{
> 				background-image: url(img/girl02.jpg);
> 				background-size: cover;
> 			}
> 			#p1{
> 				font-size: 3em;
> 				color: red;
> 				text-align: center;
> 				font-family: "楷体";
> 			}
> 			
> 			.p2{
> 				font-size: 1.2em;
> 				color: black;
> 				text-align: left;
> 				font-family: "宋体";
> 				text-indent: 2em;
> 				height: 2em;
> 				letter-spacing: 0.1em;
> 			}
> 		</style>
> 	</head>
> 	<body>
> 		<p id="p1">再见青春再见我的爱</p>
> 		
> 		<p class="p2">
> 			想在毕业和你深深的道别，告诉你我爱你。
> 
> 		</p>
> 		<p class="p2">
> 			你爱网游，常常我到过的网站，你早就体会过了，我不知道，你是否也在这，不过这又有什么关系呢？
> 
> 		</p>
> 		
> 		<p class="p2">
> 			很久很久，不知道什么时候了，喜欢你似乎是一种习惯。
> 
> 		</p>
> 		
> 		<p class="p2">
> 			七年，有七年了。
> 		</p>
> 		
> 		
> 		<p class="p2">
> 			七年之痒，我等不下去了，我知道，我输了。
> 		</p>
> 		
> 		<p class="p2">
> 			你的签名最近有更新了，我都不知道你有多久，没有去空间了？看你的日志，现在的你正在为一个女孩感到犹豫不决？
> 
> 		</p>
> 		<p class="p2">
> 			谁呢？不敢说是我，即使偶尔你会在不经意中对我的态度，说的话，做的事让我瞎想，但那只是偶尔，你爱玩。
> 
> 		</p>
> 		<p class="p2">
> 			不敢在去受一次伤，我不敢。
> 		</p>
> 	
> 		<p class="p2">
> 			把你拉黑了，不再去关注你，再见我的青春！
> 		</p>
> 		
> 	</body>
> </html>
> ```
>
> 

#### 5.3WEB中的路径

> 绝对路径：
>
> - 带协议的绝对路径
> - 不带协议的绝对路径
>
> 相对路径：
>
> [./	当前目录，可省略](http://bm.scs.gov.cn/pp/gkweb/core/web/ui/business/auth/login.html)
>
> [../	上一级目录](http://bm.scs.gov.cn/pp/gkweb/core/web/ui/business/auth/login.html)

#### 5.4背景属性

> 概念：CSS 允许应用纯色作为背景，也允许使用背景图像创建相当复杂的效果。
>
> 相关属性：
>
> | [background](pr_background.asp.htm)                       | 简写属性，作用是将背景属性设置在一个声明中。 |
> | --------------------------------------------------------- | -------------------------------------------- |
> | [background-attachment](pr_background-attachment.asp.htm) | 背景图像是否固定或者随着页面的其余部分滚动。 |
> | [background-color](pr_background-color.asp.htm)           | 设置元素的背景颜色。                         |
> | [background-image](pr_background-image.asp.htm)           | 把图像设置为背景。                           |
> | [background-position](pr_background-position.asp.htm)     | 设置背景图像的起始位置。                     |
> | [background-repeat](pr_background-repeat.asp.htm)         | 设置背景图像是否及如何重复。                 |
>
> 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>背景属性</title>
		<!--
			background-color:将颜色作为背景
			background-image:将图片作为背景
		-->
		<style>
			body{
				background-image: url(img/girl01.jpg);
				background-size: cover;
			}
		</style>
	</head>
	<body>
		<p>Hello World！</p>
	</body>
</html>

```



#### 5.5尺寸属性

> 概念：CSS 尺寸 (Dimension)属性允许你控制元素的高度和宽度。同样，它允许你增加行间距。
>
> 常用属性：
>
> 1. height:设置元素的高度
> 2. line-height:设置行高
> 3. max-height:设置元素最大高度
> 4. min-height：设置元素最小高度
> 5. width:设置元素宽度
> 6. max-width:设置元素最大宽度
> 7. min-width：设置元素最小宽度
>
> [注意：css尺寸属性对行内元素无效!但可以使用display进行转换；图片属于特殊的行内元素]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>css尺寸属性</title>
		
		<!--
			css尺寸属性对行内元素无效!
			
		-->
		<style>
			
			#d1{
				min-width: 100px;
				max-width: 300px;
				
				min-height: 100px;
				max-height: 300px;
				
				width: 500px;
				height: 500px;
				background-color: green;
				
				display: inline-block;
				
			}
			
		</style>
	</head>
	<body>
		<font id="d1">这是一个font</font>
		<!--图片属于特殊的行内元素-->
		<!--<img src="img/girl01.jpg" id="d1"/>-->
		<!--行内元素-->
		<!--<span id="d1">这是一个span</span>-->
		<!--<div id="d1">这是一个div</div>-->
		
	</body>
</html>
```

#### 5.6列表属性

> 概念：CSS 列表属性允许你放置、改变列表项标志，或者将图像作为列表项标志。
>
> 主要方法：
>
> ​	list-style-image 将图象设置为列表项标志。 
> ​	list-style-position 设置列表中列表项标志的位置。 
> ​	list-style-type 设置列表项标志的样式
>
> [注意：作用于有序列表ol或者无序列表ul当中]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>css列表属性</title>
		<!--
			list-style-image 将图象设置为列表项标志。 
			list-style-position 设置列表中列表项标志的位置。 
			list-style-type 设置列表项标志的样式
		-->
		<style>
			
			ul{
				/*文本内容的对齐方式*/
				text-align: center;
				list-style-image: url(../img/a.gif);
				/*list-style-type: circle;*/
				list-style-position: inside;
			}
			
		</style>
	</head>
	<body>
		
		<ul>
			<li>你好</li>
			<li>世界</li>
			<li>world</li>
		</ul>
		
	</body>
</html>

```

#### 5.7边框属性

> 概念：CSS边框属性允许你规定元素边框的样式、宽度和颜色。
>
> 常用属性：
>
> | [border](pr_border.asp.htm)                           | 简写属性，用于把针对四个边的属性设置在一个声明。             |
> | ----------------------------------------------------- | ------------------------------------------------------------ |
> | [border-style](pr_border-style.asp.htm)               | 用于设置元素所有边框的样式，或者单独地为各边设置边框样式。   |
> | [border-width](pr_border-width.asp.htm)               | 简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。 |
> | [border-color](pr_border-color.asp.htm)               | 简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。 |
> | [border-bottom](pr_border-bottom.asp.htm)             | 简写属性，用于把下边框的所有属性设置到一个声明中。           |
> | [border-bottom-color](pr_border-bottom_color.asp.htm) | 设置元素的下边框的颜色。                                     |
> | [border-bottom-style](pr_border-bottom_style.asp.htm) | 设置元素的下边框的样式。                                     |
> | [border-bottom-width](pr_border-bottom_width.asp.htm) | 设置元素的下边框的宽度。                                     |
> | [border-left](pr_border-left.asp.htm)                 | 简写属性，用于把左边框的所有属性设置到一个声明中。           |
> | [border-left-color](pr_border-left_color.asp.htm)     | 设置元素的左边框的颜色。                                     |
> | [border-left-style](pr_border-left_style.asp.htm)     | 设置元素的左边框的样式。                                     |
> | [border-left-width](pr_border-left_width.asp.htm)     | 设置元素的左边框的宽度。                                     |
> | [border-right](pr_border-right.asp.htm)               | 简写属性，用于把右边框的所有属性设置到一个声明中。           |
> | [border-right-color](pr_border-right_color.asp.htm)   | 设置元素的右边框的颜色。                                     |
> | [border-right-style](pr_border-right_style.asp.htm)   | 设置元素的右边框的样式。                                     |
> | [border-right-width](pr_border-right_width.asp.htm)   | 设置元素的右边框的宽度。                                     |
> | [border-top](pr_border-top.asp.htm)                   | 简写属性，用于把上边框的所有属性设置到一个声明中。           |
> | [border-top-color](pr_border-top_color.asp.htm)       | 设置元素的上边框的颜色。                                     |
> | [border-top-style](pr_border-top_style.asp.htm)       | 设置元素的上边框的样式。                                     |
> | [border-top-width](pr_border-top_width.asp.htm)       | 设置元素的上边框的宽度。                                     |

[两种写法，一种是分开写，一种是放在一起写。]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>边框属性</title>
		<style>
			img{
				/*
				 * 左边框
				 * 样式：点状
				 * 颜色：淡绿
				 * 宽度：10px
				 * 第一种写法，分开写
				 */
				
				border-left-style:dotted ;
				border-left-color: greenyellow;
				border-left-width: 10px;
				/*
				 * 上边框
				 * 样式：虚线
				 * 颜色：中绿
				 * 宽度：15px
				 * 第一种写法，分开写
				 */
				border-top-style: dashed;
				border-top-color: dodgerblue;
				border-top-width: 15px;
				/*
				 * 右边框
				 * 样式：实线
				 * 颜色：绿
				 * 宽度：20px
				 * 第二种写法，写在一起
				 */
				border-right: dashed green 50px;
				/*
				 * 下边框
				 * 样式：实线
				 * 颜色：绿
				 * 宽度：20px
				 * 第二种写法
				 */
				border-bottom:double limegreen 20px;
			}
			
		</style>
	</head>
	<body>
		<img src="img/girl03.jpg" />
	</body>
</html>

```

##### 5.7.1圆角边框

> 属性：[border-radius:圆角边框半径]()
>
> [经验：若想将一个正方形图片整成圆角边框，将圆角边框设置成50%]()
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
> 		<meta charset="UTF-8">
> 		<title>圆角边框</title>
> 		<style>
> 			img{
> 				width: 700px;
> 				height: 700px;
> 				border-radius: 50%;
> 			}
> 		</style>
> 	</head>
> 	<body>
> 		<img src="img/girl04.jpg"/>
> 	</body>
> </html>
> 
> ```
>
> 

### 六、盒子模型

> 概念：CSS 框模型 (Box Model) 规定了元素框处理元素内容、内边距、边框 和 外边距 的方式。
>
> 相关属性：
>
> ​			element:元素内容
> ​			width:元素内容的宽度
> ​			height:元素内容的高度
> ​			border:元素的边框
> ​			padding:边框到内容的距离，同时设置左上右下内边距
>
> ​			padding-left/padding-top/padding-right/padding-bottom
>
> ​			margin:边框到其他元素的距离，同时设置左上右下外边距
>
> ​			margin-left/margin-top/margin-right/margin-bottom		
>
> [注意：1.内边距和外边距的值可以是负数
> 			   2.在页面上，设置margin-right无效，因为元素默认是左对齐，不管怎么设置元素都是左对
> 齐，所以将元素设置为右对齐就可以看到效果，设置方法：float:right]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>盒子模型</title>
		<!--
			内边距：边框到元素内容的距离
			padding:同时设置左上右下内边距
			padding-left/padding-top/padding-right/padding-bottom
			外边距：边框到其他元素的距离
			margin:同时设置左上右下外边距
			margin-left/margin-top/margin-right/margin-bottom
			
			
			浏览器：元素进行渲染的时候，是从左往右进行渲染，
			相当于现实生活中，排队买东西，margin-right告诉最后一个人，离下一个人要有200米远
		-->
		<style>
			body{
				float: right;
			}
			img{
				width: 200px;
				height: 100px;
				border: 5px solid blue;
			}
			#s1{
				padding: 10px;
				margin: 20px;
			}
			#s2{
				padding: 5px;
				margin: 10px;
			}
			#s3{
				padding: 20px;
				margin: 15px;
				
			}
		</style>
	</head>
	<body>
		<img  id="s1" src="img/girl01.jpg"/>
		<img id="s2" src="img/girl02.jpg"/>
		<img id="s3" src="img/girl03.jpg"/>
	</body>
</html>


```

### 七、CSS之定位

#### 7.1固定定位

> 概念：CSS 定位 (Positioning) 属性允许你对元素进行定位。
>
> 相关属性：
>
> [position:固定(fix)、相对（relative）、绝对（absolute）、静态(static)]()
>
> | [position](pr_class_position.asp.htm)           | 把元素放置到一个静态的、相对的、绝对的、或固定的位置中。     |
> | ----------------------------------------------- | ------------------------------------------------------------ |
> | [top](pr_pos_top.asp.htm)                       | 定义了一个定位元素的上外边距边界与其包含块上边界之间的偏移。 |
> | [right](pr_pos_right.asp.htm)                   | 定义了定位元素右外边距边界与其包含块右边界之间的偏移。       |
> | [bottom](pr_pos_bottom.asp.htm)                 | 定义了定位元素下外边距边界与其包含块下边界之间的偏移。       |
> | [left](pr_pos_left.asp.htm)                     | 定义了定位元素左外边距边界与其包含块左边界之间的偏移。       |
> | [overflow](pr_pos_overflow.asp.htm)             | 设置当元素的内容溢出其区域时发生的事情。                     |
> | [clip](pr_pos_clip.asp.htm)                     | 设置元素的形状。元素被剪入这个形状之中，然后显示出来。       |
> | [vertical-align](pr_pos_vertical-align.asp.htm) | 设置元素的垂直对齐方式。                                     |
> | [z-index](pr_pos_z-index.asp.htm)               | 设置元素的堆叠顺序。                                         |

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>固定定位之美女小广告</title>
		<style>
			img{
				width: 400px;
				height: 200px;
				position: fixed;
				right: 0px;
				bottom: 0px;
			}
			p{
				font-size: 100px;
				color: blue;
			}
		</style>
	</head>
	<body>
		<a href="https://www.baidu.com/"><img src="img/girl03.jpg"/></a>
		
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		
		<p>这是一个p</p>
		<p>这是一个p</p>
		<p>这是一个p</p>
		
		<p>这是一个p</p>
		<p>这是一个p</p>
	</body>
</html>

```

#### 7.2相对定位

> 概念：如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水
> 平位置，让这个元素“相对于”它的起点进行移动。
>
> [注意：在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。他是根据原有位置进行偏移]()
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
> 		<meta charset="UTF-8">
> 		<title>相对定位</title>
> 		<!--
> 			设置为相对定位的元素框会偏移某个距离。元素仍然保持其未定位前的形状，它原本所占的空间仍保留。
> 			相对于原来的位置进行偏移！！！
> 		-->
> 		<style>
> 			span{
> 				font-size: 20px;
> 			}
> 			#s1{
> 				background-color: orange;
> 			}
> 			#s2{
> 				background-color: blue;
> 				position: relative;
> 				top: 20px;
> 				left: 20px;
> 			}
> 			#s3{
> 				background-color: green;
> 			}
> 			
> 		</style>
> 	</head>
> 	<body>
> 		<span id="s1">
> 			这是span1
> 		</span>
> 		
> 		<span id="s2">
> 			这是span2
> 		</span>
> 		
> 		<span id="s3">
> 			这是span3
> 		</span>
> 	</body>
> </html>
> 
> ```
>
> 

#### 7.3绝对定位

> 概念：绝对定位的元素的位置相对于最近的已定位父元素。
>
> [注意：绝对定位并不会在原有位置占用空间，这点与相对定位不同。元素原先在正常文档流中所占的空间会关闭，元素的偏移是根据父容器进行偏移]()
>
> ```html
> <!DOCTYPE html>
> <html>
> 	<head>
> 		<meta charset="UTF-8">
> 		<title>绝对定位</title>
> 		<!--
> 			相对于其包含块定位，
> 			元素原先在正常文档流中所占的空间会关闭
> 		
> 		-->
> 		<style>
> 			span{
> 				font-size: 20px;
> 				
> 			}
> 			#s1{
> 				background-color: orange;
> 			}
> 			#s2{
> 				background-color: red;
> 				position: absolute;
> 				top: 20px;
> 				left: 20px;
> 			}
> 			#s3{
> 				background-color: blue;
> 			}
> 		</style>
> 	</head>
> 	<body>
> 		<span id="s1">
> 			这是一个span1
> 		</span>
> 		<span id="s2">
> 			这是一个span2
> 		</span>
> 		<span id="s3">
> 			这是一个span3
> 		</span>
> 	</body>
> </html>
> 
> ```
>
> 

### 八、块级元素和行内元素

> - 块级元素：
>   块级元素前后会带有换行符,占用一整行.
>   常见的块级元素:div
>
> - 行内元素
>   行内元素前后没有换行符,只包裹内容.
>   常见的行内元素:span
>   margin-top、margin-bottom、padding-top、padding-bottom设置无效
>
>   [注意：可以使用display：inline可以将块级元素转为行内元素，也可以使用display:block将行内元素转换为块级元素。display:inline-block是行内块级元素]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>块级元素和行内元素</title>
		<style>
			div{
				background-color: orange;
                <!--display: inline;-->
				
			}
			span{
				background-color: blue;
				
                 <!--display: block;-->
			}
		</style>
	</head>
	<body>
		<div>
			这是一个div
		</div>
		
		<span>
			这是一个span
	</body>
</html>
```

### 九、伸缩布局

> 名词解释
>
> flex container:伸缩布局
>
> 主轴(main axis)：flex容器的主轴主要用来分配flex子元素，默认是水平方向（row）
> 侧轴(cross axis)：与主轴垂直的轴称为侧轴，默认是垂直方向（column）
>
> flex item:伸缩元素
>
> [格式：#conter{
>   		//让id为conter的容器为伸缩布局
>   		display: flex;
>   		//改变主轴方向
>   		flex-direction: column;]()	
>
> 
>
> [注意：主轴和侧轴并不是固定不变的，可以通过flex-direction进行切换,默认为水平方向(row)。]()
>
> 伸缩布局的水平居中和垂直居中：
>
> align-items:center	垂直居中
>
> justify-content:center	水平居中
>
> [注意：这两个居中办法只能在伸缩布局中使用，使用时先把容器设置为伸缩布局！]()

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>伸缩布局入门案例一</title>
		<!--
        	需求：左边是菜单栏（40%），右边是内容栏（60%），高度填充整个屏
        -->
        <style>
        	html{
        		height: 100%;
        	}
        	body{
        		/*按照父容器的高度的100%进行设定*/
        		height: 100%;
        	}
        	
        	#conter{
        		width: 100%;
        		/*按照父容器的高度的100%进行设定*/
        		height: 100%;
        		/*让id为conter的容器为伸缩布局*/
        		display:  flex;
        	}
        	#left{
        		background-color: red;
        		width: 40%;
        		/*按照父容器的高度的100%进行设定*/
        		height: 100%;
        	}
        	#right{
        		background-color: blue;
        		width: 60%;
        		/*按照父容器的高度的100%进行设定*/
        		height: 100%;
        	}
        </style>
	</head>
	<body>
		<div id="conter">
			<div id="left">
				left
			</div>
			<div id="right">
				right
			</div>
		</div>
	</body>
</html>

```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>伸缩布局入门案例二</title>
		<!--
        	要求：上边是菜单栏（40%），下边是内容栏（60%），宽度填充整个屏幕。
        -->
        <style>
        	html{
        		height: 100%;
        	}
        	body{
        		height: 100%;
        	}
        	#conter{
        		/*让id为conter的容器为伸缩布局*/
        		display: flex;
        		/*改变主轴方向*/
        		flex-direction: column;
        		height: 100%;
        	}
        	#top{
        		background-color: red;
        		height: 40%;
        	}
        	#bottom{
        		background-color: blue;
        		height: 60%;
        	}
        </style>
	</head>
	<body>
		<div id="conter">
			<div id="top">
				这是菜单
			</div>
			<div id="bottom">
				这是内容栏
			</div>
		</div>
	</body>
</html>

```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>注册案例</title>
		<style>
			html{
				width: 100%;
				height: 100%;
			}
			body{
				background-image: url(img/girl02.jpg);
				background-size: cover;
				margin: 0px;
				display: flex;
				align-items: center;
				justify-content: center;
				width: 100%;
				height: 100%;
			}
			#left #f1{
				color: orange;
				font-size: 30px;
				font-weight: bolder;
			}
			#left{
				width: 20%;
			}
			#left #f2{
				color: gainsboro;
				font-size: 20px;
				font-family: "微软雅黑";
				font-weight: bolder;
				
			}
			
			#container{
				width: 1000px;
				height: 600px;
				background-color: white;
				display: flex;
				
			}
			#center{
				display: flex;
				align-items: center;
				justify-content: center;
				
				width: 60%;
				padding-left: 35px;
			}
			#center input{
				margin-top: 5px;
				width: 300px;
				height: 35px;
				border: 1px solid gray;
				border-radius: 5px;
			}
			#center #code{
				width: 170px;			}
			#center #codes{
				display: flex;
				
			}
			#center #img{
				padding-left: 5px;
				width: 120px;
				height: 50px;
			}
			#center button{
				width: 150px;
				height: 35px;
				margin-top: 20px;
				background-color: blue;
			}
			#center button:active{
				color: red;
			}
			#right{
				width: 20%;
				font-size: 15px;
			}
			#right a{
				text-decoration: none;
			}
			a:hover{
				color: green;
			}
			a:active{
				color: orange;
			}
			
		</style>
	</head>
	<body>
		<div id="container">
			<div id="left">
				<font id="f1">新用户注册</font><br />
				<font id="f2">USER REGISTER</font>
			</div>
			<div id="center">
				<form>
					<table>
						<tr>
							<td>
								账户
							</td>
							<td>
								<input type="text" name="connt" placeholder="请输入账号" />
							</td>
						</tr>
						<tr>
							<td>
								密码
							</td>
							<td>
								<input type="password" name="password" placeholder="请输入密码" />
							</td>
						</tr>
						<tr>
							<td>
								Email
							</td>
							<td>
								<input type="text" name="Email" placeholder="请输入邮箱" />
							</td>
						</tr>
						<tr>
							<td>
								姓名
							</td>
							<td>
								<input type="text" name="name" placeholder="请输入姓名" />
							</td>
						</tr>
						<tr>
							<td>
								手机号
							</td>
							<td>
								<input type="text" name="phone" placeholder="请输入手机号" />
							</td>
						</tr>
						<tr>
							<td>
								性别
							</td>
							<td>
								<input type="text" name="sex" placeholder="请输性别" />
							</td>
						</tr>
						<tr>
							<td>
								出生日期
							</td>
							<td>
								<input type="text" name="birth" placeholder="yyyy-MM-dd" />
							</td>
						</tr>
						<tr >
							<td >
								验证码
							</td>
							<td id="codes" >
								<input id="code" type="text" name="check" placeholder="请输入验证码" />
								<img src="img/a.gif" id="img" id="img"/>
							</td>
						</tr>
						<tr>
							<td colspan="2">
								<button type="submit">注册</button>
							</td>
						</tr>
					</table>
					
					
				</form>
			</div>
			<div id="right">
				<font>已有账户？</font>
				<a href="伸缩布局入门案例一.html">立即登录</a>
			</div>
		</div>
	</body>
</html>

```

