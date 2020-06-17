# Js、Json、Ajax

### 01_JavaScript的概述

> * 概念
>   * JavaScript是一门脚本语言
>   * 脚本语言
>     * 不需要编译，直接就可以被浏览器解析执行.
> * 发展史
>   * 1992年，第一门脚本语言：ScriptEase，专门用于表单校验
>   * 1995年，Netscape(网景)公司开发了一门脚本语言：LiveScript，后面更名为JavaScript
>   * 1996年，微软抄袭JavaScript，开发出JScript
>   * .1997年，ECMA组织，指定了脚本语言规范：ECMAScript
> * JavaScript组成
>   * 由ECMAScript、BOM、DOM组成
>





### 02_ECMAScript和页面结合

> * 概念
>
>   * JavaScript是一门脚本，要起作用，必须结合页面使用
>
> * 分类
>
>   * 内部结合
>     * 直接在页面文件中编写script标签，将js代码编写到script标签内容中
>   * 外部结合
>     * 在页面文件中使用script标签的src属性引入外部的js文件
>
> * 代码实现
>
>   * 内部结合
>
>   ```jsp
>   <head>
>       <title>ECMAScript和页面结合之内部结合</title>
>       <%--js脚本内部结合--%>
>       <script>
>           //打印语句
>           console.log("js脚本")
>       </script>
>   </head>
>   <body>
>   hello javascript
>   </body>
>   ```
>
>   * 外部结合
>
>     * myjs.js
>
>     ```javascript
>     console.log("js脚本")
>     ```
>
>     * demo02.jsp
>
>     ```jsp
>     <head>
>         <title>ECMAScript和页面结合之外部结合</title>
>         <script src="${pageContext.request.contextPath}/myjs.js"></script>
>     </head>
>     <body>
>     
>     </body>
>     ```
>
> * 注意事项
>
>   * js脚本放置的位置会决定它的执行顺序！
>



### 03_ECMAScript之注释

> * 概念
>
>   * 用来注释js脚本代码，给开发人员看的，浏览器不会解析执行
>
> * 分类
>
>   * 单行注释
>
>     ```javascript
>     //注释内容
>     ```
>
>   * 多行注释
>
>     ```javascript
>     /*注释内容*/
>     ```
>
>     
>

### 04_ECMAScript之数据类型

* > 分类
  > * 原始数据类型
  >   * Number
  >     * 整数、小数、NaN(not a number)
  >   * string
  >     * 字符串("abc"、'abc')
  >   * boolean
  >     * true、false
  >   * null
  >     * 空对象
  >   * undefined
  >     * 定义一个变量，但是没有赋初值
  > * 引用数据类型
  >   * js对象





###  05_ECMAScript之变量

> * 概念
>   * 提高复用性，提高可维护性！
> * java是强类型语言，JavaScript是弱类型语言
>   * 强类型语言
>     * 在定义变量时，要确定数据类型，在赋值时，只能赋值指定类型的数据
>   * 弱类型语言
>     * 在定义变量时，不确定数据类型，在赋值时，赋值多种类型的数据
> * 格式
>   * var 变量名 = 值;
>





### 06_ECMAScript之typeof方法

> * typeof方法
>
>   * 查看数据的类型
>
> * 用法
>
>   ```javascript
>   typeof(值)
>   ```
>
> * 代码实现
>
>   ```javascript
>           var num = 1;
>           console.log(typeof(num));//number
>           var str = "abc";
>           console.log(typeof(str));//string
>           var flag = true;
>           console.log(typeof(flag));//boolean
>           var obj = null;
>           console.log(typeof(obj));//Object
>           var num1 ;
>           console.log(typeof(num1));//undefined
>           var num2 = NaN;
>           console.log(typeof num2);//number
>   ```
>
>   
>



### 07_ECMAScript运算

