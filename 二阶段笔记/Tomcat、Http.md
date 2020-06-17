# Tomcat

### 一、生活中的上网方式

#### 1.1生活中有哪些上网方式？

> 两种方式，可以通过浏览器(browser)进行上网,也可以通过客户端(client)进行上网

#### 1.2两种结构

##### 1.2.1	BS结构 （browser server） 浏览器服务器

> 特性：
>
> - 不需要安装客户端，只要能连上网，就能随时随地使用
>   开发人员只需要对服务器端程序进行开发、维护，降低开发维护难度和开发维护成本
>   浏览器主要负责用户界面的动态展示，只处理一些简单的逻辑功能
>   所有具体业务逻辑的处理都由服务器端程序完成，所以程序负载几乎都转移给服务器
>   端。
>   但是随着服务器负载的增加，可以平滑地增加服务器的个数并建立集群服务器系统，然
>   后在各个服务器之间做负载均衡。
>
> 优缺点：
>
> 优点：实时地更新数据(新功能的增加只需要在服务端完成, 浏览器刷新就好了),
> 缺点:将负载给了服务器

##### 1.2.2	CS结构 （client server ）客户端服务器

> 特性：
>
> - 将应用程序分为客户端和服务器端两层，客户端程序用于展示功能，为用户提供操作界
>   面，同时也可以进行业务逻辑的处理；而服务器端程序负责操作数据库完成数据处理等
>   核心业务
>   由此可见通过C/S开发模型开发的应用程序，客户端程序可以承担一部分业务逻辑处
>   理，特别是数据的预处理工作，减轻了服务器端程序的压力
>
> 优缺点：
>
> 优点:客户端也分担了一部分负载,
> 缺点:如果有新的功能要增加必须要重新下载客户端

### 二、Web相关概念

#### 2.1什么是Web？

> Web指的就是网页，我们所说的web指的是internet主机(服务器)上的供外界访问的资源
> web资源可以分为两种：静态web资源、动态web资源

#### 2.2静态Web资源

> 概念：指web页面上供人们浏览的数据，它们始终不变。例如html
> 优点:
> 1.静态网站开发简易，只需要掌握HTML、CSS和JS就可以开发
> 2.静态访问速度快，因为静态网页不需要和任何程序进行交互，更不需要对数据进行处理
> 缺点:
> 1.静态网站内容无法实时更新，因为网站由一个个的静态HTML网页构成，新增内容只能
> 2.通过开发人员修改代码
> 3.网站内容过多时，每个页面都需要单独制作，需要不断编写和维护HTML页面，增加了
> 4.网站开发人员的工作量，提高了运营费用。

#### 2.3动态Web资源

> 概念：指web页面中内容是由程序产生的，供人们浏览，并且在不同的时间点，数据不一样，并且
> 还可以实现人与人之间的交互。用到Servlet和JSP等技术.
> 优点：
> 1.维护方便、可以根据用户需求实现各种功能
> 2.查询信息方便，能存储大量数据，需要时能立即查询
> 3.网站内容可以实时动态更新
> 4.与用户交互性强，提高用户粘性
> 缺点：技术要求高

[总结：静态的web资源，只是供人们浏览，而动态的web资源，可以实现交互。]()



### 

### 三、Tomcat安装与配置

#### 3.1测试安装是否成功

> 在tomcat的安装目录下有一个bin目录 ，在目录 中有一个startup.bat文件执行它。打开浏
> 览器，在浏览器的地址栏上输入 http://localhost:8080。

#### 3.2JAVA_HOME配置

> 在tomcat的安装目录bin文件夹下的catalina.bat中使用了JAVA_HOME,所以,安装
> tomcat必须要求系统配置中有JAVA_HOME,如果没有配置，执行startup.bat文件时会
> 出现闪退效果

#### 3.3更改端口配置（默认8080，可不改）

> tomcat默认使用的8080端口，可以进行端口号的修改,修改tomcat的端口号,在
> tomcat/conf/server.xml文件, 可以添加80端口,80是http协议默认的端口。
>
> tomcat安装目录  -> conf文件夹 -> server.xml中
>
> ```xml
> <Connector port="8080" protocol="HTTP/1.1"
>            connectionTimeout="20000"
>            redirectPort="8443" />
> ```
>
> 

#### 3.4Tomcat目录结构

> bin目录：存放tomcat的可执行文件，比如startup.bat
>
> conf目录：Tomcat的配置文件，比如server.xml
>
> lib目录：Tomcat运行时所依赖的核心jar包，比如jap-api.jar、server-api.jar
>
> logs目录：存放Tomcat的执行日志
>
> temp目录：存放临时文件
>
> webapps目录：部署Web资源
>
> work目录：存放jsp转译之后的java文件

### 四、Web项目

#### 4.1项目分类

