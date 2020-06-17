# Cookie、Session会话技术

### 一、会话技术

#### 1.1概念

> 打开浏览器，访问服务器中资源，关闭浏览器；这个过程就是会话。

#### 1.2会话分类

> - Cookie会话技术；浏览器会话技术
> - Session会话技术；服务器会话技术

#### 1.3作用

> 解决ServletContext域对象、Request域对象存储数据所存在的问题
>
> - ServletContext域对象、Request域对象存在的问题
>   - ServletContext域对象可以看到所有人的购物车
>   - Request域对象，发起结算时购物车是空的

### 二、Cookie技术

#### 2.1介绍

> * 概念
>
>   * 网景公司发明。是浏览器的会话技术
>
> * Cookie的流程
>
>   * 浏览器请求服务器，请求Demo01Servlet，创建一个Cookie对象，名称为cookie1
> * 可以通过响应头Set-Cookie，携带cookie给浏览器进行保存
>   * 浏览器再次请求服务器，请求Demo02Servlet，获取cookie1对象

#### 2.2基本使用

>  * 设置Cookie
>
>    * 方式一（不推荐）
>
>      ```java
>      response.addHeader("set-cookie","msg=hellocoolie");
>      ```
>
>    * 方式二(推荐)
>
>      ```java
>      Cookie cookie = new Cookie("msg","hellocookie");
>      response.addCookie(cookie);
>      ```
>
> * 获取Cookie
>
>   * 开发步骤
>
>     * 通过request对象获取所有的Cookie对象，存储到一个数组中
>     * 遍历该数组，匹配Cookie名称
>     * 如果匹配上，就知道了指定的Cookie对象
>     * 如果匹配不上，就没有指定的Cookie对象
>
> * 代码实现
>
> ```java
> /**
> *	获取Cookie
> */
> public class Demo02Servlet extends HttpServlet {
>     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>         //Cookie随着请求发送到服务器
>         //获取请求中的所有Cookies对象
>         Cookie[] cookies = request.getCookies();
>         Cookie MsgCookie = null;
>         //获取名为msg的Cookie
>         for (Cookie cookie : cookies) {
>             if("msg".equals(cookie.getName())){
>                 //将Cookie存储到MsgCookie中
>                 MsgCookie = cookie;
>             }
>         }
>         //获取Cookie名称，Cookie值
>         if(MsgCookie != null){
>             System.out.println("Cookie的名称："+ MsgCookie.getName()+"Cookie的值"+ MsgCookie.getValue());
>         }
>     }
> 
> 
> ```
>
> 

#### 2.3Cookie的相关设置

##### 2.3.1持久化设置

> * cookie的生命周期
>
>   * 默认是随着浏览器的关闭而销毁
>
> * setMaxAge（）
>
>   * 设置cookie的存活时长，cookie就可以不随着会话的关闭而销毁！
>
>   [注意：方法中设置的单位是秒]()
>
>   ```java
>   public class Demo03Servlet extends HttpServlet {
>       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
>           Cookie cookie = new Cookie("msg","helloworld");
>           //想让cookie的存活时间为7天
>           cookie.setMaxAge(7 * 24 * 60 * 60);
>           response.addCookie(cookie);
>           //Cookie默认会跟随任何请求携带到浏览器
>   
>       }
>   ```

##### 2.3.2路径设置

> 默认情况下，Cookie对象会随着任何一个请求携带到服务器
>
> setPath（）
>
> * 设置Cookie的访问路径
>
> ```java
> Cookie cookie = new Cookie("msg","helloworld");
> cookie.setPath("/day56/demo04");
> response.addCookie(cookie);
> ```
>
> * cookie对象只有访问路径包含"/day56/demo04"，才会跟随请求携带到服务器

#### 2.4Cookie案例之记录上一次访问时间

> * 需求：
>
>   * 第一次访问，就直接打印当前时间
>   * 不是第一次访问，就打印上一次的访问时间
>
> * 开发步骤
>
>   * 获取对应的Cookie对象
>   * 判断是否是第一次访问
>   * 如果是第一次访问
>     * 打印当前时间
>     * 将当前时间存储到Cookie中
>   * 如果不是第一次访问
>     * 打印上一次访问时间
>     * 将当前时间存储到Cookie中

