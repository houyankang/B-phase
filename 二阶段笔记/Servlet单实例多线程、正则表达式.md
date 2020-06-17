### 01_Servlet的单实例多线程

> * 概念
>   * tomcat服务器根据server.xml中的Connector配置初始化线程池
>   * 当第一次请求发起时，会调度线程池分配线程处理请求，实例一个Serlvet对象
>   * 当第二次请求发起时，会再次调度线程池分配新的线程处理请求，会沿用之前Servlet对象
> * 线程安全问题
>   * 成员变量，值会发生改变，存在线程安全问题
>   * 成员变量，值不会发生改变，不存在线程安全问题
>   * 局部变量，不同的线程持有不同的局部变量，所以，不存在线程安全问题
>





### 02_自定义tomcat服务器

> * tomcat服务器执行原理
>
>   * 操作请求行、请求头、请求正文
>   * 操作响应行、响应头、响应正文
>
> * 自定义服务器
>
>   * 模仿tomcat服务器
>   * 操作请求行
>   * 操作响应行、响应头、响应正文
>
> * 代码实现
>
> ```java
> public class MyTomcatServer {
>     public static void main(String[] args) {
>         try {
>             //设置服务器端口
>             ServerSocket serverSocket = new ServerSocket(8806);
>             //获接收对应的请求
>             Socket socket = serverSocket.accept();
>             //处理请求行,获取访问资源的路径
>             InputStream inputStream = socket.getInputStream();
>             //转换成字符流
>             InputStreamReader reader = new InputStreamReader(inputStream);
>             //封装成了高效字符流
>             BufferedReader bufferedReader = new BufferedReader(reader);
>             
>             //请求方式、请求路径、协议；其中，只有请求路径有用!
>             String line = bufferedReader.readLine();
>             //"GET /day67/index.html HTTP/1.1"
>             String[] split = line.split(" ");
>             //  /day67/index.html
>             String requestURL = split[1];
>             int length = "/day67/".length();
>             //获取请求资源的相对路径  :index.html
>             requestURL = requestURL.substring(length);
>             //通过服务器将index.html响应给浏览器 ,  通过socket.getOutputStream();
>             BufferedInputStream bis = new BufferedInputStream(new FileInputStream(requestURL));
>             OutputStream outputStream = socket.getOutputStream();
>             BufferedOutputStream bos = new BufferedOutputStream(outputStream);
>             //操作响应行 （协议、响应状态码）
>             bos.write("HTTP/1.1 200 OK\r\n".getBytes());
>             //操作响应头(Content-Type)
>             bos.write("Content-Type:text/html\r\n".getBytes());
>             bos.write("\r\n".getBytes());
>             //操作响应正文
>             System.out.println(requestURL);
> 
>             int len = -1;
>             byte[] bys = new byte[8192];
>             while ((len = bis.read(bys)) != -1) {
>                 bos.write(bys,0,len);
>             }
>             bis.close();
>             bos.close();
> 
>         } catch (Exception e) {
>             e.printStackTrace();
>         }
>     }
> 
> }
> 
> ```
>
> 
>

### 03_自定义tomcat服务器优化

