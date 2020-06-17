# Jsp

### 1、Jsp介绍

#### 1.1	为什么要引入jsp?

> * html文件无法获取java程序中的数据，同时，如果使用Servlet来显示java数据又显得不太合理！
> * 综上，需要一门技术，既可以显示页面，同时也可以获取java程序中的数据

#### 1.2	什么是jsp

> * jsp：java server page
> * 简单理解为，它就是一个可以获取java数据的html文件。

### 2、jsp相关概念

#### 2.1	jsp为什么是一个Servlet

> * jsp文件会转义成对应的java文件
> * 比如：demo01.jsp转义成demo01_jsp.java，类demo01_jsp会继承于HttpJspPage，HttpJspPage又是Servlet子类，demo01.jsp就是Servlet

#### 2.2	jsp的执行流程

> * 浏览器发起请求demo01.jsp
> * demo01.jsp就会转义生成对应demo01_jsp.java
> * 在demo01_jsp类中，通过JspWriter类将demo01.jsp中的html标签作为响应正文响应给浏览器进行渲染显示！

### 3、jsp脚本

#### 3.1	作用

> 可以在页面上写java代码

#### 3.2	分类

> * 声明脚本：<%! java代码 %>
> * 片段脚本：<% java代码 %>
> * 输出脚本:：<%= 变量值 %>
>   * 声明脚本：<%! java代码 %>
>     * 在jsp对应java类中，生成一个成员变量
>   * 片段脚本：<% java代码 %>
>     * 在jsp对应的java类的_jspService方法中，生成一个局部变量
>   * 输出脚本:：<%= 变量值 %>
>     * 向浏览器输出内容，相当于response.getWriter().write()

### 4、jsp注释

#### 4.1	概念

> * jsp文件中，既可以有html代码，也可以有java代码
> * 这就意味着，jsp文件中，既可以使用html注释，也可以使用java注释，同时还可以使用jsp注释

#### 4.2	html注释

> ```html
> <!-- -->
> ```
>
> * 用来注释html代码
> * 会将注释内容生成到jsp对应的java文件中

#### 4.3	java注释

> ```java
> //
> ```
>
> * 用来注释java代码
> * 会将注释内容生成到jsp对应的java文件中

#### 4.4	jsp注释

> ```jsp
> <%--  --%>
> ```
>
> * 用来注释html代码
> * 不会讲注释内容生成到jsp对应的java文件中

### 5、jsp指令

#### 5.1	作用

> 用于指示jsp执行某些操作 、用于指示jsp表现特定行为或效果

#### 5.2	格式

> ```jsp
> <%@ 指令名称 属性名1="属性值1" 属性名2="属性值2" %>
> ```

#### 5.3	分类

> * page指令
> * taglib指令
> * include指令

### 6、include指令(了解)

#### 6.1	作用

> 用于将外部引入到jsp文件中

#### 6.2	基本使用

> ```jsp
> <%@ include file="top.jsp"%>
> ```

### 7、page指令

> ```jsp
> <%@ page import="java.util.List" %>
> <%@ page import="java.util.ArrayList" %>
> <%@ page contentType="text/html;charset=UTF-8" language="java" isELIgnored="false" errorPage="error.jsp" %>
> <%@ page isErrorPage="true" %>
> ```
>
> * contentType="text/html;charset=UTF-8"
>   * 告诉浏览器应该以utf-8解码响应正文，告诉服务器应该以utf-8对响应正文进行编码
> * language="java"
>   * 设置jsp页面能够使用的语言，不动！
> * import="java.util.List" 
>   * 在当前jsp页面中导入List类
> * isELIgnored="false"
>   * 当前jsp页面不要忽略el表达式，默认就是不忽略
> * errorPage="error.jsp"
>   * 当前jsp页面发生异常，所要跳转到页面
> * isErrorPage="true"
>   * 标记当前jsp页面是否是一个错误页面，如果为true那么就可以使用jsp内置对象exception，否则不能使用

### 8、taglib指令

#### 8.1	作用

> 在当前jsp页面中导入jstl标签库

#### 8.2	格式

> ```jsp
> <%@taglib prefix="前缀" uri="路径" %>
> ```

#### 8.3	应用场景

> * 导入jstl标签库
>
> ```jsp
> <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
> ```
>

### 9、jsp内置对象

#### 9.1	什么是jsp内置对象？

> * 可以在jsp页面上直接使用的对象
> * 九大内置对象

#### 9.2	分类

> * page
>   * 当前页面对象，java.lang.Object
> * pageContext
>   * 当前页面上下文对象，javax.servlet.jsp.PageContext
> * request
>   * 请求对象，javax.servlet.http.HttpServletRequest
> * response
>   * 响应对象，javax.servlet.http.HttpServletResponse
> * session
>   * 会话对象，javax.servlet.http.HttpSession
> * config
>   * ServletConfig对象，javax.servlet.ServletConfig
> * exception
>   * 异常对象，java.lang.Throwable
> * application
>   * ServletContext对象，javax.servlet.ServletContext
> * out
>   * JspWriter对象，javax.servlet.jsp.JspWriter

#### 9.3	为什么jsp可以直接使用内置对象

> 在jsp对应的java文件中，已经提前声明好了这些内置对象，所以可以直接使用。

#### 9.4	jsp九大内置的基本使用