```java
/**
 *  Cookie案例之显示上一次访问时间
 */
@WebServlet(name = "Demo03Servlet",urlPatterns = "/demo03")
public class Demo03Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //判断是否是一次请求
        Cookie[] cookies = request.getCookies();
        Cookie cookie = null;//记录上一次访问时间
        if(cookies != null && cookies.length != 0){
            for (Cookie sonCookie : cookies) {
                //判断Cookie名称是否为lastTime，如果是，就将Cookie值存入到cookie中
                if("lastTime".equals(sonCookie.getName())){
                    cookie = sonCookie;
                }
            }
        }
        SimpleDateFormat format = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss");
        if(cookie == null){
            //第一次访问，打印当前时间，创建Cookie对象，存储当前时间
            Date currentDate = new Date();
            System.out.println("第一次访问，时间为："+ format.format(currentDate) );
            cookie = new Cookie("lastTime",currentDate.getTime() +"");
        }else {
            //不是第一次访问，从Cookie取出上一次访问时间，并打印，获取当前时间，存储到Cookie中
            //将字符串参数转化为Long类型十进制
            long lastDateMills = Long.parseLong(cookie.getValue());
            Date lastDate = new Date(lastDateMills);
            //获取到了上一次访问时间
            String lastTimeStr = format.format(lastDate);
            System.out.println("上一次访问时间为："+ lastTimeStr);
            //获取当前时间，并存储到Cookie中
            Date currentDate = new Date();
            cookie = new Cookie("lastTime",currentDate.getTime()+"");

        }
        //将cookie发送给浏览器
        response.addCookie(cookie);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```

#### 2.5Cookie案例之商品浏览记录+显示记录

> * 需求
>
>   * 浏览商品，将商品的浏览的记录起来，并显示！
> * 开发步骤（浏览记录）
>
>   * 获取history的Cookie对象
>   * 判断商品浏览记录是否为空
>   * 如果浏览记录没有
>     * 创建Cookie，并将当前的商品记录到Cookie中
>   * 如果浏览记录有
>     * 有当前的商品，不做任何处理
>     * 没有当前商品，就需要将当前的商品拼接到已有记录中
> * 开发步骤（显示记录）
>   * 获取history对应的Cookie对象
>   * 获取对应的商品浏览记录
>   * 判断是否有浏览记录
>   * 如果没有，就显示“没有浏览记录”
>   * 如果有，就显示
>     * 处理浏览记录字符串

