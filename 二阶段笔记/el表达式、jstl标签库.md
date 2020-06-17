# el表达式,jstl标签库

### 一、el表达式

#### 1.1.el表达式介绍

> 什么是el表达式？
>
> * el(expression language)，是由jsp内置提供
> * el表达式用来替换jsp脚本得

#### 1.2作用

> * 向页面输出数据
> * 获取web对象

#### 1.3格式

> ```jsp
> ${表达式}
> ```

[注意：如果page指令中isELIgnored="true"，jsp页面就不会解析执行el表达式，会原样显示！！！]()

### 二、el获取域数据基本使用

> - El表达式怎样获取域中数据
>
>   ​		page域 	
>
> ```jsp
> ${pageScope.name}	
> ```
>
> ​				request域 
>
> ```jsp
> ${requestScope.name}
> ```
>
> ​				session域
>
> ```jsp
>  ${sessionScope.name}
> ```
>
> ​				application域 
>
> ```jsp
> ${applicationScope.name}
> ```
>
> [使用el表达式获取时，如果没有查找到结果，返回的不是null,而是一个""]()
>
> [使用${msg}没有指明域，那么就从pageScop->requestScop->sessionScop->applicationScop中依次查找]()

#### 2.1获取page域数据

```jsp
<%
pageContext.setAttribute("msg1","hello page1");
%>

${pageScope.msg1}
```

#### 2.2获取request域数据

```jsp
<%
request.setAttribute("msg1","hello page1");
%>

${requestScope.msg1}
```

#### 2.3获取session域数据

```jsp
<%
session.setAttribute("msg1","hello page1");
%>

${sessionScope.msg1}
```

#### 2.4获取application域数据

```jsp
<%
application.setAttribute("msg1","hello page1");
%>

${applicationScope.msg1}
```

### 三、el获取复杂域数据

#### 3.1获取数组

```jsp
<body>
<%
    //数组静态初始化，并存储到pageContext域中
    String[] msgs = {"张三","李四","王五"};
    pageContext.setAttribute("msgs",msgs);
%>
<%----jsp输出脚本获取------%>
<%=
    //先获取域对象，再转为数组，然后用下标取出
    ((String[])pageContext.getAttribute("msgs"))[0]
%>
<%-----el表达式获取-------%>
${pageScope.msgs[0]}
<%-----msgs不重名，会按照从小到大的域范围查询，因此可以直接写msgs[0]-------%>   
${msgs[0]}

</body>
```

#### 3.2获取List集合

```jsp
<body>
<%
    //创建集合，并存储到request域中
    List<String> list = new ArrayList<>();
    list.add("张三");
    list.add("李四");
    list.add("王五");
    request.setAttribute("msgs1",list);
%>
<%-----jsp输出脚本获取-------%>
<%=
    //先获取域对象，再转化为集合，然后用下标取出
    ((List<String>) request.getAttribute("msgs1")).get(0)
%>
<%-----el表达式获取集合对象,两种方法---------%>
${requestScope.msgs1.get(0)}
${msgs1[0]}
</body>
```

#### 3.3获取map集合

```jsp
<body>
<%
    //创建集合，并存储到session域中
    HashMap<String,Object> map = new HashMap<>();
    map.put("username","张三");
    map.put("age",16);
    session.setAttribute("map",map);
%>
<%-----jsp输出脚本获取-------%>
<%=
    //先获取域对象，再转化为map集合，然后用键取出
    ((HashMap<String,Object>)session.getAttribute("map")).get("username")
%>
<%-----el表达式获取集合对象,两种方法---------%>
${map.get("age")}
${map.age}
</body>
```

#### 3.4获取java对象

```java
<body>
<%
    //创建对象，并存储到application域中
    User user = new User();
    user.setId(1);
    user.setUsername("张三");
    user.setPassword("123456");
    application.setAttribute("user",user);
%>
<%-----jsp输出脚本获取-------%>
<%=
    //获取域对象，并转换为User对象，然后通过方法获取名字
    ((User)application.getAttribute("user")).getUsername()
%>
<%-----el表达式获取密码---------%>
${user.password}
</body>
```