> * 一元运算符
>
>   * ++，-- ， +
>
>   ```javascript
>           var num2 = ++num1;
>           console.log(num1);//2
>           console.log(num2);
>   ```
>
>   
>
> * 算术运算符
>
>   * \+ ‐ * / %
>
>   ```
>    		var num3 = 10;
>           var num4 = "2";
>           console.log(num3 / num4)
>   ```
>
>   
>
> * 赋值运算符
>
>   * = += ‐+
>
>   ```javascript
>    		var num5 = 1;
>           var num6 = 1;
>           //将等号左边的和右边的进行相加，将结果赋值给等号左边的!
>           num5 += num6;
>           console.log(num5);
>   ```
>
>   
>
> * 比较运算符
>
>   * \> < >= <= == ===(全等于)
>
>   ```javascript
>           //== : 比较值
>           var num7 = 10;
>           var num8 = "10";
>           console.log(num7 == num8);
>           //=== : 既要比较值，也要比较类型
>           console.log(num7 === num8);
>   ```
>
>   
>
> * 逻辑运算符
>
>   * && || !
>
>   ```javascript
>           var flag1 = true;
>           console.log(!flag1)
>           console.log(!0)//true
>           console.log(!NaN)//true
>           console.log(!"")//true
>           console.log(!null)//true
>           console.log(!undefined)//true
>   ```
>
>   
>
> * 三元运算符
>
>   ```javascript
>   var flag = true;
>           console.log(flag ? "为true":"为false")
>   ```
>
>   
>
> * 流程控制语句
>
>   * if...else...
>   *  switch: 
>     * 在java中，switch语句可以接受的数据类型： byte int shor char,枚举(1.5) ,String(1.7) 在JS中,switch语句可以接受任意的原始数据类型 
>   * while 
>   * do...while 
>   * for 
>
>   ```javascript
>           switch (true) {
>               case true:
>                   console.log(true)
>                   break;
>               case false:
>                   console.log(true)
>                   break;
>           }
>   
>           for (var i = 0; i < 10; i++) {
>               console.log(i)
>           }
>   ```
>
>   
>



### 08_ECMAScript基本对象

* > ECMAScript内置对象
  >
  > * Function、Array、Boolean、Date、Number、String、RegExp、Global(全局函数对象)



### 09_ECMAScript基本对象之Function对象（了解）

> * 概述
>
>   * 创建方法
>
> * 格式
>
>   ```javascript
>   var 方法名 = new Function("形式参数列表","方法体");
>   ```
>
> * 注意事项
>
>   * 不需要返回值类型
>   * 形参不需要参数类型
>   * 如果方法定义了形参，调用时，可以不传递实际参数！
>





### 10_ECMAScript之Array对象

> * 概念
>
>   * Array 对象用于在单个的变量中存储多个值。
>
> * 创建
>
>   ```
>   var arr1 = new Array("a","b","c");
>   var arr2 = ["a","b","c"];
>   ```
>
> * 常用属性
>
>   * length
>
> * 常用方法
>
>   * join
>     * 用于把数组中的所有元素放入一个字符串。
>   * pop
>     * 用于删除并返回数组的最后一个元素。
>   * push
>     * 可向数组的末尾添加一个或多个元素，并返回新的长度。
>





### 11_ECMAScript之Date对象

> * 概念
>   * Date 对象用于处理日期和时间。
> * 常用方法
>   * toLocaleString
>     * 获取本地的当前时间
>   * getFullYear
>     * 获取年份
>   * genMonth
>     * 获取月份，范围：0~11
>   * getDate
>     * 获取天
>   * getHours
>     * 获取小时
>   * getMinutes
>     * 获取分钟
>   * getSeconds
>     * 获取秒钟
>   * getTime
>     * 获取对应的毫秒值
>



### 12_ECMAScript之RegExp对象

> * 概念
>
>   * RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具。
>
> * 创建
>
>   ```javascript
>   var reg = /^正则表达式$/
>   ```
>
> * 代码实现
>
>   ```javascript
>   var reg1 = /^[a]{3}$/;
>   console.log(reg1.test("aaaa"));
>   ```
>
>   
>



### 13_ECMAScript之全局对象

> * 概念
>
>   * 全局属性和函数可用于所有内建的 JavaScript 对象。
>
> * 常用方法
>
>   * parseInt
>     * 将数字字符串转换成数字
>   * isNaN
>     * 判断变量是否是一个NaN
>   * eval
>     * 将json字符串转换成js对象，方便调用属性
>
> * 代码实现
>
>   ```javascript
>           //parseInt
>           var num1 = 1;
>           var num2 = "1";
>           console.log(num1 + parseInt(num2));
>           console.log("--------------------")
>           
>   		//isNaN:判断一个变量是否是NaN
>           //NaN走出了六亲不认的步伐！！！
>           var num3 = NaN;
>           console.log(num3 == NaN);//false
>           console.log(num3 === NaN);//false
>           console.log(isNaN(num3));//true
>           console.log("--------------------")
>           
>   		//eval：计算json字符串，返回js对象
>           var jsonStr = '{"username":"root","password":"root"}';
>           //能够通过上述的json字符串直接调用username属性和password属性?
>           //不能!需要将json字符串转换成js对象，就可以了!
>           var jsObject = eval("("+jsonStr+")");
>           console.log(jsObject.username + " , " + jsObject.password)
>   ```
>
>   
>



