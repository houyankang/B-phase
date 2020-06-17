

#   BOM、DOM



### 01_JavaScript之BOM对象

> * BOM对象
>   * bom : browser object model，浏览器对象模型
> * 分类
>   * window
>   * Navigator
>   * Screen
>   * History
>   * Location
>





### 02_BOM对象之window

> * 作用
>   * 跳转页面
>   * 获取其他bom对象
>   * 显示警告框
>   * 显示确认框
>   * 显示输入框
>   * 关闭页面
>
> * 常用属性
>
>   * location
>     * 设置跳转页面路径
>
> * 常用方法
>
>   * alert
>     * 显示警告框
>   * confirm
>     * 显示确认框
>   * prompt
>     * 显示输入框
>   * close
>     * 关闭页面
>   * setInterval
>   * setTimeout
>   * clearInterval
>   * clearTimeout
>
> * 代码实现
>
>   * location属性
>
>   ```js
>   function fn1() {
>       window.location = "${pageContext.request.contextPath}/index.jsp";
>   }
>   ```
>
>   * alert、confirm、prompt、close方法
>
>   ```js
>   function fn1() {
>       window.location = "${pageContext.request.contextPath}/index.jsp";
>       var history = window.history;
>   }
>   
>   function fn2() {
>       window.alert("删除失败1!");
>       alert("删除失败2!");
>   }
>   
>   function fn3() {
>       var flag = confirm("确认删除该用户吗?");
>       console.log(flag);
>   }
>   
>   function fn4() {
>       var content = prompt("请求输入密码:","abc");
>       console.log(content);
>   }
>   
>   function fn4() {
>       close();
>   }
>   ```
>
>   * 注意：close方法：Scripts may close only the windows that were opened by it，能够关闭的页面是由该页面打开的其他页面。
>



### 03_window对象之setInterval、setTimeout

* > 方法说明
  > * setInterval(code,millisec)：设置重复动作
  >   * code：重复调用的代码
  >   * millisec：重复间隔时间，单位为毫秒
  >   * 返回值是重复对象
  > * clearInterval(id_of_setinterval)：清除重复动作
  >   * id_of_setinterval：重复对象的id
  > * setTimeout(code,millisec)：设置延迟动作
  >   * code：延迟调用的代码
  >   * millisec：延迟时间
  >   * 返回值是延迟对象
  > * clearTimeout(id_of_settimeout)：清除延迟动作
  >   * id_of_settimeout：延迟对象的id

* 代码实现

  * setInterval方法

  ```js
  <head>
      <title>window对象之setInterval方法</title>
      <script>
          var inter ;
          function fn1() {
              inter = setInterval("showNum()",1000);
          }
  
          var num = 1;
  
          function showNum() {
              console.log(num);
              num++;
              var currentTimeStr = new Date().toLocaleString();
              console.log(currentTimeStr);
  
          }
  
          function fn2() {
              if (inter != undefined) {
                  clearInterval(inter);
              }
  
          }
  
  
      </script>
  
  </head>
  <body>
  
  <button onclick="fn1()">开始</button>
  <button onclick="fn2()">停止</button>
  </body>
  ```

  * setTimeout方法

  ```js
  <head>
      <title>window对象之setTimeout方法</title>
  
      <script>
  
          var timeOut1 ;
          var timeOut2;
  
          function fn1() {
              timeOut1 = setTimeout("showNum()",1000);//只调用了一次showNum方法
          }
  
          var num = 1;
          function showNum() {
              console.log(num);
              num++;
              var currentTimeStr = new Date().toLocaleString();
              console.log(currentTimeStr);
              //每隔一秒调用showNum方法
              timeOut2 = setTimeout("showNum()",1000);//重复调用showNum方法
          }
  
  
          function fn2() {
              if (timeOut2 != undefined) {
                  clearTimeout(timeOut2);
              }
          }
  
      </script>
  </head>
  <body>
  
  <button onclick="fn1()">开始</button>
  <button onclick="fn2()">停止</button>
  </body>
  ```

  

