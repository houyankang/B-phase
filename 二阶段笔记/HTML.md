# HTML



### 一、HTML简介

------

#### 1.1 HTML概述

> HTML全称：Hyper Text Markup Language(超文本标记语言)
>
> ​	HTML是一门用户创建网页文档的标记语言，网页本身是一种文本文件，在文本文件中添加标记符。
>
> ​	浏览器来解析HTML标记的内容（文字的处理，画面排版安排，图片如何显示、音频、视频等等）
>
> ​	HTML是用来创建网页的标记语言



#### 1.2 HTML特点

> 1、简易性：超文本标记语言的版本升级采用的超集方式。更加方便灵活
>
> 2、可扩展性：超文本标记语言采取的子类元素的方式，为系统扩展带来保证
>
> 3、平台无关性：
>
> 4、通用性：HTML是网络的通用语言，一种简单、通用的标记语言。



#### 1.3 HTML的发展

> 超文本标记语言(第一版)------1993年6月作为互联网工程小组(IETF)工作草案发布(并非标准)
>
> HTML2.0 --1995年11月
>
> HTML3.2 --1997年1月14日，W3C标准
>
> HTML4.0 --1997年12月18日  W3C标准
>
> HTML4.01 --1999年12月24日 W3C的推荐标准
>
> HTML5 ---2014年10月29日，W3C推荐标准



#### 1.4 HTML基本结构

```html
<!-- 文档声明：告诉浏览器使用HTML5版本解析 -->
<!DOCTYPE html>
<html>
    <!--网页的头部 -->
    <head>
        <!--页面的字符集编码 -->
        <meta charset="utf-8" />
        <!-- 页面的标题 -->
        <title>我的页面</title>
    </head>
    <!-- 网页的主题，显示的部分-->
    <body>
        展示的内容
    </body>
</html>
```

> 1、HTML页面包含头部head和主体body
>
> 2、HTML标签通常是成对出现的，有开始标签，有结束标签，称为对标签。没有结束标签的为 空标签
>
> 3、HTML标签都长都有属性，格式：属性名 = "属性值" 属性名 = "属性值"。多个属性用空格间隔
>
> 4、HTML标签不区分大小写，建议小写
>
> 5、HTML文件后缀名为html或htm



### 二、HTML基本标签

------

#### 2.1 结构标签

```html
<html></html>:根标签
<head> ：头标签
    <title></title>页面的标题
</head>
<body>：主体标签：显示网页内容
    
</body>
```

> 属性：
>
> color:文本的颜色  
>
> bgColor:背景色
>
> background：背景图片
>
> 颜色的表示方式：
>
> 第一种：颜色名称  red  blue green yellow orange
>
> 第二种方式：RGB模式    #000000    #ffffff  #325687



#### 2.2 排版标签

> 1、注释标签：<!-- 注释 -->
>
> 2、换行标签：<br/>
>
> 3、段落标签：<p>文本文字</p>
>
> ​		特点：段落与段落之间有行高（行间距）自带换行
>
> ​		属性：文本对齐方式 align （left、center 、right）
>
> 4、水平线标签：<hr/>
>
> ​		属性：
>
> ​				width：水平线的长度(两种：像素表示。第二种：百分比显示)
>
> ​				size：水平线的粗细（避免过粗、太丑、一般给个位数  比如 6px）
>
> ​				color：水平线的颜色
>
> ​				align：水平线的对齐方式(left、center、right)



#### 2.3 标题标签

```
<h1>-<h6>
数字越小，标题文字越大！默认加粗、默认字号、默认占据一行
```



#### 2.4 容器标签

```
<div></div> ： 块级标签，独占一行，自带换行
<span></span> ： 行级标签，所有内容都在同一行
	作用：<div>主要是结合css做页面分块 布局
		<span>：进行友好提示信息的显示
```



#### 2.5 列表标签

##### 2.5.1 无序列表

> ul(unorder list)

```html
<!--ul是无序列表，默认标识为实心圆 disc
			circle 空心圆
			square 黑色方块
		-->
		<ul type="square">
			<li>兰博基尼</li>
			<li>法拉利</li>
			<li>宾利</li>
			<li>迈凯伦</li>
		</ul>
```



##### 2.5.2 有序列表

> ol(order list)

```html
<!--ol是有序列表，默认标识为阿拉伯数字 1
			a  A 字母字典顺序
			i  I 罗马数字
		-->
		<ol type="I">
			<li>铁胆火车侠</li>
			<li>光明勇士</li>
			<li>米老鼠和唐老鸭</li>
			<li>小头儿子和隔壁老王</li>
		</ol>
```



##### 2.5.3 定义列表

> dl(defination list)定义列表
>
> dt(defination title)定义标题
>
> dd(defination description) 定义描述



```html
<dl>
			<dt>秦牛正威</dt>
			<dd>就当是一场梦，醒来还是很感动</dd>
			<dt>???</dt>
			<dd>蛋黄的长裙，蓬松的头发。</dd>
		</dl>
```



