# Vim快捷键

![image-20240315161828997](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315161828997.png)

![image-20240315161857685](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315161857685.png)

# Linux 命令

> 常用

```sh
init 0 #关机
reboot #重启
cat /proc/cpuinfo #查看CPU
cat /proc/meminfo #查看内存
fdisk -l #查看内存
uname -r #查看内核版本
man 命令 #查看命令的使用方式
ln -s  源文件绝对路径 目的链接绝对路径  #建立快捷方式 s软链接
ls -alh #a隐藏 l列表 h大小
cat -n  #查看并显示行号
cp -r   # r递归拷贝

watch -n1 [命令] #watch缺省每2秒运行一下程序，可以用-n指定间隔的时间
```



> 统计命令

| more  | 分页查看文件内容       |
| ----- | ---------------------- |
| less  | 交互式逐行查看文件内容 |
| head  | 查看文件头十行（默认） |
| tail  | 查看文件后十行（默认） |
| grep  | 查找文件中的某个关键字 |
| du    | 统计目录内容大小       |
| wc    | 统计文件内容大小       |
| alias | 命令别名建立           |
| find  | 查找文件或目录         |

```sh
head -n 5 test.txt  #查头5行

grep "12" test.txt  #匹配 -i忽略大小写，-c输出个数，-n输出所在行 ，-v不包含
grep "12$" test.txt  #匹配所有以12结尾的行

du -sh /  #统计根目录所包含文件总大小

wc -l test.txt  #计算文件行数
 
find ~/ -name test.txt #查找文件 -type f文件，-type d目录
```



# Linux目录

![image-20240315134011383](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315134011383.png)

![image-20240315134023481](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315134023481.png)



# 压缩解压缩

> gzip （只能文件）

压缩：gzip 文件名

解压缩：gunzip 压缩文件名

> bzip2（只能文件）

压缩：bzip2 文件名

解压缩：bunzip2 压缩文件名

> tar：

![image-20240315162111042](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315162111042.png)



# 软件安装

源码包安装、rpm安装、yum安装；

---

> 源码包安装，（根据软件说明安装，PREFIX是安装路径）

![image-20240315164709120](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315164709120.png)

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315170017074.png" alt="image-20240315170017074" style="zoom:70%;" />

---

> 软件包安装 rpm

![image-20240315171437246](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315171437246.png)

```sh
#参数解释
-q --query  QUERYING PACKAGESquery 
-a --al1  query/verify all packages
-p --package  query/verify a package file
-i --install  install package(s)
-l --list  List files in package
-V --verbose  provide more detailed output
```

> yum源安装

```sh
yum install -y tree #安装tree -y自动确认
yum remove -y tree #卸载
```



# 用户信息文件passwd



![image-20240315180041483](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315180041483.png)

```txt
root：用户名；

x：密码占位符，x代表有密码，无内容代表没密码；

0：UID，身份标识，0是超管；

0：GID，用户组id；

root：身份信息；

/root：用户家目录；

/bin/bash :用户命令解释器，sbin/nologin 不允许登录；
```

---

# 用户密码文件shadow

![image-20240315180939984](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315180939984.png)

每一行记录一个用户的密码信息，以`:`作为分隔符，一共9段内容；

```txt
用户名：密码密文：密码修改时间戳：密码最短有效期：密码最长有效期:密码过期时间:密码不活跃期:账户失效期:未分配功能
```

# 组管理

> 新建组

```sh
groupadd class1 #新建class1组
groupadd class2 -g 2000 #新建组并指定组ID
```

> 更新组

```sh
groupmod class2 -g 3000 #修改组ID
```

删除组

```sh
groupdel class1 
```



# 用户管理

> 建立用户 useradd

![image-20240315191444061](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315191444061.png)

```sh
useradd tom1 #创建用户，不指定组，则会自动创建同名组
```

> 修改用户信息

```sh
usermod tom1 -u 2000  #修改UID
```

> 删除用户

```sh
userdel -r tmm1 #删除用户和其家目录
```



# 用户密码管理