> * 九大内置对象
>   * page(不用)
>   * pageContext
>   * request
>   * response
>   * session
>   * application
>   * config(不用)
>   * out
>   * exception
>
> * 基本使用
>   * request
>   * response
>   * session
>   * application
>     * 就是ServletContext
>   * out
>     * 用页面输出内容

### 10、jsp中四大域对象

> 域对象
>
> * 就是可以用来存储数据对象

#### 10.1	Servlet中的域对象

> * HttpServletRequest
> * HttpSession
> * ServletContext

#### 10.2	jsp中的域对象

> * request
> * session
> * application
> * pageContext

#### 10.3	pageContext域对象

> * 作用
>
>   * 获取其他的内置对象
>   * 操作域
>     * 操作page域
>     * 操作request、session、application
>
> * 获取其他的内置对象
>
>   * 没有获取out内置对象
>
>   ```jsp
>   <%
>       pageContext.getPage();//获取内置对象page
>       pageContext.getRequest();//获取内置对象request
>       pageContext.getResponse();//获取内置对象response
>       pageContext.getSession();//获取内置对象session
>       pageContext.getServletContext();//获取application
>       pageContext.getServletConfig();//config
>       pageContext.getException();//exception
>   %>
>   ```
>
> * 操作域
>
>   * 操作page域
>
>     * 作用范围只在当前页面
>
>     ```jsp
>     <%
>         //往pageContext域中存储了一个msg变量
>         pageContext.setAttribute("msg" ,"hello page msg");
>     %>
>     
>     <%
>         //在pageContext域中取出msg变量
>         Object msg = pageContext.getAttribute("msg");
>         System.out.println(msg);
>     %>
>     ```
>
> * 操作其他域
>
>   * request域
>
>   ```jsp
>   <%
>       //定义变量的意义! 提高复用性！ 提高可维护性!
>       //String name : 参数名称
>       //Object value : 参数值
>       //int scope : 操作的域
>       pageContext.setAttribute("msg1","hello page1",PageContext.REQUEST_SCOPE);
>       //请求转发
>       request.getRequestDispatcher("/demo06.jsp").forward(request,response);
>   %>
>   
>   <%
>       //变量msg1定义到_jspService方法中
>       Object msg1 = request.getAttribute("msg1");
>       System.out.println("msg1 : "+msg1);
>   
>       Object msg11 = pageContext.getAttribute("msg1", PageContext.REQUEST_SCOPE);
>       System.out.println(msg11);
>   %>
>   ```
>
>   * request域
>
>   ```jsp
>   <%
>       //定义变量的意义! 提高复用性！ 提高可维护性!
>       //String name : 参数名称
>       //Object value : 参数值
>       //int scope : 操作的域
>       pageContext.setAttribute("msg1","hello page1",PageContext.REQUEST_SCOPE);
>       //请求转发
>       request.getRequestDispatcher("/demo06.jsp").forward(request,response);
>   %>
>   
>   <%
>       //变量msg1定义到_jspService方法中
>       Object msg1 = request.getAttribute("msg1");
>       System.out.println("msg1 : "+msg1);
>   
>       Object msg11 = pageContext.getAttribute("msg1", PageContext.REQUEST_SCOPE);
>       System.out.println(msg11);
>   %>
>   ```
>
>   * session域
>
>   ```jsp
>   <%
>       pageContext.setAttribute("msg2","hello page2",PageContext.SESSION_SCOPE);
>   %>
>   ```
>
>   - application域
>
>   ```
>   <%
>       pageContext.setAttribute("msg3","hello page3",PageContext.APPLICATION_SCOPE);
>   %>
>   ```
>
>   

### 11、jsp优化登录案例

> * 之前方案
>
>   * login.html
>     * 登录页面
>   * LoginServlet
>     * 处理登录请求
>     * 业务处理
>     * 调用dao，操作数据
>   * ShowIndexServlet(java代码)
>     * 显示用户名
>   * 存在的问题
>     * login.html
>       * 无法和java后台进行交互，无法显示错误信息
>     * ShowIndexServlet
>       * html无法和java后台进行交互，java代码应该专注于后台代码
>
> * 现在方案
>
>   * login.jsp
>     * 登录页面
>     * 显示错误信息
>   * LoginServlet
>     * 处理登录请求
>     * 业务处理
>     * 调用dao，操作数据
>   * index.jsp
>     * 显示用户名

代码实现

* login.jsp

```jsp
<%--显示错误信息--%>
//三元运算符
<%="<font color='red'>" + (request.getAttribute("errorMsg") == null ? "" : request.getAttribute("errorMsg") ) + "</font>"%>
<form action="/day62/user" method="post">
    <input type="hidden" name="methodName" value="login"/>
    账户:<input type="text" name="username"/><br>
    密码:<input type="text" name="password"/><br>
    <button type="submit">登录</button>
</form>
```

- index.jsp

```
<%
    String username = (String) session.getAttribute("username");
    if (null == username) {
        //不在登录状态
        out.write("您还没有登录;");
        out.write("<a href='/day62/login.jsp'>请登录</a>");
    } else {
        //在登录状态
        out.write("欢迎回来~~~"+username);
    }
%>
```

存在的问题

* jsp页面还存在java代码（后台代码）和html代码（前端代码）融合在一起的问题！
* 一定程度解决，可能需要jstl标签库。
* 彻底解决，得使用vue + html