# Servlet

### 一、Servlet的概述及入门

#### 1.1概念

> ​	Servlet是运算在服务器上的一个java程序，简单说，它就是一个java类。我们要使用servlet,需要导入servlet的api.java程序中可以使用tomcat相关的api，比如：servlet-api、jsp-api
> ​	Servlet主要功能在于能够和浏览器进行交互。是一个动态资源.

#### 1.2服务器编译环境确认和设置

> Extenal Libaries中必须要有服务器的jar包
>
> 若Extenal Libaries中没有支持web服务器的编译环境,解决步骤如下：
>
> A：选择工程右键->Open Module Seetings
>
> B:	选中Modules->Dependencies->Library

#### 1.3Servlet的入门案例

> A：自定义Servlet继承HttpServlet
> B:	重写doGet方法和doPost方法
> C:	在web.xml配置servlet
> 	声明自定义Servlet
> 	给自定义Servlet配置访问名称
> D：Servlet的执行流程
> 	浏览器发起请求: http://localhost:8080/day50/demo01
> 	就会在服务器中找访问名称为demo01的Servlet -> Demo01Servlet
> 	请求的处理就交给了Demo01Servlet的实例,根据请求方式get/post,决定是给doGet还是doPost方法处理!!!
> E：注意事项
> 	不管是get请求还是post请求，对于服务器来说，没差别的！！！
> 	get请求将请求参数放到请求网址
> 	post请求将请求参数放到请求正文
> 	服务器最终无非就要获取请求参数。getParameter()方法!
>
> ```java
> package servlet;
> 
> import javax.servlet.ServletException;
> import javax.servlet.http.HttpServlet;
> import javax.servlet.http.HttpServletRequest;
> import javax.servlet.http.HttpServletResponse;
> import java.io.IOException;
>     //1，自定义类继承HttpServlet
> public class Demo01Servlet extends HttpServlet {
>     //2,重写doGet和doPost方法
>     //doGet:处理get请求
>     //doPost:处理post请求
>     //在doPost方法中调用doGet方法,不管是 get请求还是 post请求，都交给doGet方法处理
>     @Override
>     protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>         //处理get请求
>         System.out.println("doGetStart!");
>     }
> 
>     @Override
>     protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>         //处理post请求
>         doGet(req,resp);
>     }
> }
> 
> ```
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
>          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>          xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
>          version="4.0">
> 
>     <!--3，配置Servlet-->
>     <!--3.1，声明Servlet-->
>     <servlet>
>         <!--servlet的名称-->
>         <servlet-name>Demo01Servlet</servlet-name>
>         <!--servlet的全类名-->
>         <servlet-class>servlet.Demo01Servlet</servlet-class>
>     </servlet>
>     <!--
>        3.2，给Servlet设置访问名称
>           Servlet should have a mapping
>     -->
>     <servlet-mapping>
>         <!--servlet的名称-->
>         <servlet-name>Demo01Servlet</servlet-name>
>         <!--servlet的访问名称,注意：必须以‘/’开头-->
>         <url-pattern>/demo01</url-pattern>
>     </servlet-mapping>
> </web-app>
> ```
>
> 

### 二、servlet实现方式

> HttpServlet继承于GenericServlet、GenericServlet实现于Servlet，也就是说Servlet是顶层接口!!!

#### 2.1方式一：实现Servlet接口

> 在servlet接口中，没有doGet和doPost方法，处理请求是service方法(抽象的)
>
> ```java
> 
> /**
>  * 实现Servlet接口
>  * 没有针对Http协议
>  */
> public class Demo03Servlet implements Servlet {
>  public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
>         System.out.println("Demo03Sevlet实现Servlet接口");
>      	//如果想要针对Http协议，就需要开发人员手动强制类型转换
>         HttpServletRequest request = (HttpServletRequest) servletRequest;
>         HttpServletResponse response = (HttpServletResponse) servletResponse;
>     }
> }
> ```
>
> 

#### 2.2方式二：继承GenericServlet类

> 在GenericServlet类中，没有doGet和doPost方法，处理请求是service方法(抽象的)
>
> ```java
> /**
>  * 继承GenericServlet
>  * 没有针对Http协议
>  */
> public class Demo02Servlet extends GenericServlet {
>     @Override
>     public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
>         System.out.println("Demo02Servlet继承GenericServlet");
>         //如果想要针对Http协议，就需要开发人员手动强制类型转换
>         HttpServletRequest request = (HttpServletRequest) servletRequest;
>         HttpServletResponse response = (HttpServletResponse) servletResponse;
>     }
> }
> 
> ```
>
> 

#### 2.3方式三：继承HttpServlet类具体方法详见1.3

> 猜想，HttpServlet类中重写service方法。
> 根据源码，发现重写service方法中，
> 有将ServletRequest强转为HttpServletRequest,
> 将ServletResponse强转为HttpServletResponse
> 以上强转是因为,ServletRequest和ServletResponse并没有针对Http协议做优化!!!无法专门针对http协议调
> 用方法!!
> HttpServletRequest和HttpServletResponse有针对http协议做优化!!!

[经验：推荐使用继承HttpServlet类，针对http协议有优化!!!]()

> 步骤：
>
> A：自定义Servlet继承HttpServlet
> B:	重写doGet方法和doPost方法
> C:	在web.xml配置servlet
> 		声明自定义Servlet
> 		给自定义Servlet配置访问名称

### 三、Servlet的生命周期

#### 3.1什么是生命周期？

> 一个事物，从开始、存活、结束！说白了，就是需要看Servlet的初始化、存活、销毁！！

#### 3.2演示生命周期

> init(ServletConfig var1):
>
> ​		监听Servlet的初始化
>
> service(ServletRequest var1, ServletResponse var2):
>
> ​		处理请求
>
> destroy():
>
> ​		监听Servlet的销毁
>
> ```java
> public interface Servlet {
>     void init(ServletConfig var1) throws ServletException;
> 
>     ServletConfig getServletConfig();
> 
>     void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;
> 
>     String getServletInfo();
> 
>     void destroy();
> }
> ```
>
> 

#### 3.3生命周期的特点

> - 第一次访问servlet,servlet会被创建，并将servlet对象常驻内存，调用init方法进行初始化操
>   作，init方法中执行一次。
>
> - 调用service方法，用于处理来自浏览器端的请求，以后都是开启一个线程来处理浏览器端请
>   求。
>
> - 当tomcat服务器正常关闭时，会调用destroy方法将servlet销毁。
>
>   [注意：Servlet默认不是随着服务器的启动而初始化，当第一次访问Servlet时才初始化，后面访问就执行处理请求会发现Servlet，是一个单例!!]()

### 四、load on startup

#### 4.1概念

> ​		根据Servlet生命周期，可知，servlet默认不会随着服务器的启动而初始化!
>
> ​		如果，就想让指定的Servlet跟随服务器启动而初始化，我们如何做？需要用到load on startup
>
> ​		load on startup可以让servlet随着服务器的启动而初始化

#### 4.2load on startup 优先级

> 有10个优先级：1~10；数字越小，优先级越高！
>
> ​		比如：Demo01Servlet，load-on-startup：1 ；Demo02Servlet ， load-on-startup ：2；
>
> ​		当服务器启动时，Demo01Servlet先初始化，然后，Demo02Servlet再初始化!
>
> ```xml
> <servlet>
>         <servlet-name>Demo05Servlet</servlet-name>
>         <servlet-class>com.qfedu.servlet.Demo05Servlet</servlet-class>
>     <!--demo05的优先级较低，后初始化-->
>         <load-on-startup>3</load-on-startup>
>     </servlet>
> 
>     <servlet-mapping>
>         <servlet-name>Demo05Servlet</servlet-name>
>         <url-pattern>/demo05</url-pattern>
>     </servlet-mapping>
> 
>     <servlet>
>         <servlet-name>Demo06Servlet</servlet-name>
>         <servlet-class>com.qfedu.servlet.Demo06Servlet</servlet-class>
>         <!--demo06优先级高，先初始化-->
>          <load-on-startup>1</load-on-startup>
>     </servlet>
> 
>     <servlet-mapping>
>         <servlet-name>Demo06Servlet</servlet-name>
>         <url-pattern>/demo06</url-pattern>
>     </servlet-mapping>
> ```
>
> 

### 五、servlet配置详解

#### 5.1步骤

> 对于servlet,我们需要在web.xml文件中对其进行配置
> 	在web.xml中声明Servlet
> 	在web.xml中给Servlet映射访问路径
>
> [注意：一个Servlet可以有多个访问名称，只需要给对应的Servlet多个<servlet-mapping>标签即可!]()

#### 5.2书写规则

> <url-parttern>书写规则

##### 2.2.1完全匹配

> 要求网址上的访问名称完全和<url-parttern>一致
>
> ​		必须以"/"开头，否则会报错:IllegalArgumentException : Invalid <url-pattern> 
>
> ```xml
>  <servlet-mapping>
>         <servlet-name>Demo07Servlet</servlet-name>
>         <!--
>             Caused by: java.lang.IllegalArgumentException: Invalid <url-pattern> [mydemo07] in servlet mapping
>             非法参数异常：非法的访问名称mydemo07在servlet映射中!
>             因为以上不满足完全匹配规则：必须以"/"开头
>         -->
>         <url-pattern>/mydemo07</url-pattern>
>   </servlet-mapping>
> ```
>
> 

##### 5.2.2目录匹配

> 要求网址上的访问名称中的目录和<url-parttern>一致
>
> ​		必须以"/"开头，以"*"结尾
>
> ​		比如:/a/b/c/*, 目录必须是/a/b/c/，后面随便写
>
> ```xml
> <servlet-mapping>
>         <servlet-name>Demo08Servlet</servlet-name>
>         <url-pattern>/a/b/c/*</url-pattern>
> </servlet-mapping>
> ```
>
> 

##### 5.2.3扩展名匹配

> 要求网址上的访问名称中的后缀和<url-parttern>一致
>
> ​		不能以"/"开头,以"*"开头，后缀名根据业务写
>
> ​		比如：*.xyz。后缀名必须是xyz，其他随意写!!!
>
> ```xml
>  <servlet-mapping>
>         <servlet-name>Demo09Servlet</servlet-name>
>         <!--        Caused by: java.lang.IllegalArgumentException: Invalid <url-pattern> [/*.xyz] in servlet mapping-->
>         <url-pattern>*.xyz</url-pattern>
>  </servlet-mapping>
> ```
>
> 

### 六、缺省Servlet

> * A_概念
>
>   url-parttern的值为"/"就是缺省Servlet
>
>   ```xml
>   <servlet-mapping>
>               <servlet-name>MyDefaultServlet</servlet-name>
>               <url-pattern>/</url-pattern>
>   </servlet-mapping>
>   ```
>
>   
>
> * B_作用
>
>   tomcat容器自带缺省Servlet
>
>   处理匹配不到的资源，返回404页面
>
>   处理静态资源，io流读写
>
> * C_自定义缺省Servlet
>
>   在当前工程中自定义Servlet，将url-parttern设置为"/"，就覆盖了tomcat容器中的缺省Servlet
>
> * D_应用
>
>   SpringMVC框架中，用于放行静态资源！

### 七、服务器中的路径问题

#### 7.1路径分类

> 带协议的绝对路径：http://localhost:8080/day51/img/girl.jpg
>
> 不带协议的绝对路径：/day51/img/girl.jpg
>
> 相对路径：
>
> ​	当前目录：./ ，可以省略
>
> ​	上一级目录：../

#### 7.2总结

> 开发中，用的比较多：不带协议的绝对路径、相对路径
>
> 

### 八、ServletConfig对象

#### 8.1概述

> ServletConfig是由tomcat容器创建，通过init方法传入给Servlet

#### 8.2作用

> - 获取Servlet的名称<servlet-name>标签内容
>
> - 获取Servlet的初始化参数
>
> ​	随着Servlet的初始化而初始化
>
> ```xml
> <servlet>
> <servlet-name>Demo11Servlet</servlet-name>
> <servlet-class>com.qfedu.servlet.Demo11Servlet</servlet-class>
> <!--Servlet的初始化参数-->
> <init-param>
>     <param-name>username</param-name>
>     <param-value>root</param-value>
> </init-param>
> <init-param>
>     <param-name>password</param-name>
>     <param-value>root123</param-value>
> </init-param>
> </servlet>
> ```
>
> getInitParameter(String parameterName)：根据参数名称获取指定的参数值
>
> getInitParameterNames():获取所有的参数名称
>
> - 获取域对象：ServletContext
>
> - ```java
>     /**
>    * 演示ServletConfig对象的作用
>     */
>     public class Demo11Servlet extends HttpServlet {
>     ```
> ```jAVA
> 
> @Override
>    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>     //1，获取ServletConfig对象
>     ServletConfig servletConfig = getServletConfig();
>     //2，ServletConfig对象作用一：获取Servlet的名称 , 获取到<servlet-name>标签内容
>     String servletName = servletConfig.getServletName();
>     System.out.println(servletName+"在运行~~~");
>     System.out.println("----------------------");
>     //3，ServletConfig对象作用二：获取Servlet中的初始化参数
>     String username = servletConfig.getInitParameter("username");
>     System.out.println(username);
>     String password = servletConfig.getInitParameter("password");
>     System.out.println(password);
>     System.out.println("----------------------");
>     //动态获取初始化参数名称
>     Enumeration<String> parameterNames = servletConfig.getInitParameterNames();
>     while (parameterNames.hasMoreElements()) {
>         String parameterName = parameterNames.nextElement();
>         String parameterValue = servletConfig.getInitParameter(parameterName);
>         System.out.println("name : " + parameterName + " , value : " + parameterValue);
> }
>    
>     //4,ServletConfig对象作用三：获取ServletContext对象(域对象!)!
> ServletContext servletContext = servletConfig.getServletContext();
> 
>}
> 
> @Override
>    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>  doGet(req, resp);
> }
> }
>  ```
> 
>

### 九、ServletContext对象

#### 9.1概念

> 相当于是整个应用程序对象

#### 9.2作用

> - ServletContext是一个域对象，可以用来存储数据
>
>   1. 在应用程序中的任何位置都能够访问
>   2. getAttribute(String parameterName) : 获取ServletContext域中指定名称的参数值
>   3. setAttribute(String paramterName,Object parameterValue):存储参数到ServletContext域中
>   4. removeAttribute(String parameterNam)：将ServletContext域中指定名称的参数移除!
>
> - 获取全局初始化参数
>
>   - 会随着服务器的启动而初始化
>   
>   - 常用方法：
>   
>     - getInitParameter(String parameterName)：根据参数名称获取全局初始化参数值
>   
>       getInitParameterNames():获取所有的全局初始化参数名称
>
> ```xml
> <context-param>
>    <param-name>username</param-name>
>    <param-value>root456</param-value>
> </context-param>
> ```
>
> - 获取服务器真实磁盘路径
>
>   - getRealPath：依据当前项目去生成真实磁盘路径，
>
>  比如：servletContext.getRealPath("upload")
>
>  "当前项目的服务器磁盘路径/upload"
>
>  比如：servletContext.getRealPath("upload/img"):
>
>  "当前项目的服务器磁盘路径/upload/img"

```java
/**
* 存入域对象
 */
        ServletConfig servletConfig = getServletConfig();
        ServletContext servletContext = servletConfig.getServletContext();
        servletContext.setAttribute("username",123456);
