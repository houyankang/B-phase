# Jquery






### 01_自定义myjs脚本库

> * 为什么要自定义myjs脚本库
>
>   * 原始的js操作，相对来说，比较复杂；可以将一些重复的动作，抽取出来，并建立一个新的脚本库
>
> * 代码实现
>
>   * 传统js
>
>   ```js
>   <head>
>       <title>自定义myjs脚本库</title>
>       <script>
>   
>           function fn1() {
>               //获取div元素
>               var ele = document.getElementById("div1");
>               // 获取 div元素标签内容
>               console.log(ele.innerHTML);
>               //设置div元素标签内容
>               ele.innerHTML = "this is a div1";
>               // 获取 div元素标签内容
>               console.log(ele.innerHTML);
>           }
>   
>           function fn2() {
>               //获取div元素
>               var ele = document.getElementById("div2");
>               // 获取 div元素标签内容
>               console.log(ele.innerHTML);
>               //设置div元素标签内容
>               ele.innerHTML = "this is a div2";
>               // 获取 div元素标签内容
>               console.log(ele.innerHTML);
>           }
>   
>       </script>
>   
>   </head>
>   <body>
>   
>   <div id="div1">
>   这是一个div1
>   </div>
>   
>   <div id="div2">
>       这是一个div2
>   </div>
>   <div id="div3">
>       这是一个div3
>   </div>
>   <button onclick="fn1()">操作1</button>
>   <button onclick="fn2()">操作2</button>
>   
>   </body>
>   ```
>
>   * 自定义myjs脚本库
>
>     * myjs.js
>
>     ```js
>     function $(id) {
>     
>         var ele = document.getElementById(id);
>     
>         //给ele添加一个方法，方法名叫html，形参content
>         ele.html = function (content) {
>             if (content != null) { //如果content不为空，就将content设置到ele对象中
>                 ele.innerHTML = content;
>             } else { // 如果content为空，就获取ele的内容
>                 return ele.innerHTML;
>             }
>         }
>     
>         return ele;
>     
>     
>     }
>     ```
>
>     * demo03.jsp
>
>     ```jsp
>     <head>
>         <title>自定义myjs脚本库</title>
>     
>         <script src="${pageContext.request.contextPath}/js/myjs.js"></script>
>         <script>
>     
>             function fn1() {
>     
>                 var content = $("div1").html();
>                 console.log(content);
>             }
>     
>             function fn2() {
>                 // var ele = $("div1");
>                 // ele.html("this is a div div div");
>                 $("div1").html("this is a div div div")
>             }
>     
>     
>         </script>
>     </head>
>     <body>
>     
>     
>     <div id="div1">
>         这是一个div1
>     </div>
>     
>     <button onclick="fn1()">获取</button>
>     <button onclick="fn2()">设置</button>
>     </body>
>     ```
>
>     
>
>   ### 03_Jquery介绍
>
>   * Jquery是什么？
>     * JQuery是一个JS的类库文件
>   * Jquery的作用？
>     * 可以简化遍历HTML文 档、操作DOM、处理事件、执行动画、开发Ajax等操作
>   * Jquery的诞生
>     * 2006年8月诞生的一个开源项目,现在Jquery团队主要包括核心库,UI和插件开发等. 开发人员,凭借简洁的语法和跨平台的兼容性.
>     * 其独特而又优雅的代码风格改变了 javascript程序员的设计思路和编写程序的方式
>
>   
>
>   
>

### 02_Jquery的基本使用

* > 开发流程
>
  > * 导入jquery的js文件到项目中
  > * 在页面中使用script标签引入外部的jquery文件
  > * 使用jquery语法操作元素

* 代码实现

  ```js
  <head>
      <title>Jquery的基本使用</title>
      <%--引入jquery类库--%>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <script>
          function fn1() {
              //$("选择器") -> 元素对应的jquery对象
              var ele = $("#div1");
              var content = ele.html();
              console.log(content);
          }
  
          function fn2() {
              //ele不是js对象，而是一个jquery对象
              var ele = $("#div1");
              ele.html("this is a div");
          }
  
  
      </script>
  </head>
  <body>
  
  
  <div id="div1">
      这是一个div
  </div>
  
  <button onclick="fn1()">获取</button>
  <button onclick="fn2()">设置</button>
  
  </body>
  ```

  

### 03_jquery对象和js对象

