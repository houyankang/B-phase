### 01_PowerDesigner概述

> * 介绍
>   * PowerDesigner是Sybase公司的一款设计软件
>   * 使用它可以方便地对系统进行分析设计，他几乎包 括了数据库模型设计的全过程
>   * 利用PowerDesigner可以制作数据流程图、概念数据模型、物理 数据模型、面向对象模型。
> * 作用
>   * 在项目设计阶段通常会使用PowerDesigner进行数据库设计。
>   * 建立概念数据模型，便于和非专业人员进行业务上的沟通
>   * 建立物理数据模型，可以用来生成对应的库表
>





### 02_概念数据模型

> * 前提
>   * 数据模型是现实世界中数据特征的抽象。数据模型应该满足三个方面的要求：
>     * 能够比较真实地模拟现实世界
>     * 容易被人理解
>     * 便于计算机实现
> * 介绍
>   * Conceptual Data Model:概念数据模型
>   * 概念数据模型也称信息模型，它以实体－联系(Entity-RelationShip,简称E-R)理论为基础，并对 这一理论进行了扩充。它从用户的观点出发对信息进行建模，主要用于数据库的概念级设计。
>   * 概念数据模型是现实世界到信息世界的第一层抽象，主要是在高水平和面向业务的角度对信息的 一种描述，通常作为业务人员和技术人员之间沟通的桥梁。作为现实世界的概念化结构，这种数 据模型使得数据库的设计人员在最初的数据库设计阶段将精力集中在数据之间的联系上，而不用 同时关注数据的底层细节
>



### 03_PowerDesigner使用之概念数据模型

* 步骤

  * 创建概念数据模型

    * ![image-20200519110254007](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519110413.png)

    * ![image-20200519110404203](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519110416.png)

* 一对一
  * 公司、注册地址
    * 一个公司只能有一个注册地址、一个注册地址只能有一个公司。
    * 公司、注册地址都必须有！
    
    
* 一对多
  * 老师、学生
    * 一个老师可以有多个学生、一个学生只能有一个老师
    * 老师可以没有学生，学生必须要有老师
    
    
* 多对多
  * 学生、课程
    * 一个学生可以有多个课程、一个课程可以有多个学生
    * 学生必须要有课程，课程可以没有学生
    
  
  
* 总结
  * 概念数据模型的关系分类
    * ![image-20200519111011485](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519111030.png)
      * 0~1个
    * ![image-20200519110840083](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519111032.png)
      * 1个
    * ![image-20200519111023964](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519111034.png)
      * 0~n个
    * ![image-20200519110941272](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519111036.png)
      * 1~n个





### 04_物理数据模型

* > 介绍
  > * Physical Data Model:物理数据模型
  > * 是概念数据模型和逻辑数据模型在计算机中的具体表示。
  > * 该模型描述了数据在物理存储介质上的 具体组织结构，不但与具体的数据库管理系统相关，同时还与具体的操作系统以及硬件有关，但 是很多工作都是由DBMS自动完成的，用户所要做的工作其实就是添加自己的索引等结构即可。



### 05_PowerDesigner使用之物理数据模型

* 开发流程
  * ![image-20200519110254007](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519110413.png)
  * ![image-20200519114637584](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519114640.png)

* 一对一
  * 将一张表的主键 为外键 指向另一张表的主键
  * ![image-20200519114655837](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519114740.png)
* 一对多
  * 在多的一方，添加一个字段作为外键，指向一的一方的主键
  * ![image-20200519114706490](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519114749.png)
* 多对多
  * 表A和表B
  * 创建一个中间表C
  * 表C作为多的一方，表A和表B作为一的一方
  * 建立表C和表A的一对多关系，建立表C和表B的一对多关系
  * ![image-20200519114722918](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519114752.png)





### 06_根据物理数据模型生成sql语句

* 步骤
  * 将数据库更改为想要的数据库
    * ![image-20200519161601606](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519163132.png)
  * 生成sql语句
    * ![image-20200519161656391](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519163129.png)
    * ![image-20200519161717945](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519163125.png)





### 07_根据概念模型生成物理模型

* 步骤
  * ![image-20200519162939091](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519163114.png)
  * ![image-20200519162957035](https://qiuzhiwei.oss-cn-beijing.aliyuncs.com/typora/20200519163108.png)



### 08_PowerDesigner逆向工程

> * 概念
>   * 正常情况下，都是先设计模型，再根据模型生成sql脚本文件
>   * 现在可以根据sql脚本文件，生成物理数据模型，这就叫做逆向工程
> * 步骤
>   * File ->reverse engineer
>



