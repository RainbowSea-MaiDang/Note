## 实验说明

> 实验环境

- Windows Server 2022
- sqli-labs-master 靶场


> 实验目标

使用SQL注入基本手法的延迟注入，完成对靶场的用户名，和密码的获取；



## 相关知识

> 注入原理

通过用户可控参数中注入SQL语句，破坏SQL语句原有结构，达到编写程序时意料之外的攻击行为；

造成原因：1.使用字符串拼接方式构造SQL语句；2.未对用户输入的数据进行足够的过滤；

> SQL注入流程

库-->表-->列-->数据

> 延时注入

当页面既没有回显，又没有报错，而且还没有布尔变化的时候，就需要使用延时注入来判断状态；

---



## 实验过程

#### 1 分析目标

> 分析目标-1.注入点判断 （数字/字符） 有无回显

![image-20240327163557188](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163557188.png)

![image-20240327163615305](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163615305.png)

由上两图得知，无回显示，无报错，无布尔状态

![image-20240327163922685](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163922685.png)

延迟了五秒后刷新；

**得出结果：无回显、无报错、无布尔状态、字符型；所以需要使用延时注入**

---

#### 2 SQL注入-判断数据库名长度

> SQL注入-2.判断数据库名长度

![image-20240327165130139](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327165130139.png)

延迟了五秒；

**得出结果：数据库名长度为8；**

---

#### 3 SQL注入-按位判断数据库名

> SQL注入-3.按位判断数据库名

![image-20240327165434903](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327165434903.png)

延迟了5秒；

**得出结果：数据库名第一位为s**

---

#### 4 SQL注入-表、列、数据

**和布尔注入差不多，不再一一缀叙；**