> * 问题
>
>   * jquery对象能否直接使用js对象的属性和方法？
>     * 不能!
>   * js对象能否直接使用jquery对象的属性和方法?
>     * 不能!
>
> * jquery对象和js对象的相互转换
>
>   * js对象 -> jquery对象
>     * $(js对象)
>   * jquery对象  -> js对象
>     * jquery对象.get(0)
>     * jquery对象[0]
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>jquery对象和js对象</title>
>       <%--
>           jquery对象能否使用js对象的属性和方法?
>               jquery对象不能使用js对象的属性和方法!
>           js对象能否使用jquery对象的属性和方法？
>               js对象不能使用jquery对象的属性和方法!
>       --%>
>       <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
>       <script>
>   
>           function fn1() {
>               //获取js对象
>               var jsObject = document.getElementById("div1");
>               //js对象能否使用jquery对象的属性和方法？
>               jsObject.html("this is a div");
>           }
>   
>           function fn2() {
>               var jqObject = $("#div1");
>               // jquery对象能否使用js对象的属性和方法?
>               jqObject.innerHTML = "this is a div";
>           }
>   
>           //需求：已有js对象，让js对象调用jquery对象的属性和方法，怎么办？
>           //可以将js对象转换成jquery对象
>           function fn3() {
>               //获取js对象
>               var jsObject = document.getElementById("div1");
>               //将js对象 -> jquery对象
>               var jqObject = $(jsObject);
>               //调用jquery对象的属性和方法
>               jqObject.html("this is a div!!!");
>           }
>   
>           //需求：已有jquery对象，让jquery对象调用js对象的属性和方法，怎么办？
>           //可以将jquery对象转换成js对象
>           function fn4() {
>               //获取jquery对象
>               var jqObject = $("#div1");
>               //jquery对象 -> js对象
>               // var jsObject = jqObject.get(0);
>               var jsObject = jqObject[0];
>               //调用js对象的属性和方法
>               jsObject.innerHTML = "this is a div ???";
>   
>   
>   
>           }
>   
>       </script>
>   
>   </head>
>   <body>
>   
>   <div id="div1">
>       这是一个div
>   </div>
>   
>   <button onclick="fn1()">操作1</button>
>   <button onclick="fn2()">操作2</button>
>   <button onclick="fn3()">转换1</button>
>   <button onclick="fn4()">转换2</button>
>   </body
>   ```
>
>   
>

### 04_jquery选择器介绍及分类

> * 概念
>   * jquery操作都需要依赖于选择器
>   * 可以让jquery代码锁定指定的元素
>   * 不仅能简化代码,而且可以达到事半功倍的效果
> * 分类
>   * 基本选择器
>   * 层次选择器
>   * 过滤选择器
>     * 基本过滤选择器
>     * 内容过滤选择器:
>     * 属性过滤选择器
>     * 子元素过滤选择器
>



### 05_jquery选择器之基本选择器

> * 基本选择器
>
>   * id选择器
>     * $("#id")
>   * class选择器
>     * $(".class")
>   * 元素选择器
>     * $("元素名")
>   * 通配符选择器
>     * $("*")
>
> * 代码实现
>
>   ```js
>   	<script>
>   		//选择id为one的元素  ID选择器
>   		function fn1(){
>   			$("#one").css("background-color","orange");
>   		}
>   		//选择class为mini的所有元素   类选择器
>   		function fn2(){
>   			$(".mini").css("background-color","pink");
>   		}
>   		//选择元素名是div的所有元素    标签选择器
>   		function fn3(){
>   			$("div").css("background-color","lightpink");
>   		}
>   		//选择所有的元素  通配符选择器
>   		function fn4(){
>   			$("*").css("background-color","pink")
>   		}
>   	</script>
>   ```
>
>   
>

### 06_jquery选择器之层次选择器

> * 层次选择器
>
>   * 从父子关系、兄弟关系来选择页面上节点
>
> * 分类
>
>   * $("a b")
>     * 获取节点a下的所有的节点b（包括孙子节点）
>   * $("a > b")
>     * 获取节点a下的所有的子节点b
>   * $("a + b")
>     * 获取节点a的下一个兄弟节点b
>   * $("a ~ b")
>     * 获取节点a的所有兄弟节点b
>
> * 代码实现
>
>   ```js
>   		//选择body内的所有div元素 $("a b")
>   		function fn1(){ 
>   		   $("body div").css("background-color","pink");
>   		}
>   		//在body内选择子元素是div的 $("a > b")
>   		function fn2(){
>   		   $("body > div").css("background-color","pink");
>   		}
>   		//选择所有id为one的下一个兄弟div元素  $("a + b")
>   		function fn3(){
>   		  $("#one + div").css("background-color","pink");
>   		}
>   		//选择id为two的元素后面的所有div兄弟元素  $("a ~ b")
>   		function fn4(){
>   			$("#one ~ div").css("background-color","pink");
>   		}
>   ```
>
>   
>

### 07_jquery选择器之基本过滤选择器

> * 基本过滤选择器
>
>   * 从位置的角度来对页面的标签进行过滤选择
>
> * 分类
>
>   * $("tagName:first"):
>     * 选择第一个tagName标签 
>   * $("tagName:last") :
>     * 选择最后一个tagName标签
>   * $("tagName:eq(2)"):
>     * 选择脚标为2的tagName标签 
>     * [注意：脚标从0开始。]()
>   * $("tagName:gt(2)"):
>     * 选择脚标大于2的tagName标签 
>   * $("tagName:lt(2)");
>     * 选择脚标小于2的tagName标签
>   * $("tagName:odd")
>     * 选择脚标为奇数的tagName标签
>   * $("tagName:even")
>     * 选择脚标为偶数的tagName标签
>
> * 代码实现
>
> ```js
> 		//选择第一个DIV元素
> 		function fn1(){
> 			$("div:first").css("background-color","pink");
> 		}
> 		//选择最后一个div元素
> 		function fn2(){
> 			$("div:last").css("background-color","pink");
> 		}
> 		//选择class不为one的所有div元素 $('dom:not(.one)')
> 		function fn3(){
> 			$("div:not(.one)").css("background-color","pink");
> 		}
> 		//选择索引值为偶数的div元素 even:偶数 odd:奇数
> 		function fn4(){
> 			$("div:even").css("background-color","pink");
> 		}
> 		//选择索引值为奇数的div元素
> 		function fn5(){
> 			$("div:odd").css("background-color","pink");
> 		}
> 		//选择索引值等于3的元素
> 		function fn6(){
> 			$("div:eq(3)").css("background-color","pink");
> 		}
> 		//选择索引值大于3的元素
> 		function fn7(){
> 			$("div:gt(3)").css("background-color","pink");
> 		}
> 		//选择索引值小于3的元素
> 		function fn8(){
> 			$("div:lt(3)").css("background-color","pink");
> 		}
> ```
>
> 
>



### 08_jquery选择器之内容过滤选择器

> * 概念
>
>   * 从内容来对页面的标签进行过滤选择
>
> * 分类
>
>   * $("tagName:contains('aaa')")
>     * 选中内容包含"aaa"的tagName元素
>   * $("tagName:empty")
>     * 选中没有任何内容的tagName元素
>   * $("tagName:has(.one)")
>     * tagName中是否包含一个class为one的子元素，如果有就选中tagName
>
> * 代码实现
>
>   ```js
>   		//选取含有文本"di"的div元素  $("tagName:contains('str')")
>   		function fn1(){
>   			$("div:contains('di')").css("background-color","pink");
>   		}
>   		//选取不包含子元素(或者文本元素)的div空元素. $("tagName:empty");
>   		function fn2(){
>   			$("div:empty").css("background-color","pink");
>   		}
>   		//选取含有class为mini元素 的div元素. $("tagName:has(.mini)")
>   		//1.选中的是DIV元素  2.子元素中的class值为mini
>   		function fn3(){
>   			$("div:has(.mini)").css("background-color","pink");
>   		}
>   ```
>
>   
>

### 09_jqeury选择器之属性过滤选择器

> * 概念
>
>   * 从属性的角度来对页面的标签进行过滤选择
>
> * 分类
>
>   * $("tagName[id]"):
>
>     * 选取含有属性id的tagName元素
>
>   * $("tagName[id='cc']"):
>
>     * 选取属性id值为"cc"的tagName元素
>
>   * $("tagName[id!='cc']"):
>
>     * 选取属性id值不为"cc"的tagName元素
>
>   * $("tagName[title^='cc']"):
>
>     * 选取属性id值以"cc"开头的tagName元素
>
>   * $("tagName[title$='cc']"):
>
>     * 选取属性id值以"cc"结束的tagName元素
>
>   * $("tagName[title*='cc']")
>
>     * 选取属性id值包含"cc"的tagName元素
>
>   * ```js
>    $("tagName[title*='cc'][name='ee'][id!='ff']");
>    ```
>
>     - 选取title属性包含"cc"，name属性值为"e"，id属性值不为"ff"的tagName
>
> * 代码实现
>
> ```js
> 		//选取含有属性title的div元素.  $("tagName[title]");
> 		function fn1(){
> 			$("div[title]").css("background-color","red");
> 		}
> 		//选取属性title值等于test的div元素. $("tagName[title='test']")
> 		function fn2(){
> 			$("div[title='test']").css("background-color","pink");
> 		}
> 		//选取属性title值不等于test的div元素. !=
> 		function fn3(){
> 			$("div[title!='test']").css("background-color","pink");
> 		}
> 		//选取属性title值以te开始 的div元素.  ^=
> 		function fn4(){
> 			$("div[title^='te']").css("background-color","pink");
> 		}
> 		//选取属性title值以est结束的div元素.  $=
> 		function fn5(){
> 			$("div[title$='est']").css("background-color","pink");
> 		}
> 		//选取属性title值含有es的div元素.     *=
> 		function fn6(){
> 			$("div[title*='es']").css("background-color","pink");
> 		}
> 		//组合属性选择器,首先选取有属性id的div元素，然后在结果中 选取属性title值 含有 es 的元素.
> 		function fn7(){
> 			$("div[id][title*='es']").css("background-color","pink");
> 		}
> ```
> 
> 
> 
> ```
>
> ```
> 
> ```