- 代码实现：

  - 页面代码

  ```html
  <a href="/day56/history?id=0">西游记</a><br>
  <a href="/day56/history?id=1">红楼梦</a><br>
  <a href="/day56/history?id=2">水浒传</a><br>
  <a href="/day56/history?id=3">三国志</a><br>
  ```

  - CookieUtils工具类
    - 获取指定名称的Cookie对象

  ```java
  public class CookieUtils {
      public static Cookie getCookie(Cookie[] cookie,String cookieName){
          //判断cookie是否存在
          if(cookie != null && cookie.length != 0){
              for (Cookie sonCookie : cookie) {
                  if(cookieName.equals(sonCookie.getName())){
                      return sonCookie;
                  }
              }
          }
          return null;
      }
  }
  ```

  

  - 商品浏览界面

  ```java
  public class HistoryServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //利用CookieUtils工具类获取指定名称的cookie对象
          Cookie cookie = CookieUtils.getCookie(request.getCookies(), "history");
          //获得id参数值
          String id = request.getParameter("id");
          //判断是否有浏览记录
          if(cookie == null){
              //没有浏览记录，创建Cookie对象，并存储浏览记录(id)
               cookie = new Cookie("history",id);
          }else {
              //之前有一些浏览记录
              String historyStr = cookie.getValue();
              if(!historyStr.contains(id)){
                  //有一些纪录，但不包含当前浏览的商品，将浏览的商品拼接到浏览记录中
                  historyStr += "-" + id;
                  cookie.setValue(historyStr);
  
              }else {
                  ////有一些记录，包含当前浏览的商品 ，不做任何处理
              }
          }
          response.addCookie(cookie);
          //上述代码，已经完成了商品浏览记录功能，剩下就是要显示商品浏览记录
          //使用重定向
          response.sendRedirect("/Day56/showHistory");
      }
  ```

  - 商品显示界面

  ```java
  public class ShowStoryServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //获取商品浏览记录
          Cookie cookie = CookieUtils.getCookie(request.getCookies(), "history");
          //记录响应正文
          StringBuffer responseContent = new StringBuffer();
          //判断是否有浏览记录
          if(cookie == null){
              //没有浏览记录
              responseContent.append("<font color='red'>没有浏览记录</font>,");
              responseContent.append("<a href='books.html'>浏览商品</a>");
          }else {
              //有浏览记录
              //获取浏览记录
              String[] bookNames = {"红楼梦","水浒传","三国演义","西游记"};
              String historyStr = cookie.getValue();
              String[] historys = historyStr.split("-");
              responseContent.append("您的浏览记录如下：<br>");
              for (String history : historys) {
                  //Integer.parseInt()将字符串转化为int类型的十进制
                 String bookName = bookNames[Integer.parseInt(history)];
                 responseContent.append(bookName + "<br>");
              }
  
          }
          //设定编码集
          response.setContentType("text/html;charset=utf-8");
          //操作响应正文
          response.getWriter().write(responseContent.toString());
      }
  ```


### 三、Session技术

#### 3.1介绍

> * Cookie之所以叫做浏览器会话，原因是Cookie的数据存储到浏览器!
>
> * Session之所以叫做服务器会话，原因是Session的数据存储到服务器!
>
> * 执行流程
>
>   * 第一次请求Demo01Servlet时，根据request.getSession方法， 新建一个session对象；
>
>   * 当第一次响应时，会将该session对象的id作为cookie头响应给浏览器保存
>
>  ```xml
>  set-cookie:JSESSIONID=4741C65CC84788A204E87EB870196EB0
>  ```
>
>   * 第二次请求Demo01Servlet时，根据request.getSession方法，请求中会有cookie头
>
>  ```xml
>  Cookie:JSESSIONID=4741C65CC84788A204E87EB870196EB0
>  ```
>
>   * 会根据该JSESSIONID去服务器中找有没有对应的session对象，如果有就直接用，没有就新建!!!

#### 3.2相关配置

> * 生命周期
>
>   * session默认是有30分钟的存活时间，参考tomcat中的web.xml
>
>   ```xml
>       <session-config>
>           <session-timeout>30</session-timeout>
>       </session-config>		
>   ```
>
>   * session和cookie是相关联的，cookie中存储了jsessionid，request.getSession方法会根据jsessionid去选择，到底是新建session对象，还是引用原来的session对象；如果，将浏览器关闭了，就意味着cookie中存储的jsessionid就会销毁，对应request.getSession就会新建一个session对象，但是原来的session对象还存在！
>   * session.invalidate方法，立马将对应的session对象销毁！后续就会新建session!
>* 注意事项
> 
>  * 关闭浏览器，session会怎么样？
>     * 意味着浏览器中保存的jsession会销毁，服务器就会创建新的jsession对象，而原来的jsession对象等着过期。
>   * 销毁session，下一次的geSession怎么样？
>    * 意味着服务器中原有的jsession对象会销毁，浏览器再发起请求时所携带的jsessionid不能找到对应的jsession对象，服务器会创建一个新的jsession对象。
> * 总结
>
>   * session只有两种情况会销毁
>     * 调用了invalidate（）方法
>     * 过了30分钟

#### 3.3基本使用

> * setAttribute（）
>   * 往session域对象中存储数据
> * getAttribute（）
>   * 从session域对象中获取数据
> * removeAttribute（）
>   * 把session域对象中的数据移除

#### 3.4session案例之登录

- c3p0配置文件[严格按要求写，不可有空格]()

