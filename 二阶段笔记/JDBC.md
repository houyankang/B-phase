# JDBC



### 一、引言

------

#### 1.1 如何操作数据

> 使用客户端工具访问数据库，需要手工建立链接，输入用户名和密码登录，编写SQL语句，点击执行，查看操作结果（结果集或受影响行数）。





#### 1.2 实际开发中，会采用客户端操作数据库吗？

> 在实际开发过程中，当用户的数据发生改变时，不可能通过客户端操作执行SQL语句，因为操作量过大！无法保证效率和正确性



### 二、JDBC（Java DataBase Connectivity）

------

#### 2.1 什么是JDBC？

> JDBC（Java DataBase Connectivity） Java连接数据库，可以使用Java语言连接数据库完成CRUD操作



#### 2.2 JDBC核心思想

> Java中定义了访问数据库的接口，可以为多种关系型数据库提供统一的访问方式。
>
> 由数据库厂商提供驱动实现类(Driver数据库驱动)





##### 2.2.1 MySQL数据库驱动

> - mysql-connector-java-5.1.X 适用于5.X版本
> - mysql-connector-java-8.0.X 适用于8.X版本



##### 2.2.2 JDBC API

> JDBC 是由多个接口和类进行功能实现

| 类型      | 全限定名               | 简介                                                         |
| --------- | ---------------------- | ------------------------------------------------------------ |
| class     | java.sql.DriverManager | 管理多个数据库驱动类，提供了获取数据库连接的方法             |
| interface | java.sql.Connection    | 代表一个数据库连接(当Connection不是NULL时，表示已连接一个数据库) |
| interface | java.sql.Statement     | 发送SQL语句到数据库的工具                                    |
| interface | java.sql.ResultSet     | 保存SQL查询语句的结果数据(结果集)                            |
| class     | java.sql.SQLException  | 处理数据库应用程序时所发生的异常                             |



#### 2.3 环境搭建

> 1. 在项目下新建 lib 文件夹，用于存放 jar 文件
> 2. 将MySQL驱动文件mysql-connector-java-5.1.25-bin.jar 复制到项目的lib文件夹中
> 3. 选中lib文件夹 右键选择 add as library，点击OK



### 三、JDBC开发步骤【`重点`】

------

#### 3.1 注册驱动

> 使用[Class.forName("com.mysql.jdbc.Driver");]() 手动加载字节码文件到JVM中

```java
Class.forName("com.mysql.jdbc.Driver");
```



#### 3.2 连接数据库

> - 通过DriverManager.getConnection(url,user,password);获得数据库连接对象
>   - URL:jdbc:mysql://localhost:3306/database
>   - user:root
>   - password:1234

```java
Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/database?useUnicode=true&characterEncoding=utf8","root","1234");
```

- [URL(Uniform Resource Locator)统一资源定位符：由协议、IP、端口、SID（程序实例名称）组成]()



#### 3.3 获取发送SQL的对象

> 通过Connection对象获得Statement对象，用于对数据库进行通用访问的

```java
Statement statement = connection.createStatement();
```



#### 3.4 执行SQL语句

> 编写SQL语句，并执行，接收执行后的结果

```java
int result = statement.executeUpdate("update stu set student_name='高强',sex='女' where student_id = 'S1003'");
```

- [注意：在编写DML语句时，一定要注意字符串参数的符号是单引号  '值']()
- [DML语句：增、删、改时，执行的结果是受影响行数(int类型)。]()
- [DQL语句：查询时，返回的是数据结果集(ResultSet结果集)]()



#### 3.5 处理结果

> 接收并处理操作结果

```java
if(result > 0){
	System.out.println("执行成功");
}
```

- [受影响行数：逻辑判断，方法返回]()
- [查询结果集：迭代、依次获取]()



#### 3.6 释放资源

> 遵循的是[先开后关]()的原则，释放过程中用到的所有资源对象

```
statement.close();
connection.close();
```



#### 3.7 综合案例

> 综合核心六步，实现增删改