### 10_jquery选择器之子元素过滤选择器

> * 概念
>
>   * 从父子关系对标签进行过滤选择
>
> * 分类
>
>     * $("tagName :nth-child(2)"):
>         * tagName元素下的第二个子元素([脚标从1开始]())
>     * $("tagName :first-child"):
>         * tagName元素下的第一个子元素
>     * $("tagName :last-child"):
>         * tagName元素下的最后一个子元素 
>     * $("tagName :only-child"):
>         * tagName元素下的仅仅只有一个子元素,那么选中这个子元素
>
>     [注意：冒号之前必须要加空格！]()
>
>     
>
> * 代码实现
>
>  ```js
>  		//选取class为one的div下的第2个子元素  
>  		function fn1(){
>  			$("div[class='one'] :nth-child(2)").css("background-color","pink");
>  		}
>  		//选取class为one的div下的第1个子元素
>  		function fn2(){
>  			// $("div[class='one'] :nth-child(1)").css("background-color","pink");
>  			$("div[class='one'] :first-child").css("background-color","pink");
>  		}
>  		//选取每个父元素下的最后一个子元素
>  		function fn3(){
>  			$("div :last-child").css("background-color","pink");
>  		}
>  		//如果父元素下的仅仅只有一个子元素,那么选中这个子元素  
>  		function fn4(){
>  			$("div :only-child").css("background-color","pink");
>  		}
>  ```
>
>  
>

