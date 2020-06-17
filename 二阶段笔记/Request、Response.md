

# Request、Response

### 一、Request、Response对象介绍

#### 1.1概念

> 当浏览器发起请求后，服务器会创建一个请求对象、一个响应对象，通过service方法传入给Serlvet

#### 1.2作用

> * request对象处理请求信息(请求行、请求头、请求正文)
> * response对象处理响应信息(响应行、响应头、响应正文)

#### 1.3ServletRequest和HttpServletRequest的关系、ServletResponse和HttpServletResponse的关系

> * ServletRequest是HttpServletRequest的父接口，
>
> * ServletResponse是HttpServletResponse的父接口，
>
> * HttpServletRequest针对Http协议、HttpServletResponse针对Http协议

### 二、response操作

#### 2.1response操作响应行

> * setStatus:操作正常响应状态码，比如：200、302
>
>   * 200:告诉浏览器，响应成功
>
>   * 302:重定向
>
>   * 304:页面没有发生改变
>
> ```java
> resp.setStatus(200);
> ```
> - sendError:操作错误响应状态码，比如: 404
>
>   - ```java
>       response.sendError(404);
>       ```
>
>    

#### 2.2response操作响应头

> * setHeader:直接覆盖响应头原有值
>
> ```java
>  	//操作响应头
>         //setHeader():覆盖原有的响应头的值
>         //addHeader():在原有的响应头的值后面追加 (Cookie)
>         //服务器告诉浏览器，给的响应正文的类型是text/html，告诉你应该以utf-8进行解码
>         response.setHeader("Content-Type","text/html;charset=utf-8");
>         System.out.println("Demo02Servlet doPost");
> ```
>
> 
>
> * addHeader:在响应头原有值的后面追加(Cookie)

#### 2.3response操作重定向

##### 2.3.1重定向的流程

> * 当浏览器访问一个资源Demo03Servlet，访问名称为“/demo03”
> * Demo03Servlet进行重定向
>   * 操作响应状态码302
>   * 操作响应头Location，服务器告诉浏览器，重定向的资源的访问路径
> * 浏览器进行一个新的请求，完成重定向

##### 2.3.2实现代码

###### 2.3.2.1方式1

```java
//操作响应状态码302
response.setStatus(302);
//操作响应头Location，服务器告诉浏览器，重定向的资源的访问路径
response.setHeader("Location","demo04");
```

###### 2.3.2.2方式2

```java
response.sendRedirect("demo04");
```

[相当于方式1]()

#### 2.4response操作定时跳转

##### 2.4.1概念

> * 一个资源定时一段时间之后，跳转到另外一个资源
> * 操作响应头refresh

##### 2.4.2代码实现

```java
resp.setHeader("refresh","5;url=demo07");
```

#### 2.5response操作响应正文(重点)

> * 响应正文
>
>   * 就是浏览器显示的主体内容
>
> * 常用方法
>
>   * response.getWriter().write()：操作响应正文
>
> * 注意事项
>
>   * 响应正文中文乱码
>
>     * 本质原因，服务器的编码和浏览器的解码，格式不同！
>     * setCharacterEncoding("utf-8")：[方式1]()
>       * 告诉服务器，应该以utf-8格式编码响应正文
>     * setHeader("Content-Type","text/html;charset=utf-8"):
>       * 告诉浏览器 , 响应正文是文本+html标签，应该以utf-8格式解码响应正文
>
>     * setContentType("text/html;charset=utf-8")[方式2，相当于方式1]()
>       * 告诉服务器，应该以utf-8格式编码响应正文
>       * 同时告诉浏览器 , 响应正文是文本+html标签，应该以utf-8格式解码响应正文