### 14_Json介绍

> * 概念
>
>   * JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。
>   * 它基于ECMAScript的 一个子集。 
>   * JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习 惯。这些特性使JSON成为理想的数据交换语言。 
>   * 易于人阅读和编写，同时也易于机器解析 和生成(网络传输速率)。
>
> * 语法
>
>   * 单一对象
>     * {"属性名1":"属性值1" , "属性名2":"属性值2"}
>   * 多个对象
>     * [{"属性名1":"属性值1" , "属性名2":"属性值2"} , {"属性名1":"属性值1" , "属性名2":"属性值2"}]
>
>   * 解释
>     * a.数据在键值对里面 
>     * b.数据之间由逗号分隔 
>     * c.大括号保存对象 
>     * d.中括号保存数组 
>     * e.Json值 
>       * 数字（整数或浮点数） 
>       * 字符串（在双引号中） 
>       * 逻辑值（true 或 false） 
>       * 数组（在中括号中） 
>       * 对象（在大括号中） 
>       * null
>



### 15_Java对象手动转换json字符串

* 代码实现

  * Province.java

  ```java
  public class Province {
  
      private Integer pId;
      private String pName;
      private List<City> cityList;
  
      public Province() {
      }
  
      public Province(Integer pId, String pName) {
          this.pId = pId;
          this.pName = pName;
      }
  
      @Override
      public String toString() {
          return "Province{" +
                  "pId=" + pId +
                  ", pName='" + pName + '\'' +
                  ", cityList=" + cityList +
                  '}';
      }
  
      public List<City> getCityList() {
          return cityList;
      }
  
      public void setCityList(List<City> cityList) {
          this.cityList = cityList;
      }
  
      public Province(Integer pId, String pName, List<City> cityList) {
          this.pId = pId;
          this.pName = pName;
          this.cityList = cityList;
      }
  
      public Integer getpId() {
      return pId;
      }

      public void setpId(Integer pId) {
          this.pId = pId;
      }
  
      public String getpName() {
          return pName;
      }
  
      public void setpName(String pName) {
          this.pName = pName;
      }
  
  }
  ```
  
  * 测试代码
  
  ```java
         //单一对象
          Province p1 = new Province(1,"湖北省");
          Province p2 = new Province(2,"湖南省");
          //p1 -> json字符串
          //pId=1、pName="湖北省"
          String jsonStr1 = "{'pId':1,'pName':'湖北省'}";
        String jsonStr2 = "{'pId':2,'pName':'湖南省'}";
          //一组对象 (单列集合、双列集合)
          //单列集合
          //Province
          List<Province> provinceList = new ArrayList<>();
          provinceList.add(p1);
          provinceList.add(p2);
          // provinceList -> json字符串
          String jsonStr3 = "[{'pId':1,'pName':'湖北省'},{'pId':2,'pName':'湖南省'}]";
          //双列集合
          //entry : 键值对对象
          Map<String,Province> map = new HashMap<>();
          map.put("p1",p1);
          map.put("p2",p2);
          //map -> json字符串
          String jsonStr4 = "{'p1':{'pId':1,'pName':'湖北省'},'p2':{'pId':2,'pName':'湖南省'}}";
  ```
  
  - City.java
  
  ```java
  public class City {
  
      private Integer cId;
      private String cName;
  
      public City() {
      }
  
      public City(Integer cId, String cName) {
          this.cId = cId;
          this.cName = cName;
      }
  
      public Integer getcId() {
          return cId;
      }
  
      public void setcId(Integer cId) {
          this.cId = cId;
      }
  
      public String getcName() {
          return cName;
      }
  
      public void setcName(String cName) {
          this.cName = cName;
      }
  
      @Override
      public String toString() {
          return "City{" +
                  "cId=" + cId +
                  ", cName='" + cName + '\'' +
                  '}';
      }
  }
  ```
  
  - 测试代码
  
  ```java
          Province p1 = new Province(1,"湖北省");
  
          List<City> cityList1 = new ArrayList<>();
          cityList1.add(new City(11,"武汉市"));
          cityList1.add(new City(12,"孝感市"));
          cityList1.add(new City(13,"襄阳市"));
  
          p1.setCityList(cityList1);
          //p1 -> json字符串
          String jsonStr1 = "{'pId':1,'pName':'湖北省','cityList':[{'cId':11,'cName':'武汉市'},{'cId':12,'cName':'孝感市'},{'cId':13,'cName':'襄阳市'}]}";
  
          Province p2 = new Province(2,"湖南省");
  
          List<City> cityList2 = new ArrayList<>();
          cityList2.add(new City(21,"长沙市"));
          cityList2.add(new City(22,"岳阳市"));
          cityList2.add(new City(23,"张家界市"));
  
          p2.setCityList(cityList2);
  
          List<Province> provinceList = new ArrayList<>();
          provinceList.add(p1);
          provinceList.add(p2);
  
          //provinceList -> json字符串
          String jsonStr2 = "[{'pId':1,'pName':'湖北省','cityList':[{'cId':11,'cName':'武汉市'},{'cId':12,'cName':'孝感市'},{'cId':13,'cName':'襄阳市'}]}," +
                  "{'pId':2,'pName':'湖南省','cityList':[{'cId':21,'cName':'长沙市'},{'cId':22,'cName':'岳阳市'},{'cId':23,'cName':'张家界市'}]}]";
  ```

