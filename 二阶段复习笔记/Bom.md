# Bom:        Browser Object Model，浏览器对象模型  

### 1、window对象

> 常用方法：
>
> - ​	open()  打开一个新的窗口。
> - ​    resizeTo() 将窗口的大小更改为指定的宽度和高度值。 
> - ​    moveTo() 将窗口左上角的屏幕位置移动到指定的 x 和 y 位置。 
> - ​    moveBy() 相对于原来的窗口移动指定的x、y值。
> - ​    setInterval() 每经过指定毫秒值后就会执行指定的代码，会返回一个ID。
> - ​    clearInterval() 根据一个任务的ID取消的定时任务。
> - ​     setTimeout() 经过指定毫秒值后执行指定的代码一次。

[注意：使用window对象的任何属性与方法都可以省略window对象不写的  ]()

- 测试代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>window</title>
	</head>
	<body>
		<input type="button" value="打开新窗口" onclick="testOpen()"/>
		<input type="button" value="更改窗口大小" onclick="testResizeTo()"/>
		<input type="button" value="移动窗口之绝对定位" onclick="testMoveTo()"/>
		<input type="button" value="移动窗口之相对定位" onclick="testMoveBy()"/>
	</body>
	<script>
		//打开新窗口
		function testOpen(){
			window.open("index.html","_blank","location=no,toolbar=no");
		}
		//更改窗口尺寸
		function testResizeTo(){
			window.resizeTo("200","300");
		}
		//移动窗口之绝对定位
		function testMoveTo(){
			window.moveTo(0,200);
		}
		//移动窗口之相对定位
		function testMoveBy(){
			window.moveBy("100","200");
		}
		//每经过指定毫秒值后就会执行指定的代码
		var id = window.setInterval("testOpen()",5000);
		//取消执行指定代码
		window.clearInterval(id);
		//经过指定毫秒值后执行指定 的代码一次
		window.setTimeout("testOpen()",1000);
	</script>
</html>
```

### 2、常用事件

#### 2.1	        鼠标点击相关  

> - ​			onclick 在用户用鼠标左键单击对象时触发。 
> - ​          ondblclick 当用户双击对象时触发。 
> - ​          onmousedown 当用户用任何鼠标按钮单击对象时触发。 
> - ​          onmouseup 当用户在鼠标位于对象之上时释放鼠标按钮时触发。

```js
<body >
		<span id="span"></span>
	
		<input type="button" value="鼠标单击" onclick="testOnClick()" />
		<input type="button" value="鼠标双击" ondblclick="testOnDBClick()" />
		<input type="button" value="按下鼠标" onmousedown="testOnMouseDown()" />
		<input type="button" value="释放鼠标" onmouseup="testOnMouseUp()" />
		
</body>
	<script>
		var span = document.getElementById("span");
		
		//鼠标单击
		function testOnClick(){
			span.innerHTML = "鼠标单击了";
		}
		//鼠标双击
		function testOnDBClick(){
			span.innerHTML = "鼠标双击了";
		}
		//鼠标按下
		 function testOnMouseDown(){
		 	span.innerHTML = "鼠标按下了";
		 }
		 //释放鼠标
		 function testOnMouseUp(){
		 	span.innerHTML = "鼠标释放了";
		 }
		
	</script>
```

#### 2.2	        鼠标移动相关  

> - ​			onmouseout 当用户将鼠标指针移出对象边界时触发。 
> - ​          onmousemove 当用户将鼠标划过对象时触发

```js
<body >
		<span id="span"></span>
	
		<input type="button" value="鼠标移出" onmouseout="testOnMouseOut()" />
		<input type="button" value="鼠标划过" onmousemove="testOnMouseMove()" />
		
</body>
	<script>
		var span = document.getElementById("span");
		
		 //鼠标移入
		 function testOnMouseOut(){
		 	span.innerHTML = "鼠标移出了";
		 }
		 //鼠标移除
		 function testOnMouseMove(){
		 	span.innerHTML = "鼠标划过了";
		 }
		
	</script>
```

#### 2.3	        焦点相关

> - ​			onblur 在对象失去输入焦点时触发。 
> - ​          onfocus 当对象获得焦点时触发

```js
<body >
		<input type="text" onblur="testOnBlur()" onfocus="tsetOnFocus()"/>
		<span id="span"></span>
		