```java
public class Demo01Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //告诉浏服务器，编码方式为utf-8
        response.setCharacterEncoding("utf-8");
        //还得告诉浏览器，编码格式也为utf-8
        response.setHeader("Content-Type","text/html;charset=utf-8");
        String msg = "Hello World，老邱" ;
        response.getWriter().write(msg);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

### 三、request操作

#### 3.1request操作请求行

> 常用方法
>
> * getRequestURI
>   * 获取请求路径
> * getMethod
>   * 获取请求方式
> * getRemoteAddr
>   * 获取请求ip
> * getLocalPort
>   * 获取请求端口
> * getQueryString
>   * 请求网址"?"后面的路径

```java
public class Demo02Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("Demo02Servlet");
        //获取请求路径
        String requestURI = request.getRequestURI();
        System.out.println(requestURI);
        //获取请求方式
        String method = request.getMethod();
        System.out.println(method);
        //获取请求IP
        String remoteAddr = request.getRemoteAddr();
        System.out.println(remoteAddr);
        //获取请求端口
        int localPort = request.getLocalPort();
        System.out.println(localPort);
        //获取请求网址后的请求参数(?后面的内容)
        String queryString = request.getQueryString();
        System.out.println(queryString);

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```

#### 3.2request操作请求头

> getHeader()
>
> * 获取指定请求头的值

```java
public class Demo03Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取User-Agent请求头：判定请求是由哪种浏览器发起
        String userAgent = request.getHeader("User-Agent");
        System.out.println(userAgent);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

#### 3.3request操作请求参数

> * 请求正文（get请求，没有请求正文）
>
>   * post+请求参数
>
> * 请求参数
>
>   * 不管是get请求 还是 post请求 都有!!!
> * 常用方法
>
>   * getParameter
>     * 获取指定请求参数值
>   * getParameterNames
>     * 获取所有请求参数名称
>   * getParameterValues(String parameterName)
>     * 获取指定请求参数所有值
>   * getParameterMap
>     * 键，获取所有请求参数名称 , 相当于getParameterNames方法
>     * 值，获取指定请求参数所有值，相当于getParameterValues方法
>
> ```java
> public class Demo04Servlet extends HttpServlet {
>     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>         //获取指定参数值
>         String username = request.getParameter("username");
>         System.out.println(username);
>         System.out.println("---------");
>         //获取所有参数名称
>         Enumeration<String> parameterNames = request.getParameterNames();
>        while (parameterNames.hasMoreElements()){
>            String parName = parameterNames.nextElement();
>            System.out.println(parName);
>            //获取对应参数值
>            String parameter = request.getParameter(parName);
>            System.out.println("参数名称："+parName+",对应参数值："+parameter);
>        }
>         System.out.println("---------------");
>        //获取指定参数所有值
>         String[] hobbies = request.getParameterValues("hobbies");
>         for (String hobby : hobbies) {
>             System.out.println(hobby);
>         }
>         System.out.println("-----------");
>         //获取所有参数的对应map
>         //获取请求参数对应的map :
>         //getParameterMap() -> Map(String,String[])
>         //键：请求参数名称  相当于 getParameterNames
>         //值：一组请求参数值 相当于 getParameterValues
>         Map<String, String[]> parameterMap = request.getParameterMap();
>         //双列集合：获取到所有的实体对象(键值对象)
>         Set<Map.Entry<String, String[]>> entries = parameterMap.entrySet();
>         for (Map.Entry<String, String[]> entry : entries) {
>             //键 - 请求参数名称
>             String key = entry.getKey();
>             //值 - 请求参数的值
>             String[] value = entry.getValue();
>             //创建一个可变长字符串存储值
>             StringBuffer stringBuffer = new StringBuffer();
> 
>             for (String s : value) {
>                 stringBuffer.append(s +" ");
>             }
>             System.out.println("参数名称："+ key+ ",参数值："+ stringBuffer);
>         }
> 
> 
>     }
> 
>     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>         doPost(request, response);
>     }
> }
> 
> ```

### 四、请求参数中文乱码

#### 4.1请求参数中文乱码之post

> * 本质
>
>   * 请求正文中的中文参数乱码
>
> * 解决方案
>
>   * request.setCharacterEncoding("utf-8")[方法1]()
>
>     * 告诉服务器应该以utf-8解码请求正文
>
>   * 逆向，先编码再解码[方法2]()
>
>     * 先将乱码字符串以iso8859-1编码成字节
>     * 将字节以utf-8解码成字符串
>
>  ```java
> String username = request.getParameter("username"); 
> username = new String(username.getBytes("iso8859-1"),"utf-8");
>  ```
>
> * 注意事项
>
>   * 将tomcat容器的URIEncoding="utf-8"，对Query String中的请求参数有效，对请求正文中无效，对post请求下的中文乱码无效!
>
> 

