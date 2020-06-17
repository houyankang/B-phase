### 01_千锋旅游网之页眉

* 效果图
  
* ![image-20200518102408947](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200518111928.png)
  
* 页眉组成

  * 一个容器三行
  * 第一行
    * 图片
  * 第二行
    * 导航条
  * 第三行
    * 轮播图

* 代码实现

  ```html
  <head>
      <title>千锋旅游网</title>
  
      <link href="${pageContext.request.contextPath}/bootstrap/css/bootstrap.min.css" rel="stylesheet">
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <script src="${pageContext.request.contextPath}/bootstrap/js/bootstrap.min.js"></script>
      <style>
          #top img{
              width: 100%;
          }
          .jx {
              margin-top: 10px;
              border-bottom: 1px solid orange;
              padding-bottom: 5px;
              margin-bottom: 20px;
  
          }
  
          #footer img{
              width: 100%;
          }
      </style>
  </head>
  <body>
  
  <div class="container-fluid" id="top">
  
      <%--头部logo--%>
      <div class="row">
          <img src="img/top_banner.jpg">
      </div>
  
      <%--导航条--%>
      <div class="row">
          <nav class="navbar navbar-default">
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
                          <li><a href="#">Python</a></li>
  
                      </ul>
                      <form class="navbar-form navbar-left">
                          <div class="form-group">
                              <input type="text" class="form-control" placeholder="请输入路线">
                          </div>
                          <button type="submit" class="btn btn-default">搜索</button>
                      </form>
                      <ul class="nav navbar-nav navbar-right">
                          <li><a href="#">联系客服</a></li>
                          <li class="dropdown">
                              <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">我的 <span class="caret"></span></a>
                              <ul class="dropdown-menu">
                                  <li><a href="#">个人中心</a></li>
                                  <li><a href="#">我的路线</a></li>
                                  <li><a href="#">我的订单</a></li>
                                  <li role="separator" class="divider"></li>
                                  <li><a href="#">注销登录</a></li>
                              </ul>
                          </li>
                      </ul>
                  </div><!-- /.navbar-collapse -->
              </div><!-- /.container-fluid -->
          </nav>
      </div>
  
      <%--轮播图--%>
      <div class="row">
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
                      <img src="img/banner_1.jpg" alt="...">
                      <div class="carousel-caption">
  
                      </div>
                  </div>
                  <div class="item">
                      <img src="img/banner_2.jpg" alt="...">
                      <div class="carousel-caption">
  
                      </div>
                  </div>
                  <div class="item">
                      <img src="img/banner_3.jpg" alt="...">
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
      </div>
  </div>
  ```
  
  



### 02_千锋旅游网之主体

* 效果图
  
* ![image-20200518111604479](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200518111610.png)
  
* 组成

  * 一个container容器，由5行组成
  * 第一行
    * 图片
  * 第二行
    * 四个元素，要给元素占3列
  * 第三行
    * 和第二行一样
  * 第四行
    * 和第一行一样
  * 第五行
    * 由两个元素组成（左元素、右元素）
      * 左元素，占4列
        * 图片
      * 有元素，占8列
        * 由两行组成，每一行都有3个元素

* 代码实现

  ```html
  <div class="container">
  
      <%--第一行--%>
      <div class="row jx">
          <img src="img/icon_5.jpg">千锋精选
      </div>
      <%--第二行--%>
      <div class="row">
  
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_2.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_2.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_3.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_4.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
      </div>
      <%--第三行--%>
      <div class="row">
  
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_2.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_2.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_3.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
          <div class="col-lg-3 col-md-6" >
              <div class="thumbnail">
                  <img src="img/jingxuan_4.jpg">
                  <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                  <font color="orange">$699</font>
              </div>
          </div>
      </div>
  
      <%--第四行--%>
      <div class="row jx">
          <img src="img/icon_6.jpg">国内精选
      </div>
  
      <%--第五行--%>
      <div class="row">
          <%--第一个元素,占4列--%>
          <div class="col-md-4">
              <div class="thumbnail">
                  <img src="img/guonei_1.jpg">
              </div>
  
          </div>
          <%--第二个元素，占8列--%>
          <div class="col-md-8">
  
              <div class="row">
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
              </div>
              <div class="row">
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
                  <div class="col-lg-4 col-md-12" >
                      <div class="thumbnail">
                          <img src="img/jingxuan_2.jpg">
                          <p>上海直飞三亚5天4晚自由行(春节预售+亲子/蜜月/休闲游首选+豪华酒店人选+接送机)</p>
                          <font color="orange">$699</font>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
  ```

  

