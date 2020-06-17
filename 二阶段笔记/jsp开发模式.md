# JSP开发模式

### 1、Jsp模式

#### 1.1	jsp + javaBean模式

> * jsp
>   * 处理请求
>   * 业务处理
>   * 操作数据库
>   * 显示数据
> * javaBean
>   * 封装数据
>
> * 优缺点
>   * 开发简单，维护难；代码几乎都在jsp中。

#### 1.2	servlet + jsp + javaBean 模式

> * servlet
>   * 处理请求
>   * 业务处理
>   * 操作数据库
> * jsp
>   * 显示数据
> * javaBean
>   * 封装数据
> * 优缺点
>   * 开发较难，维护简单。



### 2、BeanUtils框架的使用

> * 概念
>
>   * 可以将请求参数封装到java对象中
>
> * 开发步骤
>
>   * 导包
>     * commons-beanutils-1.9.4.jar
>     * commons-collections-3.2.2.jar
>     * commons-logging-1.2.jar
>
>   

- 代码实现

```java
Map<String, String[]> map = request.getParameterMap();
User user = new User();
System.out.println(user);
try {
    //调用BeanUtils的populate方法
    BeanUtils.populate(user,map);
    System.out.println(user);
} catch (Exception e) {
    e.printStackTrace();
}
```

[注意：页面上的name属性值要和java对象中的属性名一致！]()

### 3、自定义BeanUtils框架

- 代码实现
  - MyBeanUtils

  ```java
  public class MyBeanUtils {
      /**
       * 将map集合中的请求参数值封装到对象t中
       *
       * @param t
       * @param map : 键：参数名称；值：一组参数值。
       * @param <T>
       */
      public static <T> void populate(T t, Map<String, ? extends Object> map) {
          //获取t的反射对象
          Class<?> clazz = t.getClass();
          //获取对应的对象所拥有的所有属性
          Field[] fields = clazz.getDeclaredFields();
          for (Field field : fields) {
              //获取各个属性名称
              String fieldName = field.getName();
              //拼接set方法
              String methodName = "set" + fieldName.substring(0, 1).toUpperCase() + fieldName.substring(1);
              System.out.println(methodName);
  
              //获取属性类型
              Class<?> type = field.getType();
              try {
                  //获得方法名
                  Method method = clazz.getMethod(methodName, type);
                  if (method != null) {
                      //第二个参数：请求参数的值
                      //id、username、password、age
                      Object object = map.get(fieldName);
                      if (object != null) {
                          //参数存在
                          //因为map集合的键为String类型，需要强转
                          String[] strs = (String[]) object;
                          //id,phone等为Integer类型，需要类型转换
                          if (type.getName().equals("java.lang.Integer")) {
                              //String类型转换为Integer类型后，方法执行
                              method.invoke(t, Integer.parseInt(strs[0]));
                          } else {
                              //本身为String类型，方法直接执行
                              method.invoke(t, strs[0]);
                          }
                      }
                  }
              } catch (Exception e) {
                  throw new MyNoSuchMethodException("field " + fieldName + " there is no setter method!!!");
              }
          }
      }
  }
  
  ```

  
  - MyNoSuchMethodException自定义异常

  ```java
  public class MyNoSuchMethodException extends RuntimeException{
  
      public MyNoSuchMethodException() {
      }
  
      public MyNoSuchMethodException(String message) {
          super(message);
      }
  
      public MyNoSuchMethodException(String message, Throwable cause) {
          super(message, cause);
      }
  
      public MyNoSuchMethodException(Throwable cause) {
          super(cause);
      }
  
      public MyNoSuchMethodException(String message, Throwable cause, boolean enableSuppression, boolean writableStackTrace) {
          super(message, cause, enableSuppression, writableStackTrace);
      }
  }
  ```

  ### 4、MVC设计模式
  
  > * 概念
  >
  >   * 它是一种软件设计典范，用一种业务逻辑，数据，界面分离的方式来组织代码，将业务逻辑聚集 到一个部件中，方便程序的重复使用，提高我们的开发效率。
  >   * jsp的model2模式是mvc设计模式的一种!!
  >
  > * 组成
  >
  >   * m
  >     * model
  >       * 数据封装
  >   * v
  >     * view
  >       * 显示页面
  >   * c
  >     * controller
  >       * 请求处理
  >       * 业务处理
  >       * 操作数据库
  >
  >   * 存在的弊端
  >     * c中的代码太多，职责不单一！需要使用到三层结构
  >
  > * 三层结构
  >
  >   * c
  >     * controller
  >       * 请求处理
  >     * service
  >       * 业务处理
  >     * dao
  >       * 操作数据库