### 16_jackson使用

> * 作用
>
>   * 将对象转换为json字符串
>   * 将json字符串转换为对象
>
> * 代码实现
>
>   * 将对象转换为json字符串(掌握)
>
>   ```java
>           //将java对象转换为json字符串
>           Province p1 = new Province(1,"湖北省");
>           List<City> cityList1 = new ArrayList<>();
>           cityList1.add(new City(11,"武汉市"));
>           cityList1.add(new City(12,"孝感市"));
>           cityList1.add(new City(13,"襄阳市"));
>           p1.setCityList(cityList1);
>           //p1 -> json字符串
>           ObjectMapper objectMapper = new ObjectMapper();
>           String jsonStr1 = objectMapper.writeValueAsString(p1);
>           System.out.println(jsonStr1);
>   
>           Province p2 = new Province(2,"湖南省");
>           List<City> cityList2 = new ArrayList<>();
>           cityList2.add(new City(21,"长沙市"));
>           cityList2.add(new City(22,"岳阳市"));
>           cityList2.add(new City(23,"张家界市"));
>           p2.setCityList(cityList2);
>   
>   
>           //provinceList -> json字符串
>           List<Province> provinceList = new ArrayList<>();
>           provinceList.add(p1);
>           provinceList.add(p2);
>           String jsonStr2 = objectMapper.writeValueAsString(provinceList);
>           System.out.println(jsonStr2);
>   
>           //map -> json字符串
>           Map<String,Province> map = new HashMap<>();
>           map.put("p1",p1);
>           map.put("p2",p2);
>           String jsonStr3 = objectMapper.writeValueAsString(map);
>           System.out.println(jsonStr3);
>   ```
>
>   * 将json字符串转换为对象(了解)
>
>   ```java
>           //jsonStr1 -> Province对象
>           Province province = objectMapper.readValue(jsonStr1, Province.class);
>           System.out.println(province);
>   
>           //jsonStr2 -> List对象
>           List<Province> list = objectMapper.readValue(jsonStr2, List.class);
>           System.out.println(list);
>   
>           //jsonStr3 -> Map对象
>           Map<String,Province> myMap = objectMapper.readValue(jsonStr3,Map.class);
>           System.out.println(myMap);
>   ```
>
>   
>



### 17_ajax的概述

> * 概述
>   * ajax：Asynchronous javascript and xml，异步JavaScript和Xml
> * 作用
>   * 局部刷新页面
>   * 发起异步请求
> * 和同步请求区别
>   * 同步请求：当一个页面中的内容发生改变时，需要全部刷新。当一个请求发起时，其他的请求不能发起
>   * 异步请求，当一个页面中的内容发生改变时，可以局部刷新。当一个请求发起时，其他的请求也能发起
>