> A、Web静态项目
>
> ​			包含都是静态资源：html、js、css、图片、音频等等
>
> B、Web动态项目: 不是必须包含动态资源
>
> ​			包含都是静态资源：html、js、css、图片、音频等等
>
> ​			那么和静态项目的区别在哪里？可以有动态资源及WEB-INF文件夹
>
> ​			通过http://localhost:8080/    访问的资源是来自于tomcat服务器的动态web项目(内置),
>
> ​			而在tomcat的一个安装目录中，是由一个webapps的文件夹专门用来部署web项目
>
> [总结：一个静态web项目，肯定都是静态资源]()
>
> ​	[		而一个动态Web项目，可以有静态资源，也可以有动态志愿，但必须有WEB_INF文件夹及web.xml]()

#### 4.2web.xml

> 可以将tomcat/webapps/ROOT应用下的web.xml文件内容复制到我们自己的web.xml文件
> 中

#### 4.3如何设置工程的默认访问界面？

> 在tomcat/conf/web.xml文件，将这个文件理解成是我们所有的tomcat下的web应用程序
> 中的web.xml文件的父类文件。
> 在这段声明就规定了web应用中哪些文件是默认被访问的。如果我们在自己项目的web.xml
> 文件中将上述内容覆盖了，就可以设置自己项目的默认访问页面。

tomcat安装目录 -> conf文件夹 -> web.xml

​	

```xml
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
```

​	上述配置代码，是设置tomcat容器中的每个项目的默认页面是index.html、index.htm、index.jsp

​	如果，不想遵守以上约定，怎么处理？

​		方式一：直接修改tomcat中的web.xml，

​			

```xml
    <welcome-file-list>
        <welcome-file>demo01.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
```

​		但是这样处理存在问题，所有的项目的欢迎页面都会跟随改变!!!

​	方式二：直接修改项目自带的web.xml

​		每一个web动态项目都会包含web.xml

​		加入以下代码：

```xml
    <welcome-file-list>
        <welcome-file>demo01.html</welcome-file>
        <welcome-file>demo01.htm</welcome-file>
        <welcome-file>demo01.jsp</welcome-file>
    </welcome-file-list>
```

​			以上配置仅针对当前项目有效!!!

#### 4.4项目中的wb.xml和tomcat中的web.xml，有什么关系？

> ​	类似于java中的继承关系(父子关系),
>
> ​	如果tomcat中的web.xml的配置无法满足当前的项目的需求，那么就可以更改项目中的web.xml，覆盖tomcat中的web.xml配置

### 五、Tomcat部署Web项目的方式

#### 5.1方式一：直接将web应用程序放置到webapps目录

> 直接将一个web应用程序放置在tomcat/webapps目录下。这时web应用程序目录名称就是
> 我们访问tomcat下的这个应用程序的名称

#### 5.2方式二：虚拟目录初级版

> 将一个不在tomcat下的web应用程序部署加载。可以在tomcat/conf/server.xml文件中配
> 置，在server.xml文件中的[<Host>标签]()中添加一段配置

​	将tomcat目录以外的资源部署到容器中

​	在tomcat的目录 ->  conf文件夹 -> server.xml中 , 加一个<Contex>

​	

```xml
<Context docBase="项目路径" path="项目访问名称"/>
```

​		从tomcat6.0开始，以上的配置方案，并不推荐使用!!!

​		改动了tomcat的server.xml文件，一旦出错，tomcat容器就无法打开!!!

#### 5.3方式三：虚拟目录优化版

>
> 在tomcat/conf/Catalina/localhost下创建任意名称的一个xml文件，例如创建一个
> good.xml文件，在good.xml中书写<Context docBase="磁盘路径" />
> 这种方案配置，xml文件的名称就是访问路径，在浏览器中访问http://localhost/good就可
> 以。

​	1_tomcat安装目录 -> conf文件夹 -> catalina -> localhost

​	2_新建一个任意名称的xml文件

