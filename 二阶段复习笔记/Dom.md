# DOM：         Document Object Model，即文档对象模型  

### 1、document入门

> 常用属性：
>
> -  	all	获取当前文档所有节点
>   - nodeName 	获取节点名称
>   - nodeType     获取节点类型
> - ​    images  获取当前文档所有<img>节点
> - ​    links  获取当前文档所有<a>标签节点

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>获取节点</title>
	</head>
	<body>
		<img src="" alt="这是一张图片">
		<img src="" alt="这是一张图片">
		<img src="" alt="这是一张图片">
		<input type="button" value="一键换图" onclick="setImg()" />
		<a href="#">百度1</a>
		<a href="#">百度1</a>
		<a href="#">百度1</a>
		<input type="button" value="给a标签插入链接" onclick="setHref()" />
	</body>
	<script>
		function setImg(){
			//获取所有的img节点
			var imgs = document.images;
			for(var i = 0; i < imgs.length; i ++){
                //给img对象设置图片链接
				imgs[i].src = "img/a.jpg";
                //调整图片宽高
				imgs[i].weight = 300;
				imgs[i].height = 200;
			}
		}
		
		function setHref(){
			//获取a标签节点
			var links = document.links;
			for(var i = 0;i < links.length;i++){
                //给单个节点设置链接
				links[i].href = "http://www.baidu.com";
			}
		}
		//获取所有节点，并打印节点名称
		var allNodes = document.all;
		for(var i = 0;i < allNodes.length;i++){
            //打印所有节点名称
			console.log(allNodes[i].nodeName);
		}
	</script>
</html>

```

### 2、根据属性找节点

> - ​		document.getElementById("html元素的id属性值") 
>   - 根据id获取节点
> - ​      document.getElementsByTagName("标签名") 
>   - 根据标签名获取节点
> - ​      document.getElementsByName("html元素的name属性值")
>   - 根据name属性获取节点
> - ​      document.getElementsByClassName("html元素的class属性值")
>   - 根据类名获取节点

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>根据属性找节点</title>
	</head>
	<body>
		<input type="text" id="userName" /><br />
		<input type="button" value="设置用户名" onclick="setUser()" /><br />
		<img src="" alt="这是图片" />
		<img src="" alt="这是图片" class="imgClass"/>
		<img src="" alt="这是图片" class="imgClass"/><br />
		<input type="button" value="设置图片" onclick="setImg()" /><br />
		<div>这是div标签</div>
		<div>这是div标签</div>
		<div>这是div标签</div><br />
		<input type="button" value="设置div标签" onclick="setDiv()" /><br />
		<span name = "span">这是span</span>
		<span name = "span">这是span</span>
		<span name = "span">这是span</span><br />
		<input type="button" value="设置span标签" onclick="setSpan()" /><br />
	</body>
	<script>
		//设置用户名
		function setUser(){
			//根据id获取节点
			var user = document.getElementById("userName");
			user.value = "张三";
		}
		//设置图片
		function setImg(){
			//根据类名获取节点
			var imgs = document.getElementsByClassName("imgClass");
			for(var i = 0;i < imgs.length;i++){
				imgs[i].src = "img/a.jpg";
				imgs[i].width = 200;
				imgs[i].height = 200;
			}
		}
		//设置div
		function setDiv(){
			//根据标签名获取节点
			var divs = document.getElementsByTagName("div");
			for(var i = 0;i < divs.length;i++){
				divs[i].innerHTML = "div".fontcolor("red");
				
			}
		}
		//设置span
		function setSpan(){
			//根据名称获取节点
			var spans = document.getElementsByName("span");
			for(var i = 0;i < spans.length;i++){
				spans[i].innerHTML = "HelloSpan".fontcolor("blue");
			}
		}
	</script>
</html>

```

### 3、综合案例：选购商品

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>案例</title>
	</head>
	<script>
		//全选/全不选
		function checkAll(){
			//获取所有item对象
			var items = document.getElementsByName("item");
			//获取全选对象
			var all = document.getElementsByName("all")[0];
			for(var i = 0;i < items.length;i++){
				items[i].checked = all.checked;
			}
		}
		//计算总价格
		function getSum(){
			//获取所有item对象
			var items = document.getElementsByName("item");
			var result = 0;
			for(var i = 0 ; i < items.length ; i++){
				if(items[i].checked){
					var price = parseInt(items[i].value);
					result += price;
				}
			}
			//根据id获取span对象
			var span = document.getElementById("sumid");
			span.innerHTML = ("总价格为："+result +"元").fontcolor("blue");
		}
	</script>
	<body>
		<div>商品列表</div>
		<input type="checkbox" name="item" value="3000" />笔记本