用户密码状态：LK密码锁定；NP没有密码；PS有可用密码；

> 设置密码

```sh
passwd tom1
```

> 锁定密码（账号不可登录）

```sh
passwd -l tom1
```

> 解锁密码

```sh
passwd -u tom1
```

> 查看用户密码状态

```sh
passwd -S tom1
```



# 权限管理

> 权限表达

![image-20240315193159473](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315193159473.png)

分别是：用户权限、所属组权限、其他用户权限；

```sh
r  读    （对目录来说：列出目录内容）   4
w  写    （对目录来说：创建删除目录中文件） 2
x 执行   （对目录来说：可以进入目录） 1
```

---

> 权限修改

```sh
chmod  对象 运算符 权限 文件或目录
```

| 对象             | 运算符                        | 权限  |
| ---------------- | ----------------------------- | ----- |
| u （文件所有者） | +（添加） -（去除） =（赋予） | r w x |
| g （所属组）     |                               |       |
| o  (其他用户)    |                               |       |
| a （所有人）     |                               |       |

```sh
chmod u-r /tom.txt  #去除了tom文件所有者的读权限
chmod u+r /tom.txt  #赋予了tom文件所有者的读权限
chmod a=r /tom.txt  #赋予了tom文件所有人的读权限
```

chomd 777 -R #递归设置权限

---

> 特殊权限

```sh
  t #粘滞位，有t权限的目录，只有文件所有者可以删除该目录下创建的文件
  s #SGID对目录有效，在该目录下创建的文件或目录会继承父目录的属组；SUID对可执行文件有效，谁运行谁就有文件所有者的权限；
```

---



# sudo 权限控制

一般情况下，使用sudo是在申请root权限去执行某一个命令，要求输入密码时，输入的是当前用户密码；

> sudoers

配置文件/etc/sudoers 是sudo的配置文件；

![image-20240315201728508](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315201728508.png)

root用户，可以在任何地方，任何组，执行任何命令

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240315201235034.png" alt="image-20240315201235034" style="zoom: 67%;" />

```sh
#在配置文件/etc/sudoers中添加，使得tom 可以执行sudo id
tom   ALL=(ALL:ALL) /usr/bin/id

tom   ALL=(ALL:ALL) NOPASSWD: /usr/bin/id #表执行时不需要密码

#执行
sudo id
```





# 远程登录

> Telnet和SSH

Telnet缺点：账号密码明文传输；

SSH缺点：可以被账号爆破(可以试错密码无限次)、非信任地址登录(任何人任何地点尝试登录)；

---



# 日志

> 日志分类：内核及系统日志、用户日志、程序日志

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20240317104525767.png" alt="image-20240317104525767" style="zoom:80%;" />

---

> 日志级别

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317105331068.png" alt="image-20240317105331068" style="zoom:80%;" />

---

> 日志管理工具 rsyslog

作用：统一管理日志，是否进行日志记录、记录什么类型日志、记录哪一个级别、日志存储位置；

配置文件：/etc/rsyslog.conf 

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317105729242.png" alt="image-20240317105729242" style="zoom:67%;" />

解释

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317105805481.png" alt="image-20240317105805481" style="zoom:80%;" />

---

# 日志服务器配置

> 配置思路

![image-20240317110306017](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317110306017.png)

server为发送端，syslog为接收端

---

> ​	发送端配置-在rsyslog的配置文件 /etc/rsyslog.conf下配置（添加一句）

```sh
authpriv.* @@172.16.1.254:514   #所有级别的登录日志 都发往ip为172.16.1.254，端口为514
systemctl restart rsyslog #重启
```

---

> 接收端配置--在rsyslog的配置文件 /etc/rsyslog.conf下配置 

1.开启TCP协议以及514端口 （19行）

```sh
# Provides TCP syslog reception
$ModLoad imtcp
@InputTCPServerRun 514
```

2.添加规则（最好就在第一步下直接添加）