### 18_XMLHttpRequest对象概述

> * 常用属性
>   * onreadstatechange
>     * 用于监听异步请求对象状态(readyState)改变
>   * status
>     * 服务器响应状态码
>   * readyState
>     * 异步请求对象的状态
>       * 0：异步请求对象还没有初始化完成
>       * 1：开始发起请求
>       * 2：发起请求完成
>       * 3：开始读取服务器的响应
>       * 4：读取服务器响应完成
>   * responseText
>     * 响应正文
> * 常用方法
>   * open(请求方式，请求路径，flag)
>     * flag：为true就是异步请求；否则为同步请求
>   * send
>     * 发送参数
>   * setRequestHeader
>     * 设置请求头
>





### 19_Ajax入门案例之get请求

> * 开发流程
>
>   * 创建异步请求对象
>   * 监听异步请求对象状态改变
>     * 判断服务器响应状态码为200
>     * 判断异步请求对象状态为4
>   * 打开连接
>     * 设置请求方式
>     * 设置请求路径
>     * 设置异步请求
>   * 发送参数
>
> * 代码实现
>
>   * 创建异步请求对象
>
>   ```js
>           function createXMLHttpRequest() {
>               var xmlHttp;
>               try { // Firefox, Opera 8.0+, Safari，Google
>                   xmlHttp = new XMLHttpRequest();
>               } catch (e) {
>                   try {// Internet Explorer
>                       xmlHttp = new ActiveXObject("Msxml2.XMLHTTP");
>                   } catch (e) {
>                       try {
>                           xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
>                       } catch (e) {
>   
>                       }
>                   }
>               }
>               return xmlHttp;
>           }
>   		var xhr = createXMLHttpRequest();
>   ```
>
>   * 监听异步请求对象状态改变
>     * 判断服务器响应状态码为200
>     * 判断异步请求对象状态为4
>
>   ```js
>   xhr.onreadystatechange = function () {
>               //当异步请求对象状态发生改变就会执行本方法
>               console.log("异步请求对象，状态发生改变" + xhr.readyState);
>               //主要是监听readyState属性改变
>               //判断请求是否成功？
>               //首先判断服务器响应状态码status,再判断异步请求对象是否读取服务器响应成功？readyState
>               if (xhr.status == 200 && xhr.readyState == 4) {
>                   //获取的服务器传输过来的json字符串
>                   var responseText =xhr.responseText;
>                   //将json字符串 -> js对象
>                   var jsObj = eval("("+responseText+")");
>                   console.log(jsObj.flag);
>                   console.log(jsObj.msg);
>               }
>   
>           }
>   ```
>
>   * 打开连接
>     * 设置请求方式
>     * 设置请求路径
>     * 设置异步请求
>
>   ```js
>   xhr.open("get","${pageContext.request.contextPath}/demo01?username=root&password=root",true);
>   ```
>
>   * 发送参数
>
>   ```js
>   xhr.send("");
>   ```
>
>   
>

### 20_Ajax入门案例之post请求