> * 存在问题
>   * 服务器只能接收一次请求
>   * 服务器是单线程
>
> * 解决方案
>
>   * 加入无限循环
>   * 加入多线程
>
> * 代码实现
>
>   ```java
>       public static void main(String[] args) {
>           try {
>               ServerSocket serverSocket = new ServerSocket(8282);
>               while (true) {
>                   //阻塞
>                   //没有请求时，阻塞这个代码，不会创建线程
>                   Socket socket = serverSocket.accept();
>                   new Thread(){
>                       @Override
>                       public void run() {
>                           try {
>   
>                               //处理请求行,获取访问资源的路径
>                               InputStream inputStream = socket.getInputStream();
>                               //转换流
>                               InputStreamReader reader = new InputStreamReader(inputStream);
>                               //封装成了高效字符流
>                               BufferedReader bufferedReader = new BufferedReader(reader);
>                               //"GET /day67_02/index.html HTTP/1.1"
>                               //请求方式、请求路径、协议；其中，只有请求路径有用!
>                               String line = bufferedReader.readLine();
>                               String[] requestInfos = line.split(" ");
>                               String requestURL = requestInfos[1];
>                               System.out.println(requestURL);
>                               int length = "/day67/".length();
>                               //获取请求资源的相对路径
>                               requestURL = requestURL.substring(length);
>   
>                               //通过服务器将index.html响应给浏览器 ,  通过socket.getOutputStream();
>   
>                               OutputStream outputStream = socket.getOutputStream();
>                               BufferedOutputStream bos = new BufferedOutputStream(outputStream);
>                               //操作响应行 （协议、响应状态码）
>                               bos.write("HTTP/1.1 200 OK\r\n".getBytes());
>                               //操作响应头(Content-Type)
>                               bos.write("Content-Type:text/html\r\n".getBytes());
>                               bos.write("\r\n".getBytes());
>                               //操作响应正文
>                               BufferedInputStream bis = new BufferedInputStream(new FileInputStream(requestURL));
>                               int len = -1;
>                               byte[] bys = new byte[8192];
>                               while ((len = bis.read(bys)) != -1) {
>                                   bos.write(bys,0,len);
>                               }
>                               bis.close();
>                               bos.close();
>                           } catch (Exception e) {
>                               e.printStackTrace();
>                           }
>   
>                       }
>                   }.start();
>   
>               }
>   
>   
>           } catch (Exception e) {
>               e.printStackTrace();
>           }
>   
>   
>       }
>   ```
>
>   
>

### 04_正则表达式概念及基本使用

> * 概念
>
>   * 是指一个用来描述或者匹配一系列符合某个语法规则的字符串的单个字符串。其实就是一种 规则。有自己特殊的应用。
>
> * 作用
>
>   * 主要是用来做表单的内容的规则校验
>
> * 基本使用
>
>   * 需求
>
>     * 键盘录入一个qq号码，要求该号码长度在5~15之间，不能以0开头，必须全部都是数字
>
>   * 代码实现
>
>     * 传统方式
>
>     ```java
>             Scanner scanner = new Scanner(System.in);
>             while (true) {
>                 System.out.println("请输入您的qq号码:");
>                 String qqStr = scanner.nextLine();
>                 //判断qq号码的长度
>                 if (qqStr.length() >= 5 && qqStr.length() <= 15) {
>                     if (!qqStr.startsWith("0")) {
>                         //获取字符串中每一个字符
>                         boolean isNum = true;//记录是否是一个数字，只要字符串中有一个字符不是数字，那么就为false
>                         for (int i = 0; i < qqStr.length(); i++) {
>                             char chr = qqStr.charAt(i);
>                             //判断字符是否是数字
>                             //12ac345
>                             if (!Character.isDigit(chr)) {
>                                 //该字符不是一个数字
>                                 isNum = false;
>                                 break;
>                             }
>                         }
>                         //判断字符串是否都是数字
>                         if (isNum) {
>                             System.out.println("您的qq号，很棒哟~~~");
>                         } else {
>                             System.out.println("必须都是数字");
>                         }
>     
>                     } else {
>                         System.out.println("不能以0开头");
>                     }
>                 } else {
>                     System.out.println("qq号码的长度不对!");
>                 }
>     
>             }
>     ```
>
>     * 正则表达式
>
>     ```java
>             Scanner scanner = new Scanner(System.in);
>             while (true) {
>                 System.out.println("请输入您的qq号码:");
>                 String qqStr = scanner.nextLine();
>                 //qq号正则表达式
>                 String reg = "[1-9]{1}[0-9]{4,14}";
>                 System.out.println( qqStr.matches(reg) ? "qq号很不错哟~~~" : "qq号格式有误!" );
>             }
>     ```
>
>     
>

### 05_正则表达式之字符类

> * 概念
>   * 规定字符串的内容!
> * 常见规则
>   * [abc]
>     * 任意一个字符，要么是a，要么是b，要么是c
>   * [^abc]
>     * 任意一个字符串，不可以是a、b、c
>   * [a-zA-Z]
>     * 任意一个字符，范围在：a-z之间或A-Z之间
>   * [0-9]
>     * 任意一个字符，范围在0-9之间
> * 注意事项
>   * 只要没有标明长度，那么默认长度就是1！！！
>



