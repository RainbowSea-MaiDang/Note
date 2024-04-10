# Nginx 解析漏洞



## 漏洞描述

Nginx 解析漏洞是一种安全漏洞，它允许攻击者在 Nginx 服务器上执行任意代码。这种漏洞通常是由于 Nginx 配置文件中的解析错误或不安全的设置导致的。攻击者可以利用这个漏洞来获取敏感信息、修改服务器配置或者执行其他恶意操作。



## 影响版本

该漏洞与Nginx、php版本无关，属于用户配置不当造成的解析漏洞



## 漏洞复现

利用vulhub靶场进行漏洞复现。

> 环境启动

![image-20240410152540532](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410152540532.png)





## 漏洞验证

访问如下两个网址，看看有什么不同

```http
http://192.168.1.11/uploadfiles/nginx.png
http://192.168.1.11/uploadfiles/nginx.png/.php
```

![image-20240410175730375](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410175730375.png)

可以看到，本来只是一张图片，在请求上添加`/.php`后就被执行了；

我们可以去找找问题所在，查看一下这个请求的资源`nginx.png`

![image-20240410153619323](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410153619323.png)

![image-20240410153639427](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410153639427.png)

当我们使用`xxd`以十六进制形式打开图片，我们可以看到，该图片有一个执行`phpinfo()`的php代码，由此可知，请求添加`/.php`可以解析文件，那么是否意味着可以解析我们的木马；

尝试上传木马文件

![image-20240410154232757](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410154232757.png)

我们发现直接上传会失败，使用BP抓包重放试试

![image-20240410154204865](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410154204865.png)

可以看到，依然失败，接下来我们去审计一下代码，寻找漏洞以便上传木马

![image-20240410153931117](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410153931117.png)

在审计文件上传代码后，我们可以发现，该服务使用了` getimagesize `函数对文件内容进行检查所上传的文件是否为图片，并且使用了白名单策略，限制文件类型为`image`,文件后缀名为`gif、png、jpg、jpeg`,还使用`getimagesize`，那么我们就不能不能直接上传pho文件，需要通过BP抓包然后修改属性，再重放。

![image-20240410154410272](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410154410272.png)

可以看到，我们针对性的修改了请求包，上传成功

![image-20240410154456104](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410154456104.png)

访问，可以看到确实上传成功了，每次都使用蚁剑进行连接，今天换换花样，我们使用msf进行菜刀连接。

使用`search caidao` 查找一下模块

![image-20240410171322244](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410171322244.png)

可以看到，成功找到了， `use 0`选中模块

![image-20240410171420622](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410171420622.png)

配置参数，rhosts是目标ip，targeturl是木马文件的url， password是连接密码

![image-20240410171438224](C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240410171438224.png)

执行run后，可以看到成功连接

![image-20240410171519129](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240410171519129.png)



## 修复建议

这个漏洞其实是由php.ini中cgi.fix pathinfo配置导致的，如果开启，那么php解析时候，先解析最后一个，发现没有，就去解析上一级，造成漏洞。修复可以选择配置`cgi.fix pathinfo=0`禁用