```properties
c3p0.driverClass=com.mysql.jdbc.Driver
c3p0.jdbcUrl=jdbc:mysql://localhost:3306/account
c3p0.user=root
c3p0.password=1234
```

- 连接池工具

```java
public class JDBCUtils {
    //随着JDBCUtils类的加载而加载，且只加载一次
    private static ComboPooledDataSource detaSource;
    static {
        detaSource = new ComboPooledDataSource();
    }
    //返回连接池对象
    public static ComboPooledDataSource getDetaSource(){
        return detaSource;
    }
}

```

- 登录功能

  - UserDaoImpl

  ```java
  public class UserDaoImpl implements UserDao {
      @Override
      public  User login(User inputUser) throws SQLException {
          QueryRunner queryRunner = new QueryRunner(JDBCUtils.getDetaSource());
  
          User existUser = queryRunner.query("select * from t_user where username = ? and password = ?",
                  new BeanHandler<User>(User.class),
                  inputUser.getUsername(),
                  inputUser.getPassword());
          return existUser;
  
      }
  }
  ```

  - login.html

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>登录</title>
  </head>
  <body>
      <form action="/day57/login" method="post">
          账号：<input type="text" name="username"><br>
          密码：<input type="text" name="password"><br>
          验证码：<input type="text" name="vaildateCode"><img src="/day57/creatCode"><br>
          <button type="submit">登录</button>
  
      </form>
  
  </body>
  </html>
  ```
```java
  
- LoginServlet
  
  ```java
  
  @WebServlet(name = "LoginServlet",urlPatterns = "/login")
  public class LoginServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //获取输入的验证码
          String vaildateCode = request.getParameter("vaildateCode");
          //将存入到session中的随机验证码取出
          Object existCode = request.getSession().getAttribute("existCode");
          if(vaildateCode.equals(existCode)){
              //校验成功，进入登录流程
              //获取到username和password的参数值
              String username = request.getParameter("username");
              String password = request.getParameter("password");
              //将获取到的参数值存入到一个User对象中
              User inputUser = new User();
              inputUser.setUsername(username);
              inputUser.setPassword(password);
              //将此对象传入到UserDaoImpl中的login方法中，判断是否会返回一个User对象
              UserDao userDao = new UserDaoImpl();
              try {
                  User existUser = userDao.login(inputUser);
                  //判断是否登陆成功
                  if(existUser == null){
                      //登录失败，跳转到登录界面
                      System.out.println("登录失败！");
                      request.getRequestDispatcher("/login.html").forward(request,response);
                  }else {
                      //登陆成功，将对象传入到session域中并跳转到显示用户信息
                      System.out.println("登录成功");
                      request.getSession().setAttribute("existUser",existUser);
                      response.sendRedirect("/day57/showIndex");
  
                  }
              } catch (SQLException e) {
                  e.printStackTrace();
              }
          }else {
              //校验失败，返回登录界面
              request.getRequestDispatcher("/login.html").forward(request,response);
          }
  
      }
  
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request, response);
    }
  }
```

  - ShowServlet

  ```java
  @WebServlet(name = "ShowServlet",urlPatterns = "/showIndex")
  public class ShowServlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          response.setContentType("text/html;charset=utf-8");
          //取出session中的existUser对象
          User existUser = (User) request.getSession().getAttribute("existUser");
          //判断是否在登录状态，不在登录状态则重新登陆
          if(existUser == null){
              //方式一：提示下，未登录
             	//response.getWriter().write("您还没有登录,<a href='/day57/login.html'>请登录</a>");
              //方式二：跳转到登录页面
              response.sendRedirect("/day57/login.html");
          }else {
              response.getWriter().write("登陆成功，欢迎"+existUser.getUsername());
          }
  
      }
  
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request, response);
    }
  }
  ```

  [注意事项：]()

  * 第三方jar包，必须放到WEB-INF文件夹中
  * 登录失败使用请求转发、登录成功使用重定向!


#### 3.5session案例之随机验证码