```java
 public static void main(String[] args)throws Exception {
        //1.注册驱动
        Class.forName("com.mysql.jdbc.Driver");

        //2.连接数据库
        String url = "jdbc:mysql://localhost:3306/companydb?useUnicode=true&characterEncoding=utf8";
        String user = "root";
        String password="1234";
        Connection connection=DriverManager.getConnection(url,user,password);

        //3.获取发送SQL的对象
        Statement statement = connection.createStatement();

        //4.编写SQL语句，执行SQL语句(返回受影响行数)
        //新增
//        String sql = "insert into stu(student_id,student_name,sex,birthday,phone,GradeId) values ('S1005','高强','女','1999-09-09','15612341234',3)";
//        String sql = "delete from stu where student_id = 'S1005'";删除
        //修改
        String sql = "update stu set student_name='高强',sex='女' where student_id = 'S1003'";
        int result = statement.executeUpdate(sql);
        //5.处理数据
        if(result > 0){
            System.out.println("执行成功！");
        }
        //6.释放资源 先开后关
        statement.close();
        connection.close();

    }
```



### 四、 ResultSet(结果集)

------

> 在执行查询SQL后，存放查询到的结果集数据



#### 4.1 接收结果集

> [ResultSet rs = statement.executeQuery(sql)]()

```java
ResultSet rs = statement.executeQuery("SELECT * FROM stu");
```



#### 4.2 遍历ResultSet中的数据

> ResultSet以表(Table)结构进行临时结果的存储，需要通过JDBC API将其中的数据进行依次获取
>
> - 数据行指针：初始位置在第一行数据前，每调用一次boolean next()方法，ResultSet中指针向下移动一行，结果为true，表示当前行有数据
> - rs.getXxx("列名"); 根据列名获得数据
> - rs.getXxx(整数下标); 代表根据列的编号顺序获得！从1开始

```java
boolean next() throws SQLException;//判断rs结果集中下一行是否有数据
```



##### 4.2.1 遍历方法

```java
int getInt(int columnIndex) throws SQLException;//获得当前行的第N列的int值
int getInt(String columnLabel) throws SQLException;//获得当前行columnLabel列的int值
```

- [注意：列的编号从1开始]()



#### 4.3 综合案例

> 对stu表所有的数据进行遍历



##### 4.3.1 根据列的名称获取

```java
package com.qf.day42.t2.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class TestDql {
    public static void main(String[] args)  throws Exception{
        //1.注册驱动
        Class.forName("com.mysql.jdbc.Driver");

        //2.获得连接
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/companydb?useUnicode=true&characterEncoding=utf8","root","1234");

        //3.获取执行SQL的对象
        Statement statement = connection.createStatement();

        //4.编写SQL语句
        String sql = "select student_id,student_name,sex,birthday,phone,GradeId from stu;";
        ResultSet resultSet = statement.executeQuery(sql);

        //5.处理结果 （结果集！）
        while(resultSet.next()){//判断结果集中是否有下一行！
            //根据列名获取当前行每一列的数据
            String student_id = resultSet.getString("student_id");
            String student_name = resultSet.getString("student_name");
            String sex = resultSet.getString("sex");
            String birthday = resultSet.getString("birthday");
            String phone = resultSet.getString("phone");
            int gradeId = resultSet.getInt("gradeId");
            System.out.println(student_id+"\t"+student_name+"\t"+sex+"\t"+birthday+"\t"+phone+"\t"+gradeId);
        }

        //6.释放资源
        resultSet.close();
        statement.close();
        connection.close();

    }
}

```



##### 4.3.2 根据列的下标获取

```java
 //5.处理结果 （结果集！）
        while(resultSet.next()){//判断结果集中是否有下一行！
            //根据列的编号获取当前行每一列的数据
            String student_id = resultSet.getString(1);
            String student_name = resultSet.getString(2);
            String sex = resultSet.getString(3);
            String birthday = resultSet.getString(4);
            String phone=  resultSet.getString(5);
            int gradeId  = resultSet.getInt(6);
            System.out.println(student_id+"\t"+student_name+"\t"+sex+"\t"+birthday+"\t"+phone+"\t"+gradeId);
 }
```



