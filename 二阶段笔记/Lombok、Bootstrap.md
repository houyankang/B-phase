### 01_BaseServlet再优化

* 优化思路

  * 可以将方法的返回值转换为json，并将该json字符串作为服务器响应正文返回给浏览器

* 代码实现

  ```java
  @WebServlet(name = "BaseServlet",urlPatterns = "/base")
  public class BaseServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          String methodName = request.getParameter("methodName");
          try {
              Method method = this.getClass().getMethod(methodName, HttpServletRequest.class, HttpServletResponse.class);
              if (null != method) {
                  Object returnValue =  method.invoke(this,request,response);
                  //判断方法上是否有@MyResponseBody注解
                  boolean present = method.isAnnotationPresent(MyResponseBody.class);
                  if (present) {
                      //有@MyResponseBody注解,方法的返回值是一个json字符串
                      if (returnValue.getClass() == String.class) {
                          //返回值是一个json字符串
                          response.setContentType("application/json;charset=utf-8");
                          response.getWriter().write(returnValue+"");
                      } else {
                          //返回值是一个java对象
                          JsonUtils.writeJsonStr(response,returnValue);
                      }
  
                  } else {
                      //没有@MyResponseBody注解,就是资源的路径
                      String newReturnValue = (String) returnValue;
                      if (null != returnValue) {
                          //是否有":"
                          int index = newReturnValue.lastIndexOf(":");
                          if (-1 == index) {
                              //没有":"
                              request.getRequestDispatcher(newReturnValue).forward(request,response);
                          } else {
                              //有":"
                              String path = newReturnValue.substring(index + 1);
                              if (newReturnValue.startsWith("redirect")){
                                  //重定向
                                  response.sendRedirect(request.getContextPath() + File.separator + path);
                              } else if (newReturnValue.startsWith("forward")){
                                  //请求转发
                                  request.getRequestDispatcher(path).forward(request,response);
                              }
                          }
                      }
                  }
  
  
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request, response);
      }
  }
  ```

  

### 02_lombok概述

* 概念
  * 面对工作中大量重复的,毫无技术含量的get,set方法,你是不是怨恨过?
  * Lombok是一种java使用技术,可用来帮助开发人员消除java中的冗长的代码,尤其是对于简单的 Java对象(POJO),它通过注解实现这一目的.
* 注解
  * ![image-20200516105455839](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200516141343.png)



### 03_lombok的环境搭建

* 给idea配置Lombok插件
  * file -> settings -> plugins
* 当前工程导入lombok.jar
* enable annotation processing
  * ![image-20200516110303728](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200516141346.png)





### 04_lombok之@Getter、@Setter注解

* @Getter

  ```java
  @Target({ElementType.FIELD, ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface Getter {
      AccessLevel value() default AccessLevel.PUBLIC;//更改get方法的权限修饰符
  }
  ```

  * 生成get方法
  * 既可以用到类上，也可以用到成员变量上

* @Setter

  ```java
  @Target({ElementType.FIELD, ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface Setter {
      AccessLevel value() default AccessLevel.PUBLIC;//更改set方法的权限修饰符
  }
  ```

  * 生成set方法
  * 既可以用到类上，也可以用到成员变量上





### 05_lombok之@ToString注解

* @ToString

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface ToString {
  
      String[] exclude() default {};//排除某些属性
  
      String[] of() default {};//包含某些属性
  
  }
  ```

  * 生成toString方法
  * 只能使用到类上
  
* 常用属性

  * exclude
    * 排除指定属性
  * of
    * 包含指定属性



### 06_lombok之@NoArgsConstructor、@AllArgsConstructor

* NoArgsConstructor

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface NoArgsConstructor {
  
      AccessLevel access() default AccessLevel.PUBLIC;//设置方法的权限修饰符
  
  }
  
  ```

  * 生成无参构造方法