</body>
<script>
		var span = document.getElementById("span");
		 //文本框获取焦点
		 function tsetOnFocus(){
		 	span.innerHTML = "获取焦点".fontcolor("blue");
		 }
		 //文本框失去焦点
		 function testOnBlur(){
		 	span.innerHTML = "失去焦点".fontcolor("red");
		 }
		
</script>
```

#### 2.4	其他事件

> - ​		  onchange 当对象或选中区的内容改变时触发。 
> - ​         onload 在浏览器完成对象的装载后立即触发。 
> - ​         onsubmit 当表单将要被提交时触发。
>   - [注意：当该方法有返回值时，使用该方法要在前面加上return]()

```js
<body onload="testOnload()">
		<form onsubmit=" return testOnSubmit()">
			<span id="span"></span>
			<select onchange="testOnChange()">
				<option>郑州</option>
				<option>北京</option>
				<option>上海</option>
			</select><br />
			<button type="submit" >提交</button>
		<hr />
		</form>
</body>
<script>
		var span = document.getElementById("span");
		  //内容发生改变
		 function testOnChange(){
		 	span.innerHTML = "内容发生改变".fontcolor("green");
		 }
		 //页面加载完成
		 function testOnload(){
		 	alert("页面加载完成。。")
		 }
		 //表单提交
		 function testOnSubmit(){
		 	alert("表单提交了");
		 }
		
</script>
```

### 3、location对象

> 常用方法：
>
> - ​			href属性 设置或获取整个 URL 为字符串。
> - ​          reload()  重新刷新当前页面
> - ​			location.href	获取当前地址
> - ​			location.host	获取主机号+端口号
> - ​			location.hostname	获取主机号
> - ​			location.port	获取端口号
> - ​			location.protocol	获取协议

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>Location对象</title>
	</head>
	<body>
		<input type="button" value="刷新" onclick="onReload()" />
		<input type="button" value="跳转到新浪" onclick="onHref()" />
	</body>
	<script>
		//刷新
		function onReload(){
			location.reload();
		}
		//跳转到新浪
		function onHref(){
			location.href = "http://www.sina.com";
		}
		//获取当前地址	http://127.0.0.1:8020/Bom/test3.html
		document.writeln(location.href+"<br>");
		//获取主机号+端口号	127.0.0.1:8020
		document.writeln(location.host+"<br>");
		//获取主机号	127.0.0.1
		document.writeln(location.hostname+"<br>");
		//获取端口号	8020
		document.writeln(location.port+"<br>");
		//获取协议		http:
		document.writeln(location.protocol+"<br>");

	</script>
</html>

```

### 4、screen对象

> 常用方法：
>
> - ​			availHeight    获取系统屏幕的工作区域高度，排除 Windows 任务栏。 
> - ​          availWidth    获取系统屏幕的工作区域宽度，排除 Windows 任务栏。
> - ​          height        获取屏幕的垂直分辨率。 
> - ​          width         获取屏幕的水平分辨率

```js
<script>
		document.writeln("<pre>"+"不包含任务栏的高度：" + screen.availHeight);
		document.writeln("不包含任务栏的宽度：" + screen.availWidth);
		document.writeln("包含任务栏的高度：" + screen.height);
		document.writeln("包含任务栏的宽度：" + screen.width+"</pre>");
</script>
	
```

### 5、综合案例：随机选择英雄

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>随机选择英雄</title>
	</head>
	<body onload="girls()">
		<center>
			<span id="span"></span>
			<hr />
			<input type="button" style="font-size: 50px;" value="暂停" onclick="stop()" />
			<input type="button" style="font-size: 50px;" value="开始" onclick="start()" />
		</center>
	</body>
	<script>
		var span = document.getElementById("span");
		function girls(){
			var girslArr =["貂蝉","小乔","大乔","嫦娥","后羿","鲁班","狄仁杰"];
			//获取随机下标
			var index = Math.floor(Math.random() * girslArr.length);
			var girl = girslArr[index];
			//将对象放入到span中
			span.innerHTML = girl.fontcolor("red");
			//设置css样式
			span.style.backgroundColor = "yellow";
			span.style.fontSize = "150px";
			
		}
		var id = null;
		function start(){
			//设置定时器
			id = setInterval("girls()",50);
		}
		function stop(){
			//取消定时器
			clearInterval(id);
		}
	</script>
</html>

```