### 4、javaWeb综合案例

#### 4.1	jsp优化准备工作

> * 环境准备
>
>   * tomcat8.5
>   * idea2020.1
>   * jdk1.8
>
> * 导入jar包
>
>   * BeanUtils
>   * DbUtils
>   * c3p0
>   * mysql驱动
>   * jstl

#### 4.2	综合案例三层结构优化之登录

> 开发流程
>
> * UserServlet
>   * login方法
>     * 调用UserService的login方法
> * UserService
>   * login方法，返回User对象
>     * 调用UserDao的login方法
> * UserDao
>   * login方法，返回User对象
>     * 操作数据库，并将记录封装到User对象
> * 登录成功
>   * 修改登录状态，重定向到首页
> * 登录失败
>   * 记录错误信息，请求转发到登录页面

- 代码实现

  - UserDao

  ```java
  /**
   * 操作数据库
   */
  public class UserDaoImpl implements UserDao {
      QueryRunner queryRunner = new QueryRunner(JDBCUtil.getDataSource());
      @Override
      public List<User> selectUserList() throws Exception {
          return queryRunner.query("select * from t_user",
                  new BeanListHandler<User>(User.class));
  
      }
  
      @Override
      public User Login(User inputUser) throws Exception {
          return queryRunner.query("select * from t_user where username = ? and password = ?",
                  new BeanHandler<User>(User.class),
                  inputUser.getUsername(),
                  inputUser.getPassword());
      }
  
      @Override
      public int deleteUserById(Integer id) throws Exception {
          return queryRunner.update("delete from t_user where id = ?",
                  id);
  
      }
  
      @Override
      public User selectUserById(Integer id) throws Exception {
          return queryRunner.query("select * from t_user where id = ?"
                  ,new BeanHandler<User>(User.class),id);
      }
  
      @Override
      public void updateUserById(User inputUser) throws Exception {
          queryRunner.update("update t_user set username = ?,password = ? where id = ?",
                  inputUser.getUsername(),
                  inputUser.getPassword(),
                  inputUser.getId());
      }
  
  
  }
  ```

  - UserService

  ```java
  /**
   * 业务处理
   */
  public class UserServiceImpl implements UserService {
  
  
      UserDao userDao = new UserDaoImpl();
      @Override
      public List<User> selectUserList() throws Exception {
          return userDao.selectUserList();
      }
  
      @Override
      public User Login(User inputUser) throws Exception {
          return userDao.Login(inputUser);
      }
  
      @Override
      public boolean deleteUserById(Integer id) throws Exception {
          return userDao.deleteUserById(id) == 1;
      }
  
      @Override
      public User selectUserById(Integer id) throws Exception {
          return userDao.selectUserById(id);
      }
  
      @Override
      public void updateUserById(User inputUser) throws Exception {
          userDao.updateUserById(inputUser);
      }
  }
  
  ```

  - UserServlet类的login方法

  ```java
   /**
       * 登录操作
       * @param request
       * @param response
       * @return
       */
      public String login(HttpServletRequest request ,HttpServletResponse response){
          private UserService userService = new UserServiceImpl();
          User inputUser = new User();
          try {
              //将请求参数封装到inputUser中
              BeanUtils.populate(inputUser,request.getParameterMap());
              User existUser = userService.Login(inputUser);
              //判断existUser是否存在
              if(existUser != null){
                  //修改登录状态，并跳转到selectUserList,由selectUserList跳转到首页
                  request.getSession().setAttribute("existUser",existUser);
                  return "response:/user?methodName=selectUserList";
              }else {
                  //用户不存在，记录错误信息，跳转到登录界面
                  request.setAttribute("errorMsg","账户或密码错误");
                  return "/login.jsp";
              }
  
          } catch (Exception e) {
              e.printStackTrace();
          }
          //有异常，应该有返回值 。意味着登录失败，返回登录页面，重新登录
          return "/login.jsp";
      }
  ```

  
  - login.jsp

  ```jsp
  <body>
  <font color="red">${errorMsg}</font>
  <form action="${pageContext.request.contextPath}/user" method="post">
      <input type="hidden" name="methodName" value="login">
      账户：<input type="text" name="username"><br>
      密码：<input type="text" name="password"><br>
      <button type="submit">登录</button>
  
  </form>
  
  </body>
  ```

  - index.jsp

  ```jsp
  <body>
      欢迎回来~~~${existUser.username} <a href="${pageContext.request.contextPath}/user?methodName=logout">注销</a>
      <table border="1px" cellspacing="0px" cellpadding="15px" width="500px" heigh="200px">
        <tr>
          <td>ID</td>
          <td>账户</td>
          <td>密码</td>
          <td>操作</td>
        </tr>
  
        <c:forEach items="${userList}" var="user">
          <tr>
            <td>${user.id}</td>
            <td>${user.username}</td>
            <td>${user.password}</td>
            <td>
              <a href="${pageContext.request.contextPath}/user?methodName=deleteUserById&id=${user.id}">删除</a>
              <a href="${pageContext.request.contextPath}/user?methodName=toUpdateUserById&id=${user.id}">修改</a>
            </td>
          </tr>
        </c:forEach>
  
      </table>
  
    </body>
  ```