* AllArgsConstructor

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface AllArgsConstructor {
  
      AccessLevel access() default AccessLevel.PUBLIC;//设置方法的权限修饰符
  
  }
  ```

  * 根据类中的所有字段生成有参构造方法





### 07_lombok之@Data

* @Data

  ```java
  @Target({ElementType.TYPE})
  @Retention(RetentionPolicy.SOURCE)
  public @interface Data {
      String staticConstructor() default "";
  }
  ```

  * 生成无参构造、get/set方法、hashCode方法、equals方法、toString方法

* 代码实现

  ```java
  @Data
  @NoArgsConstructor
  @AllArgsConstructor
  public class User {
  
      private Integer id;
      private String username;
      private String password;
      private String email;
  
  }
  ```

  

### 08_Bootstrap概念

* 介绍
  * Bootstrap是一个前端框架，由Twitter开发，非常受欢迎。
  * Bootstrap 是基于 HTML、CSS、JavaScript 的，它简洁灵活，使得 Web 开发更加快捷。
* 框架
  * 相当于半成品；开发人员基于框架可以进行二次开发，大大的节省开发人员的开发时间。
* 特点
  * 定义了很多的css样式和js插件。我们开发人员直接可以使用这些样式和插件得到丰富的 页面效果
  * 支持响应式布局，写一套页面就可以在不同分辨率的设备上有比较好的效果。





### 09_Bootstrap入门案例

* 开发流程

  * 下载Bootstrap的相关资源
    * https://www.bootcss.com/
  * 将bootstrap资源导入到项目
    * ![image-20200516145617224](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200516145805.png)

  * 将bootstrap资源导入到页面
    * 导入bootstrap.css样式文件
    * 导入jquery.js类库文件
    * 导入boostrap.js类库我呢见

* 代码实现

  ```html
  <head>
      <title>Bootstrap的入门</title>
      <!-- Bootstrap的样式文件 -->
      <link href="${pageContext.request.contextPath}/bootstrap/css/bootstrap.min.css" rel="stylesheet">
      <!-- Jquery的类库文件 -->
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <!-- Bootstrap的类库文件 -->
      <script src="${pageContext.request.contextPath}/bootstrap/js/bootstrap.min.js"></script>
  
  
  </head>
  <body>
  <h1>你好，世界！</h1>
  </body>
  ```

  



### 10_Bootstrap之响应式布局

* 概念

  * Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。

* 组成

  * 栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。
  * 栅格系统容器包含行；行包含列，列包含内容
  * 栅格系统容器
    * container
    * container-fluid
  * 行
    * row
  * 列
    * col(col-lg、col-md、col-sm、col-xs)

* 栅格参数

  * ![image-20200516152941758](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200516152946.png)

* 需求：

  * 整个容器占满屏幕的宽度,
  * 在lg分辨率(大桌面)下,要求每一个元素占1个位置,
  * 在md分辨率(桌面)下,每一个元素占2个位置;
  * 在sm分辨率(平板)下,每一个元素占3个位置;
  * 在xs分辨率(手机)下,每一个元素占6个位置。
  
* 代码实现

  ```html
  <head>
      <title>Bootstrap的栅格系统</title>
      <%--导入bootstrap的样式文件--%>
      <link href="bootstrap/css/bootstrap.min.css" rel="stylesheet">
      <%--导入jquery--%>
      <script src="js/jquery-3.2.1.min.js"></script>
      <%--导入bootstrap的脚本文件--%>
      <script src="bootstrap/js/bootstrap.min.js"></script>
  <%--
      1，定义一个栅格系统容器
      2，定义行
      3，定义列
  --%>
      <style>
          .one{
              background-color: pink;
          }
          .two{
              background-color: dodgerblue;
          }
          .three{
              background-color: green;
          }
          .four{
              background-color: orange;
          }
  
      </style>
  
  </head>
  <body>
  <%--1,定义栅格容器--%>
  <div class="container-fluid">
      <%--2,定义行--%>
      <div class="row">
          <div class="one col-lg-1 col-md-2 col-sm-3 col-xs-6">1</div>
          <div class="two col-lg-1 col-md-2 col-sm-3 col-xs-6">2</div>
          <div class="three col-lg-1 col-md-2 col-sm-3 col-xs-6">3</div>
          <div class="four col-lg-1 col-md-2 col-sm-3 col-xs-6">4</div>
  
          <div class="one col-lg-1 col-md-2 col-sm-3 col-xs-6">5</div>
          <div class="two col-lg-1 col-md-2 col-sm-3 col-xs-6">6</div>
          <div class="three col-lg-1 col-md-2 col-sm-3 col-xs-6">7</div>
          <div class="four col-lg-1 col-md-2 col-sm-3 col-xs-6">8</div>
  
          <div class="one col-lg-1 col-md-2 col-sm-3 col-xs-6">9</div>
          <div class="two col-lg-1 col-md-2 col-sm-3 col-xs-6">10</div>
          <div class="three col-lg-1 col-md-2 col-sm-3 col-xs-6">11</div>
          <div class="four col-lg-1 col-md-2 col-sm-3 col-xs-6">12</div>
      </div>
  
  </div>
  ```

  

### 11_Bootstrap之全局css样式

* 按钮

  ```html
  <!-- Standard button -->
  <button type="button" class="btn btn-default">（默认样式）Default</button>
  
  <!-- Provides extra visual weight and identifies the primary action in a set of buttons -->
  <button type="button" class="btn btn-primary">（首选项）Primary</button>
  
  <!-- Indicates a successful or positive action -->
  <button type="button" class="btn btn-success">（成功）Success</button>
  
  <!-- Contextual button for informational alert messages -->
  <button type="button" class="btn btn-info">（一般信息）Info</button>
  
  <!-- Indicates caution should be taken with this action -->
  <button type="button" class="btn btn-warning">（警告）Warning</button>
  
  <!-- Indicates a dangerous or potentially negative action -->
  <button type="button" class="btn btn-danger">（危险）Danger</button>
  
  <!-- Deemphasize a button by making it look like a link while maintaining button behavior -->
  <button type="button" class="btn btn-link">（链接）Link</button>
  ```

  

* 图片

  ```html
  
  <img src="img/girl.jpg" class="img-rounded">
  
  <img src="img/girl.jpg" class="img-circle">
  
  <img src="img/girl.jpg" class="img-thumbnail">
  ```

  

* 表格

  ```html
              <table class="table"  >
                  <tr class="danger">
                      <td>ID</td>
                      <td>账户</td>
                      <td>密码</td>
                      <td>操作</td>
                  </tr>
  
                  <tr>
  
                      <td>1</td>
                      <td>张三</td>
                      <td>root</td>
                      <td>
                          <a href="javascript:void(0);" class="btn btn-success">删除</a>
                      </td>
                  </tr>
                  <tr>
  
                      <td>2</td>
                      <td>李四</td>
                      <td>root</td>
                      <td>
                          <a href="javascript:void(0);" class="btn btn-default">删除</a>
                      </td>
                  </tr>
              </table>
  ```

  

* 表单

  ```html
  <form class="form-horizontal">
      <div class="form-group">
          <label for="inputEmail3" class="col-sm-2 control-label">账户</label>
          <div class="col-sm-10">
              <input type="email" class="i1 form-control" id="inputEmail3" placeholder="Email">
          </div>
      </div>
      <div class="form-group">
          <label for="inputPassword3" class=" col-sm-2 control-label">密码</label>
          <div class="col-sm-10">
              <input type="password" class="i1 form-control" id="inputPassword3" placeholder="Password">
          </div>
      </div>
      <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
              <div class="checkbox">
                  <label>
                      <input type="checkbox"> 记住我
                  </label>
              </div>
          </div>
      </div>
      <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
              <button type="submit" class="btn btn-default">登录</button>
          </div>
      </div>
  </form>
  ```

  

### 12_Bootstrap之组件

* 导航条

  ```html
  <nav class="navbar navbar-default navbar-inverse">
      <div class="container-fluid">
          <!-- Brand and toggle get grouped for better mobile display -->
          <div class="navbar-header">
              <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
                  <span class="sr-only">Toggle navigation</span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
              </button>
              <a class="navbar-brand" href="#">千锋教育</a>
          </div>
  
          <!-- Collect the nav links, forms, and other content for toggling -->
          <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
              <ul class="nav navbar-nav">
                  <li class="active"><a href="#">Java <span class="sr-only">(current)</span></a></li>
                  <li><a href="#">Html</a></li>
                  <li class="dropdown">
                      <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">更多课程 <span class="caret"></span></a>
                      <ul class="dropdown-menu">
                              <li><a href="#">Python</a></li>
                          <li><a href="#">大数据</a></li>
                      </ul>
                  </li>
              </ul>
              <form class="navbar-form navbar-left">
                  <div class="form-group">
                      <input type="text" class="form-control" placeholder="请输入课程名称">
                  </div>
                  <button type="submit" class="btn btn-default">搜索</button>
              </form>
              <ul class="nav navbar-nav navbar-right">
                  <li><a href="#">联系老邱</a></li>
                  <li class="dropdown">
                      <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">我的 <span class="caret"></span></a>
                      <ul class="dropdown-menu">
                          <li><a href="#">个人中心</a></li>
                          <li><a href="#">我的订单</a></li>
                          <li><a href="#">课程中心</a></li>
                          <li role="separator" class="divider"></li>
                          <li><a href="#">退出登录</a></li>
                      </ul>
                  </li>
              </ul>
          </div><!-- /.navbar-collapse -->
      </div><!-- /.container-fluid -->
  </nav>
  ```

  

* 分页工具条

  ```html
  <nav aria-label="Page navigation">
      <ul class="pagination">
  
  
          <li class="disabled">
              <a href="#" aria-label="Previous">
                  <span aria-hidden="true">&laquo;</span>
              </a>
          </li>
  
          <li class="active"><a href="#">1</a></li>
          <li><a href="#">2</a></li>
          <li><a href="#">3</a></li>
          <li><a href="#">4</a></li>
          <li><a href="#">5</a></li>
  
  
          <li>
              <a href="#" aria-label="Next">
                  <span aria-hidden="true">&raquo;</span>
              </a>
          </li>
      </ul>
  </nav>
  ```

  



### 13_Bootstrap之插件

* 轮播图

  * 指示器
  * 轮播元素
  * 控制器

  ```html
  <div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
      <!-- Indicators -->
      <ol class="carousel-indicators">
          <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
          <li data-target="#carousel-example-generic" data-slide-to="1"></li>
          <li data-target="#carousel-example-generic" data-slide-to="2"></li>
      </ol>
  
      <!-- Wrapper for slides -->
      <div class="carousel-inner" role="listbox">
          <div class="item active">
              <img src="img/b1.jpg" alt="...">
              <div class="carousel-caption">
              </div>
          </div>
          <div class="item">
              <img src="img/b2.jpg" alt="...">
              <div class="carousel-caption">
              </div>
          </div>
  
          <div class="item">
              <img src="img/b3.jpg" alt="...">
              <div class="carousel-caption">
              </div>
          </div>
      </div>
  
      <!-- Controls -->
      <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
          <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
          <span class="sr-only">Previous</span>
      </a>
      <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
          <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
          <span class="sr-only">Next</span>
      </a>
  </div>
  ```

  