```java
public class Demo05Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //浏览器告诉服务器，应以utf-8编码
//        request.setCharacterEncoding("utf-8");
        String username = request.getParameter("username");
        username = new String(username.getBytes("iso8859-1"),"utf-8");
        System.out.println(username);


        System.out.println(username);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }

```

#### 4.2请求参数中文乱码之get

> * 本质
>
>   * Query String中的中文参数乱码
>
> * 解决方案
>
> * [方案一：]()
>
>   * 逆向，先编码在解码
>
>     * 先将乱码字符串以iso8859-1编码成字节
>     * 将字节以utf-8解码成字符串
>
>  ```java
> String username = request.getParameter("username"); 
> username = new String(username.getBytes("iso8859-1"),"utf-8");
>  ```
>
> [方案二：仅针对get方式有效]()
>
>   * 修改tomcat容器的URIEncoding="utf-8"
>
>  ```xml
>  <Connector port="8080" protocol="HTTP/1.1"
>             connectionTimeout="20000"
>             URIEncoding="utf-8"
>             redirectPort="8443" />
>  ```
>
> * 注意事项
>
>   * request.setCharacterEncoding("utf-8")对get请求无效，告诉服务器应该以utf-8来解码请求正文，跟Query String 没有关系!

#### 4.3请求参数中文乱码终极解决方案

> 方案：tomcat8.5  +  
>
> * tomcat8.5 
>   * 相当于是tomcat7.0修改了URIEncoding="utf-8"
>   * 就解决了get请求参数中文乱码问题
> * request.setCharacterEncoding("utf-8")
>   * 就解决了post请求参数中文乱码问题

### 五、请求转发

#### 5.1request操作请求转发

> * 请求转发
>   * 服务器中，从一个资源跳转到另外一个资源
> * 流程
>   * 浏览器发起请求，请求Demo01Servlet
>   * Demo01Servlet，请求转发到Demo02Servlet
>   * 在服务器内部，直接从Demo01Servlet跳转到了Demo02Servlet
> * 注意事项
>   * 转发只有一次请求
> * 方法：
> * request.getRequestDispatcher("[转发地址]()").forward(request,response);
>
> 

```java
public class Demo02Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("Demo02Servlet");
        //转发到Demo03Servlet
        //获取一个转发器对象，传入一个转发地址
        RequestDispatcher demo03 = request.getRequestDispatcher("demo03");
        demo03.forward(request,response);

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```



#### 5.2请求转发和重定向的区别

> * 请求次数
>   * 重定向有2次请求
>   * 转发有1次请求
> * 跳转区别
>   * 重定向既可以站内资源进行跳转，站外资源也可以进行跳转
>   * 转发只能站内资源进行跳转
> * 路径区别
>   * 要转发的资源的相对路径无区别
>   * 要转发的资源的绝对路径有区别
>     * 重定向，是从先从项目开始找，再找资源	[/项目名/资源名]()
>     * 转发，是直接从项目中找资源[直接/资源名]()

```java
public class Demo04Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //重定向
        response.setStatus(302);
        response.sendRedirect("http://www.baidu.com/");
       
      
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

### 六、request作为域对象

> * 域对象
>   * 可以存储数据的对象
> * 回顾ServletContext域对象的作用范
>   * 不同设备、当前项目中的任意一个资源都可以访问ServletContext域中的数据！
> * request域对象的作用范围
>   * request对象的生命周期
>     * 发起请求时，request初始化
>     * 响应时，request销毁
>   * [request域对象的作用范围在一次请求中!]()
>
> * request在重定向和转发中使用!
>   * [重定向中不能使用request域对象]()
>   * [转发中可以使用request域对象]()
>
> - request域操作数据的方法和ServletContext域是一样
>   - setAttribute（）往域中存储数据
>   - getAttribute（）获取域中的指定数据
>   - removeAttribute（）移除域中的指定数据

```java
public class Demo05Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String msg = "hello servlet";
        request.setAttribute("msg",msg);
        //转发到demo06去获得域对象中的数据
        request.getRequestDispatcher("demo06").forward(request,response);

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

```java
public class Demo06Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Object msg = request.getAttribute("msg");
        System.out.println(msg);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```