##### 2.5.4 列表嵌套

```html
<ul>
			<li>最新娱乐新闻</li>
			<li>
				<dl>
					<dt>青春有你2</dt>
					<dd>非常庞大的导师阵容，Ella，Jony J，蔡徐坤，Lisa</dd>
				</dl>
			</li>
			<li>
				猎心者
				<ol>
					<li>戴猛。。。</li>
					<li>廖朵朵。。。</li>
					<li>花笙。。。</li>
				</ol>
			</li>
		</ul>		
```



#### 2.6 图片标签

```
<img /> 独立标签
属性：
	src 图片地址
	width 图片的宽度
	height 图片的高度
	border 边框
	alt 图片的文字说明 当图片未能正确加载时，才显示
	title 鼠标悬停时，显示的文字
```

```html
<img src="img/微信图片_20200306173413.jpg"
			width="500px"
			height="900px"
			 />
		<img src="img/timg.jpg"
			width="500px"
			height="500px"
			border="5"
			alt="给你点赞的小脑斧"
			title="给你点赞的大脑斧"
			 />
```



#### 2.7 链接标签

> 超链接可以是文本，也可以是图片，可以点击链接标签，进入新的文档，或者是当前文档中的某个部分

```html
<a>文本或图片</a>、
属性：
			href="跳转的地址"跳转外网需要添加协议
			target:_self(当前文档)
					_blank(新页面,会一直打开新的)
					_search 之前打开的页面存在，则不打开新的页面，直接复用
			name 充当锚点（顶部、底部）
			需要为标签提供name属性，进行赋值
			需要点击跳转的标签href属性给 #name
```



#### 2.8 表格标签

> 表格由<table>标签来定义，每个表格均有若干行(由tr标签定义行)，每行由若干个单元格组成(由td标签来定义)。每一个数据单元可以包含文本、图片、列表。。。。。。



##### 2.8.1 普通表格

> table   tr   td

```html
<!--创建表格 table   行  tr   列  td
			table属性：
			默认没有边框体现
			border:边框的宽度
			bordercolor:边框的颜色
			cellspacing:单元格的间距
			cellpadding:单元格与内容的间距
			width:宽度
			height:高度
			align:控制表格的对齐方式 left center right
			td的属性：
			align:控制的单元格内容的对齐方式 left center right
			valign:控制单元格内容的垂直对齐方式 top middle bottom
		-->
		<table border="1" bordercolor="red" cellspacing="10" cellpadding="10"
			width="300px" height="300px" align="center">
			<tr>
				<td align="center">学号</td>
				<td align="center">姓名</td>
				<td align="center">性别</td>
			</tr>
			<tr>
				<td valign="bottom">S1001</td>
				<td valign="middle">张阔</td>
				<td valign="top">男</td>
			</tr>
		</table>
```



##### 2.8.2 表格的表头

> th

```html
<!-- th作为表头，默认居中，加粗 -->
<table border="1">
			<tr>
				<th>学号</th>
				<th>姓名</th>
				<th>分数</th>
			</tr>
			<tr>
				<td>S1002</td>
				<td>刘欣</td>
				<td>100</td>
			</tr>
		</table>
```



##### 2.8.3 表格的列合并

> colspan

```html
<table border="1" bordercolor="red">
			<tr>
				<td align="center" colspan="4">学生信息表</td>
			</tr>
			<tr>
				<td>学号</td>
				<td>姓名</td>
				<td colspan="2">各科成绩</td>
			</tr>
			<tr>
				<td>1</td>
				<td>哆啦A梦</td>
				<td>80</td>
				<td>90</td>
			</tr>
		</table>
```



##### 2.8.4 表格的行合并

> rowspan

```html
<table border="1" bordercolor="blue">
			<tr>
				<td colspan="4" align="center">学生表</td>
			</tr>
			<tr>
				<td>学号</td>
				<td>姓名</td>
				<td>语文成绩</td>
				<td>数学成绩</td>
			</tr>
			<tr>
				<td rowspan="2">1</td>
				<td rowspan="2">光头强</td>
				<td>80</td>
				<td>90</td>
			</tr>
			<tr>
				<td>100</td>
				<td>99</td>
			</tr>
		</table>
```



#### 2.9 文本格式化标签

```html
		<!--粗体文本-->
		<b>今天天气好</b><br />
		<!--大号字-->
		<big>今天天气好</big><br />
		<!--着重文字-->
		<em>今天天气好</em><br />
		<!--斜体字 物理上把字体倾斜-->
		<i>今天天气好</i><br />
		<!--小号字-->
		<small>今天天气好</small><br />
		<!--定义加重语气-->
		<strong>今天天气好</strong><br />
		<!--下标字-->
		CO<sub>2</sub><br />
		<!--上标字-->
		孙悟空三打张阔<sup>①</sup><br />
		<!--插入字-->
		<ins>今天天气好</ins><br />
		<!--删除字-->
		<del>今天天气好</del>
```