### 四、el表达式执行运算

#### 4.1算术运算

> [+]()
> [-]()
> [*]()
> [/](/)	:div
> [%]()	:mod

```jsp
<body>

<%
    request.setAttribute("num1",100);
    request.setAttribute("num2",200);
%>
${num1 + num2}
${num2 div num1}
</body>
```

#### 4.2关系运算

> [>]() : gt
> [=]() : ge
> [<]() : lt
> [<=]() : le
> [==]() : eq
> [!=]() : ne
>
> gt:greater
> ge:greater equals
> lt:litter
> le:litter equals
> eq:equals
> ne:not equals

```jsp
<body>

<%
    request.setAttribute("num1",100);
    request.setAttribute("num2",200);
%>
${num1 > num2}
${num2 gt num1}
</body>
```



#### 4.3逻辑运算

> [&&]() : and
> [| |]() : or
> [!]()  : not

```jsp
<body>

<%
    request.setAttribute("flag1",true);
    request.setAttribute("flag2",false);
%>
${flag1 && flag2}
${flag1 || flag2}
</body>
```

#### 4.4三元运算

> ${num1 gt num2 ? "num1大于num2" : "num1不大于num2"}

### 五、el表达式中web对象

#### 5.1	11个web对象

> * pageScope
>
>   * 是page域对象
>
> * requestScope
>
>   * 是request域对象
>
> * sessionScope
>
>   * 是session域对象
>
> * applicationScope
>
>   * 是application域对象
>
> * param
>
>   * 相当于request.getParameter()
>
>   ```jsp
>   <body>
>   ${param.username}
>   ${param.password}
>   
>   </body>
>   ```
>
> * paramValues
>
>   * 相当于request.getParameterValues()
>
>   ```jsp
>   ${paramValues.username[0]}
>   ```
>
> * header
>
>   * 获取单个请求头值
>
> * headerValues
>
>   * 获取一组请求头的值
>
> * initParam
>
>   * 获取初始化参数
>
>   ```jsp
>   ${initParam.username}
>   ```
>
> * cookie
>
>   * Map<String,Cookie>，键是cookie名称，值是cookie对象
>
>   ```jsp
>   {cookie}
>   ```
>
> * pageContext
>
>   * 相当于pageContext对象，获取jsp九大内置对象

#### 5.2常用web对象

> * pageScope
> * requestScope
> * sessionScope
> * applicationScope
> * cookie
> * pageContext

#### 5.3应用场景

> 获取当前项目路径
>
> ```jsp
> ${pageContext.request.contextPath}
> ```

### 六、jstl标签库介绍

#### 6.1概述

> * jstl (java standard tag libarary)
> * 和el表达式结合使用，可以让功能更加强大！

#### 6.2环境准备

> - 导入jar包
>   - jstl.jar
>   - standard.jar

#### 6.3在jsp页面导入jstl标签库

> - 使用taglib指令
>
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8" language="java" %>
> <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
> <html>
> <head>
>     <title>jstl标签库环境准备</title>
> </head>
> <body>
> <%
>     int num = 1;
>     request.setAttribute("num",num);
> %>
> <c:if test="${num == 1}">
>     num等于1
> </c:if>
> <c:if test="${num != 1}">
>     num不等于1
> </c:if>
> 
> </body>
> </html>
> ```
>
> 

### 七、jstl核心标签

#### 7.1	set标签

> 向域对象(page域、request域、session域、application域)中存储数据
>
> * var：参数名称
> * scope：域
> * value：参数值

```jsp
<c:set var="msg" scope="request" value="hello jstl"></c:set>
${msg}
```

#### 7.2	remove标签

> 移除域对象中的数据
>
> * var：参数名称
> * scope：域

```jsp
<c:remove var="msg" scope="request"></c:remove>