### 11_jquery的dom操作

* > 常用方法
  > * html()
  >   * 设置/获取标签[内容]()，解析html标签，相当于innerHTML
  > * text()
  >   * 设置/获取标签[内容]()，不解析html标签，相当于innerText
  > * val()
  >   * 设置/获取[value属性]()值，相当于value属性
  > * attr()
  >   * 设置/获取[属性]()值，相当于setAttribute/getAttribute
  > * removeAttr()
  >   * 移除[属性]()，相当于removeAttribute

* 代码实现

  ```js
  <head>
      <title>jquery的dom操作</title>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <%--
          * html() : 设置/获取标签内容，解析html标签，相当于innerHTML
          * text() : 设置/获取标签内容，不解析html标签，相当于innerText
          * val()  : 获取value属性值，相当于value属性
          * attr() : 设置属性值，相当于setAttribute
          * removeAttr() : 移除属性值，相当于removeAttribute方法
      --%>
      <script>
  
          function fn1() {
              $("#div1").html("<font color='red'>这是红的!</font>")
          }
  
          function fn2() {
              $("#div1").text("<font color='red'>这是红的!</font>")
          }
  
          function fn3() {
              // $("#username").val("设置你");
              console.log($("#username").val())
          }
  
          function fn4() {
              $("#div1").attr("class","bbbb");
              console.log($("#div1").attr("class"));
          }
  
          function fn5() {
              $("#div1").removeAttr("class");
              console.log($("#div1").attr("class"));
          }
      </script>
  
  </head>
  <body>
  
      <div id="div1" class="aaaa">
          这是一个div
      </div>
  
      <input type="text" id="username"/>
  
      <button onclick="fn1()">html()</button>
      <button onclick="fn2()">text()</button>
      <button onclick="fn3()">val()</button>
      <button onclick="fn4()">attr()</button>
      <button onclick="fn5()">removeAttr()</button>
  </body>
  ```


