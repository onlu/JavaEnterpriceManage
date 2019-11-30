# 企业管理系统
## 一、需求
### 1.系统用户模块
    ①用户可以使用用户名和密码登录该系统
    ②系统登录页面需要对用户名和密码进行校验，用户名不能为空，密码非空，且长度在3-10位之间
    ③密码再数据库中存储的形式是以加密的方式进行存储的。加密算法采用的是MD5加密方式。
    ④如果系统用户登录失败时，给出系统提示
    ⑤用户点击退出管理按钮，跳转回用户的登录页面，完成用户退出的功能
### 2.员工管理模块
    ①员工查询功能，需要把所有的数据显示到页面上，并且提供分页
    ②员工的新增功能，需要对数据进行校验，保存成功后跳转到用户的列表页面
    ③修改员工，对数据进行校验，修改成功后跳转到用户的列表页面
    ④删除员工，对员工删除时需要先询问是否删除，用户点击却行才会删除，删除成功后跳转到用户列表页面
### 3.系统权限功能
    ①系统中的功能必须是在用户登录的情况下才能使用，如果没有登录，会跳转到登录页面
## 二、数据库设计
创建数据库：
```SQL
    create database txweb;
    use txweb;
```
用户表：
```SQL
create table t_user(
    id int primary key auto_increment,
    username varchar(30),
    password varchar(50),
    nickname varchar(30)
);
 
insert into t_user values(1,'admin','e10adc3949ba59abbe56e057f20f883e','管理员')
```
员工表：
```SQL
create table t_emp(
    id int primary key auto_increment,
    ename varchar(30),
    age int(3),
    sex char(1),
    sal double,
    birthday varchar(15),
    edate varchar(15)
);

INSERT INTO `t_emp` VALUES(1,'美美',20,'女',10000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(2,'小凤',25,'女',8000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(3,'冠希',35,'男',12000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(4,'熊大',22,'男',10000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(5,'熊二',11,'女',10000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(6,'光头强',12,'男',8000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(7,'喜羊羊',20,'女',10000,'1990-11-11','2018-11-11');
INSERT INTO `t_emp` VALUES(8,'二狗',20,'女',10000,'1990-11-11','2018-11-11');

```
**注意：先启动Mysql服务，在创建Mysql数据库前一定要先设置好字符编码集，UTF-8（Unicode）最常用，否则插入数据可能都是？？？的乱码。**


## 三、架构选择
### 1.架构的选择
本项目采用MVC设计模式思想，使用JavaBean、Servlet和JSP作为MVC的组件进行开发。服务器端采用三层架构的方式，分成了表现层、业务层和持久层。

> 三层架构
>> 表现层：使用JSP和Servlet程序，与浏览器客户端进行数据的交互。
>> 业务层：使用Service程序，进行业务逻辑处理和事务处理。
>> 持久层：使用Dao程序，进行数据库的持久化操作。数据库使用Mysql数据库。