电脑3000元<br />
		<input type="checkbox" name="item" value="3000" />笔记本电脑3000元<br />
		<input type="checkbox" name="item" value="3000" />笔记本
电脑3000元<br />
		<input type="checkbox" name="item" value="3000" />笔记本电脑3000元<br />
		<input type="checkbox" name="item" value="3000" />笔记本电脑3000元<br />
		<input type="checkbox" name="item" value="3000" />笔记本电脑3000元<br />
		<input type="checkbox" name="all" onclick="checkAll()" />全/不选<br />
		<input type="button" value="总金额：" onclick="getSum()" />
		<span id="sumid"></span>

	</body>
</html>

```

### 4、通过节点关系找标签

#### 4.1	         通过关系(父子关系、兄弟关系)找标签  

> - ​		 parentNode 获取当前元素的父节点。
> - ​        childNodes 获取当前元素的所有下一级子元素。
> - ​        firstChild 获取当前节点的第一个子节点。
> - ​        lastChild  获取当前节点的最后一个子节点。
> - ​		 nextSibling   获取当前节点的下一个节点。（获取当前节点相邻的下一个平级节点）
> - ​        previousSibling 获取当前节点的上一个节点。（获取当前节点相邻的上一个平级节点 ）

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>通过节点关系找标签</title>
	</head>
	<body>
	</body>
	<script>
		//获取body节点
		var bodyNode = document.body;
		//获取父节点
		document.write(bodyNode.parentNode.nodeName);
		//获取子节点
		var childsNode = bodyNode.childNodes;
		for(var  i = 0 ; i < childsNode.length;i++){
			document.write(childsNode[i].nodeName );
		}
		//获取body节点的第一个子节点
		document.write(bodyNode.firstChild.nodeName);
		//获取body节点的最后一个子节点
		document.write(bodyNode.lastChild.nodeName);
		//获取当前节点的下一个平级节点
		document.write(bodyNode.nextSibling.nodeName);
		//获取当前节点的上一个平级节点
		document.write(bodyNode.previousSibling)
	</script>
</html>

```

#### 4.2	标签类型

> -   	 	  文本节点的类型： 3
> - ​      注释的节点类型： 8
> - ​      标签节点的类型： 1

### 5、创建节点，插入节点

#### 5.1	常用属性

> 常用属性：
>
> - nodeType 节点类型 
> -  	  nodeName 节点名称
> - nodeValue节点值
>   - 元素节点的 nodeName 是标签名称 
>   -  属性节点的 nodeName 是属性名称 
>   - 文本节点的 nodeName 永远是 #text 
>   - 文档节点的永远是 nodeName 永远是 #document 

#### 5.2	注意事项

> 注意事项：
>
> - ​    对于文本节点，nodeValue 属性是所包含的文本。
> - ​    对于属性节点，nodeValue 属性是属性值。
> - ​    对于注释节点，nodeValue 属性注释内容。
> - ​    nodeValue 属性对于文档节点和元素节点是不可用的。

#### 5.3	常用方法

> 常用方法：
>
> - ​	document.createElement("标签名")    创建新元素节点
> - ​    setAttribute:  设置节点的属性  
> - ​    appendChild 添加子节点  
> - ​     elt.insertBefore(newNode, childNode)    添加到elt中，childNode之前  
>   - 注意： [elt必须是childNode的直接父节点]()  
> - elt.removeChild(child)  删除指定的子节点  
>   -  注意： [elt必须是child的直接父节点]()  

```js
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>插入节点练习</title>
	</head>
	<script>
		var num = 1;
		
		function add(){
			
			//创建一个input元素节点
			var inputNode = document.createElement("input");
			//设置属性
			inputNode.setAttribute("type","button");
			inputNode.setAttribute("value","按钮"+num);
			inputNode.setAttribute("class","btnClass");
			num++;
			//获取body节点
			var bodyNode = document.body;
			bodyNode.appendChild(inputNode);
			
		}
		function remove(){
			//获取body节点
			var bodyNode = document.body;
			//获取要移除的子节点
			var childs = document.getElementsByClassName("btnClass");
			for(var i = 0;i < childs.length;i++){
				bodyNode.removeChild(childs[i]);
			}
			
		}
	</script>
	<body>
		<input type="button" value="插入按钮" onclick="add()" /><br />
		<input type="button" value="移除按钮" onclick="remove()"/>
	</body>
</html>

```

#### 5.4	添加、删除练习