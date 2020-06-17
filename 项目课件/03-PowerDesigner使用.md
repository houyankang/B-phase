### 01_Power Designer介绍
*   PowerDesigner是Sybase公司的一款软件，使用它可以方便地对系统进行分析设计，他几乎包括了数据库模型设计的全过程。利用PowerDesigner可以制作数据流程图、概念数据模型、物理数据模型、面向对象模型。
*   在项目设计阶段通常会使用PowerDesigner进行数据库设计。使用PowerDesigner可以更加直观的表现出数据库中表之间的关系，并且可以直接导出相应的建表语句。


### 02_Power Designer使用之概念数据模型
*   Conceptual Data Model:概念数据模型
*   数据模型是现实世界中数据特征的抽象。数据模型应该满足三个方面的要求：
    *   能够比较真实地模拟现实世界
    *   容易为人所理解
    *   便于计算机实现
*   概念数据模型也称信息模型，它以实体－联系(Entity-RelationShip,简称E-R)理论为基础，并对这一理论进行了扩充。它从用户的观点出发对信息进行建模，主要用于数据库的概念级设计。
*   概念数据模型是现实世界到信息世界的第一层抽象，主要是在高水平和面向业务的角度对信息的一种描述，通常作为业务人员和技术人员之间沟通的桥梁。作为现实世界的概念化结构，这种数据模型使得数据库的设计人员在最初的数据库设计阶段将精力集中在数据之间的联系上，而不用同时关注数据的底层细节
*   ![image](https://note.youdao.com/yws/res/20749/AA44893F26364E9485711762B7EFF8FD)


### 03_Power Designer使用之物理数据模型
*   Physical Data Model:物理数据模型
*   是概念数据模型和逻辑数据模型在计算机中的具体表示。该模型描述了数据在物理存储介质上的具体组织结构，不但与具体的数据库管理系统相关，同时还与具体的操作系统以及硬件有关，但是很多工作都是由DBMS自动完成的，用户所要做的工作其实就是添加自己的索引等结构即可。
*    创建数据模型PDM
    *    ![image](https://note.youdao.com/yws/res/20742/DC5F80AF3FDE432BA522EEA5DA73FFFF)
*    选择数据库类型
    *    ![image](https://note.youdao.com/yws/res/20745/335692FAC1CF42FA9D808482FA51AF24)
*    创建表,字段和约束
*    从PDM导出SQL脚本


### 04_Power Designer使用之逆向工程
*   上面我们是首先创建PDM模型，然后通过PowerDesigner提供的功能导出SQL脚本。实际上这个过程也可以反过来，也就是我们可以通过SQL脚本逆向生成PDM模型，这称为逆向工程，操作如下
*   ![image](https://note.youdao.com/yws/res/20774/8C8C044E35C14D5CAB84EE08CE97C4A8)
*   ![image](https://note.youdao.com/yws/res/20770/D2E99E3FBD9C4E8BB01A53FF6721DA82)
*   ![image](https://note.youdao.com/yws/res/20768/6823086ECB254BC3901C7E84CF58FCC5)
*   ![image](https://note.youdao.com/yws/res/20766/76E7A5D84DE844F3BC9D3876E0C96435)


### 05_婚礼汇Conceptual Data Model
*   酒店
    *   ![image](https://note.youdao.com/yws/res/20772/6CFC5290483C4686856875AFFC5B75D6)
*   房间
    *   ![image](https://note.youdao.com/yws/res/20762/4C620460183F40C0B08F2310033DB721)
*   套餐
    *   ![image](https://note.youdao.com/yws/res/20765/56EAD68961944A18B732727077ED6866)
*   酒店信息
    *   ![image](https://note.youdao.com/yws/res/20752/C5678D9B5579457FAB1A6D498C13C427)
*   酒店,房间,套餐,酒店信息ER图
    *   ![image](https://note.youdao.com/yws/res/20741/EB077D319B2D416DA4827CE4237078AD)
*   购物车
    *   ![image](https://note.youdao.com/yws/res/20763/1D3D8F70BC43496798244D97C87CE03D)
*   用户
    *   ![image](https://note.youdao.com/yws/res/20760/926DDE011C3143A1A9ABC8EA570A4BEA)
*   购物车,用户ER图
    *   ![image](https://note.youdao.com/yws/res/20746/D3E5AA8318C44705B6943E8894E22370)


### 06_婚礼汇Physical Data Model
*   酒店
    *   ![image](https://note.youdao.com/yws/res/20771/081717BBFA44432691ECA1CD6EFF2AD5)
*   房间
    *   ![image](https://note.youdao.com/yws/res/20747/A3DAE8A9C0594904B3FBC225EC6996A0)
*   套餐
    *   ![image](https://note.youdao.com/yws/res/20759/9A02F9C86FC94518B72FBE9E3F479647)
*   酒店信息
    *   ![image](https://note.youdao.com/yws/res/20743/25204C6C022249FFBF02D59337AE098C)
*   酒店,房间,套餐,酒店信息物理模型图
    *   ![image](https://note.youdao.com/yws/res/20740/164C1EBEDB0C4AB7A0ED8E750975A722)
*   购物车
    *   ![image](https://note.youdao.com/yws/res/20751/88A0D97DE0EA4FC0A1FF7E04FF9752F1)
*   用户
    *   ![image](https://note.youdao.com/yws/res/20754/A649B33D38764E01A4BD0284BD6495CA)
*   购物车,用户物理模型图
    *   ![image](https://note.youdao.com/yws/res/20755/29CF079057A74222AE0CC6C0DE700662)