### 06_正则表达式之预定义字符类

> * 概念
>   
>   * 一些有特定含义的表达式
>   
> * 作用
>   
>   * 减少编写正则表达式的麻烦
>   
> * 常见预定义字符
>   ```
>   . 任何字符。
>   \d 数字：[0-9]
>   \D 非数字:[^0-9]
>   \w 单词字符：[a-zA-Z_0-9]
>   \W 非单词字符:[^\w]
>   \s 空白字符:[ \t\n\x0B\f\r]
>   \S 非空白字符:[^\s]
>   ```
>
> * 代码实现
>
>   ```java
>   //        . 任何字符。
>           String reg1 = ".";
>           System.out.println(">a".matches(reg1));
>   //        \d 数字：[0-9]
>           String reg2 = "\\d";
>           System.out.println("11".matches(reg2));
>   //        \D 非数字:[^0-9]
>           String reg3 = "[^0-9]";
>           System.out.println("a".matches(reg3));
>           String reg4 = "\\D";
>           System.out.println("1".matches(reg4));
>   //        \w 单词字符：[a-zA-Z_0-9]
>           String reg5 = "\\w";
>           System.out.println("_".matches(reg5));
>           String reg6 = "[a-zA-Z0-9_]";
>           System.out.println("_".matches(reg6));
>   //        \W 非单词字符:[^\w]
>           String reg7 = "[^a-zA-Z0-9_]";
>           System.out.println("a".matches(reg7));
>           String reg8 = "[^\\w]";
>           System.out.println("!".matches(reg8));
>           String reg9 = "[\\W]";
>           System.out.println("!".matches(reg9));
>   //        \s 空白字符:[ \t\n\x0B\f\r]
>           String reg10 = "\\s";
>           System.out.println(" ".matches(reg10));
>   //        \S 非空白字符:[^\s]
>           String reg11 = "\\S";
>           System.out.println("!".matches(reg11));
>   ```
>
>   
>
> * 注意事项
>
>   * 正则表达式中，如果没有写[]，那么就会给每一个字符加[]
>
>   * 比如：
>
>     ```java
>     "abc" == "[a][b][c]"
>     ```
>
>   * 代码实现
>
>     ```java
>             String reg1 = "[abc]";//任意一个字符，要么是a、b、c
>             String reg2 = "[a][b][c]";//等价于"abc" ,正则表达式中，如果没写[]，会给每个字符加[]!!!
>             System.out.println("a".matches(reg1));//true
>             System.out.println("a".matches(reg2));
>             System.out.println("---------------");
>             System.out.println("abc".matches(reg1));//false
>             System.out.println("abc".matches(reg2));//true
>     ```
>
>     
>

### 07_正则表达式之数量词

> * 概念
>
>   * 规定某一个字符的长度
>
> * 常见数量词
>
>   * X：要么是一个字符类、要么是一个预定义字符类
>
>   ```java
>   X?：X，要么只有一个，要么没有
>   X*：X，从0次到多次
>   X+：X，从1次到多次
>   X{n}：X,正好n次    
>   X{n,}：X，从n次到多次
>   X{n,m}：X，从n次到m次    
>   ```
>
> * 代码实现
>
>   ```java
>   //        X? :X，一次或一次也没有
>           String reg1 = "[a]?";//要么是“a”要么什么都没有
>           System.out.println("aaa".matches(reg1));
>   //        X* :X，零次到多次
>           String reg2 = "[a]*";
>           System.out.println("b".matches(reg2));
>   //        X+ :X，一次到 多次
>           String reg3 = "[a]+";
>           System.out.println("".matches(reg3));
>   //        X{n} :X，恰好 n 次
>           String reg4 = "[ab]{3}";//内容由a或b组成，长度为3
>           System.out.println("aaa".matches(reg4));
>   //        X{n,} :X，至少 n 次
>           //0次到多次
>           String reg5 = "[abc]{0,}";//内容由a组成，0次到多次!
>           System.out.println("aaaa".matches(reg5));
>           //1次到多次
>           String reg6 = "[a]{1,}";
>           System.out.println("".matches(reg6));
>   //        X{n,m} :X，至少 n 次，但是不超过 m 次
>           String reg7 = "[abc]{2,3}";
>           System.out.println("abc".matches(reg7));
>   ```
>
>   
>