### 12_jquery练习

* > 需求
>
  > * 获取第2个li节点的title属性 
  > * 获取第2个li节点的文本内容

* 代码实现

  ```html
  <head>
      <title>jquery练习</title>
      <script src=""></script>
      <%--
      获取第2个li节点的title属性
      获取第2个li节点的文本内容
      --%>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <script>
  
          /**
           * 获取第2个li节点的title属性
           */
          function fn1() {
              //基本过滤选择器 : 从位置的角度
              var title = $("li:eq(1)").attr("title");
              console.log(title);
          }
  
          function fn2() {
              //子元素过滤选择器：从子元素的角度
              var title = $("ul :nth-child(2)").attr("title");
              console.log(title);
          }
  
          /**
           * 获取第2个li节点的文本内容
           */
          function fn3() {
              //val():获取value属性
              var title = $("li:eq(1)");
              var content = title.html();
              console.log(content);
  
          }
  
      </script>
  </head>
  <body>
      <ul>
          <li title='苹果11'>苹果</li>
          <li title='橘子22'>橘子</li>
          <li title='菠萝33'>菠萝</li>
      </ul>
  
      <button onclick="fn1()">获取1</button>
      <button onclick="fn2()">获取2</button>
      <button onclick="fn3()">获取3</button>
  </body>
  ```

  

### 13_jquery事件

> * 概念
>
>   * jQuery 事件处理函数是 jQuery 中的核心函数。
>
> * 语法
>
>   * jquery对象.事件函数
>
> * 代码实现
>
>   ```html
>   <head>
>       <title>js中处理事件</title>
>       <script src="js/jquery-3.2.1.min.js"></script>
>       <script>
>   
>           //js方式一
>           function fn1() {
>               console.log("点击111")
>           }
>   
>           
>           window.onload = function () {
>               //js方式二：js的dom分配
>               var ele = document.getElementById("btn1");
>               ele.onclick  = function () {
>                   console.log("点击222")
>               }
>   
>   			//jquery方式
>               $("#btn2").click(function () {
>                   console.log("点击333")
>               });
>           }
>   
>   
>   
>   
>       </script>
>   </head>
>   <body>
>       <button onclick="fn1()">点击1</button>
>       <button id="btn1">点击2</button>
>       <button id="btn2">点击3</button>
>   </body>
>   ```
>
>   
>



### 14_jquery事件之监听页面加载完成

* 代码实现

  * js方式

  ```js
  window.onload = function () {
      console.log("页面加载完成1");
  }
  ```

  * jquery方式完整版

  ```js
  $(document).ready(function () {
      console.log("页面加载完成2")
  })
  ```

  * jquery方式简化版

  ```js
  $(function () {
      console.log("页面加载完成3")
  })
  ```





### 15_jquery事件之事件绑定

* 事件绑定方式分类

  * 方式一

    ```js
    jquery对象.事件名(function(){
        
        
    });
    ```

  * 方式二

    ```js
    jquery对象.bind("事件名",function(){
        
        
    });
    ```

* 代码实现

  ```html
  <head>
      <title>jquery事件绑定</title>
      <script src="js/jquery-3.2.1.min.js"></script>
      <script>
  
          $(function () {//监听页面加载完成
  
              //jquery事件绑定方式一
              $("#btn").click(function () {
                  console.log("点击111")
              });
  
              //jquery事件绑定方式二
              //第一个参数：绑定的事件名
              //第二个参数：监听器
              $("#btn2").bind("click",function () {
                  console.log("点击222")
              })
  
          })
  
  
  
  
      </script>
  </head>
  <body>
  
      <button id="btn" >点击1</button>
  
      <button id="btn2" >点击2</button>
  
  </body>
  ```

  

### 16_jquery事件练习

