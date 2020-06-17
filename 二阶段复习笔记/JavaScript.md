# JavaScript

### 一、JS编写及其引入方式

#### 1.1         可以使用<script>标签体内进行编写  

```js
		<script>
			
			alert("学习ing")
			var result = confirm("你今天学习了吗？");
			alert(result)
			var age = prompt("请输入你的年龄：");
			document.write(age);
		</script>
```

#### 1.2	引入JS

- js文件

```js
alert("今天记得学习喲.......")

```

- test1.html	引入js文件

```js
<script src="js/1.js">
    
 </script>
```

#### 1.3	注意事项

> 1. [ <script>是有开始标签与结束标签的，千万不要在一个标签中结束了。    ]()
> 2. [ 如果<script>已经用于引入了js文件，那么该<script>标签体就不能再写js代码了  ]()

#### 1.4	js常用的函数

> - alert("显示的内容") 
>   - 弹出框   
> -  confirm("确认删除吗?")  
>   - 点击确定返回true否则返回false  
> -  prompt("请输入你的名字")  
>   - 点击确定返回输入的内容否则返回null  

```js
<script>	
			alert("学习ing")
			var result = confirm("你今天学习了吗？");
			alert(result)
			var age = prompt("请输入你的年龄：");
			document.write(age);
</script>
```

### 二、声明变量

#### 2.1	声明变量格式

> [var	变量名 =  数据]()

#### 2.2	注意事项

> 1. [在js中声明变量是 使用var关键字声明的，js中的变量可以存储任意的数据类型数据  ]()
> 2. [js中变量数据类型是根据存储的值决定的，可以随时更改存储数据的类型]()
> 3. [定义了多个同名的变量是，后定义的同名变量是覆盖前面定义的同名变量]()
> 4. [声明变量的时候可以省略var关键字，但是不建议省略  ]()

#### 2.3	js中的数据类型

> - number 	小数与整数  
> -  string  字符串  
>   - [注意：js中没有字符的概念，只有字符串，字符串可以写在单引号或双引号中  ]()
> - boolean 布尔数据类型  
> - undefined 代表该变量没有定义  

#### 2.4	如何获取数据类型

> 使用[typeof方法]()来获取数据的类型

```js
<script>
			
			var a = 12;
			document.write("a的数据类型是：" +typeof (a) +"<br />");//number
			var b = 3.14;
			document.write("b的数据类型是:" + typeof + b +"<br />");//number
			var c = true;
			document.write("c的数据类型是：" +typeof c +"<br />")//boolean
			var d = "你好啊，勇士。"
			document.write("d的数据类型是：" + typeof d + d +"<br />" )//string
			
			var e = NaN;
			document.write("e的数据类型是" +typeof e)//number
			
</script>
```

### 三、字符转化成数字

#### 3.1	常用方法

> - parseInt() 可以把一个字符串转换成整数。
>
> - parseFloat() 可以把一个字符串转换成小数

```js
<script>
		var a = "123";
		document.write(parseInt(a) +"<br />");//123
		var b = "3.14";
		document.write(parseFloat(b) +"<br />");//3.14
		var c = "123abc123";
		document.write(parseInt(c))//123
</script>
```

#### 3.2	注意事项

> 1. parseInt方法如果接收的字符串含有非数字的字符，那么parseInt方法会从字符串的首个字符开始寻找，一直找到非数字字符为止，然后就使用前面的数字字符转换成数字  。
>
>    ```js
>    var c = "123abc123";
>    document.write(parseInt(c))//123
>    ```
>
> 2. js提供一个IsNaN的方法让我们判断该字符串是否是 一个数字
>
>    ```js
>    <script>
>    		var a = "123";
>    		document.write(isNaN(a));//false
>    		var b = 123;
>    		document.write(isNaN(b));//false
>    		var c = "你好";
>    		document.write(isNaN(c));//true
>    </script>  
>    ```

[NaN: not a number	不是一个数字]()

### 四、运算符

#### 4.1	逻辑运算符

> &&	、	||

```js
<script>
			
			document.write((true&&true)+"<br/>");//true
			document.write((true&&false)+"<br/>");//false
			document.write((false&&true)+"<br/>");//false
			document.write((false&&false)+"<br/>");//false
			
			
			document.write((true||true)+"<br/>");//true
			document.write((true||false)+"<br/>");//true
			document.write((false||true)+"<br/>");//true
			document.write((false||false)+"<br/>");//false

</script>
```

#### 4.2	三目运算符

> 布尔表达式	?	值1	:	值2;  

```js
<script>
		
			var age = 16;
			document.write(age >= 18 ? "成年" : "未成年");//未成年
</script>
```

### 五、流程控制语句

#### 5.1	if语句