### 三、基本标签的综合案例

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>综合案例</title>
	</head>
	<body>
		<!--头部-->
		<div>
			<table width="100%" align="center">
				<tr>
					<td align="left">
						千锋教育-稀有的坚持全程面授品质的大型IT教育机构
					</td>
					<td align="right">
						<a>好程序员特训营&nbsp;&nbsp;</a>
						<a>JavaEE分布式开发&nbsp;&nbsp;</a>
						<a>JavaSE核心基础&nbsp;&nbsp;</a>
						<a>加入我们</a>
					</td>
				</tr>
				<tr>
					<td>
						<img src="img/new_logo.png" />
					</td>
					<td align="right">
						<img src="img/nav_r_ico.png" />
					</td>
				</tr>
				<tr>
					<td colspan="2" align="center">
						<hr/>
						<span>首页&nbsp;&nbsp;</span>
						<span>课程培训&nbsp;&nbsp;</span>
						<span>教学保障&nbsp;&nbsp;</span>
						<span>免费视频&nbsp;&nbsp;</span>
						<span>公开课&nbsp;&nbsp;</span>
						<span>企业合作&nbsp;&nbsp;</span>
						<span>就业喜报&nbsp;&nbsp;</span>
						<span>学员天地&nbsp;&nbsp;</span>
						<span>关于千锋&nbsp;&nbsp;</span>
						<span>加入我们</span>
						<hr />
					</td>
				</tr>
				<tr>
					<td colspan="2" align="right">
						首页>课程培训>JavaEE列表
					</td>
				</tr>
			</table>
		</div>
		<!--中间部分-->
		<div>
			<table>
				<tr>
					<td>
						<h3>课程培训</h3>
						<h4>共108种课程内容</h4>
					</td>
				</tr>
				<tr>
					<td>
						<hr />
						<img src="img/001.png" />
					</td>
				</tr>
			</table>
			<table align="center" width="100%">
				<tr align="center">
					<td>
						<img src="img/002.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/003.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/004.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/005.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/006.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
				</tr>
				<tr align="center">
					<td>
						<img src="img/007.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/008.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/009.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/010.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
					<td>
						<img src="img/011.png" /><br />
						<div align="center">书名：XXX</div>
						<div align="center">售价：180</div>
					</td>
				</tr>
			</table>
		</div>
		<!--底部-->
		<div>
			<table width="90%" align="center">
				<tr>
					<td><img src="img/012.png" /></td>
				</tr>
			</table>	
		</div>
	</body>
</html>

```

#### 

### 四、表单标签

> 文本框：<input type="text">
>
> 密码框：<input type="password">
>
> 单选框：<input type="radio">
>
> 下拉框：<select><option>
>
> 多选框：<input type="checkbox">
>
> 上传文件框：<input type="file">
>
> 文本域：<textarea>
>
> 提交按钮：<input type="sunmit">
>
> 重置按钮：<input type="reset">
>
> [**注意：**外部必须嵌套一个form标签,只有嵌套这个标签，浏览器上的内容才能够提交到服务器上！！]()

![1586254858222](C:\Users\侯彦康\AppData\Roaming\Typora\typora-user-images\1586254858222.png)



```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>表单标签练习</title>
		<!--
			账户:<input> type="text" value:默认值 placeholder:提示
			密码:<input> type="password" value:默认值  placeholder:提示
			性别:<input> type="radio" checked:默认选中  value:默认值
			地址：<select>/<option>  selected:默认选中
			爱好：<input> checkbox
			介绍: <textarea></textarea>
			提交/重置 :<input> type="submit" , <input> type="reset"
			
		-->
	</head>
	<body>
		<form>
			用户名：
			<input type="text" name="username" placeholder="请输入账户"/><br />
			密码：
			<input type="password" name="password" placeholder="请输入密码"/><br />
			性别：
			<input type="radio" name="sex"/ value="male" checked="checked">男
			<input type="radio" name="sex"/ value="female">女<br />
			地址：
			<select>
				<option value="Hubei" selected="selected">湖北</option>
				<option value="Jiangxi">江西</option>
			</select><br />
			爱好：
			<input type="checkbox" name="hobbys" value="Yumaoqiu"/>羽毛球
			<input type="checkbox" name="hobbys" value="basketball"/>篮球
			<input type="checkbox" name="hobbys" value="pingpang"/>乒乓球<br />
			照片：
			<input type="file" name="picture"/><br />
			介绍：
			<input type="textarea" placeholder="请输入自我介绍"/><br />
			<!--
            	
            	描述：提交和重置方法一：用<input type = "">
            	<input type="submit" />  提交
			
				<input type="reset" /><br />  重置
            -->
            <!--
            	
            	描述：提交和重置方法二：使用button
            -->
			<button type="submit">提交</button>
			<button type="reset">重置</button>
		</form>
	</body>
</html>

```