### 五、常见错误

> - java.lang.ClassNotFoundException  找不到类(类名书写错误、没有导入jar包)
> - com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException 与SQL语句相关的错误（表名列名书写错误、约束错误、插入的值是String类型，但是没有加单引号）建议：在客户端工具中测试sql语句后，再粘贴到代码中来
> - com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry 'S1003' for key 'PRIMARY'  原因：主键值已存在！更改要插入的主键值
> - com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException:Unknown column 'password' in 
>   - 可能输入的值的类型不对，确定插入元素时，对应的值的类型是否争取



### 六、综合案例【登录】

------



#### 6.1 创建表

> - 创建一张用户表 User
>   - id 主键、自动增长
>   - username 字符串类型 非空
>   - password 字符串类型 非空
>   - phone 字符串类型
> - 插入2条测试语句



#### 6.2 实现登录

> - 通过控制台，用户输入用户名和密码
> - 用户输入的用户名和密码作为参数，编写查询SQL语句。
> - 如果查询到用户，则用户存在，提示登录成功，反之，提示失败！



### 七、SQL注入问题

------

#### 7.1 什么是SQL注入

> 当用户输入的数据中有SQL关键字或语法时，并且参与了SQL语句的编译，导致SQL语句编译后条件结果为true，一直得到正确的结果。称为SQL注入



#### 7.2如何避免SQL注入

> 由于编写的SQL语句，是在用户输入数据后，整合后再编译成SQL语句。所以为了避免SQL注入的问题，使SQL语句在用户输入数据前，SQL语句已经完成编译，成为了完整的SQL语句，再进行填充数据



### 八、 PreparedStatement【`重点`】

------

> PreparedStatement接口继承了Statement接口。执行SQL语句的方法没有区别！



#### 8.1 PreparedStatement的应用

> 作用：1.预编译SQL语句，效率高！
>
> ​				2.安全，避免SQL注入
>
> ​				3.可以动态的填充数据，执行多个同构的SQL语句



##### 8.1.1 参数标记

```java
//1.预编译SQL语句
PreparedStatement pstmt = connection.prepareStatement(sql);
```

- [注意：PreparedStatement应用时，SQL字符串的参数都由?符号站位，被称为参数标记。在执行该SQL语句前，要为每个?参数赋值]()



##### 8.1.2 动态参数绑定

> [pstmt.setXxx(下标,值);]() 参数下标是从1开始，为指定占位符下标绑定值

```java
//2.为占位符下标赋值
pstmt.setString(1,username);
pstmt.setString(2,password);
```



### 九、综合练习

------

#### 9.1创建数据库、表

> 数据库 Account
>
> - 创建一张表 t_ccount。有以下列
>   - cardId：字符串，主键
>   - password：字符串，非空
>   - username：字符串，非空
>   - balance：小数，非空
>   - phone：字符串，非空



#### 9.2 创建项目通过JDBC实现功能

> 创建AccountSystem类，完成下列功能
>
> - 开户：控制台输入所有的账户信息，使用PreparedStatement添加至t_account表
> - 存款：控制台输入卡号、密码、存储金额进行修改
> - 取款：输入卡号、密码、取款金额
> - 转账：输入卡号、密码、对方卡号、转账金额进行修改
> - 修改密码：控制台输入卡号、密码，再输入新密码进行修改
> - 注销：控制台输入卡号、密码，删除对应的账户信息





### 十、封装工具类

------

#### 10.1 重用性方案

> - 封装了获取连接、释放资源两个方法
>   - 提供public static Connection getConnection()方法
>   - 提供public static void closeAll(Connection conn,Statement statement,ResultSet resultSet)



##### 10.1.1 工具实现