### 03_千锋旅游网之页脚

* 效果
  
* ![image-20200518112346928](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200518112351.png)
  
* 组成

  * 一个container-fluid容器一行

* 代码实现

  ```html
  <style>
      #footer img{
          width: 100%;
      }
  </style>
  <%--页脚--%>
  <div class="container-fluid" id="footer">
      <div class="row">
          <img src="img/footer_service.png">
      </div>
  </div>
  ```

  



### 04_Bootstrap Validator概念

* 概念
  * 基于前端框架的表单校验，可以提升用户使用体验
  * Bootstrap Validator是基于Bootstrap、jquery组成。



### 05_Bootstrap Validator入门案例

* 开发流程

  * 当前项目引入BootStrap Validator相关的资源
    * 引入bootstrap.css
    * 引入bootstrapValidator.css
    * 引入jquery.js
    * 引入bootstrap.js
    * 引入bootstrapValidator.js
  * 编写form表单
    * 给需要表单校验的字段加上div(class="form-group")
  * 编写js校验规则

* 代码实现

  ```html
  <head>
      <title>Bootstrap Validator入门案例</title>
  
  
      <%--引入bootstrap.css--%>
      <link href="${pageContext.request.contextPath}/bootstrap/css/bootstrap.min.css" rel="stylesheet">
      <%--引入BootstrapValidator.css--%>
      <link href="${pageContext.request.contextPath}/bootstrapvalidator/css/bootstrapValidator.min.css" rel="stylesheet">
  
      <%--引入jquery.js--%>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <%--引入Bootstrap.js--%>
      <script src="${pageContext.request.contextPath}/bootstrap/js/bootstrap.min.js"></script>
      <%--引入BootstrapValidator.js--%>
      <script src="${pageContext.request.contextPath}/bootstrapvalidator/js/bootstrapValidator.min.js"></script>
  
      <script>
  
          $(function () {//页面加载完成
              $("#myForm").bootstrapValidator({
                  message : "this is not a valid field",//设置提示信息
                  fields:{//设置要校验的字段集合
                      username:{
                          validators:{
                              notEmpty:{
                              },
                              stringLength:{
                                  min:6,
                                  max:10
                              },
                              regexp:{
                                  regexp: /^[a-z0-9]{6,10}$/
                              }
                          }
                      },
                      password:{
                          validators:{
                              notEmpty:{
                              },
                              stringLength:{
                                  min:6,
                                  max:10
                              },
                              regexp:{
                                  regexp: /^[a-z0-9]{6,10}$/
                              }
                          }
                      }
                  }
  
              });
  
          })
  
      </script>
  
  </head>
  <body>
  
  <form id="myForm" action="${pageContext.request.contextPath}/demo01" method="post">
  
      <div class="form-group">
          账户:<input type="text" name="username"><br>
      </div>
      <div class="form-group">
          密码:<input type="text" name="password"><br>
      </div>
      <div class="form-group">
          <button type="submit">提交</button>
      </div>
  
  </form>
  ```

  



### 05_Bootstrap Validator高级使用

* 需求：

  * 不同错误提示不同的中文错误信息
  * 密码不能和账户一样! 使用different属性!
  * 确认密码和密码必须一致！使用identical属性!
  * 邮箱要满足邮箱格式！使用emailAddress属性!