### 04_BOM对象之Location对象

> * 概述
>
>   * Location 对象包含有关当前 URL 的信息。
>
> * 常用属性
>
>   * href
>     * 设置或返回完整的 URL。
>
> * 常用方法
>
>   * reload
>     * 重新加载当前页面
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>BOM对象之Location对象</title>
>       <script>
>   
>           function fn1() {
>               location.href = "index.jsp";
>           }
>           
>           function fn2() {
>               //刷新页面
>               location.reload();
>           }
>   
>       </script>
>   </head>
>   <body>
>   
>   <button onclick="fn1()">跳转</button>
>   <button onclick="fn2()">刷新</button>
>   
>   </body>
>   ```
>
>   
>

### 05_BOM对象之History对象

> * 概述
>
>   * History 对象包含用户（在浏览器窗口中）访问过的 URL。
>
> * 常用方法
>
>   * back
>     * 加载 history 列表中的前一个 URL。
>   * forward
>     * 加载 history 列表中的下一个 URL。
>   * go
>     * 加载 history 列表中的某个具体页面。
>     * go(-1)：相当于back方法
>     * go(1)：相当于forward方法
>
> * 代码实现
>
>   * demo10.jsp
>
>   ```js
>   <head>
>       <title>BOM对象之History对象</title>
>       <script>
>   
>           function fn1() {
>               //下一页
>               history.forward();
>           }
>   
>       </script>
>   </head>
>   <body>
>   demo10 demo10 demo10<br>
>   
>   <a href="demo11.jsp">跳转到demo11</a><br>
>   <button onclick="fn1()">下一页</button>
>   
>   </body>
>   ```
>
>   * demo11.jsp
>
>   ```js
>   <head>
>       <title>BOM对象之History对象</title>
>       <script>
>   
>           function fn1() {
>               // history.back();
>               history.go(-1)
>           }
>   
>           function fn2() {
>               // history.forward();
>               history.go(1)
>           }
>   
>       </script>
>   </head>
>   <body>
>   demo11 demo11 demo11<br>
>   <button onclick="fn1()">上一页</button><br>
>   <a href="demo12.jsp">跳转到demo12</a><br>
>   <button onclick="fn2()">下一页</button><br>
>   </body>
>   ```
>
>   * demo12.jsp
>
>   ```js
>   <head>
>       <title>BOM对象之History对象</title>
>       <script>
>   
>           function fn1() {
>               history.back();
>           }
>   
>       </script>
>   </head>
>   <body>
>   demo12 demo12 demo12<br>
>   <button onclick="fn1()">上一页</button><br>
>   </body>
>   ```
>
>   
>





### 06_Javascript之DOM

> * 概念
>
>   * dom : document object model，文档对象模型
>
> * 分类
>
>   * Xml DOM
>     * 既可以操作xml文件，也可以操作html文件
>   * Html DOM
>     * 只能操作html文件
>
> * Xml DOM树
>
>   * ![image-20200511152308611](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200511155913.png)
>
>   * bookstore.xml
>
>     ```xml
>     <?xml version="1.0" encoding="UTF-8" ?>
>     <bookstore>
>     
>         <book category="魔幻小说">
>             <title lang="中文">Harry Potter</title>
>             <author>JK.Rowling</author>
>             <year>2005</year>
>             <price>29.99</price>
>         </book>
>     
>     </bookstore>
>     ```
>
>   * 根据bookstore.xml会生成上图所示的dom树型结构图
>
> * Html DOM树
>
>   * ![image-20200511152538095](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200511155916.png)
>
>   * demo13.jsp
>
>     ```jsp
>     <html>
>     <head>
>         <title>文档标题</title>
>     </head>
>     <body>
>     	<a href="index.jsp">我的链接</a>
>     	<h1>我的标题</h1>
>     </body>
>     </html>
>     ```
>
> * 总结
>
>   * html是由xml衍生出来的!!!
>





### 07_XmlDOM之Document对象

> * 概述
>
>   * Document 对象是一棵文档树的根，可为我们提供对文档数据的最初（或最顶层）的访问入口。
>
> * 作用
>
>   * 创建元素节点、文本节点、属性节点、注释节点
>   * 获取元素节点
>
> * 常用方法
>
>   * createElement
>     * 创建元素节点对象
>   * createTextNode
>     * 创建文本节点对象
>   * getElementById
>     * 根据id获取元素节点对象
>   * getElementsByTagName
>     * 根据标签名称获取一组元素节点对象
>
> * 代码实现
>
>   ```js
>           function fn1() {
>               //创建元素节点
>               var aEle = document.createElement("a");
>               //创建文本节点
>               var textEle = document.createTextNode("我是超链接");
>   
>               //获取元素节点
>               //根据指定id获取元素对象
>               var ele1 = document.getElementById("abc");
>               //根据指定标签名称获取元素对象
>               var ele2 = document.getElementsByTagName("a")[0];
>           }
>   ```
>
>   
>

### 08_XmlDOM之Element对象

> * 概述
>
>   * Element 对象表示 XML 文档中的元素。元素可包含属性、其他元素或文本。如果元素含有文本，则在文本节点中表示该文本。
>
> * 作用
>
>   * 操作该元素中的属性节点
>   * 操作该元素中的子元素节点
>   * 操作该元素中的文本节点
>
> * 常用方法
>
>   * getAttribute
>     * 返回指定属性的值
>   * setAttribute
>     * 设置属性值
>   * removeAttribute
>     * 移除指定属性
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>XmlDOM之element对象</title>
>   
>       <script>
>   
>           function fn1() {
>               //获取输入框中的name属性值
>               var ele = document.getElementById("username");
>               var value = ele.getAttribute("name");
>               console.log(value)
>           }
>   
>           function fn2() {
>               //设置输入框中的name属性值
>               var ele = document.getElementById("username");
>               ele.setAttribute("name","myUsername");
>   
>           }
>   
>           function fn3() {
>               // 移除输入框中的name属性
>               var ele = document.getElementById("username");
>               ele.removeAttribute("name");
>           }
>   
>           function fn4() {
>               var ele = document.getElementById("username");
>               //注意：通过getAttribute获取属性值，该属性值必须显式地设置到标签上！
>               var value = ele.getAttribute("value");
>               console.log(value)
>           }
>   
>       </script>
>   </head>
>   <body>
>       <input type="text" name="username" id="username" value="zhangsan"/>
>       <button onclick="fn1()">获取</button>
>       <button onclick="fn2()">设置</button>
>       <button onclick="fn3()">移除</button>
>       <button onclick="fn4()">获取value属性</button>
>   </body>
>   ```
>
>   