```java
package com.qf.day43.t1;

import sun.plugin2.gluegen.runtime.CPU;

import java.sql.*;

/**
 * 数据库工具类
 * 1、提供连接 -->Connection
 * 2、提供统一资源关闭
 * 可重用性方案
 */
public class DBUtils {


    static {
        try {
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    //硬编码
    //获得连接
    public static Connection getConnection() {
        Connection connection = null;
        try {
            connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/companydb?useUnicode=true&characterEncoding=UTF8", "root", "1234");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return connection;
    }

    //释放资源
    public static void closeAll(Connection connection, Statement statement, ResultSet resultSet) {
        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```



#### 10.2 跨平台方案

> - 定义 private static final Properties properties = new Properties();//配置文件集合
>
> - 定义static{
>
>   ​		//首次使用工具类，触发类加载
>
>   ​		InputStream is = DBUtils.class.getResourceAsStream("路径");//复用本类自带流，读取配置文件
>
>   ​		properties.load(is);//将is流中的配置文件信息，加载到集合中
>
>   ​		Class.forName(properties.getProperty("driver"));
>
>   }
>
> - 在getConnection方法中。应用properties.getProperty("url");



##### 10.2.1 实现

> 在src目录下新建db.properties文件

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/companydb?useUnicode=true&characterEncoding=utf8
username=root
password=123456
```



> DBUtils代码实现

```java
package com.qf.day43.t2;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.sql.*;
import java.util.Properties;

/**
 * 数据库工具类
 * 1、获取连接 connection
 * 2、释放资源
 * 可跨平台方案
 */
public class DBUtils {
   private static final Properties properties = new Properties();
    static {
        try {
                //适用类自身自带的流                                        路径
                InputStream is = DBUtils.class.getResourceAsStream("/db.properties");

                properties.load(is);//通过流，将配置信息的内容分割成键值对

                Class.forName(properties.getProperty("driver"));
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
        }
    }