* 代码实现

  ```html
  <head>
      <title>BootstrapValidator高级使用</title>
  
      <%--引入bootstrap.css--%>
      <link href="${pageContext.request.contextPath}/bootstrap/css/bootstrap.min.css" rel="stylesheet">
      <%--引入BootstrapValidator.css--%>
      <link href="${pageContext.request.contextPath}/bootstrapvalidator/css/bootstrapValidator.min.css" rel="stylesheet">
  
      <%--引入jquery.js--%>
      <script src="${pageContext.request.contextPath}/js/jquery-3.2.1.min.js"></script>
      <%--引入Bootstrap.js--%>
      <script src="${pageContext.request.contextPath}/bootstrap/js/bootstrap.min.js"></script>
      <%--引入BootstrapValidator.js--%>
      <script src="${pageContext.request.contextPath}/bootstrapvalidator/js/bootstrapValidator.min.js"></script>
  
      <%--
          1，不同错误提示不同的中文错误信息
          2，密码不能和账户一样! 使用different属性!
          3，确认密码和密码必须一致，使用identical属性！
          4，邮箱要满足邮箱格式！使用emailAddress属性!
      --%>
  
      <script>
  
          $(function () {
              $("#myForm").bootstrapValidator({
                  message: "this is not valiad field",
                  fields: {
                      username: {
                          validators: {
                              notEmpty: {
                                  message: "账户不能为空"
                              },
                              stringLength: {
                                  message: "账户长度在6~10之间",
                                  min: 6,
                                  max: 10
                              },
                              regexp: {
                                  message: "账户由小写字母、数字组成",
                                  regexp: /^[a-z0-9]{6,10}$/
                              }
                          }
  
                      },
                      password: {
                          validators: {
                              notEmpty: {
                                  message: "密码不能为空"
                              },
                              stringLength: {
                                  message: "密码长度在6~10之间",
                                  min: 6,
                                  max: 10
                              },
                              regexp: {
                                  message: "密码由小写字母、数字组成",
                                  regexp: /^[a-z0-9]{6,10}$/
                              },
                              different: {
                                  message: "账户和密码不能一致",
                                  field: "username"
                              }
                          }
                      },
                      repassword: {
                          validators: {
                              notEmpty: {
                                  message: "确认密码不能为空"
                              },
                              stringLength: {
                                  message: "确认密码长度在6~10之间",
                                  min: 6,
                                  max: 10
                              },
                              regexp: {
                                  message: "确认密码由小写字母、数字组成",
                                  regexp: /^[a-z0-9]{6,10}$/
                              },
                              identical: {
                                  message: "两次密码不一致",
                                  field: "password"
                              }
                          }
                      },
                      email: {
                          validators: {
                              notEmpty: {
                                  message: "邮箱不能为空"
                              },
                              emailAddress: {
                                  message: "邮箱格式不对"
                              }
                          }
                      }
                  }
              });
          })
  
      </script>
  </head>
  <body>
  
  
  <form id="myForm" action="${pageContext.request.contextPath}/demo01" method="post">
  
      <div class="form-group">
          账户:<input type="text" name="username"/><br>
      </div>
      <div class="form-group">
          密码:<input type="text" name="password"/><br>
      </div>
      <div class="form-group">
          确认密码:<input type="text" name="repassword"/><br>
      </div>
      <div class="form-group">
          邮箱:<input type="text" name="email"/><br>
      </div>
  
      <div class="form-group">
          <button type="submit">提交</button>
      </div>
  </form>
  
  </body>
  ```

  

### 06_Echarts入门案例

* 概念

  * ECharts 是一款由百度前端技术部开发的，基于 Javascript 的数据可视化图表库，提供直 观，生动，可交互，可个性化定制的数据可视化图表。

* 官网

  * https://echarts.apache.org/zh/index.html

* 开发流程

  * 引入Echarts资源
  * 定义具备宽高的Echarts容器
  * 初始化Echarts对象
  * 设置Echarts属性

* 代码实现

  ```html
  <head>
      <title>echarts入门</title>
      <%--1,引入echarts.js--%>
      <script src="echarts/echarts.min.js"></script>
      <script src="js/jquery-3.2.1.min.js"></script>
  
  
      <script>
  
          $(function () {
              <%--3,初始化echarts容器--%>
              var myChart = echarts.init(document.getElementById('main'));
              <%--4,设定echarts的属性--%>
  
              myChart.setOption({
                  title: {
                      text: 'ECharts 入门示例'
                  },
                  tooltip: {},
                  legend: {
                      data:['销量']
                  },
                  xAxis: {
                      data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
                  },
                  yAxis: {},
                  series: [{
                      name: '销量',
                      type: 'bar',
                      data: [5, 20, 36, 10, 10, 20]
                  }]
              })
          })
  
      </script>
  </head>
  <body>
  
  <%--2,设定一个具备宽高的echarts容器--%>
  <div id="main" style="width: 600px;height: 400px">
  
  </div>
  
  </body>
  ```

  

### 07_Echarts之折线图

* 开发流程

  * 引入Echarts资源
  * 定义具备宽高的Echarts容器
  * 初始化Echarts对象
  * 设置Echarts属性