```sh
：fromhost-ip,isequal,"172.16.1.10" /var/log/client_secure/172.16.1.100.log #接收来自于100的日志保存到/var...
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317111805793.png" alt="image-20240317111805793" style="zoom:80%;" />

3.重启

---





# 初始化配置

> 配置ip    IPADDR网络 ； NETMASK 掩码；GATEWAY网关；DNS1 域名解析；

```sh
ip addr add 192.168.2.254/24 dev ens33  #临时配置IP
ip route add default via 192.168.100.2 #临时配置网关

vi /etc/sysconfig/network-scripts/ifcfg-网卡名 #永久配置
systemctl restart network  #重启网卡
```

> 关闭防火墙

```sh
systemctl list-unit-files | grep "firewalld"   #查看防火墙服务
systemctl status firewalld #查看防火墙状态
iptables -vnL  #查看防火墙策略

systemctl stop firewalld.service  #关闭
systemctl disable firewalld.service  #禁止开机自启
```

> 关闭selinux ；selinux作用是给所有文件打标签

```sh
vi /etc/selinux/config 
# SELINUX=Enfocing--->SELINUX=disable
```

> 关闭虚拟化服务 (重启生效)

```sh
systemctl stop libvirtd.service 
systemctl disable libvirtd.service 
```

> 光盘自动挂载 （注意不成功一般是虚拟机iso没有勾选已连接）

```sh
systemctl list-unit-files |grep "autofs" #查看
yum install autofs -y #没有则安装
systemctl start autofs.service
systemctl enable autofs.service

cd /misc/cd #挂载到 /misc/cd
```

> yum源配置

```sh
cd /etc/yum.repos.d/  #进入文件夹
rm -rf *
vi /etc/yum.repos.d/local.repo

yum clean all
yum repolist
```

```sh
[centos7]
name=centos7
baseurl=file:/misc/cd
gpgcheck=0
enabled=1
```



# linux搭建网络拓扑

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317132844879.png" alt="image-20240317132844879" style="zoom:80%;" />

---

1.网络配置

> 网关服务器配置  ens33-V8  ens36-V1   ens37-V2

```sh
# cat ifcfg-ens33 联通公网
TYPE=Ethernet
BOOTPROTO=static
NAME=ens33
DEVICE=ens33
ONBOOT=yes

IPADDR=192.168.100.10
NETMASK=255.255.255.0
GATEWAY=192.168.100.2
DNS1=8.8.8.8

# cat ifcfg-ens36 联通客户机
TYPE=Ethernet
BOOTPROTO=static
NAME=ens36
DEVICE=ens36
ONBOOT=yes

IPADDR=192.168.1.254
NETMASK=255.255.255.0
DNS1=8.8.8.8

# cat ifcfg-ens37 联通服务器
TYPE=Ethernet
BOOTPROTO=static
NAME=ens37
DEVICE=ens37
ONBOOT=yes

IPADDR=172.16.1.254
NETMASK=255.255.255.0
DNS1=8.8.8.8
```

> Server 服务器配置 ens33-V2

```sh
# cat ifcfg-ens33 
TYPE=Ethernet
BOOTPROTO=static
NAME=ens33
DEVICE=ens33
ONBOOT=yes

IPADDR=172.16.1.100
NETMASK=255.255.255.0
GATEWAY=172.16.1.254
DNS1=8.8.8.8
```

> Syslog 日志备份服务器 ens33-V2

```sh
# cat ifcfg-ens33 
TYPE=Ethernet
BOOTPROTO=static
NAME=ens33
DEVICE=ens33
ONBOOT=yes

IPADDR=172.16.1.200
NETMASK=255.255.255.0
GATEWAY=172.16.1.254
DNS1=8.8.8.8
```

> client 客户端 ens33-V1

```sh
# cat ifcfg-ens33 
TYPE=Ethernet
BOOTPROTO=static
NAME=ens36
DEVICE=ens36
ONBOOT=yes

IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.254
DNS1=8.8.8.8
```

---

2.开启网关服务器的路由转发

```sh
vim /etc/sysctl.conf 
# 写入： net.ipv4.ip_forward=1