#### 4.3 综合案例三层结构优化之注销登录

> 开发步骤
>
> * login.jsp上需要加一个“注销”的按钮
> * 注销成功
>   * 跳转到登录页面
> * 注销失败
>   * 跳转到首页，重新进行手动注销

#### 4.4 综合案例三层结构优化之用户列表

> 开发步骤
>
> * 登录成功，重定向到UserServlet中的selectUserList方法
> * 在selectUserList方法中获取用户列表，并将其保存
> * 再请求转发到index.jsp

- 代码实现

  - UserDao

  ```java
      @Override
      public List<User> selectUserList() throws Exception {
          return new QueryRunner(JDBCUtils.getDataSource())
                  .query("select * from tb_user",
                          new BeanListHandler<User>(User.class));
      }
  ```

  - UserServlet类的selectUserList方法

  ```java
      public String selectUserList(HttpServletRequest request,HttpServletResponse response) throws Exception {
          List<User> userList = userService.selectUserList();
          request.getSession().setAttribute("userList",userList);
          return "/index.jsp";
      }
  ```

  - index.jsp

  ```jsp
  <body>
  
    <%--
    在登录状态
      显示用户名
    --%>
      <c:if test="${existUser != null}">
          欢迎回来~~~  ${existUser.username}  <a href="${pageContext.request.contextPath}/user?methodName=logout">注销</a>
          <%--显示用户列表--%>
          <table border="1px" cellspacing="0px" cellpadding="15px" width="500px" height="200px">
              <tr>
                  <td>ID</td>
                  <td>账户</td>
                  <td>密码</td>
              </tr>
  
              <c:forEach items="${userList}" var="user">
                  <tr>
                      <td>${user.id}</td>
                      <td>${user.username}</td>
                      <td>${user.password}</td>
                  </tr>
              </c:forEach>
  
  
          </table>
      </c:if>
  
    <%--
    不在登录状态
       提示登录
    --%>
      <c:if test="${existUser == null}">
          您还没有登录，<a href="${pageContext.request.contextPath}/login.jsp">请登录</a>
      </c:if>
  
  </body>
  ```

  #### 4.4 综合案例之登录校验

  > * 需求：
  >
  >   * 只要不在登录状态就自动跳转到登录页面
  >
  > * 开发步骤
  >
  >   * 定义过滤器
  >   * 判断是否和登录相关
  >   * 和登录相关，直接放行
  >     * 访问登录页面
  >     * 处理登录，请求参数methodName="login"
  >   * 和登录无关，进行登录状态判断
  >     * 不在登录状态，跳转到login.jsp
  >     * 在登录状态，直接放行

```java
@WebFilter(filterName = "LoginFilter",urlPatterns = "/*")
public class LoginFilter implements Filter {
    public void destroy() {
    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {

        HttpServletRequest request = (HttpServletRequest) req;
        HttpServletResponse response = (HttpServletResponse) resp;
        //获取登陆路径,和方法参数
        String requestURI = request.getRequestURI();
        String methodName = request.getParameter("methodName");
        //判断登陆路径是否包含登录资源
        if(requestURI.contains("login") ||(methodName != null && methodName.equals("login"))){
            //和登录相关的资源，直接放行
            chain.doFilter(request, response);
        }else {
            //和登录无关的资源，判断是否在登录状态
            User existUser = (User) request.getSession().getAttribute("existUser");
            if(existUser != null){
                //在登录状态，直接放行
                chain.doFilter(request, response);
            }else {
                //不在登录状态,返回登录界面
                request.getRequestDispatcher("/login.jsp").forward(request,response);

            }
        }



    }

    public void init(FilterConfig config) throws ServletException {

    }

}

```