* 代码实现

  ```html
  <html>
  <head>
      <title>Echarts折线图</title>
      <script src="echarts/echarts.min.js"></script>
      <script src="js/jquery-3.2.1.min.js"></script>
      <script>
          $(function () {
              var eCharts = echarts.init(document.getElementById("main"));
              var option = {
                  xAxis: {
                      type: 'category',
                      data: ['星期一', '星期二', '星期三', '星期四', '星期五', '星期六', '星期日']
                  },
                  yAxis: {
                      type: 'value'
                  },
                  series: [{
                      data: [1000, 932, 901, 934, 1290, 1330, 2000],
                      type: 'line'
                  }]
              };
              eCharts.setOption(option);
          })
  
  
      </script>
  </head>
  <body>
  
  <div id="main" style="width: 600px;height: 400px"></div>
  
  </body>
  ```

  

### 08_Echarts之饼状图

* 代码实现

  ```java
  <html>
  <head>
      <title>Echarts饼状图</title>
      <script src="echarts/echarts.min.js"></script>
      <script src="js/jquery-3.2.1.min.js"></script>
      <script>
          $(function () {
              var eCharts = echarts.init(document.getElementById("main"));
              var option = option = {
                  tooltip: {
                      trigger: 'item',
                      formatter: '{a} <br/>{b}: {c} ({d}%)'
                  },
                  legend: {
                      orient: 'vertical',
                      left: 10,
                      data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎']
                  },
                  series: [
                      {
                          name: '访问来源',
                          type: 'pie',
                          radius: ['40%', '60%'],
                          avoidLabelOverlap: false,
                          label: {
                              show: false,
                              position: 'center'
                          },
                          emphasis: {
                              label: {
                                  show: true,
                                  fontSize: '30',
                                  fontWeight: 'bold'
                              }
                          },
                          labelLine: {
                              show: false
                          },
                          data: [
                              {value: 335, name: '直接访问'},
                              {value: 310, name: '邮件营销'},
                              {value: 234, name: '联盟广告'},
                              {value: 135, name: '视频广告'},
                              {value: 1548, name: '搜索引擎'}
                          ]
                      }
                  ]
              };
              eCharts.setOption(option);
          })
  
  
      </script>
  </head>
  <body>
  
  <div id="main" style="width: 600px;height: 400px"></div>
  
  </body>
  ```

  

### 09_Echarts之异步加载

* 概念

  * 异步请求服务器中的数据，并将该数据设置到Echarts容器中

* 开发流程

  * 引入echarts相关资源
  * 定义一个具备宽高的echarts容器
  * 初始化echarts容器
  * 使用jquery进行异步加载
    * 请求成功，使用后台数据给echarts容器设置参数

* 代码实现

  * demo07.jsp

  ```html
  <html>
  <head>
      <title>Echarts饼状图</title>
      <script src="echarts/echarts.min.js"></script>
      <script src="js/jquery-3.2.1.min.js"></script>
      <script>
          $(function () {
              var eCharts = echarts.init(document.getElementById("main"));
  
              $.get("${pageContext.request.contextPath}/demo01",{},function (data) {
                  console.log(data);
                  var option = {
                      xAxis: {
                          type: 'category',
                          data: data.list1
                      },
                      yAxis: {
                          type: 'value'
                      },
                      series: [{
                          data: data.list2,
                          type: 'line',
                          smooth: true
                      }]
                  };
  
                  eCharts.setOption(option);
              },"json");
  
  
          })
  
  
      </script>
  </head>
  <body>
  
  <div id="main" style="width: 600px;height: 400px"></div>
  
  </body>
  </html>
  ```

  * Demo01Servlet

  ```java
  @WebServlet(name = "Demo01Servlet",urlPatterns = "/demo01")
  public class Demo01Servlet extends HttpServlet {
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          System.out.println("Demo01Servlet");
          SaleService saleService = new SaleServiceImpl();
          try {
              List<Sale> saleList = saleService.selectSalesList();
              List<String> weekList = new ArrayList<>();
              List<Integer> salesList = new ArrayList<>();
              for (Sale sale : saleList) {
                  weekList.add(sale.getWeekName());
                  salesList.add(sale.getSales());
              }
              Map<String,Object> map = new HashMap<>();
              map.put("list1",weekList);
              map.put("list2",salesList);
              JsonUtils.writeJsonStr(response,map);
  
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          doPost(request, response);
      }
  }
  ```

  