    public static Connection getConnection(){
        Connection connection = null;
        try {
            connection = DriverManager.getConnection(properties.getProperty("url"),properties.getProperty("username"),properties.getProperty("password"));
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return connection;
    }


    //释放资源
    public static void closeAll(Connection connection, Statement statement, ResultSet resultSet) {
        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```





### 十一、ORM

------

> ORM（Object Relational Mapping）
>
> 从数据库查询到的结果集(ResultSet)在进行遍历时，逐行遍历，取出的都是零散的数据。在实际应用开发中，我们需要将零散的数据进行封装整理



#### 11.1 ORM 实体类(entity)：零散数据的载体

> - 一行数据中，多个零散的数据进行整理
> - 通过entity的规则对表中的数据进行对象的封装
> - [表名=类名；列名=属性名；提供各个属性的get、set方法]()
> - 提供无参构造方法、(视情况添加有参构造)



##### 11.1.1 ORM应用

```java
package com.qf.day43.t2;

public class User {
    private int id;
    private String username;
    private String password;
    private String sex;
    private String email;
    private String address;
    public User(){}

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", sex='" + sex + '\'' +
                ", email='" + email + '\'' +
                ", address='" + address + '\'' +
                '}';
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public User(int id, String username, String password, String sex, String email, String address) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.sex = sex;
        this.email = email;
        this.address = address;
    }
}

```



```java
package com.qf.day43.t2;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class OrmSelect {
    public static void main(String[] args) {
        Connection connection = DBUtils.getConnection();
        String sql = "select id,username,PASSWORD,sex,email,address from `user`;";
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;
        try {
            preparedStatement = connection.prepareStatement(sql);
            System.out.println(preparedStatement);
            resultSet = preparedStatement.executeQuery();
            while (resultSet.next()) {//拿到每一行数据、
                //拿到每一列的数据
                User user = new User();
                int id = resultSet.getInt("id");
                String username = resultSet.getString("username");
                String password = resultSet.getString("password");
                String sex = resultSet.getString("sex");
                String email = resultSet.getString("email");
                String address = resultSet.getString("address");
                //将一行中零散的数据，封装在一个User对象里。
                user.setId(id);
                user.setUsername(username);
                user.setPassword(password);
                user.setSex(sex);
                user.setEmail(email);
                user.setAddress(address);
                System.out.println(user);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DBUtils.closeAll(connection, preparedStatement, resultSet);
        }
    }
}

```



### 十二、DAO（Data Access Object）

------

> 数据访问对象
>
> - 将所有对同一张表的操作都封装在一个XXXDaoImpl对象中。
> - 根据增删改查的不同功能，实现具体的方法(insert,update,delete,select,selectAll)
> - [经验：对于任何一张表中的数据进行操作时，无非就是增、删、改、查。应将对于一张表的所有操作统一封装在一个数据访问对象中。重用]()





### 十三、日期类型

------

> - java.util.Date
>   - Java语言常规应用层面的日期类型。可以通过字符串创建对应的时间对象
>   - 无法直接通过JDBC插入数据库
> - java.sql.Date
>   - 不可以通过字符串创建对应的时间对象。只能通过毫秒值创建对象(1970年1月1日至今的毫秒值)
>   - 可以直接通过JDBC插入数据库



#### 13.1 日期格式化工具

> SimpleDateFormat   日期格式化

```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");//按照指定格式转换成util.Date类型
java.util.Date date = sdf.parse("2000-01-01");
```



#### 13.2 日期工具类 DateUtil

```java
package com.qf.day43.t4;

import java.text.ParseException;
import java.text.SimpleDateFormat;

/**
 * 日期转换
 * 字符串转UtilDate
 * 字符串转SqlDate
 * utilDate转成Sqldate
 */
public class DateUtils {
    private static final SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");

    //字符串转Util
    public static java.util.Date strToUtilDate(String str) {
        try {
            return simpleDateFormat.parse(str);
        } catch (ParseException e) {
            e.printStackTrace();
        }
        return null;
    }
    //字符串转sql
//    public static java.sql.Date strToSqlDate(String str){
//        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");
//        try {
//            java.util.Date date = simpleDateFormat.parse(str);
//            return new java.sql.Date(date.getTime());
//        } catch (ParseException e) {
//            e.printStackTrace();
//        }
//        return null;
//    }

    //util转sql
    public static java.sql.Date utilToSql(java.util.Date date){
        return new java.sql.Date(date.getTime());
    }

}

```



##### 13.2.1 测试

```java
package com.qf.day43.t4;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;


public class TestDatetimes {
    public static void main(String[] args) throws ParseException {
        //1.java.util.Date 当前系统时间
//        System.out.println(new java.util.Date());
//
//        //自定义一个时间
//        String str = "1999-09-09";
//        //日期转换   字符串转为 java.util.Date
//        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        
//        //将日期字符串转换成 util.Date类型
//        java.util.Date utilDate  = sdf.parse(str);
//        System.out.println(utilDate);
//
//        //sql.Date  需要毫秒值，来构建一个日期
//        java.sql.Date sqlDate = new java.sql.Date(utilDate.getTime());
//        System.out.println(sqlDate);
//
//
//        java.util.Date date = DateUtils.strToUtilDate("2002-3-18");
//        System.out.println(date);
//
//        java.sql.Date date2 = DateUtils.utilToSql(date);
//        System.out.println(date2);

        System.out.println(new java.util.Date());

        System.out.println(new java.sql.Date(new java.util.Date().getTime()));
    }
}

```



### 作业：user\userinfo

| 列名          | 类型               | 说明     |
| ------------- | ------------------ | -------- |
| user_id       | 整数、主键         | 用户编号 |
| user_name     | 字符串，唯一，非空 | 用户名称 |
| user_pwd      | 字符串，非空       | 用户密码 |
| user_borndate | DATE               | 出生日期 |
| user_email    | 字符串，非空       | 邮箱     |
| user_address  | 字符串             | 地址     |

注意：采用DAO+Entity完成

com.qf.xxx.entity

​		User

com.qf.xxx.dao

​		UserDaoImpl

​				完成五个方法、增、删、改、查、查所有





### 十四、连接池

------

> JDBC每次连接数据库，都要获得一个连接对象。每次创建一个连接对象，都是一个较大的资源，如果在连接量较大的场景下，会极大的浪费资源。容易内存溢出。



#### 14.1 自定义连接池

> Java中提供了一个接口DataSource，通过实现该接口，可以创建连接池



#### 14.2 Druid（德鲁伊）

> Druid 是目前比较流行高性能的，分布式列存储
>
> 一、亚秒级查询
>
> 二、实时数据注入
>
> 三、可扩展的PB级存储
>
> 四、多环境部署
>
> 五、丰富的社区



##### 14.2.1 Druid配置

> - 创建database.properties 配置文件
> - 引入druid-1.1.5.jar



##### 14.2.2 database.properties 文件配置

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://localhost:3306/userinfo?useUnicode=true&characterEncoding=utf8
username=root
password=123456
#初始化连接
initialSize=10
#最大连接数量
maxActive=30
#最小空闲连接
minIdle=5
#超时等待时间以毫秒为单位
maxWait=5000
```



##### 14.2.3 连接池工具类

```java
package com.qf.day44.t2;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.xml.transform.Result;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

public class DBPoolUtils {
    //连接池对象
    private static DruidDataSource ds;

    static {
        Properties properties = new Properties();
        InputStream is = DBPoolUtils.class.getResourceAsStream("/database.properties");
        try {
            properties.load(is);
            //使用德鲁伊工厂创建连接池
            ds = (DruidDataSource) DruidDataSourceFactory.createDataSource(properties);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() {
        try {
            //在连接池中获得Connection
            return ds.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }

    public static void closeAll(Connection connection, Statement statement, ResultSet resultSet) {
        try {
            if (resultSet != null) {
                resultSet.close();
            }
            if (statement != null) {
                statement.close();
            }
            if (connection != null) {
                connection.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```

- [注意：连接池中获得的Connection是DruidPooledConnection实现类，调用的close()方法不是关闭资源，而是将资源放回池中！]()



### 十五、Service(Biz/Business)

------

#### 15.1 业务

> 概念：用户要完成的一个业务功能，是由一个或多个的DAO调用组成。
>
> 软件、程序提供的一个功能都叫业务



#### 15.2 业务层的实现

```java
package com.qf.day44.t3;

/**
 * Userinfo的业务逻辑层对象
 */
public class UserinfoServiceImpl {

    /**
     * 用户的注册功能（业务）
     */
    public String register(Userinfo userinfo){//1.接收参数
        UserinfoDaoImpl userinfoDao = new UserinfoDaoImpl();

        //2.调用数据访问层对象的查询方法！
        Userinfo check = userinfoDao.select(userinfo.getUser_name());
        if(check!=null){//用户存在！~
            return "用户名已存在！";
        }
        //3.调用数据访问层对象的新增方法
        int result = userinfoDao.insert(userinfo);
        //4.将操作结果返回给调用者
        if(result >0 ){
            return "注册成功！";
        }else{
            return "注册失败！";
        }
    }
    /**
    * 登录功能业务
    */
    public Userinfo login(String user_name,String user_pwd){//收参
        UserinfoDaoImpl userinfoDao = new UserinfoDaoImpl();
        //2.调用数据访问层对象的查询方法
        Userinfo userinfo = userinfoDao.select(user_name);

        //3.接收结果，处理结果
        if(userinfo!=null){//用户存在！
            //检验查询到的用户密码和输入的密码是否一致!
            if(userinfo.getUser_pwd().equals(user_pwd)){
                return userinfo;
            }
        }
        //4.响应给调用者结果
        return null;
    }
}

```



#### 15.3 复用

> - DAO数据访问操作复用
> - 业务功能的复用    //不同的终端访问



#### 15.4 转账案例

> 代码参考Day44下的accounts项目



#### 15.5 解决转账事务问题

> 1、传递Connection：如果将Service获得的Connection对象，传递给DAO各个方法。可以。//BadSmell 臭味
>
> ​												定义接口是为了更容易更换实现！而将Connection参数定义在接口方法中，就会污染当前接口，而无法复用。JDBC-Connection。MyBatis使用SqlSession
>
> 2、单例：当前项目只能有一个客户端连接



### 十六、ThreadLocal

------

> 线程工具类：在整个线程中，一直到释放资源，用的是同一个Connection连接对象。



#### 16.1 ThreadLocal

> 1、在整个线程(单条执行路径中)所持有的Map中，存储一个键(threadlocal)值（connection）对
>
> 2、线程（Thread）对象中持有一个ThreadLocalMap类型的对象(ThreadthreadLocals)，threadLocals中保存了以ThreadLocal对象为Key，set进去的值为Value
>
> 3、每个线程均可绑定多个ThreadLocal，一个线程中可存储多个ThreadLocal



##### 16.1.1 ThreadLocal代码

```java
//绑定到线程中！ 绑定到当前线程中
        ThreadLocal<Connection> threadLocal = new ThreadLocal<Connection>();//0x112233

//        Thread
        //获得当前线程对象-->t.threadLocals集合为空-->create-->table[entry]-->key=0x112233 value=connection
        threadLocal.set(null);
        //获得当前线程对象-->getMap--->t.threadLocals-->getEntry（0x112233）-->entry-->entry.value
        Connection connection = threadLocal.get();

        ThreadLocal<Integer> threadLocal1 = new ThreadLocal<Integer>();//0x2345

        //每个线程可以绑定多个ThreadLocal，
        threadLocal1.set(123);

        Integer i = threadLocal1.get();
        System.out.println(i);
```



#### 16.2 ThreadLocal事务控制优化

> 将业务层的多步事务控制操作，封装在DBUtils工具类里。实现复用



##### 16.2.1 DBUtils封装事务控制

```java
  //开启事务
    public static void begin(){
        Connection connection = getConnection();
        try {
            connection.setAutoCommit(false);
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    //提交事务
    public static void commit(){
        Connection connection = getConnection();
        try {
            connection.commit();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            DBUtils.closeAll(connection,null,null);
        }
    }
    //回滚事务
    public static void rollback(){
        Connection connection = getConnection();
        try {
            connection.rollback();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            DBUtils.closeAll(connection,null,null);
        }
    }
```



### 十七、三层架构设计

------

> - 表示层：
>   - 命名：xxxVIew
>   - 职责：收集用户的数据和需求、展示数据
> - 业务逻辑层
>   - 命名：XXXServiceImpl
>   - 职责：数据的加工处理、调用Dao组合完成业务实现、控制事务
> - 数据访问层
>   - 命名：xxxDaoImpl
>   - 职责：向业务层提供数据，将业务层加工处理后的数据同步到数据库
>
> 





### 十八、工具类型的封装及普适性泛型工具

------



#### 18.1 封装DML方法

```java
public int commonsUpdate(String sql, Object... args) {
        Connection connection = null;
        PreparedStatement preparedStatement = null;

        try {
            connection = DBUtils.getConnection();
            preparedStatement = connection.prepareStatement(sql);

            for (int i = 0; i < args.length; i++) {
                preparedStatement.setObject(i + 1, args[i]);
            }

            return preparedStatement.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DBUtils.closeAll(null, preparedStatement, null);
        }
        return 0;
    }
```



#### 18.2 封装DQL方法

```java
 /**
     * 公共查询方法 (可查询单个对象，也可查询多个对象,可以查任何一张表)
     *
     * @param sql
     * @param args
     * @return
     */
    //                              select * from t_account
    //                              select * from t_student
    //工具不知道查的是什么  调用者知道
    //封装对象、对象赋值  调用者清楚
    public List<T> commonsSelect(String sql, RowMapper<T> rowMapper, Object... args) {

        List<T> elements = new ArrayList<T>();

        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            connection = DBUtils.getConnection();
            preparedStatement = connection.prepareStatement(sql);

            if(args !=null){
                for (int i = 0; i < args.length; i++) {
                    preparedStatement.setObject(i + 1, args[i]);
                }
            }


            resultSet = preparedStatement.executeQuery();

            while (resultSet.next()) {
                //根据查询到的结果完成ORM，如何进行对象的创建及赋值？
                T t = rowMapper.getRow(resultSet);//回调---->调用者提供的一个封装方法ORM
                elements.add(t);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            DBUtils.closeAll(null, preparedStatement, resultSet);
        }
        return elements;
    }
```



### 十九、Apache的DbUtils使用

------

> Commons DbUtils 是Apache组织提供的一个对JDBC进行简单封装的开源工具类库，使用它能勾简化JDBC应用程序的开发！同时，不会影响程序的性能



#### 19.1 DbUtils简介

> - DbUtils是Java编程中数据库操作实用小工具，小巧、简单、实用
>   - 对于数据表的查询操作，可以吧结果转换为List、Array、Set等集合。便于操作
>   - 对于数据表的DML操作，也变得很简单(只需要写SQL语句);



##### 19.1.1 DbUtils主要包含

> - ResultSetHandler接口：转换类型接口
>   - BeanHandler类：实现类，把一条记录转换成对象
>   - BeanListHandler类：实现类，把多条记录转换成List集合。
>   - ScalarHandler类：实现类，适合获取一行一列的数据。
> - QueryRunner：执行sql语句的类
>   - 增、删、改：update();
>   - 查询：query();
>
> ​	





#### 19.2 DbUtils的使用步骤

> - 导入jar包
>   - mysql连接驱动jar包
>   - druid-1.1.5.jar
>   - database.properties配置文件
>   - [commons-dbutils-1.6.jar]()



##### 19.2.1 代码实现

##### DBUtils工具类

```java
package com.project.utils;

import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

/**
 * 连接池工具类
 */
public class DBUtils {
    private static DruidDataSource dataSource;

    static {
        Properties properties = new Properties();
        InputStream is = DBUtils.class.getResourceAsStream("/database.properties");
        try {
            properties.load(is);
            dataSource = (DruidDataSource) DruidDataSourceFactory.createDataSource(properties);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    // 返回一个数据源
    public static DataSource getDataSource(){
        return dataSource;
    }
}

```

##### UserDaoImpl 数据访问对象

```java
package com.project.dao.impl;

import com.project.dao.UserDao;
import com.project.entity.User;
import com.project.utils.DBUtils;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;

import java.sql.SQLException;
import java.util.List;

public class UserDaoImpl implements UserDao {
    //1.创建QueryRunner对象，并传递一个数据源对象
    private QueryRunner queryRunner = new QueryRunner(DBUtils.getDataSource());
    @Override
    public int insert(User user) {
        Object[] params={user.getId(),user.getUsername(),user.getPassword(),user.getSex(),user.getEmail(),user.getAddress()};
        try {
            return queryRunner.update("insert into user (id,username,password,sex,email,address) values(?,?,?,?,?,?)",params);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return 0;
    }

    @Override
    public int update(User user) {
        Object[] params={user.getUsername(),user.getPassword(),user.getSex(),user.getEmail(),user.getAddress(),user.getId()};
        try {
            return queryRunner.update("update user set username=?,password=?,sex=?,email=?,address=? where id = ?",params);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return 0;
    }

    @Override
    public int delete(int id) {
        try {
            return queryRunner.update("delete from user where id = ?",id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return 0;
    }

    @Override
    public User select(int id) {
        try {
            //把查询到的记录封装成 指定对象
            return queryRunner.query("select * from user where id = ?", new BeanHandler<User>(User.class), id);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }

    /**
     * 查询所有
     * @return
     */
    @Override
    public List<User> selectAll() {
        try {
            return queryRunner.query("select * from user;",new BeanListHandler<User>(User.class));
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return null;
    }
}

```

