### 08_正则表达式的分割功能

> * 需求
>
>   * "a,b,c,d"、 "a,,b,,c,,d"、 "a,b,,c,,,d"、 "a,,b,,,c,d,,,,,e" 将以上四个字符串按照逗号进行分割。
>
> * 代码实现
>
>   ```java
>   //        "a,b,c,d"
>           String str1 = "a,b,c,d";
>           String reg1 = "[,]{1}";
>           String[] strs1 = str1.split(reg1);
>           for (String str : strs1) {
>               System.out.println(str);
>           }
>           System.out.println("-----------");
>   //        "a,,b,,c,,d"
>           String str2 = "a,,b,,c,,d";
>   //        String reg2 = ",,";
>           String reg2 = "[,]{2}";
>           String[] strs2 = str2.split(reg2);
>           for (String str : strs2) {
>               System.out.println(str);
>           }
>           System.out.println("-----------");
>   //        "a,b,,c,,,d"
>           String str3 = "a,b,,c,,,d";
>           String reg3 = "[,]{1,3}";
>           String[] strs3 = str3.split(reg3);
>           for (String str : strs3) {
>               System.out.println(str);
>           }
>           System.out.println("-----------");
>   //        "a,,,,,,,,,b,,,,,,,,,c,,,,,d,,,,,,,,e"
>           String str4 = "a,,,,,,,,,b,,,,,,,,,c,d,,,,,,,,e";
>           String reg4 = "[,]+";
>           String[] strs4 = str4.split(reg4);
>           for (String str : strs4) {
>               System.out.println(str);
>           }
>   ```
>
>   
>

### 09_Pattern类和Matcher类

> * Pattern类
>
>   * 相当于就是正则表达式，现在是正则对象
>
> * Matcher类
>
>   * 匹配对象，完成匹配功能等
>
> * 经典调用
>
>   ```java
>           //正则表达式
>           String reg = "[a]{3}";
>           //正则表达式 转换为 正则对象
>           Pattern pattern = Pattern.compile(reg);
>           //匹配字符串，匹配对象
>           Matcher matcher = pattern.matcher("aaa");
>           //开始匹配
>           boolean flag = matcher.matches();
>           System.out.println(flag);
>   ```
>
>   
>

### 10_正则表达式的获取功能

> * 需求
>
>   * 把一个字符串中的手机号码获取出来
>
> * 方法介绍
>
>   * Matcher类
>     * find方法：在字符串中找到和正则匹配得上的子字符串，如果找到了返回true，否则返回false
>     * group方法：获取字符串中找到和正则匹配得上的子字符串
>
> * 代码实现
>
>   ```java
>           String str = "18627775385...fadsfds18627775383..dsfjdsa18627775384";
>           String reg = "[1]{1}[356789]{1}\\d{9}";
>           //获取正则对象
>           Pattern pattern = Pattern.compile(reg);
>           //获取匹配对象
>           Matcher matcher = pattern.matcher(str);
>           //开始查找手机号
>           //find:在str中找子字符串，子字符串要和正则匹配
>           List<String> phones = new ArrayList<>();
>           while (matcher.find()) {
>               //找到了手机号，获取手机号
>               String phone = matcher.group();
>               phones.add(phone);
>           }
>   
>           for (String phone : phones) {
>               System.out.println(phone);
>           }
>   ```
>
>   

### 11_正则表达式综合案例

> 需求
>
> * 创建一个User对象，有三个字段：账户、密码、邮箱，有如下要求： 
>   * a.账户： 由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10 [A-Z]{1}[a-zA-Z0-9]{5,9} 
>   * b.密码: 由数字、字母和_组成，第一位置上必须是字母，长度为6 [a-zA-Z]{1}\w{5} 
>   * c.邮箱： 由字母、@和.组成，长度范围为8~10,必须是qq邮箱 [a-zA-Z]{1,3}@qq\.com