> * 需求：
>
>   * 输入框获取焦点时,输入框内容置为空;
>   * 失去焦点时,输入内容设置为"请输入用户名"
>
> * 开发流程
>
>   * 输入框获取焦点时，只有当输入内容为“请输入用户名”，才需要将输入内容置为空
>   * 输入框失去焦点时，只有当输入内容为空，才需要将输入内容置为“请输入用户名”
>
> * 代码实现
>
>   ```html
>   <head>
>       <title>jquery事件练习</title>
>   
>       <script src="js/jquery-3.2.1.min.js"></script>
>   
>       <script>
>   
>           $(function () {
>               $("#username").focus(function () {//监听获取焦点
>                   console.log("获取焦点");
>                   //只有当value=”请输入用户名“
>                   if ($("#username").val() == "请输入用户名") {
>                       $("#username").val("");
>                   }
>               });
>   
>               $("#username").blur(function () {//监听失去焦点
>                   console.log("失去焦点")
>                   if ($("#username").val() == "") {
>                       $("#username").val("请输入用户名");
>                   }
>   
>               });
>           })
>   
>   
>       </script>
>   
>   </head>
>   <body>
>   
>   
>   <input type="text" id="username" value="请输入用户名"/>
>   
>   </body>
>   ```
>
>   
>

### 17_jquery的遍历

* jquery遍历语法

  * 方式一
    * 内置对象this：当前元素对象，是一个js对象

  ```js
  jquery数组对象.each(function(index,element){
      
      
  });
  ```

  * 方式二
    * 内置对象this：当前元素对象，是一个js对象

  ```js
  $.each(jquery数组对象,function(index,element){
      
      
  });
  ```

  

* javascript遍历

  ```js
  function fn1() {
      var lis = document.getElementsByTagName("li");
  
      for (var i = 0; i < lis.length; i++) {
          var li = lis[i];
          console.log(li.innerHTML);
      }
  
  }
  ```

* jquery遍历

  * 方式一

    ```js
    //jquery方式一
    function fn2() {
        var lis = $("ul > li");
        lis.each(function (index,element) {
            //index:当前元素的脚标
            //element:当前元素(js对象)
            console.log("index : " + index);
            console.log("text : " + element.innerHTML);
            console.log("text : " + $(element).html());
        });
    }
    
    //jquery方式一
    function fn3() {
        var lis = $("ul > li");
        lis.each(function (index) {
            console.log("index : " + index);
            //this:内置对象,js对象，当前元素
            console.log(this.innerHTML);
            console.log($(this).html());
        })
    }
    ```

  * 方式二

    ```js
    //jquery方式二
            function fn4() {
                var lis = $("ul > li");
                $.each(lis,function (index,element) {
                    console.log(index);
                    console.log(element.innerHTML);
                    console.log(this.innerHTML);
                })
            }
    ```

    

### 18_jquery的异步请求

* 概念
  * jQuery 提供了供 AJAX 开发的丰富函数（方法）库。
  * 通过 jQuery AJAX，使用 HTTP Get 和 HTTP Post，您都可以从远程服务器请求 TXT、HTML、XML 或 JSON。
* 分类
  * $.ajax(options)
    * 把远程数据加载到 XMLHttpRequest 对象中
  * $.get(url,data,callback,type)
    * 使用 HTTP GET 来加载远程数据
  * $.post(url,data,callback,type)
    * 使用 HTTP POST 来加载远程数据





### 19_jquery异步请求之get