> * 开发流程
>
>   * 创建异步请求对象
>   * 监听异步请求对象状态改变
>     * 判断服务器响应状态码为200
>     * 判断异步请求对象状态为4
>   * 打开连接
>     * 设置请求方式
>     * 设置请求路径
>     * 设置异步请求
>   * 设置请求头Content-Type
>   * 发送参数
>
> * 代码实现
>
>   * 创建异步请求对象
>
>   ```js
>           function createXMLHttpRequest() {
>               var xmlHttp;
>               try { // Firefox, Opera 8.0+, Safari，Google
>                   xmlHttp = new XMLHttpRequest();
>               } catch (e) {
>                   try {// Internet Explorer
>                       xmlHttp = new ActiveXObject("Msxml2.XMLHTTP");
>                   } catch (e) {
>                       try {
>                           xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
>                       } catch (e) {
>   
>                       }
>                   }
>               }
>               return xmlHttp;
>           }
>   
>           //1,创建异步请求对象
>           var xhr = createXMLHttpRequest();
>   ```
>
>   * 监听异步请求对象状态改变
>     * 判断服务器响应状态码为200
>     * 判断异步请求对象状态为4
>
>   ```js
>           xhr.onreadystatechange = function () {
>               //当异步请求对象状态发生改变就会执行本方法
>               console.log("异步请求对象，状态发生改变" + xhr.readyState);
>               //主要是监听readyState属性改变
>               //判断请求是否成功？
>               //首先判断服务器响应状态码status,再判断异步请求对象是否读取服务器响应成功？readyState
>               if (xhr.status == 200 && xhr.readyState == 4) {
>                   //获取的服务器传输过来的json字符串
>                   var responseText =xhr.responseText;
>                   //将json字符串 -> js对象
>                   var jsObj = eval("("+responseText+")");
>                   console.log(jsObj.flag);
>                   console.log(jsObj.msg);
>                   var ele = document.getElementById("div");
>                   if (jsObj.flag) {
>                       //用户名可用
>                       ele.innerHTML = "<font color='blue'>"+jsObj.msg+"</font>";
>                   } else {
>                       //用户名不可用
>                       ele.innerHTML = "<font color='red'>"+jsObj.msg+"</font>";
>                   }
>               }
>   
>           }
>   ```
>
>   * 打开连接
>     * 设置请求方式
>     * 设置请求路径
>     * 设置异步请求
>
>   ```js
>   xhr.open("post","${pageContext.request.contextPath}/demo01",true);
>   ```
>
>   * 设置请求头
>
>   ```js
>   xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
>   ```
>
>   * 发送参数
>
>   ```js
>    xhr.send("username=root1&password=root");
>   ```
>
>   
>



### 21_ECMAScript之方法

> * 分类
>
>   * 方式一
>
>   ```js
>   function 方法名(形参列表) {
>   	方法体;
>   }
>   ```
>
>   * 方式二
>
>   ```js
>   var 方法名 = function(形参列表){
>       方法体;
>   }
>   ```
>
>   * 方式三
>
>   ```js
>   var 方法体 = new Function("形参列表","方法体");
>   ```
>
>   
>
> * 代码实现
>
>   * 方式一
>
>   ```js
>    function method01(msg1, msg2, msg3) {
>               // console.log(msg1 + " , " + msg2 + " , " + msg3);
>               //arguments:属于方法的内置对象,包含是实际参数
>               for (var i = 0; i < arguments.length; i++) {
>                   console.log(arguments[i]);
>               }
>               
>               return "hello js function1";
>           }
>   ```
>
>   * 方式二
>
>   ```js
>   var method02 = function (msg1, msg2, msg3) {
>               // console.log(msg1 + " , " + msg2 + " , " + msg3);
>               //arguments:属于方法的内置对象,包含是实际参数
>               for (var i = 0; i < arguments.length; i++) {
>                   console.log(arguments[i]);
>               }
>               return "hello js function2";
>           }
>   ```
>
>   * 方式三
>
>   ```js
>   var method03 = new Function("msg1,msg2,msg3", "console.log(msg1+','+msg2+','+msg3);return 'hello js function3';");
>   ```
>
> * 注意事项
>   
>   * 在方法中，有一个内置对象arguments，包含所有的实际参数
>





### 22_ECMAScript之事件

> * 概念
>
>   * 事件源：发生事件的源头
>   * 监听器：发生事件后触发的组件
>   * 事件绑定：将事件源和监听器关联
>   * 事件：能够触发监听器的事
>
> * 事件注册
>
>   * 使用标签中的事件属性
>
>   ```js
>   <button onclick="fn1()">按钮1</button>
>   <script>
>       // 2,监听器
>       function fn1() {
>           console.log("按钮1点击了~~~~")
>       }
>   </script>
>   ```
>
>   * 使用js的dom分配
>
>   ```js
>   <button id="btn">按钮2</button>
>   <script>
>   
>   
>       // 不推荐使用，有问题!!!
>       var fn2 = function () {
>           console.log("按钮2点击了~~~~")
>       }
>       ele.onclick = fn2;
>   
>   
>       ele.onclick = function () {
>           console.log("按钮2点击了~~~~");
>       };
>   
>   </script>
>   ```
>
>   
>



### 23_ECMAScript常用事件之onload