### 09_Xml DOM之Node对象

> * 概念
>
>   * Node对象是整个 DOM 的主要数据类型。
>   * Node对象可以是元素节点、属性节点、文本节点。
>
> * 常用属性
>
>   * childNodes
>   * firstChild
>   * lastChild
>   * nodeType
>     * | 元素类型 | 节点类型 |
>       | -------- | -------- |
>      | 元素     | 1        |
>      | 属性     | 2        |
>      | 文本     | 3        |
>      | 注释     | 8        |
>      | 文档     | 9        |
>   * parentNode
>
> * 常用方法
>
>   * appendChild
>   * removeChild
>
> * 代码实现
>
> ```js
> <head>
>    <title>Xml DOM之Node对象</title>
> <%--
>    需求1:给父div中添加一个子div，子div中的内容为”学好java”；
>    需求2:移除父div中指定的子元素
> --%>
> 
>    <script>
> 
>        function fn1() {
>            //1,获取父div
>            var parentDiv = document.getElementById("parentDiv");
>            //2,给父div添加一个子div
>            //2.1,创建子div元素对象
>            var childDiv = document.createElement("div");
>            //2.2,创建文本节点，内容为:”学好java”
>            var textNode = document.createTextNode("学好java");
>            //2.3,创建属性节点，属性名为id，值为childDiv
>            childDiv.setAttribute("id","childDiv");
>            //2.4,父div 包含  子div ；子div 包含 ”学好java”
>            childDiv.appendChild(textNode);
>            parentDiv.appendChild(childDiv);
> 
>        }
>        
>        function fn2() {
>            //1,获取父div
>            var parentDiv = document.getElementById("parentDiv");
>            //2,获取子div
>            var childDiv = document.getElementById("childDiv");
>            //2，移除childDiv元素
>            parentDiv.removeChild(childDiv);
>        }
> 
> 
>    </script>
> 
> </head>
> <body>
> 
> <div id="parentDiv">
>    父div
> </div>
> 
> <button onclick="fn1()">添加</button>
> <button onclick="fn2()">删除</button>
> 
> 
> </body>
> ```
>
> 
>