sysctl -p #刷新
```

此时192网段的客户端可以ping通172网段的服务器；

```sh
yum install wireshark-gnome.x86_64 -y  #可以在网关服务器上安装鲨鱼抓包
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317143535676.png" alt="image-20240317143535676" style="zoom:50%;" />

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317143915273.png" alt="image-20240317143915273" style="zoom:50%;" />

---

3.配置日志服务器

> 发送端server服务器配置 -rsyslog的配置文件 /etc/rsyslog.conf下配置 (并重启服务)

```sh
authpriv.* @@172.16.1.200:514  #日志备份服务器的ip和端口
```

> 接收端Syslog日志备份服务器配置- -rsyslog的配置文件 /etc/rsyslog.conf下配置 (并重启服务)

```sh
# Provides TCP syslog reception
$ModLoad imtcp   #协议
@InputTCPServerRun 514 #端口
:fromhost-ip,isequal,"172.16.1.100" /var/log/client_secure/172.16.1.100.log #接收来自100的日志保存到/var...
```

![image-20240317145530797](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317145530797.png)

---

4.在网关服务器上开启NAT地址转换，使得客户端联通外网，服务器不需要；

> 使用iptables 防火墙规则做SNAT  （-p 协议；-s 源地址；-o 出接口网卡；-j 控制类型）

```sh
[root@localhost ~]# iptables -t nat -I POSTROUTING -p all -s 192.168.1.0/24 -o ens33 -j SNAT --to-source 192.168.100.10 
[root@localhost ~]# iptables -t nat -I POSTROUTING -p all -s 0.0.0.0/0 -o ens33 -j SNAT --to-source 192.168.100.10

[root@localhost ~]# iptables -t nat -nvL  查看配置
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317152208523.png" alt="image-20240317152208523" style="zoom:67%;" />

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317152300196.png" alt="image-20240317152300196" style="zoom:67%;" />

---

5. 网关服务器部署DHCP

> 安装DHCP服务

```sh
yum install dhcp -y
```

> 配置dhcp

```sh
vim /etc/dhcp/dhcpd.conf  

:r /usr/share/doc/dhcp*/dhcpd.conf.example #末行模式复制模板到该文件
```

删除无用，只保留如下(精简)

```sh
subnet 192.168.1.0 netmask 255.255.255.0 {   #网段
  range 192.168.1.128 192.168.1.200;     #地址池
  option domain-name-servers 192.168.1.254;  #DNS，本DNS指向了自己
  option routers 192.168.1.254; #网关
  default-lease-time 600;  #租约
  max-lease-time 7200;
}
```

```sh
systemctl start dhcpd
systemctl enable dhcpd
```

客户机申请ip抓包

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317154557711.png" alt="image-20240317154557711" style="zoom:80%;" />

由于客户机是dhcp，又由于网关服务器的dns指向自己，所以客户机不能进行域名解析；

---

6.网关服务器部署DNS

> 安装DNS

```sh
yum install bind -y
```

> 配置DNS (/etc/named.conf) 

```sh
[root@localhost ~]# vim /etc/named.conf 

 11       
 12 options {
 13         listen-on port 53 { 192.168.1.254; };  #指向本机
 14         listen-on-v6 port 53 { ::1; };
 15         directory       "/var/named";
 16         dump-file       "/var/named/data/cache_dump.db";
 17         statistics-file "/var/named/data/named_stats.txt";
 18         memstatistics-file "/var/named/data/named_mem_stats.txt";
 19         #allow-query     { localhost; };  #注释以允许所有
 20 
 21         //...
 31         recursion yes;
 32 
 33         dnssec-enable no;   #关闭
 34         dnssec-validation no; #关闭
 35 
 36         /* Path to ISC DLV key */
 37         bindkeys-file "/etc/named.iscdlv.key";
 38 
 39         managed-keys-directory "/var/named/dynamic";
 40 
 41         pid-file "/run/named/named.pid";
 42         session-keyfile "/run/named/session.key";
 43 };
 44 
 45 logging {
 46         channel default_debug {
 47                 file "data/named.run";
 48                 severity dynamic;
 49         };
 50 };
