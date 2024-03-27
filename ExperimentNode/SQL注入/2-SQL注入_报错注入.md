## 实验说明

> 实验环境

- Windows Server 2022
- sqli-labs-master 靶场




> 实验目标

使用报错注入手法，完成对靶场的用户名，和密码的获取；



## 相关知识

### 注入原理

通过用户可控参数中注入SQL语句，破坏SQL语句原有结构，达到编写程序时意料之外的攻击行为；

造成原因：1.使用字符串拼接方式构造SQL语句；2.未对用户输入的数据进行足够的过滤；

> SQL注入流程

库-->表-->列-->数据

> 报错注入

适用于数据库中SQL 语句的报错信息会显示在页面中，可以利用报错信息进行注入。 

报错注入的原理，是在错误信息中执行SQL 语句。

---



## 实验过程

#### 1 分析目标

> 分析目标-1.注入点判断 （数字/字符）

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327145709870.png" alt="image-20240327145709870"  />

可以观察到，没有回显

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327145756647.png" alt="image-20240327145756647"  />

**得出结果：该注入点为 字符型，且为单引号；无回显有报错**

---

#### 2 SQL注入-查询数据库

> SQL注入-2.查询数据库名

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327150349694.png" alt="image-20240327150349694"  />

**得出结果：数据库名为security**

---

#### 3 SQL注入-查询表

> SQL注入-3.查询security数据库中所有表

![image-20240327154507533](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327154507533.png)

**得出结果是 emails、referers、uagents、users 四张表**

---

#### 4 SQL注入-查询列

> SQL注入-4.查询users表中所有列

![image-20240327155012836](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327155012836.png)

**得出结果：id、username、password三列**

---

#### 5 SQL注入-查询数据

> SQL注入-5.查询用户名和密码

![image-20240327155313471](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327155313471.png)

**得出结果：多个用户和密码，而且没有显示完全，可以使用 substr( )函数多次截取，这里不再缀叙；**

---