> 格式：
>
> ​			if(判断条件){
>
> ​       		符合条件执行的代码 
>
> ​     	 } 

[注意：在js中的if语句条件不单止可以写布尔表达式，还可以写任何的数据  ]()

[			number 非0为true, 0为false  ]()

[		   string 内容不为空是true， 内容为空的时候是false  ]()

[          undefined：false  ]()

[			NaN:  false]()

[			Null:  false]()

```js
<script>
		
		var a = 1;
		var b = "a";
		var c ;
		var d = NaN;
		if(d){
			document.write("true" +"<br />")
		}else{
			document.write(false +"<br />");
		}
	
		
</script>
```

#### 5.2	switch语句

> 格式：
>
> ​		
>
> ```
> switch(变量){
> 	case 1 : 值1；
> 		break;
> 	case 2:  值2；
> 		break;
> 	case 3 : 值3；
> 		break;
> 		.......
> 	default: 以上条件都不满足时执行的语句
> 		break;				
> }
> 
> ```

[注意：         在js中switch后面可以跟其他类型  ]()

```js
<script>

		var e = "c"
		switch(e){
			case "a":
				document.write("e的值是："+e);
				break;
			case "b":
				document.write("e的值是：" +e);
				break;
				
			default:
				document.write("e的值既不是a也不是b")
		}
		
		
</script>
```

### 六、循环语句

#### 6.1	while循环

> 格式：
>
> ​	while(判断的条件){
>
> ​         循环体内容 
>
> ​       }

```js
<script>

		document.write(result+"<br />");
		var i = 1;
		var result1 = 0;
		while(i <= 100){
			result1 += i;
			i++;
		}
		document.write(result1 +"<br />");

		
</script>
```

#### 6.2	do...while循环

> 格式：
>
> do{
>
> ​      循环语句；
>
> ​    }while(判断条件);

```js
	<script>

		//打印1-100的和
		var i = 1;
		var result2 = 0;
		do{
			result2 += i;
			i++;
		}while(i <= 100);
		document.write(result2+"<br />")
	

		//计算1-100奇数的总和
		var result4 = 0;
		var i = 1;
		do{
			if(i % 2 == 1){
				result4 += i;
			}
			i++;
		}while(i <= 100)
		
		document.write(result4);
		
	</script>
```

#### 6.3	for循环

> 格式：
>
> for(初始化语句; 判断的条件 ; 循环后的语句){
>
> ​       循环体语句； 
>
> ​      }

```js
<script>
		//打印1-100的和
		var result = 0;
		for(var i = 1;i <= 100;i++){
			result += i;
		}
		document.write(result+"<br />");
	
		//打印9*9乘法表
		for(var i = 1; i <= 9;i++){
			for(var j = 1;j <= i;j++){
				document.write(j +"*" +i +"=" +i*j +"&nbsp;&nbsp;&nbsp;&nbsp");
			}
			document.write("<br />")
		}
		
		
		//计算1-100偶数中的总和
		
		var result3 = 0;
		for(var i = 1;i <=100; i++){
			if(i % 2 == 0){
				result3 += i;
			}
		}
		document.write(result3 +"<br />")
		
	
</script>
```

### 七、函数

#### 7.1	函数的定义

> 格式：
>
> function 函数名(形参列表){
>
> ​      函数体 ; 
>
> ​    }

#### 7.2	注意事项

> 1. 在 javascript中函数 定义形参时是不能使用var关键字声明变量的。
>
> ​    2. 在javascript中 的函数是没有 返回值类型 的，如果函数需要返回数据给调用者，直接返回即可，如果不需要返回则不返回。
>
> ​    3. 在 javascript中是没有函数 重载 的概念 的，后定义的同名函数会直接覆盖前面定义同名函数。

#### 7.3	函数练习案例

- if控制语句

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>月份练习</title>
	</head>
	<script>
		function checkDays(){
			var monthStr = document.getElementById("month").value;
			var month = parseInt(monthStr);
			
			if(month ==1 || month == 3 || month ==5 || month == 7 || month == 8 || month ==10 || month ==12){
				alert(month +"月有31天，祝您天天开心");
			}else if(month == 2){
				alert(month +"月有28天，祝您天天开心");
			}else if(month ==4 || month == 6 || month ==8 || month == 11){
				alert(month +"月有30天，祝您天天开心");
			}else{
				alert("月份输入错误，请重新输入！");
			}
			
		}
		
	</script>
	<body>
		<input type="text" id="month" />
		<input type="submit" value="查询" onclick="checkDays()" />
	</body>
</html>