> 显示验证码
>
> 1. 创建图片对象
> 2. 画背景
> 3. 画边框
> 4. 画干扰线
> 5. 产生四位随机数，存储到session
> 6. 画四位随机数
> 7. 将图片响应到浏览器

- 显示验证码

```java

protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int width = 60;//定义图片宽度
        int height = 32;//定义图片高度
        //创建图片对象
        BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE_INT_RGB);
        //创建画笔对象
        Graphics g = image.getGraphics();
        //设置背景颜色
        g.setColor(new Color(0xDCDCDC));
        g.fillRect(0, 0, width, height);//实心矩形
        //设置边框
        g.setColor(Color.black);
        g.drawRect(0, 0, width - 1, height - 1);//空心矩形

        Random rdm = new Random();
        //画干扰椭圆
        for (int i = 0; i < 50; i++) {
            int x = rdm.nextInt(width);
            int y = rdm.nextInt(height);
            g.drawOval(x, y, 0, 0);
        }
        //产生随机字符串
        String hash1 = Integer.toHexString(rdm.nextInt());
        //生成四位随机验证码
        String capstr = hash1.substring(0, 4);
        //将产生的验证码存储到session域中，方便以后进行验证码校验!
        request.getSession().setAttribute("existCode", capstr);
        System.out.println(capstr);
        g.setColor(new Color(0, 100, 0));
        g.setFont(new Font("Candara", Font.BOLD, 24));
        g.drawString(capstr, 8, 24);
        g.dispose();
        //将图片响应到浏览器
        response.setContentType("image/jpeg");
        OutputStream strm = response.getOutputStream();
        ImageIO.write(image, "jpeg", strm);
        strm.close();
    }
```



- 校验验证码

```java
//获取输入的验证码
String validateCode = request.getParameter("validateCode");
//将输入的验证码和产生的随机验证码进行校验
String existCode = (String) request.getSession().getAttribute("existCode");
if (validateCode.equals(existCode)) {
    //校验通过，完成登录功能
} else {
    //校验不通过，跳转到登录页面

}
```

### 四、回顾自定义DBUtils

#### 4.1自定义DbUtils之增删改

> * 相同点
>
>   * 1，获取连接
>   * 4，执行sql语句
>   * 5，释放资源
>
> * 不同点
>
>   * 2，sql语句
>   * 3，设置参数

- 代码实现

```java
 /**
     * 增删改通用方法
     */
    public static void update(String sql,Object...parameters){
        //获取连接
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try {
            connection = JDBCUtils.getConnection();
            preparedStatement = connection.prepareStatement(sql);
            //循环看有多少个参数
            //设置参数值的时候，参照的是parameters的个数! 应该参照有多少个问号？
            ParameterMetaData parameterMetaData = preparedStatement.getParameterMetaData();
            for (int i = 0;i < parameterMetaData.getParameterCount();i++){
                preparedStatement.setObject(i+1,parameters[i]);
            }
            preparedStatement.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            JDBCUtils.release(connection,preparedStatement);
        }

    }
```

#### 4.2自定义DbUtils之查询

> * 相同点
>   * 1，获取连接
>   * 5，释放资源
> * 不同点
>   * 2，sql语句
>   * 3，设置参数
>   * 4，处理结果集

代码实现