### 10_Xml DOM练习

* 需求

  * 需求1：如下代码，在id为"child1"的子div的父div中添加其他的子div

    ```js
    <body>
        <div >
        	<div id="child1">子div1</div>
        </div>
    	<button onclick="fn1()">添加</button>
    </body>
    
            function fn1() {
                var childDiv = document.getElementById("child1");
                //获取父div
                var parentDiv = childDiv.parentNode;
                //创建子div
                var childDiv2 = document.createElement("div");
                var textNode = document.createTextNode("hello dom");
                childDiv2.appendChild(textNode);
    
                parentDiv.appendChild(childDiv2);
            }
    ```

    

  * 需求2：如下代码，获取父div中的子元素的类型

    > ```jsp
    > 
    > <div id="parent">
    >     这是一个div1
    >     <div>这是一个div2</div>
    > </div>
    >         function fn1() {
    >             var parent = document.getElementById("parent");
    >             var childNodes = parent.childNodes;
    >             for (var i = 0; i < childNodes.length; i++) {
    >                 var childNode = childNodes[i];
    >                 console.log(childNode.nodeName+","+childNode.nodeType);
    >             }
    >         }
    > ```

  * 需求3：移除父div中的第一个子div

    ```js
    function fn2() {
        //获取父div
        var parentDiv = document.getElementsByTagName("div")[0];
        //获取所有子节点  ： 有元素节点、文本节点
        // var childNodes = parentDiv.childNodes;
        // console.log(childNodes.length)
        var childDivs = parentDiv.getElementsByTagName("div");
        var firstDiv = childDivs[0];
        console.log(firstDiv);
        if (undefined != firstDiv) {
            parentDiv.removeChild(firstDiv);
        }
    }
    ```

  * 需求4：移除父div中的最后一个子div

    ```js
    function fn3() {
        var parentDiv = document.getElementsByTagName("div")[0];
        //获取所有子节点  ： 有元素节点、文本节点
        // var childNodes = parentDiv.childNodes;
        // console.log(childNodes.length)
        var childDivs = parentDiv.getElementsByTagName("div");
        var lastDiv = childDivs[childDivs.length-1];
        if (undefined != lastDiv) {
            parentDiv.removeChild(lastDiv);
        }
    }
    ```

    

### 11_Html DOM

> * 概念
>
>   * **HTML DOM 定义了访问和操作HTML文档的标准方法。**
>   * **HTML DOM 把 HTML 文档呈现为带有元素、属性和文本的树结构（节点树）。**
>
> * document对象
>
>   * getElementById
>   * getElementByTagName
>
> * innerHTML、innerText
>
>   * innerHTML
>
>     * 用于往标签中插入内容（包含html标签）、解析html标签
>
>   * innerText
>
>     * 用于往标签中插入内容（包含html标签）、不能解析html标签
>
>   * 代码实现
>
>     ```js
>     <head>
>         <title>Html DOM之innerHTML、innerText</title>
>         <script>
>     
>             function fn1() {
>     
>                 var div = document.getElementById("parent");
>                 //Xml DOM
>                 // var text = document.createTextNode("你好世界");
>                 // div.appendChild(text);
>     
>                 //Html DOM
>                 //innerHTML、innerText：设置/获取标签内容
>                 // div.innerHTML = "<font color='red'>你好世界!!</font>";
>                 // div.innerText = "<font color='red'>你好世界!!</font>";
>                 console.log(div.innerHTML)
>                 console.log(div.innerText)
>             }
>     
>         </script>
>     
>     </head>
>     <body>
>     
>     <div id="parent">
>         parent parent parent
>     </div>
>     <button onclick="fn1()">添加</button>
>     </body>
>     ```
>
>     
>

