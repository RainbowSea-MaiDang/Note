## 实验说明

> 实验环境

- Windows Server 2022
- sqli-labs-master 靶场




> 实验目标

使用布尔盲注手法，完成对靶场的用户名，和密码的获取；



## 相关知识

> 注入原理

通过用户可控参数中注入SQL语句，破坏SQL语句原有结构，达到编写程序时意料之外的攻击行为；

造成原因：1.使用字符串拼接方式构造SQL语句；2.未对用户输入的数据进行足够的过滤；

> SQL注入流程

库-->表-->列-->数据

> 布尔盲注

页面中有布尔类型的状态，可以根据布尔类型状态，对数据库中的内容进行判断。比如猜密码长度；

---



## 实验过程

#### 1 分析目标

> 分析目标-1.注入点判断 （数字/字符） 有无回显

![image-20240327160030453](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160030453.png)

上图知无回显

![image-20240327160046674](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160046674.png)

上图无报错

![image-20240327160532833](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160532833.png)

**得出结果：字符型，无回显无报错，但有布尔类型**

---

#### 2 SQL注入-判断数据库名长度

> SQL注入-2.判断数据库名长度

![image-20240327160743646](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160743646.png)

可知，长度不大于10

![image-20240327160815357](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160815357.png)

可知长度在6-10之间

![image-20240327160847807](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327160847807.png)

**得出结果：数据库名长度为8**

---

#### 3 SQL注入-按位判断数据库名

> SQL注入-3.按位判断数据库名

![image-20240327161011995](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327161011995.png)

可知第一位的ASCII码职小于等于120

![image-20240327161115418](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327161115418.png)

**得出结果：第一位的ASCII码等于115，为字母s**

一直循环往复下去会得到完整的数据库名，建议使用脚本完成

---

#### 4 SQL注入-判断表名长度

得到数据库名后开始获取表名

> SQL注入-4.判断表名长度

![image-20240327162435838](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327162435838.png)

可知表明大于5

![image-20240327162510970](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327162510970.png)

可知表名在6-8之间

![image-20240327162606250](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327162606250.png)

**得出结果：表名长度为6**

---

#### 5 SQL注入-按位判断表名

> SQL注入-5.按位判断表名

![image-20240327162831211](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327162831211.png)

可知表名第一位的ASCII码大于97

![image-20240327162921354](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327162921354.png)

可知表名第一位ASCII码在98-110之间

![image-20240327163014555](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240327163014555.png)

**得出结果：表名第一位ASCII码为101，为字母e**

一直循环往复下去会得到完整的表名，建议使用脚本完成

---

#### 6 SQL注入-判断列、数据...

**随后的列、数据以此类推，循环往复，不再缀叙**