​	3_需要到xml文件中编写如下代码：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Context docBase="C:\Users\qiuzhiwei\Desktop\dynamicproject"/>
```

### 	六、访问部署成功之后的项目中的资源

> 1_访问到tomcat容器
>
> ​			http://localhost:8080/
>
> ​	2_访问到项目
>
> ​			http://localhost:8080/dynamicproject/
>
> ​	3_访问到资源
>
> ​			http://localhost:8080/dynamicproject/a.jpg
>
>   	4_注意事项
>
> ​			如果访问路径只写到http://localhost:8080/dynamicproject/,默认访问index开头的html文件或jsp文件...

### 七、在idea下开发Web应用

#### 7.1创建Web项目步骤

> A：创建一个JavaWeb工程，Java Enterprise ->Web Application
>
> B:	项目名称、工作空间的选择
>
> C:	JavaWeb目录介绍
>
> ​			src:	存放java代码
>
> ​			web：存放web资源，比如：html、js、css、图片、jsp等等
>
> ​			WEB-INF：存放java文件转译之后的class文件

#### 7.2idea配置Tomcat

> A：选择项目启动按钮左边的Edit Configurations
>
> B：点击加号 ->tomcat server -> local
>
> C：点击Configure -> 点击加号 -> 选择tomcat
>
> D：配置Tomcat插件
>
> ​		On update action:	Redeploy（重新部署项目）
>
> ​		On frame deactivation：Update classes and resources
>
> E：在Deploment中设置项目访问名称

#### 7.3idea部署web项目的方式

> A：概念
> 	idea部署web项目的方式，本质就是虚拟目录优化版，但是有一些区别!
> B：步骤
> 	根据本地安装的tomcat，会给当前项目生成一个tomcat镜像，部署到tomcat镜像相当于部署到本地
> tomcat中
> 	tomcat镜像部署项目的方式是虚拟目录优化版， 镜像的安装目录 -> conf -> catalina -> localhost ,就找到
> 了day50.xml配置文
>
> ```xml
> <Context path="/day50"
> docBase="F:\workspace\nz2002\day50\out\artifacts\day50_war_exploded" />
> ```
>
> ​	以上配置说明,
> ​	day50 项 目 ， 它 的 访 问 名 称 是 "/day50" ， day50 的 资 源 部 署 路 径是:"F:\workspace\nz2002\day50\out\artifacts\day50_war_exploded",
> ​	
> ​	这就要求，day50项目中的资源应该都需要放到day50_war_exploded文件夹中!!!

#### 7.4idea中的web项目的哪些内容部署到tomcat中

> A：概念
> 	根据上一个知识点，只有资源来到了day50_war_exploded文件夹中，才意味着部署成功！！！
> B：到底有哪些可以部署？
> 	src文件夹:
> 		可以部署上去!部署到了项目中的\WEB-INF\classes文件夹中
> 	web文件夹：
> 		可以部署上去！部署到了项目目录中!
> 	day50项目下：
> 		不可以部署上去

### 八、Http协议

#### 8.1相关概念

> A：协议
> 	两个设备进行数据交换的约定!
> B：Http协议
> 	超文本传输协议(hypertext transfer protocl)
> 	超文本：字符、音频、视频、图片等等
> 	基于tcp协议。tomcat服务器底层实现本质上就是TCP(Socket)

#### 8.2通过抓包的方式演示http协议

> 经过演示发现，浏览器和服务器，它们之间进行交互，是一个请求-响应模型!!!
> 请求：
> 	请求行
> 	请求头
> 	请求正文
> 响应：
> 	响应行
> 	响应头
> 	响应正文

#### 8.3请求的执行流程

> A：发起请求
> B：域名解析
> 	先看本地域名解析器(C:\Windows\System32\drivers\etc\host)，
> 	如果本地解析器无法解析，那么就交给互联网上的DNS解析器
> 	得到IP
>
> C:	TCP三次握手
>
> ​	请求访问、应答、开始连接
>
> D：根据ip和端口，可以得到一个Socket对象，执行请求
> 		携带请求行、请求头、请求正文
> E：服务器响应浏览器
> 	携带响应行、响应头、响应正文
>
> 

#### 8.4http请求

> A：请求组成
> 	请求行、请求头、请求正文
> B：请求行
> 	Request URL : 请求路径，告诉服务器要请求的资源路径
> 	Request Method : 请求方式 , GET/POST
> 	protocol : http协议版本
>
> C：GET请求和POST请求 [面试重点]()
> 	**get请求只能携带小数据、get请求下的请求参数会直接拼接到Request URL(请求网址)后面，**QueryStringParameters**
> 	**post请求可以携带大数据、post请求下的请求参数会存放到请求正文**
> 	请求参数：比如，表单中的输入框中的值.
> 	如果我们要做文件上传，需要用到post请求，文件比较大!!
> D:	请求头
> 	Content-Type:浏览器告诉服务器，请求正文的数据类型
> 	User-Agent:浏览器告诉服务器，我是个什么样的浏览器
> E:	请求正文
> 	请求正文，**只有当请求方式为post，且有请求参数时才会有请求正文**！！！在Form Data中显示

#### 8.5Http响应

> A：Http响应组成
> 	响应行、响应头、响应正文
> B：响应行
> 	Status Code : 响应状态码
> 常见的有：
> 	200：服务器响应成功
> 	302: 告诉浏览器，进行重定向
> 	304: 页面上的内容没有发生改变，不需要重新请求服务器
> 	404: 没有对应的服务器资源
> 	500:服务器内部错误!
> C：响应头
> 	Location：告诉浏览器重定向的资源路径，需要结合响应状态码302使用
> 	Content-Type:	服务器告诉浏览器，响应正文的数据类型
> 	
> 	Content-Type:	text/html;charset=utf-8; 服务器告诉浏览器，响应正文是文本和html标签；告诉浏览器，应该以utf-8的形式进行解码！浏览器就会以html标签及utf-8的形式对响应正文进行渲染显示！！！
> 	
> 	refresh:	定时跳转
> 	
> 	Content-Disposition:	文件下载
> 
> D：响应正文
> 	浏览器显示的内容