#### 4.5 综合案例三层结构优化之删除用户

> 开发步骤
>
> * 给table每一行加删除按钮
> * 不管是删除成功，还是删除失败，都应该重新获取用户列表并显示
>   * 转发到UserServlet类的selectUserList方法

- 代码实现

  - index.jsp

  ```jsp
  ......
  
  <c:forEach items="${userList}" var="user">
      <tr>
          <td>${user.id}</td>
          <td>${user.username}</td>
          <td>${user.password}</td>
          <td>
              <a href="${pageContext.request.contextPath}/user?methodName=deleteUserById&id=${user.id}">删除</a>
          </td>
      </tr>
  </c:forEach>
  
  ......
  ```

  - UserDao

  ```java
      @Override
      public int deleteUserById(Integer id) throws Exception {
          return new QueryRunner(JDBCUtils.getDataSource())
                  .update("delete from tb_user where id = ?",
                          id);
      }
  ```

  - UserService

  ```java
      @Override
      public boolean deleteUserById(Integer id) throws Exception {
          return userDao.deleteUserById(id) == 1;
      }
  ```

  - UserServlet的deleteUserById方法

  ```java
    public String deleteUserById(HttpServletRequest request,HttpServletResponse response){
          Integer id = Integer.parseInt(request.getParameter("id"));
          try {
              boolean flag = userService.deleteUserById(id);
          } catch (Exception e) {
              e.printStackTrace();
          }
          //获取用户列表
          return "/user?methodName=selectUserList";
      }
  ```

  #### 4.6 综合案例三层结构优化之修改用户

  > 开发步骤
  >
  > * 在table的每一行中加修改按钮
  > * 当点击table中修改按钮，跳转到UserServlet类中的toUpdateUserById方法
  > * UserServlet类中的toUpdateUserById方法
  >   * 获取用户信息
  >   * 跳转到修改用户页面
  > * 当点击修改页面中的修改按钮，开始修改
  >   * 修改成功，跳转到UserServlet类中的selectUserList方法
  >   * 修改失败，跳转到toUpdateUserById方法，让它重新进行修改用户

- 代码实现

  - UserDao

  ```java
      @Override
      public void updateUserById(User inputUser) throws Exception {
          new QueryRunner(JDBCUtils.getDataSource())
                  .update("update tb_user set username = ? , password = ? where id = ?",
                          inputUser.getUsername(),
                          inputUser.getPassword(),
                          inputUser.getId());
      }
  ```

  - UserServlet类toUpdateUserById方法

  ```java
      public String toUpdateUserById(HttpServletRequest request,HttpServletResponse response) {
          Integer id = Integer.parseInt(request.getParameter("id"));
          User user = null;
          try {
              user = userService.selectUserById(id);
          } catch (Exception e) {
              e.printStackTrace();
          }
          request.setAttribute("user",user);
          return "/updateUser.jsp";
  
      }
  ```

  - updateUser.jsp

  ```jsp
  <body>
  <font color="red">${errorMsg}</font>
  <form action="${pageContext.request.contextPath}/user" method="post">
  
      <input type="hidden" name="methodName" value="updateUserById"/>
      <input type="hidden" name="id" value="${user.id}">
      账户:<input type="text" name="username" value="${user.username}"><br>
      密码:<input type="text" name="password" value="${user.password}"><br>
      <button type="submit">修改</button>
  </form>
  
  </body>
  ```

  - UserServlet类updateUserById方法

  ```java
      public String updateUserById(HttpServletRequest request,HttpServletResponse response){
          User inputUser = new User();
          try {
  
              BeanUtils.populate(inputUser,request.getParameterMap());
              userService.updateUserById(inputUser);
              //修改成功
              return "/user?methodName=selectUserList";
          } catch (Exception e) {
              e.printStackTrace();
          }
          request.setAttribute("errorMsg","修改失败");
          //修改失败
          return "/user?methodName=toUpdateUserById&id="+inputUser.getId();
      }
  ```

  