${msg}<br>
```

#### 7.3	catch标签

> 捕获jsp页面的异常，相当于try...catch
>
> * var：声明异常对象名称，比如：var="e" ，变量e就可以接收异常对象

```jsp
<c:catch var="e">
    <%
        int num = 1 / 0;
    %>
</c:catch>
${e}<br>
```

#### 7.4	if标签

> 条件判断
>
> * test ：编写条件

```jsp
<c:set var="num" value="2" scope="request"></c:set>
<c:if test="${num == 1}">
    num 等于 1
</c:if>

<c:if test="${num != 1}">
    num 不等于 1
</c:if>
```

#### 7.5	forEach标签

> 遍历集合或数组
>
> * begin：开始
> * end：结束
> * step：步数
> * var：元素名称
> * items：集合/数组
> * varStatus：元素状态对象
>   * first：是否是第一个元素
>   * last：是否是最后一个元素
>   * current：当前元素
>   * index“：当前脚标

```jsp

<!-- 基本使用 -->
<c:forEach begin="1" end="10" step="3" var="num">
    ${num}
</c:forEach>

<%
    List<String> strs  = new ArrayList<>();
    strs.add("aaa");
    strs.add("bbb");
    strs.add("ccc");
    request.setAttribute("strs",strs);
%>
<!-- 相当于普通for循环 -->
<c:forEach begin="0" end="${strs.size() - 1}" step="1" var="i">
    ${strs[i]}
</c:forEach>

<!-- 相当于增强for循环 -->
<c:forEach var="str" items="${strs}" varStatus="status">
	${str}<br>
    ${status.current} -- ${status.index} -- ${status.first} -- ${status.last}<br>
</c:forEach>
```

#### 7.6	forToken标签

> 分割字符串
>
> * items：要分割的字符串
> * delims：分割的规则
> * var：分割产生的元素

```jsp
<%
    String msg1 = "aaa--bbb--ccc";
    request.setAttribute("msg1",msg1);
%>

<c:forTokens items="${msg1}" delims="--" var="sonMsg">
    ${sonMsg}
</c:forTokens>
```

### 八、jstl综合案例

#### 8.1准备工作

- 导入jar包
- ProductDao

```java
public class ProductDaoImpl implements ProductDao {
    @Override
    public List<Product> selectProductList() throws Exception {
        return new QueryRunner(JDBCUtils.getDataSource())
                .query("select * from tb_product",
                        new BeanListHandler<Product>(Product.class));
    }
 }
```

- ProductServlet

```java
@WebServlet(name = "ProductServlet" ,urlPatterns = "/selectProductList")
public class ProductServlet extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        ProductDao productDao = new ProductDaoImpl();
        try {
            List<Product> productList = productDao.selectProductList();
            System.out.println(productList);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```

#### 8.2jstl综合案例功能完成

代码实现

* productList.jsp

```jsp
<table border="1px" cellspacing="0px" cellpadding="10px" width="500px" height="200px">
    <tr>
        <td>ID</td>
        <td>名称</td>
        <td>单价</td>
        <td>数量</td>
        <td>小计</td>
    </tr>
    <%--循环之前，总价为0--%>
    <c:set var="total" value="0" scope="page"></c:set>
    <c:forEach items="${productList}" var="product">
        <%--forEach标签，循环一次就是一个小计!--%>
        <tr>
            <td>${product.id}</td>
            <td>${product.name}</td>
            <td>${product.price}</td>
            <td>${product.count}</td>
            <td>${product.price * product.count}</td>
        </tr>
        <c:set var="total" value="${total + product.price * product.count}" scope="page"></c:set>
    </c:forEach>
    <%--循环之后，计算出总价--%>
    <tr>
        <td colspan="5" align="right">
            总价：${total}元
        </td>
    </tr>

</table>
```