```

```sh
systemctl start named.service
systemctl enable named.service
```

此时，客户端可以进行解析，正常ping通百度；

---

7.DNS欺骗

> 主配置文件修改  (末尾添加)

```sh
[root@localhost ~]# vim /etc/named.conf

//...
zone "jd.com" IN {
        type master;
        file "jd.com.zone";
};
```

> 区域配置文件

```sh
[root@localhost ~]# cd /var/named/
[root@localhost named]# cp -a named.empty jd.com.zone  #一定要（cp -a ）连同权限一起复制；名字和主配置文件写的一致
[root@localhost named]# vi jd.com.zone 
[root@localhost named]# cat jd.com.zone 
$TTL 3H
@	IN SOA	jd.com. hehe.jd.com. (
					0	; serial
					1D	; refresh
					1H	; retry
					1W	; expire
					3H )	; minimum
	NS	ns.jd.com.
ns	A	192.168.1.254
www	A	172.16.1.100
```

```sh
systemctl restart named.service  #重启生效
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240317165807541.png" alt="image-20240317165807541" style="zoom:67%;" />

---



# iptables包过滤防火墙

表的作用就是容纳各种规则链

![image-20240319181521523](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240319181521523.png)

规则链的作用就是对数据包进行过滤或处理，链中可以容纳各种防护墙规则，根据处理数据包的不同时机

![image-20240319181551428](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240319181551428.png)

![image-20240319181603004](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240319181603004.png)

> 语法

iptables 操作哪个张表，哪个链，符合什么流量，执行什么动作，

```sh
iptables  -t  表名  选项  [数字]  链名  [匹配条件]  [-j 控制类型]。

#选项：-A尾部追加 -I 开头或指定序号添加 -D删除链内指定序号规则 -F删除链内所有规则
#控制类型：ACCEPT 允许；DROP 拒绝； REJECT 拒绝并提示; LOG 记录日志并传给下一个规则；
```

- 不指定表名时，默认指filter 表；
- 不指定链名时，默认值表内所有链；
- 不指定序号的时，默认第一条规则；
- 从上到下，依次匹配；
- 如果匹配到了规则，立即执行动作（控制类型），结束匹配；

```sh
iptables -t filter -I INPUT -p icmp -j REJECT  #禁ping本机
iptables -t filter -I FORWARD -j ACCEPT #开启转发
iptables -A FORWARD ! -p icmp -j ACCEPT # ! 标识条件取反
iptables -A INPUT -i eth1 -s 192.168.0.0/16 -j DROP # 阻止192.168.0.0/16通过外网接口eth1 
iptables -A FORWARD -s 192.168.4.0/24 -p udp --dport 53 -j ACCEPT #允许来自ip：53 协议udp的通过(DNS)

#只允许网关ping别人，不允许反ping
iptables -t filter -I INPUT -p icmp --icmp-type 8 -j DROP #8是别人发起的请求
iptables -t filter -I INPUT -p icmp --icmp-type 0 -j ACCEPT #
iptables -t filter -I INPUT -p icmp --icmp-type 3 -j ACCEPT #
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240319183115344.png" alt="image-20240319183115344" style="zoom:80%;" />

> 导出备份规则

```sh
iptables-save > /opt/iprules_all.txt
```

> 导入

```sh
iptables-restore < /opt/iprules_all.txt
```

> SNAT 策略

```sh
#静态
iptables -t nat -I POSTROUTING -p all -o ens35 -j SNAT --to-source 10.10.10.21

#动态
iptables -t nat -I POSTROUTING -o ens35 -j MASQUERADE
```

> DNAT 策略

```sh
iptables -t nat -I PREROUTING -d 10.10.10.21 -i ens35 -p tcp --dport 8088 -j DNAT --to-destination
172.16.2.100:80
#将172.16.2.100:80 映射到对外接口10.10.10.21:8088
```



# 计划任务

```sh
at now +1 min
at> echo "My Name is ROOT" > /tmp/root
at> <EOT> 
# 1分钟后执行
```