### 12_Html DOM操作html标签

> * 需求：
>
>   * 动态获取文本输入框中的内容
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>XmlDOM</title>
>   
>       <script>
>   
>           function fn1() {
>               console.log("内容发生改变~~~");
>               var ele = document.getElementsByName("username")[0];
>       		console.log(ele.value);
>               //Html DOM中有一个Text对象:value属性：获取/设置value属性值
>               ele.value = "helloworld";
>           }
>   
>       </script>
>   </head>
>   <body>
>   <input type="text" name="username" onchange="fn1()"/>
>   </body>
>   ```
>
>   
>

### 13_Html DOM操作Html样式

> * 需求
>
>   * 修改div元素的边框、宽度、内容字体大小.
>
> * 语法
>
>   ```js
>   元素对象.style.属性名 = "属性值";
>   ```
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>Html DOM操作样式</title>
>       <style>
>           div{
>               background-color: deepskyblue;
>           }
>       </style>
>       <script>
>           // 修改div元素的边框、宽度、内容字体大小.
>           function fn1() {
>               var div = document.getElementById("div");
>               div.style.border="10px solid green";
>               div.style.width = "200px";
>               div.style.fontSize = "50px";
>           }
>   
>       </script>
>   </head>
>   <body>
>   
>   
>   <div id="div">
>       这是一个div
>   </div>
>   <button onclick="fn1()">修改</button>
>   </body>
>   ```
>
>   
>



### 14_Javascript综合案例一

> * 需求:
>
>   * 得到select下的所有的option中的文本信息
>
> * 解决方案
>
>   * XmlDOM
>   * HtmlDOM
>
> * 代码实现
>
>   * Xml DOM
>
> ```js
>        function fn1() {
>            var select = document.getElementById("sel");
>            var childNodes = select.childNodes;
>            for (var i = 0; i < childNodes.length; i++) {
>                //既可以是换行符(3)，也可以是option元素(1)
>                var childNode = childNodes[i];
>                if (childNode.nodeType == 1) {
>                    //就是一个option元素
>                    //获取"小学"...节点对象
>                    //因为文本节点是option节点的第一个节点对象
>                    var textNode = childNode.firstChild;
>                    //获取文本节点值
>                    var nodeValue = textNode.nodeValue;
>                    console.log(nodeValue);
>                }
>            }
>        }
> ```
>
>   * Html DOM
>
> ```js
>        //Html DOM
>        function fn2() {
>            //获取select对象
>            var select = document.getElementById("sel");
>            //获取所有option
>            var options = select.options;
>            for (var i = 0; i < options.length; i++) {
>                //获取每一个option对象
>                var option = options[i];
>                console.log("text : " + option.text + " , value : "+ option.value);
>            }
>        }
> ```
>
>   * html代码
>
> ```html
> <select id="sel">
>    <option value="xx">小学</option>
>    <option value="cz">初中</option>
>    <option value="gz">高中</option>
>    <option value="dx">大学</option>
> </select><br>
> <button onclick="fn1()">获取1</button><br>
> <button onclick="fn2()">获取2</button><br>
> ```
>
> 
>

### 15_Javascript综合案例二