- 代码实现

  - MyIllegalArgumentsException.java

  ```java
  package com.qfedu.exception;
  
  public class MyIllegalArgumentsException extends RuntimeException{
  
  
      public MyIllegalArgumentsException() {
      }
  
      public MyIllegalArgumentsException(String message) {
          super(message);
      }
  
      public MyIllegalArgumentsException(String message, Throwable cause) {
          super(message, cause);
      }
  
      public MyIllegalArgumentsException(Throwable cause) {
          super(cause);
      }
  
      public MyIllegalArgumentsException(String message, Throwable cause, boolean enableSuppression, boolean writableStackTrace) {
          super(message, cause, enableSuppression, writableStackTrace);
      }
  }
  
  ```

  - User.java

  ```java
  package com.qfedu.bean;
  
  import com.qfedu.exception.MyIllegalArgumentsException;
  
  public class User {
  
      private String username;//由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10
      private String password;//由数字、字母和_组成，第一位置上必须是字母，长度为6
      private String email;//由字母、@和.组成，长度范围为8~10,必须是qq邮箱
  
  
      public User() {
      }
  
      public User(String username, String password, String email) {
          if (validateUsername(username)) {
              this.username = username;
          } else {
  //            System.out.println("账户错误，由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10");
              throw new MyIllegalArgumentsException("账户错误，由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10");
          }
          if (validatePassword(password)) {
              this.password = password;
          } else {
  //            System.out.println("密码错误，由数字、字母和_组成，第一位置上必须是字母，长度为6");
              throw new MyIllegalArgumentsException("密码错误，由数字、字母和_组成，第一位置上必须是字母，长度为6");
          }
          if (validateEmail(email)) {
              this.email = email;
          } else {
  //            System.out.println("邮箱错误，由字母、@和.组成，长度范围为8~10,必须是qq邮箱");
              throw new MyIllegalArgumentsException("邮箱错误，由字母、@和.组成，长度范围为8~10,必须是qq邮箱");
          }
  
      }
  
      public String getUsername() {
          return username;
      }
  
      public void setUsername(String username) {
          //设置用户名之前校验
          boolean flag = validateUsername(username);
          if (flag) {
              this.username = username;
          } else {
  //            System.out.println("账户错误，由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10");
              throw new MyIllegalArgumentsException("账户错误，由数字和字母组成,第一个位置上必须是大写字母，长度范围为6~10");
          }
  
  
      }
  
      public String getPassword() {
          return password;
      }
  
      public void setPassword(String password) {
          boolean flag = validatePassword(password);
          if (flag) {
              this.password = password;
          } else {
  //            System.out.println("密码错误，由数字、字母和_组成，第一位置上必须是字母，长度为6");
              throw new MyIllegalArgumentsException("密码错误，由数字、字母和_组成，第一位置上必须是字母，长度为6");
          }
  
      }
  
      public String getEmail() {
          return email;
      }
  
      public void setEmail(String email) {
          if (validateEmail(email)) {
              this.email = email;
          } else {
  //            System.out.println("邮箱错误，由字母、@和.组成，长度范围为8~10,必须是qq邮箱");
              throw new MyIllegalArgumentsException("邮箱错误，由字母、@和.组成，长度范围为8~10,必须是qq邮箱");
          }
  
      }
  
      @Override
      public String toString() {
          return "User{" +
                  "username='" + username + '\'' +
                  ", password='" + password + '\'' +
                  ", email='" + email + '\'' +
                  '}';
      }
  
      /**
       * 校验用户名
       */
      private boolean validateUsername(String username){
          String reg = "[A-Z]{1}[a-zA-Z0-9]{5,9}";
          boolean matches = username.matches(reg);
          return matches;
      }
  
      /**
       * 校验密码
       */
      private boolean validatePassword(String password){
          String reg = "[a-zA-Z]{1}\\w{5}";
          boolean matches = password.matches(reg);
          return matches;
      }
  
      /**
       * 校验邮箱
       */
      private boolean validateEmail(String email){
          String reg = "[a-zA-Z]{1,3}@qq\\.com";
          boolean matches = email.matches(reg);
          return matches;
      }
  
  }
  ```

  - Demo01.java

  ```java
          User user = new User();
          user.setUsername("qiu123456");
          user.setPassword("qiu121");
          user.setEmail("qzw@qq.com");
          System.out.println(user);
  ```

  