* MyResultSetHandler接口

  * 处理结果集，并得到想要的类型的数据

  ```java
  public interface MyResultSetHandler<T> {
  
  
      /**
       * 处理结果集，并返回想要的类型的数据
       * @param resultSet 结果集
       * @return 要的类型的数据
       * @throws Exception
       */
      T handle(ResultSet resultSet) throws Exception;
  
  }
  ```

  - 通用query方法

  ```java
   /**
       * 查询通用方法
       */
      public static<T> T query(String sql,MyResuletsetHandler<T> handler,Object...parameters){
          Connection connection = null;
          PreparedStatement preparedStatement = null;
          ResultSet resultSet = null;
          try {
              connection = JDBCUtils.getConnection();
              preparedStatement = connection.prepareStatement(sql);
              for (int i = 0;i < preparedStatement.getParameterMetaData().getParameterCount();i++){
                  preparedStatement.setObject(i+1,parameters[i]);
              }
              resultSet = preparedStatement.executeQuery();
              T t = handler.handle(resultSet);
              return t;
          } catch (Exception e) {
              e.printStackTrace();
          }finally {
              JDBCUtils.release(connection,preparedStatement,resultSet);
          }
  
          return null;
      }
  ```

  - 测试代码

  ```java
  public static void main(String[] args) {
          User existUser = MyDBUtils.query("select * from t_user where id = ?",
                  new MyResuletsetHandler<User>() {
                      @Override
                      public User handle(ResultSet resultSet) throws Exception {
                          User user = null;
                          while (resultSet.next()) {
                              int id = resultSet.getInt("id");
                              String username = resultSet.getString("username");
                              String password = resultSet.getString("password");
                              user = new User(id, username, password);
                          }
                          return user;
                      }
                  }, 4);
          System.out.println(existUser);
      }
  ```

  * 存在的问题

    * 结果集的处理太麻烦，具体体现在处理结果集的具体实现上！！

  * 解决思路

    * 如果结果集处理之后返回的是单条记录，封装好一个MyBeanHandler
    * 如果结果集处理之后返回的是多条记录，封装好一个MyBeanListHandler

#### 4.3自定义DbUtils之MyBeanHandler

> * 概念
>
>   * 封装单条记录的结果集处理
>
> * 开发步骤
>
>   * MyResultSetHandler接口上的泛型由MyBeanHandler的泛型确定
>   * 声明一个Class对象的引用
>   * 重写handle方法

- 代码实现

```java
public class MyBeanHandler<T> implements  MyResultSetHandler<T> {

    private Class<T> clazz;//User类Class对象，也可以是Student类Class对象

    public MyBeanHandler(Class<T> clazz) {
        this.clazz = clazz;
    }

    @Override
    public T handle(ResultSet resultSet) throws Exception {
        T t = clazz.newInstance();
        //处理结果集
        while (resultSet.next()){
            //id属性值,username属性值,password属性值
            Field[] fields = clazz.getDeclaredFields();
            for (Field field : fields) {
                //字段名称
                String fieldName = field.getName();
                //字段值
                Object fieldValue = resultSet.getObject(fieldName);
                //将字段值设置Class对象对应的java实体对象
                //获取字段对应set方法
                String methodName = "set" + fieldName.substring(0,1).toUpperCase() + fieldName.substring(1);
                Method method = clazz.getMethod(methodName, field.getType());
                if (null != method) {
                    method.invoke(t,fieldValue);
                }
            }


        }
        return t;
    }
}
```

#### 4.4自定义DbUtils之MyBeanListHandler

> * 概念
>
>   * 封装多条记录的结果集处理
>
> * 开发步骤
>
>   * MyResultSetHandler接口上的泛型由MyBeanListHandler的泛型确定
>     * 已经确定了返回的是集合，只是不确定集合中的元素的类型
>     * MyBeanListHandler只确定集合中元素的类型就可以了
>   * 声明一个Class对象的引用
>   * 重写handle方法

- 代码实现

```java
public class MyBeanListHandler<T> implements MyResultSetHandler<List<T>> {

    private Class<? extends T> clazz;//集合中元素的Class对象

    public MyBeanListHandler(Class<? extends T> clazz) {
        this.clazz = clazz;
    }

    @Override
    public List<T> handle(ResultSet resultSet) throws Exception {
        List<T> list = new ArrayList<>();
        while (resultSet.next()) {
            //循环一次,就是一条记录,就是一个对象
            T t = clazz.newInstance();
            Field[] fields = clazz.getDeclaredFields();
            for (Field field : fields) {
                String fieldName = field.getName();
                Object fieldValue = resultSet.getObject(fieldName);
                //获取set方法
                String methodName = "set"+fieldName.substring(0,1).toUpperCase()+fieldName.substring(1);
                Method method = clazz.getMethod(methodName, field.getType());
                if (null != method) {
                    method.invoke(t,fieldValue);
                }
            }
            list.add(t);
        }
        return list;
    }
}
```

