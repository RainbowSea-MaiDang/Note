## 实验说明

> 实验环境

- Windows Server 2022
- sqli-labs-master 靶场




> 实验目标

分别使用SQL的五大基本注入手法，完成对靶场的用户名，和密码的获取；



## 相关知识

### SQL注入原理

通过用户可控参数中注入SQL语句，破坏SQL语句原有结构，达到编写程序时意料之外的攻击行为；

造成原因：1.使用字符串拼接方式构造SQL语句；2.未对用户输入的数据进行足够的过滤；

> SQL注入流程

库-->表-->列-->数据



### 五大注入手法

> 联合查询

适用数据库中的内容会回显到页面中来的情况。联合查询就是利用union select 语句，该语句会同时执行两条select 语句，实现跨库、跨 表查询。

必要条件 ：1.两条select 语句查询结果具有相同列数； 2.对应的列数据类型相同；

> 报错注入

适用于数据库中SQL 语句的报错信息会显示在页面中，可以利用报错信息进行注入。 

报错注入的原理，是在错误信息中执行SQL 语句。

> 布尔盲注

页面中有布尔类型的状态，可以根据布尔类型状态，对数据库中的内容进行判断。比如猜密码长度；

> 延时注入

当页面既没有回显，又没有报错，而且还没有布尔变化的时候，就需要使用延时注入来判断状态；

> 堆叠查询

即一次HTTP 请求，可以同时执行多条SQL 语句，包括增删改查操作



---



### 4.使用延时注入

#### 4.1 分析目标

> 分析目标-1.注入点判断 （数字/字符） 有无回显

![image-20240327163557188](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163557188.png)

![image-20240327163615305](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163615305.png)

由上两图得知，无回显示，无报错，无布尔状态

![image-20240327163922685](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163922685.png)

得知，延迟了五秒后刷新

**得出结果：无回显、无报错、无布尔状态、字符型**

---

#### 4.2 SQL注入-判断数据库名长度

> SQL注入-2.判断数据库名长度

![image-20240327165130139](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240327165130139.png)

延迟了五秒；

**得出结果：数据库名长度为8；**

---

#### 4.3 SQL注入-按位判断数据库名

> SQL注入-3.按位判断数据库名

![image-20240327165434903](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240327165434903.png)

延迟了5秒；

**得出结果：数据库名第一位为s**

---

#### 4.4 SQL注入-表、列、数据

**和上述布尔注入差不多，不再一一缀叙；**

---



### 使用堆叠查询



![image-20240327170223454](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240327170223454.png)

![image-20240327170159989](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240327170159989.png)

**得出结果：有回显，有报错，字符型**



![image-20240327170524508](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240327170524508.png)