> * $.get(url,data,callback,type)
>
>   * url
>     * 请求服务器资源的路径
>   * data
>     * 请求参数，遵守json格式(键值对)
>   * callback
>     * 请求成功后，回调的函数
>   * type
>     * 服务器响应给浏览器的数据类型(html,xml,json,jasonp,script,text)
>
> * 代码实现
>
>   * Demo01Servlet.java
>
>   ```java
>   @WebServlet(name = "Demo01Servlet" ,urlPatterns = "/demo01")
>   public class Demo01Servlet extends HttpServlet {
>       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>           String username = request.getParameter("username");
>           String password = request.getParameter("password");
>           String msg = "登录成功";
>           boolean flag = true;
>           if (username.equals("root") && password.equals("root123")) {
>                msg = "登录成功";
>                flag = true;
>           } else {
>               msg = "登录失败";
>               flag = false;
>           }
>           Map<String,Object> map = new HashMap<>();
>           map.put("msg",msg);
>           map.put("flag",flag);
>   
>           ObjectMapper objectMapper = new ObjectMapper();
>           String jsonStr = objectMapper.writeValueAsString(map);
>           //服务器告诉浏览器，响应正文是json字符串，浏览器应该以utf-8对响应正文进行解码
>           response.setContentType("json/application;charset=utf-8");
>           response.getWriter().write(jsonStr);
>   
>       }
>   
>       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>           doPost(request,response);
>       }
>   }
>   ```
>
>   * $.get(url,data,callback,type)
>
>   ```html
>   <head>
>       <title>jquery异步请求之get</title>
>       <script src="js/jquery-3.2.1.min.js"></script>
>       <script>
>   
>           function fn1() {
>               //$.get(url,data,callback,type);
>               var url = "${pageContext.request.contextPath}/demo01";
>               var data = {"username": "root", "password": "root1234"};
>               var callback = function (data) {//data:服务器的响应正文
>                   //猜测data是json字符串，data就是js对象!
>                   //type=json,get方法内部就会自动将服务器返回的json字符串解析成js对象
>                   console.log(data.flag);
>                   console.log(data.msg);
>                   // var jsObj = eval("("+data+")");
>                   // console.log(jsObj.msg)
>               };
>               var type = "json";
>               $.get(url, data, callback, type);
>           }
>   
>           function fn2() {
>               $.get("${pageContext.request.contextPath}/demo01", {
>                   "username": "root",
>                   "password": "root1234"
>               }, function (data) {
>                   console.log(data.flag);
>                   console.log(data.msg);
>               }, "json");
>           }
>   
>       </script>
>   </head>
>   <body>
>   
>       <button onclick="fn1()">get请求1</button>
>       <button onclick="fn2()">get请求2</button>
>   
>   </body>
>   ```
>
>   
>



### 20_jquery异步请求之post

* > $.post(url,data,callback,type)
>
  > * url
  >   * 请求服务器资源的路径
  > * data
  >   * 请求参数，遵守json格式（键值对）
  > * callback
  >   * 请求成功后，回调的函数
  > * type
  >   * 服务器响应给浏览器的数据类型(html,xml,json,jasonp,script,text)

* 代码实现

  * $.post(url,data,callback,type)

  ```html
  <head>
      <title>jquery异步请求之post</title>
      <script src="js/jquery-3.2.1.min.js"></script>
      <script>
  
          function fn1() {
              //$.post(url,data,callback,type);
              $.post("${pageContext.request.contextPath}/demo02",{
                  "username":"root",
                  "password":"root123"
              },function (data) {
                  console.log(data);
              },"json");
  
          }
  
      </script>
  </head>
  <body>
  
  <button onclick="fn1()">post请求</button>
  
  </body>
  ```

  * Demo02Servlet.java

  ```java
  @WebServlet(name = "Demo02Servlet" ,urlPatterns = "/demo02")
  public class Demo02Servlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          String username = request.getParameter("username");
          String password = request.getParameter("password");
          String msg = "登录成功";
          boolean flag = true;
          if (username.equals("root") && password.equals("root123")) {
               msg = "登录成功";
               flag = true;
          } else {
              msg = "登录失败";
              flag = false;
          }
          Map<String,Object> map = new HashMap<>();
          map.put("msg",msg);
          map.put("flag",flag);
  
          JsonUtils.writeJsonStr(response,map);
  
      }
  
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request,response);
      }
  }
  ```

  * JsonUtils.java
    * 将java对象转换成json字符串
    * 将json字符串响应到浏览器

  ```java
  /**
   * json工具类
   * @author qiuzhiwei
   */
  public class JsonUtils {
  
      /**
       * 将java对象转换成json字符串
       * @param object
       * @return
       * @throws Exception
       */
      public static String toJsonStr(Object object) throws Exception {
          return new ObjectMapper().writeValueAsString(object);
      }
  
      /**
       * 将java对象转换为json字符串，并将json字符串响应到浏览器
       * @param response : 响应对象
       * @param object : java对象
       */
      public static void writeJsonStr(HttpServletResponse response , Object object){
          response.setContentType("json/application;charset=utf-8");
          try {
              String jsonStr = toJsonStr(object);
              response.getWriter().write(jsonStr);
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
  
  
  }
  ```

  



### 21_jquery异步请求之ajax