> * 概述
>
>   * 某个页面或图像被完成加载
>
> * 代码实现
>
>   * 监听图片加载完成
>
>   ```js
>   <img id="girl" src="girl01.jpg" onload="fn1()">
>   
>   <script>
>        function fn1() {
>           console.log("这是一个美女，我正在用~~~")
>       }
>   
>   </script>
>   ```
>
>   * 监听页面加载完成
>
>   ```js
>   <head>
>       <title>ECMAScript常用事件之onload</title>
>       <%--如果使用dom分配事件，推荐使用这种方式!!--%>
>       <script>
>           window.onload = function () {
>               console.log("页面加载完成");
>               var ele = document.getElementById("girl");
>               ele.onclick = function () {
>                   console.log("我正在疯狂地点击美女~~~")
>               }
>           }
>       </script>
>   </head>
>   <body>
>   
>   <img src="girl01.jpg" id="girl" >
>   
>   </body>
>   ```
>
>   

### 24_ECMAScript事件之onfocus、onblur

> * onfocus、onblur
>
>   * 监听元素获取焦点、失去焦点
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>ECMAScript事件之onfocus、onblur</title>
>       <%--
>           onfocus：监听获取焦点
>           onblur：监听失去焦点
>       --%>
>       <script>
>   
>           function fn1() {
>               console.log("1获取焦点");
>           }
>           function fn2() {
>               console.log("1失去焦点");
>           }
>   
>           function fn3() {
>               console.log("2获取焦点");
>           }
>           function fn4() {
>               console.log("2失去焦点");
>           }
>   
>       </script>
>   </head>
>   <body>
>   <input type="text" onfocus="fn1()" onblur="fn2()"/>
>   <input type="text" onfocus="fn3()" onblur="fn4()"/>
>   </body>
>   ```
>
>   
>

### 25_ECMAScript事件之onkeydown、onkeyup

> * onkeydown、onkeyup
>
>   * 监听键盘按下、键盘松开
>
> * 代码实现
>
>   * 内置一个事件对象event，通过event对象的属性keyCode可用获取按下的键值
>
>   ```js
>   <head>
>       <title>ECMAScript事件之onkeydown、onkeyup</title>
>   
>       <script>
>   
>           function fn1() {
>               console.log("键盘按下" + event.keyCode);
>           }
>   
>           function fn2() {
>               console.log("键盘松开" + event.keyCode);
>           }
>   
>       </script>
>   
>   </head>
>   <body>
>   
>   <input type="text" onkeydown="fn1()" onkeyup="fn2()"/>
>   
>   </body>
>   ```
>
>   
>

### 26_ECMAScript事件之onmousedown、onmousemove、onmouseup

> * onmousedown、onmousemove、onmouseup
>
>   * 监听鼠标按下、鼠标移动、鼠标松开
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>ECMAScript事件之onmousedown、onmousemove、onmouseup</title>
>       <script>
>           function fn1() {
>               console.log("鼠标按下");
>           }
>   
>           function fn2() {
>               console.log("鼠标移动");
>           }
>   
>           function fn3() {
>               console.log("鼠标松开");
>           }
>   
>   
>       </script>
>   
>   </head>
>   <body onmousedown="fn1()" onmousemove="fn2()" onmouseup="fn3()">
>   </body>
>   ```
>
>   
>



### 27_ECMAScript事件之onchange

> * onchange
>
>   * 用户改变域的内容
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>ECMAScript事件之onchange</title>
>       <script>
>           function fn1() {
>               console.log("内容发生改变")
>           }
>   
>           function fn2() {
>               console.log("内容发生改变2")
>           }
>       </script>
>   </head>
>   <body>
>   
>   <input type="text" onchange="fn1()"/>
>   
>   <select onchange="fn2()">
>       <option>选项一</option>
>       <option>选项二</option>
>   </select>
>   ```
>
>   
>

### 28_ECMAScript事件之onsubmit

> * onsubmit
>
>   * 监听表单提交
>
> * 代码实现
>
>   ```js
>   <head>
>       <title>ECMAScript事件之onsubmit</title>
>       <script>
>           /**
>            * 监听表单提交
>            * 拦截表单提交
>            */
>           function fn1() {
>               console.log("表单提交1");
>               var num = 2;
>               if (num == 1) {
>                   return true;//放行表单提交
>               } else {
>                   return false;//拦截表单提交
>               }
>   
>           }
>   
>   
>       </script>
>   </head>
>   <body>
>   
>   <form action="index.jsp" onsubmit="return fn1()">
>       账户:<input type="text" name="username"/>
>       <button type="submit">提交</button>
>   </form>
>   
>   </body>
>   ```