```

- switch控制语句

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>月份案例</title>
	</head>
	<script>
		function checkDays(){
			var month = document.getElementById("month").value;
			switch(month){
				case "1":
				case "3":
				case "5":
				case "7":
				case "8":
				case "10":
				case "12":
					alert(month+"月有31天，祝您天天开心！");
					break;
				case "2":
					alert(month+"月有28天，祝您天天开心！");
					break;
				case "4":
				case "6":
				case "9":
				case "11":
					alert(month+"月有30天，祝您天天开心！");
					break;
				default:
					alert("不存在该月份，请您重新输入");
				
			}
		}
		
	</script>
	<body>
		请输入月份：<input type="text" id="month" />
		<input type="submit" value="查询" onclick="checkDays()"/>
	</body>
</html>

```

### 八、String对象

#### 8.1	创建方式

> 方式一：
>
> ​	var	str	= 	new String("字符串的内容");
>
> 方式二：
>
> ​	var	str	=    "字符串的内容"  ；

#### 8.2	常用方法

> -    anchor（）  生产  锚点 
> - ​    charAt()   返回指定索引位置处的字符。
> - ​    fontcolor() 把带有 COLOR 属性的一个 HTML <FONT> 标记放置在 String 对象中的文本两端
> - ​    indexOf()  返回 String 对象内第一次出现子字符串的字符位置
> - ​    italics()  把 HTML <I> 标记放置在 String 对象中的文本两端。 
> - ​    link()     把一个有 HREF 属性的 HTML 锚点放置在 String 对象中的文本两端。   
> - ​    replace()   返回根据正则表达式进行文字替换后的字符串的复制   
> - ​    split()    切割  
> - ​    Substr(a,b)    截取子串，第一个参数表示下标，第二个参数表示长度
> - ​    toUpperCase() 转大写
> - ​    toLowerCase  转小写
>
> [注意：在使用replace()方法时，在需要被替换的字符后面加上/g，就会全部替换]()
>
> ```js
> //将o全部替换为0
> document.write("helloword".replace(/o/g,0)+"<br />")
> ```
>
> 

```js
	<script>
		
		var a = "这是顶部";
		//设置锚点
		a.anchor("top");
		
		var b ="dsafasd";
		//获取下标0的字符
		document.write(b.charAt(0))
		//获取字符s的下标索引
		document.write(b.indexOf('s'));
		//字体设置为斜体
		document.write("比萨斜塔".italics())
		//大写转小写
		document.write("SADAD".toLowerCase())
		//小写转大写
		document.write("dasas".toUpperCase())
		//将文本内容设置为红色
		document.write("爱情公寓".fontcolor("red"))
		//设置外部链接
		document.write("百度一下，你就知道".link("http://www.baidu.com"))
		//替换字符
		document.write("哈哈哈你好啊".replace("哈","呵呵呵呵"))
		//从下标0开始截取字符，截取3位		0,1,2，
		document.write("0123456".substr(0,3)+"<br />")

		var b = "a,b,c,d,e,f";
		//按照“，”分割字符串
		var stuArr = b.split(",")
		for(var i =0 ;i <stuArr.length;i++){
			document.write(stuArr[i]+"<br>") ;
		}
		//将o全部替换为0
		document.write("helloword".replace(/o/g,0)+"<br />")
		//将hello替换为你好
		document.write("helloworld".replace(/hello/g,"你好"))
	</script>
	<body>
		<div style="height: 1000px;"></div>
		<a href="#top">返回顶部</a>
	</body>
```



### 九、Date对象

#### 9.1	创建方式

> [var	dete	= new Date;]()

#### 9.2	常用方法

> - date.getFullYear()	获取年份
> - date.getMonth() 	 获取月份
>   - [注意：月份是从0-11，实际运用中要	+1]()
> -  date.getDate()   	 获取天数
> - date.getHours()     	 获取小时数
> - date.getMinutes()   	 获取分钟数
> - date.getSeconds()     	 获取秒数

#### 9.3	动态显示当前系统时间

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>动态获取系统时间</title>
	</head>
	
	<body>
		<span id="timeInfo"></span>
	</body>
	<script>
		function getTime(){
			var date = new Date();
			var year = date.getFullYear();
			var month = date.getMonth() +1;
			var days = date.getDate();
			var hours = date.getHours();
			var minutes = date.getMinutes();
			var seconds = date.getSeconds();
			
			var timeInfo = year + "年" + month + "月" + days +"日"+ hours +":"+ minutes +":"+seconds;
			var timeObj = document.getElementById("timeInfo");
            //将获取到的时间拼接起来，显示到span标签中
			timeObj.innerHTML = timeInfo;
		}	
		getTime();
		//每隔1秒调用一次方法
		window.setInterval("getTime()",1000);
		
	</script>
</html>