> * 概念
>
>   * *$.ajax(options)* 是低层级 AJAX 函数的语法。
>   * $.ajax 提供了比高层级函数更多的功能，但是同时也更难使用。
>   * option 参数设置的是 name|value 对，定义 url 数据、密码、数据类型、过滤器、字符集、超时以及错误函数。
>
> * 属性
>
>   * async
>     * 设置是否为异步请求
>   * contentType
>     * 设置请求头Content-Type，默认值：”application/x-www-form-urlencoded“
>   * data
>     * 请求参数
>   * dataType
>     * 响应正文的数据类型(html,xml,json,jasonp,script,text)
>   * complete(XHR, TS)
>     * 请求完成的回调函数
>   * error
>     * 请求失败的回调函数
>   * success
>     * 请求成功的回调函数
>   * timeout
>     * 设置请求延迟时间
>   * type
>     * 请求方式(Get/Post)
>   * url
>     * 请求路径
>   * xhr
>     * 获取异步请求对象
>
> * 常用属性
>
>   * data、dataType、success、type、url
>
> * 代码实现
>
>   ```html
>   <head>
>       <title>jquery异步请求之ajax</title>
>   
>   
>       <script src="js/jquery-3.2.1.min.js"></script>
>       <script>
>   
>           function fn1() {
>   
>   
>               $.ajax({
>                   type:"post",
>                   url:"${pageContext.request.contextPath}/demo02",
>                   data:{
>                       "username" :"root",
>                       "password" :"root123"
>                   },
>                   success:function (data) {
>                       console.log(data.flag);
>                       console.log(data.msg);
>                   },
>                   dataType:"json",
>               });
>           }
>   
>   
>       </script>
>   </head>
>   <body>
>   <button onclick="fn1()">ajax请求</button>
>   
>   </body>
>   </html>
>   ```
>
>   
>

### 22_jquery异步请求之校验用户名是否存在

* 需求：
  
  * 验证用户名是否存在，并给出合适的提示！
* 代码实现

  * regist.jsp

  ```html
  <head>
      <title>用户注册</title>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <script>
  
          function checkUsername() {
              var username = $("#username").val();
              console.log(username);
              $.post("${pageContext.request.contextPath}/checkUsername",{
                  "username":username,
              },function (data) {
                  console.log(data);
                  var flag = data.flag;
                  var msg = data.msg;
                  var btn = $("button[type='submit']");
                  if (flag) {
                      //用户名可用
                      $("#span").html("<font color='#1e90ff'>"+msg+"</font>");
                      //让按钮可以点击
                      btn.attr("disabled",false);
                  } else {
                      //用户名存在
                      $("#span").html("<font color='red'>"+msg+"</font>");
                      //禁用按钮
                      btn.attr("disabled",true);
  
                  }
              },"json");
          }
  
  
      </script>
  </head>
  <body>
  
  <form action="${pageContext.request.contextPath}/regist" method="post">
  
      账户:<input type="text" name="username" id="username" onchange="checkUsername()"/><span id="span"></span><br>
      密码:<input type="text" name="password"/><br>
      <button type="submit"  >注册</button>
  
  </form>
  
  
  </body>
  ```

  * CheckUsernameServlet.java

  ```java
  request.setCharacterEncoding("utf-8");
  String username = request.getParameter("username");
  UserService userService = new UserServiceImpl();
  try {
      boolean flag = userService.checkUsername(username);
      String msg = flag ? "用户名可用" : "用户名存在";
      Map<String,Object> map = new HashMap<>();
      map.put("flag",flag);
      map.put("msg",msg);
      //将map转换成json字符串，并将对应json字符串响应到浏览器
      JsonUtils.writeJsonStr(response,map);
  } catch (Exception e) {
      e.printStackTrace();
  }
  ```

  * UserService.java

  ```java
  public class UserServiceImpl implements UserService {
  
      private UserDao userDao = new UserDaoImpl();
  
  
      @Override
      public boolean checkUsername(String username) throws Exception {
  
          User existUser = userDao.checkUsername(username);
          if (null != existUser) {
              //用户名已存在
              return false;
          } else {
              //用户名可用
              return true;
          }
      }
  
  
  }
  ```

  * UserDao.java

  ```java
  public class UserDaoImpl implements UserDao {
      @Override
      public User checkUsername(String username) throws Exception {
  
          return new QueryRunner(JDBCUtils.getDataSource())
                  .query("select * from tb_user where username = ?",
                          new BeanHandler<User>(User.class),
                          username);
  
      }
  }
  ```

  