/**
 * 获取域对象
 */
  		ServletContext servletContext = getServletContext();
        Object attributeNames1 = servletContext.getAttribute("username");
        System.out.println(attributeNames1);
/**
 * 移除域对象
 */
		ServletContext servletContext = getServletContext();
        servletContext.removeAttribute("username");
```

#### 9.3站点访问次数案例

```java
/**
 * 站点访问次数案例
 */
@WebServlet(name = "Case", urlPatterns = "/case")
public class Case extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //从域中获取一个count
        ServletContext servletContext = getServletContext();
        //后面需要用到count++，强转为Integer类型
        Integer count = (Integer) servletContext.getAttribute("count");
        //判断该站点是否第一次被访问，count==null时为第一次被访问
        if(null == count){
            count = 1;
            System.out.println("站点访问次数："+ count);
            //将计数器存储到域中
            servletContext.setAttribute("count",count);
        }else {
            count++;
            System.out.println("站点访问次数："+ count);
            //将计数器存储到域中
            servletContext.setAttribute("count",count);
        }


    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

### 十、Servlet3.0

#### 10.1概念

> Servlet2.5，不支持注解开发。
>
> Servlet3.0，支持注解开发。

#### 10.2常用注解

> @Test:单元测试
>
> @Override:方法重写
>
> @WebServlet:	声明配置Servlet，取代了web.xml配置
>
> ```java
> @WebServlet(name = "Demo18Servlet",urlPatterns = "/demo18")
> public class Demo18Servlet extends HttpServlet {
> 
> }
> ```
>
> 以上配置代码，相当于web.xml配置如下：
>
> ```xml
> <servlet>
>     <servlet-name>Demo18Servlet</servlet-name>
>     <servlet-class>com.qfedu.servlet.Demo18Servlet</servlet-class>
> </servlet>
> <servlet-mapping>
>     <servlet-name>Demo18Servlet</servlet-name>
>     <url-pattern>/demo18</url-pattern>
> </servlet-mapping>
> ```
>
> 

#### 10.3常用属性

> * name:	String类型
>   * 设置Servlet名称
> * urlPatterns:  String[]类型
>   * 设置Servlet的访问路径
> * loadOnStartup:  int类型
>   * 设置Servlet的load-on-startup属性
> * initParams:  WebInitParam[]类型
>   * 设置Servlet的初始化参数

```java
@WebServlet(name = "Demo01Servlet" ,
        urlPatterns = {"/demo01" ,"/mydemo01"},
        loadOnStartup = 1,
        initParams ={ @WebInitParam(name = "username",value = "root") ,
                @WebInitParam(name = "password",value = "root123") })
```