> * 需求
>
>   * 得到select下的选中的option中的文本信息和value属性的值
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>Javascript综合案例二</title>
>       <%--得到select下的选中的option中的文本信息和value属性的值--%>
>       <script>
>   
>           function fn1() {
>               //获取selec选中的option中的value属性值及文本内容
>               var select = document.getElementById("sel");
>               //获取到被选中的选项的索引
>               var selectedIndex = select.selectedIndex;
>               //获取所有option数组
>               var options = select.options;
>               //通过数组、索引获取对应option对象
>               var option = options[selectedIndex];
>               var text = option.text;
>               var value = option.value;
>               console.log("text : " + text + " , value : " + value);
>   
>           }
>   
>       </script>
>   </head>
>   <body>
>   <select id="sel" onchange="fn1()">
>       <option value="xx">小学</option>
>       <option value="cz">初中</option>
>       <option value="gz">高中</option>
>       <option value="dx">大学</option>
>   </select>
>   </body>
>   ```
>
>   
>

### 16_Javascript综合案例三

> * 需求
>
>   * 在select下增加一个选项"硕士"
>
> * 代码实现
>
>   ```js
>       <script>
>   
>           //Xml DOM
>           function fn1() {
>               var select = document.getElementById("sel");
>               //创建一个option对象
>               var option = document.createElement("option");
>               option.setAttribute("value","ss");
>               var text = document.createTextNode("硕士");
>               option.appendChild(text);
>               select.appendChild(option);
>           }
>   
>   
>           //Html DOM
>           function fn2() {
>               var select = document.getElementById("sel");
>               var option = document.createElement("option");
>               option.text = "博士";
>               option.value = "bs";
>               select.add(option);
>           }
>   
>       </script>
>   ```
>
>   
>

### 17_Javascript综合案例四

> * 需求
>
>   * 当选择 全选/全不选时，下面的四个爱好，都会与我们全选/全不选一样。 
>   * 当选择全选按钮时，要求四个爱好项全都选择。 
>   * 当选择全不选按钮时，要求四个爱好项全都不选择。 
>   * 当选择反选时，要求四个爱好项，选择的取消，没有选择的选中。
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>Javascript综合案例4</title>
>       <script>
>           function selectAll() {
>               var hobbys = document.getElementsByClassName("hobbys");
>               var all = document.getElementById("all");
>               for (var i = 0; i < hobbys.length; i++) {
>                   var hobby = hobbys[i];
>                   //将每个爱好的多选框的选中状态，应该设置和
>                   hobby.checked = all.checked;
>               }
>           }
>   
>           /**
>            * 全选
>            */
>           function fn1() {
>               //全选 : 让所有多选框选中
>               //获取所有的多选框
>               var hobbys = document.getElementsByClassName("hobbys");
>               for (var i = 0; i < hobbys.length; i++) {
>                   console.log("设置~~~")
>                   //获取每一个多选框
>                   var hobby = hobbys[i];
>                   //让多选框选中
>                   if (!hobby.checked) {
>                       hobby.checked = true;
>                   }
>   
>               }
>   
>           }
>   
>           /**
>            * 全不选
>            */
>           function fn2() {
>               //全不选
>               var hobbys = document.getElementsByClassName("hobbys");
>               for (var i = 0; i < hobbys.length; i++) {
>                   var hobby = hobbys[i];
>                   if (hobby.checked) {
>                       hobby.checked = false;
>                   }
>               }
>           }
>   
>           function fn3() {
>               //反选
>               var hobbys = document.getElementsByClassName("hobbys");
>               for (var i = 0; i < hobbys.length; i++) {
>                   var hobby = hobbys[i];
>                   //获取之前的选中状态
>                   var oldChecked = hobby.checked;
>                   //取反获取新的选中状态
>                   var newChecked = !oldChecked;
>                   hobby.checked = newChecked;
>               }
>   
>           }
>   
>       </script>
>   </head>
>   <body>
>   
>       <input type="checkbox" onchange="selectAll()" id="all"/>全选/全不选
>       <br>
>       <br>
>       <input type="checkbox" class="hobbys"/>篮球
>       <input type="checkbox" class="hobbys"/> 足球
>       <input type="checkbox" class="hobbys"/>乒乓球
>       <input type="checkbox" class="hobbys">排球
>       <br>
>       <br>
>   
>       <button onclick="fn1()">全选</button>   <button onclick="fn2()">全不选</button>  <button onclick="fn3()">反选</button>
>   
>   </body>
>   ```
>
>   
>

