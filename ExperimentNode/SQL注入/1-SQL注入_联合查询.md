## 实验说明

> 实验环境

- Windows Server 2022

- sqli-labs-master 靶场

  


> 实验目标

使用联合查询注入手法，完成对靶场的用户名，和密码的获取；



## 相关知识

### 注入原理

通过用户可控参数中注入SQL语句，破坏SQL语句原有结构，达到编写程序时意料之外的攻击行为；

造成原因：1.使用字符串拼接方式构造SQL语句；2.未对用户输入的数据进行足够的过滤；

> SQL注入流程

库-->表-->列-->数据

> 联合查询

适用数据库中的内容会回显到页面中来的情况。联合查询就是利用union select 语句，该语句会同时执行两条select 语句，实现跨库、跨 表查询。

必要条件 ：1.两条select 语句查询结果具有相同列数； 2.对应的列数据类型相同；

---



## 实验过程

#### 1 分析目标

> 分析目标-1.注入点判断 （数字/字符）

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327143723097.png" alt="image-20240327143723097"  />

**得出结果：该注入点为 字符型，且为单引号**

---

> 分析目标-2.判断列数

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327144313171.png" alt="image-20240327144313171"  />

得出结果不为4，减一继续判断

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327144338164.png" alt="image-20240327144338164"  />

**得出结果：列数为3**

---

> 分析目标-3.判断显示位置

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327144546394.png" alt="image-20240327144546394"  />

**得出结果：2，3出有回显**

---



#### 2 SQL注入-查询数据库

> SQL注入-4.查询数据库名和版本号

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327144851137.png" alt="image-20240327144851137"  />

**得出结果：数据库名为security 版本号为 5.5.53**

---

#### 3 SQL注入-查询表

> SQL注入-5.查询数据库中所有表

![image-20240327152751885](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327152751885.png)

**所得结果是 emails、referers、uagents、users 四张表**

---

#### 4 SQL注入-查询列

> SQL注入-6.通过表查询所有列名

![image-20240327153437659](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327153437659.png)

**所得结果是 id、username、password 三给列**

---

#### 5 SQL注入-查询数据

> SQL注入-7.通过列查询用户账号密码

![image-20240327153735515](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327153735515.png)

**所得结果：用户名：Dumb ，密码：Dumb**