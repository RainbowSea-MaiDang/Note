## 实验说明

> 实验环境

- Windows Server 2022
- Kali Linux
- DVWA靶场

> 实验目标

通过不断调整DVWA靶场的难度，不断尝试突匹方法，完成任意文件上传



## 相关知识

### 任意文件上传漏洞原理

> 漏洞原理

开放了文件上传功能，且没有做相关的过滤和限制，或限制不足，导致任意文件上传；

---

> 漏洞危害

1. 获取webshell
2. 控制网站、控制服务器。

---

> 漏洞防御

代码层面：

1. 检测网页Token 值，防止数据包重放； 
2. 检测文件重命名； 
3. 文件后缀名白名单检测； 
4. 文件类型白名单检测； 
5. 文件内容头部检测； 
6. 二次渲染，生成新文件； 
7. 删除缓存文件。

服务器层面：

1. 严格控制权限，执行权限与写权限分离
2. 不使用PUT 方法
3. 建立单独的文件存储服务器，类似于站库分离

---



## 实验过程

> 攻击1

当我想上传一句话木马到DVWA的时候，会显示不允许

![image-20240329152040366](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329152040366.png)

> 防御1

查看源代码，我们发现，此处采取了黑白名单策略，限制了文件类型；

```php
// Is it an image?
if( ( $uploaded_type == "image/jpeg" || $uploaded_type == "image/png" ) &&
 ( $uploaded_size < 100000 ) ) { 
   //...
```

---

> 攻击2

此时，我通过BP调整文件类型，发现文件上传成功；

![image-20240329153335618](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329153335618.png)

通过上传提示的路径，成功访问并执行phpinfo()；

![image-20240329153417829](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329153417829.png)

---

> 防御2

当调整DVWA靶场难度后，我们发现，使用攻击2的方式失败，查看源码，我们发现，该代码进行了改写，添加了检测文件内容的条件：getimagesize( $uploaded_tmp ) ) 函数

```php
// Is it an image?
if( ( strtolower( $uploaded_ext ) == "jpg" || strtolower( $uploaded_ext ) == "jpeg" || strtolower( $uploaded_ext )
== "png" ) &&
 ( $uploaded_size < 100000 ) &&
getimagesize( $uploaded_tmp ) ) {   
```

> 攻击3

由于getimagesize() 函数进行文件内容检测，只检测文件头部。

我通过BP调整文件内容，调整后缀、类型并在文件内容头部添加一个图片的头部信息，发现文件上传成功；

![image-20240329155058169](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329155058169.png)

---

> 防御3

当DVWA调整到完美难度时，我们发现其对代码进行了非常高的优化，优化内容包括：

```txt
检测Token 值，防止数据包重放
文件重命名
文件后缀名白名单检测
文件类型白名单检测
文件内容头部检测
二次渲染，生成新文件
删除缓存文件
```

---