```

### 十、Math对象

#### 10.1	常用方法

> - ​	 ceil   向上取整
> - ​     floor（）  向下取整
> - ​     random() 随机数方法 // 产生的伪随机数介于 0 和 1 之间（含 0，不含 1），
> - ​     round   四舍五入

#### 10.2	相关案例

```js
<script>
		//向上取整		4
		document.write(Math.ceil(3.14)+ "<br />");
		//向下取整		3
		document.write(Math.floor(3.14)+ "<br />");
		//四舍五入		6
		document.write(Math.round(5.52)+ "<br />");
		//获取1-10之间的数字	
		var math = Math.random();
		document.write(Math.ceil(math*10));
		
</script>
```

### 十一、数组对象

#### 11.1	创建数组方式

> 方式1：
>
> ​	         var 变量名 = new Array(); 创建一个长度为0的数组。  
>
> 方式2：
>
> ​        	 var 变量名= new Array(长度) 创建一个指定长度的数组对象  。
>
> 方式3：
>
> ​        	var 变量名 = new Array("元素1","元素2"...); 给数组指定元素创建数组的对象。 
>
> 方式4：
>
> ​			var 变量名 = ["元素1","元素2"...]; 

#### 11.2	注意事项

[在js中数组的长度是可以发生变化的 。 ]()

```js
		var arr3 = new Array(1,2,3);
		document.write(arr3.length +"<br />");//3
		arr3[10] = 5;
		document.write(arr3.length +"<br />");//11
```

#### 11.3	数组常用方法

> - ​         pop ：移除数组中的最后一个元素并返回该元素  
> - ​         push("永康")：将新元素添加到一个数组中，并返回数组的新长度值  
> - ​         reverse()：翻转数组的元素  
> - ​         shift()：移除数组中第一个元素，并且返回  

#### 11.4	相关案例

```js
	<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>数组使用</title>
	</head>
	<script>
		//创建一个长度为0的数组
		var arr1 = new Array();
		document.write(arr1.length +"<br />");//0
		var arr2 = new Array(10);
		document.write(arr2.length +"<br />");//10
		var arr3 = new Array(1,2,3);
		document.write(arr3.length +"<br />");//3
	
		
		var arr4 = ["a","b","c","d"];
		
		//移除数组的最后一个元素并返回该元素
		document.write(arr4.pop() +"<br />")//d
		//添加，并返回新长度
		document.write(arr4.push("e") +"<br />")//4
		//翻转数组
		document.write(arr4.reverse() +"<br />")//e,c,b,a
		//删除第一个元素，并返回
		document.write(arr4.shift() +"<br />")//e
		
		
	</script>
	<body>
	</body>
</html>

```

### 十二、自定义对象

#### 12.1	自定义对象的方式

> 方式1：使用无参的函数创建对象
>
> ```js
> 	function Person(){}
> 	var p = new Person();
> 	p.id = 1;
> 	p.name = "张三";
> 	document.write(p.id +"----"+p.name);  
> ```
> 方式2：使用带参的函数创建对象  
>
> ```js
> 	function Person(id,name){
> 		this.id = id;
> 		this.name = name;
> 		this.say = function(){
> 			alert("你好啊"+name);
> 		}
> 	}
> 	var p2 = new Person(2,"李四");
> 	p2.say();
> ```
> 方式3：使用Object函数创建对象  
>
> ```js
> 	var p3 = new Object()
> 	p3.id=3;
> 	p3.name = "王五";
> 	document.write(p3.id + "--------"+ p3.name +"<br />")
> ```
> 方式4：使用字面量的方式创建  
>
> ```js
> 	var p4 = {
> 		id : 4,
> 		name :"赵六",
> 		sayHello : function(){
> 			alert("你好啊"+this.name);
> 		}
> 	}
> 	p4.sayHello();
> ```

### 十三、         **js中!=，==，!==，===的用法和区别（面试题）**  

> ​	     [注意 ：   == 和 != 比较若类型不同，先偿试转换类型，再作值比较，最后返回值比较结果]()  
>
> ​         [				而=== 和 !== 只有在相同类型下,才会比较其值]()  

```JS
<script type="text/javascript">	    
		var num = 1;
		var str = '1';
		var test = 1;
		
		document.write(test == num); //true　相同类型　相同值
		document.write(test === num);//true　相同类型　相同值
		document.write(test !== num);//false test与num类型相同，其值也相同,　非运算肯定是false
		 
		 
		document.write(num == str);  //true 　把str转换为数字，检查其是否相等。
		document.write(num != str);  //false  == 的 非运算
		document.write(num === str); //false  类型不同，直接返回false
		document.write(num !== str); //true   num 与 str类型不同 意味着其两者不等　非运算自然是true
		
		//== 和 != 比较若类型不同，先偿试转换类型，再作值比较，最后返回值比较结果 。
		//而=== 和 !== 只有在相同类型下,才会比较其值。
	</script>

```