### 18_Javascript综合案例五

> * 需求
>
>   * 完成如下图所示效果
>
>     * ![image-20200512164715245](C:\Users\qiuzhiwei\AppData\Roaming\Typora\typora-user-images\image-20200512164715245.png)
>
>     * 所有内容不可以为空 
>     * 邮箱必须邮箱的规则 
>     * 用户名与密码长度必须6位以上 
>     * 密码与重复密码必须一致
>
>   * 开发流程
>
>     * 在表单校验之前，要清空原来的错误提示信息
>     * 校验表单不能为空（账户、密码、重复密码、邮箱）
>
>   * 代码实现
>
>     * clearSpan方法
>       * 清空原有的错误提示信息
>
>     ```js
>     function clearSpan() {
>         var spans = document.getElementsByTagName("span");
>         for (var i = 0; i < spans.length; i++) {
>             var span = spans[i];
>             span.innerHTML = "";
>         }
>     }
>     ```
>
>     * checkNull方法
>       * 非空校验
>
>     ```js
>     function checkNull(id) {
>         var ele = document.getElementById(id);
>         var value = ele.value;
>         var reg = /^\s*$/;
>         if (reg.test(value)) {
>             //输入框为空
>             var spn = document.getElementById(id+"_error");
>             spn.innerHTML = "<font color='red'>"+id+"不能不为空</font>";
>             return false;
>         } else {
>             //输入框不为空
>             return true;
>         }
>     }
>     ```
>
>     * checkLength方法
>       * 长度校验
>
>     ```js
>     function checkLength(id) {
>         var reg = /^.{6,}$/;
>         var ele = document.getElementById(id);
>         var value = ele.value;
>         if (reg.test(value)) {
>             //长度6个以上
>             return true;
>         } else {
>             //长度不对
>             var span = document.getElementById(id + "_error");
>             span.innerHTML = "<font color='red'>" + id + "长度应该为6</font>";
>             return false;
>         }
>     }
>     ```
>
>     * checkEquals方法
>       * 校验密码和确认密码是否一致
>
>     ```js
>     function checkEquals() {
>         var ele1 = document.getElementById("password");
>         var ele2 = document.getElementById("repassword");
>         var password = ele1.value;
>         var repassword = ele2.value;
>         if (password == repassword) {
>             return true;
>         } else {
>             var span = document.getElementById("repassword_error");
>             span.innerHTML = "<font color='red'>两次密码不一致</font>";
>             return false;
>         }
>     }
>     ```
>
>     * checkEmail方法
>       * 校验邮箱
>
>     ```js
>     function checkEmail() {
>         var reg = /^(\w)+@(\w)+(.\w+)+$/;
>         var ele = document.getElementById("email");
>         var value = ele.value;
>         if (reg.test(value)) {
>             //满足邮箱格式
>             return true;
>         } else {
>             //不满足邮箱格式
>             var span = document.getElementById("email_error");
>             span.innerHTML = "<font color='red'>邮箱格式不对</font>";
>             return false;
>         }
>     }
>     ```
>
>     * checkInfo方法
>       * 先清空原有错误提示信息
>       * 校验账户
>         * 校验账户是否为空
>         * 校验账户长度
>       * 校验密码
>         * 校验密码是否为空
>         * 校验密码长度
>       * 校验确认密码
>         * 校验确认密码是否为空
>         * 校验确认密码长度
>         * 校验密码和确认密码是否一致
>       * 校验邮箱
>         * 校验邮箱是否为空
>         * 校验邮箱格式
>
>     ```js
>     function checkInfo() {
>         clearSpan();
>         return  checkNull("username") && checkLength("username") &&
>                 checkNull("password") && checkLength("password") &&
>                 checkNull("repassword") && checkLength("repassword") && checkEquals() &&
>                 checkNull("email") && checkEmail();
>     }
>     ```
>
> 
>
> 

