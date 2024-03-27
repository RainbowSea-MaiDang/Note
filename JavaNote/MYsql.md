



# 1.Mysql平台安装-使用

安装：

```shell
sudo docker run -itd -p 3306:3306  \
    -e MYSQL_ALLOW_EMPTY_PASSWORD="root" \
    --name mysql \
    mysql \
    --character-set-server=utf8 \
    --collation-server=utf8_general_ci \
    --default-authentication-plugin=mysql_native_password
```

进入：

```shell
#验证是否登录
sudo docker ps

#进入服务
sudo docker exec -it mysql bash

#登录
mysql -uroot -p000000
```

使用：

```sql
--创建数据库
create database if not exists 数据库名;

--删除数据库
drop database if exists hee;

--切换数据库
use `数据库名`;

--查看所有数据库
show databases

#查看表
show 表名;

#查看表结构
desc 表名；

#查看表内容
select * from 表名;
```



## cmd启动关闭mysql

```shell
net start mysql #启动

mysql -u root -p123456  #进入

net stop mysql #关闭

```



## mysql启动报错处理方案：

**ERROR 2003 (HY000): Can‘t connect to MySQL server on ‘localhost‘ (10061)**

```shell
#1、首先以管理员身份启动cmd，要不然服务禁止访问。

#2、关闭服务
net stop mysql

#3、移除服务
mysqld --remove mysql

#4、进入MySQL安装目录（安装目录不是存储目录）中找到data文件，清空其中全部文件

#5、注册服务
mysqld -install

#6、初始化
mysqld --initialize --console

#7、启动服务，并将第6步获取的随机密码进行登录
net start mysql
mysql -u root -p

#8、修改密码
ALTER USER 'root'@'localhost' IDENTIFIED WITH MYSQL_NATIVE_PASSWORD BY '新密码';
```







# 2.操作数据库

## 2.1数据库的列类型

> **数值**

| **tinyint**  | **1字节 十分小**               |          |
| ------------ | ------------------------------ | -------- |
| **smallint** | **2字节 比较小**               |          |
| **int**      | **4字节 标准整形**             | **常用** |
| **bigint**   | **8字节**                      | **常用** |
| **float**    | **4字节**                      |          |
| **double**   | **8字节 精度**                 |          |
| **decimal**  | **字符串形式浮点数，金融计算** | **常用** |

> **字符串**

| **char**    | **字符串固定大小 0-255** |          |
| ----------- | ------------------------ | -------- |
| **varchar** | **可变字符串 0-65536**   | **常用** |
| **text**    | **文本串**               | **常用** |

> **日期时间**

| **data**      | **YYYY-MM-DD  日期**               |          |
| :------------ | ---------------------------------- | -------- |
| **time**      | **HH:mm：ss  时间**                |          |
| **datetime**  | **YYYY-MM-DD HH:mm：ss  日期时间** | **常用** |
| **timestamp** | **时间戳  1970.1.1到现在的毫秒数** | **常用** |





## 2.2数据库的字段属性

| Unsingned      | 无符号整数，不能声明为负数                                   |
| -------------- | ------------------------------------------------------------ |
| zerofill       | 不足的位数使用0来填充                                        |
| null           | 如果不填，默认为null                                         |
| not null       | 非空，如果不赋值则报错                                       |
| auto_increment | 自增。自动在上一条记录基础上+1（默认） 通常用于设置主键      |
| default        | 默认。设置默认的值，如果不指定该列值，则有默认值             |
| comment        | 注释 ，用于注释字段含义 例如        `id`  int(4) comment '学号'; |

列级完整性约束

| not null    | 限制列取值非空     |
| ----------- | ------------------ |
| default     | 指定列的默认值     |
| unique      | 限制列取值不能重复 |
| check       | 限定列取值范围     |
| primary key | 定义主码           |
| foreign key | 定义外码           |





## 2.3创建数据库表

> ```sql
> //格式
> create table [if not exists] `表名`(
>   '字段名'   列类型   [属性]  [索引]  [注释]
> ）[表类型] [字符集设置] [注释]
> ```

```sql
create table if not exists `student`(
	`studentno` int(4) not null comment '学号',
    `studentname` varchar(20) default null comment '学生姓名',
    `email` varchar (50) not null comment '邮箱账号允许为空',
    `identitycard` varchar(18) default null comment '身份证号',
    primary key (`studentno`),
    unique key `identitycard`(`identitycard`),
    key `email` (`email`)
)engine=InnoDB default charset=utf8;
```



## 2.4修改表

> 修改表名

```sql
--格式  alter table 旧表名 rename as 新表名
alter table t1 rename as t2;
```

> 增加表字段

```sql
--格式 alter table 表名 add 字段名 列属性
alter table t2 add id int(10);
```

> 修改表字段(重命名，修改约束)

```sql
alter table t2 modify id varchar(10);   --修改约束
alter table t2 change id ids varchar(10);  --重命名
```

> 删除表的字段

```sql
alter table t1 drop ids;
```

> 删除表

```sql
drop table if exists t2;
```

> 清空表 (完全清空)  与delete区别：truncate会让自增列归零，重新计数

```sql
truncate t1;
```





 

# 3.DML数据库操纵语言-增删改

| 关键字 |   作用   |                             用法                             |
| :----: | :------: | :----------------------------------------------------------: |
| insert | 插入语句 | insert  into 表名（[字段1，字段2···]）values （'值1'，‘值2'),（'值1'，‘值2') |
| update | 修改语句 | update  表名  set  原值1=新值1，[原值2=新值2]  where [条件]  |
| delete | 删除语句 |                delete from 表名 where [条件]                 |





# 4.DQL数据库查询语言-查

> select完整语法  [可选]   {必选} 

```sql
select [all | distinct]
{* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,···]]}
from table_name [as table_alias]
	[left | right | inner join table_name2]  --联合查询
	[where ...] --指定结果需要满足的条件
	[group by ...]  --指定结果需要按照哪几个字段来分组
	[having] --过滤分组的记录必须满足的条件
	[order by ...] --指定查询记录按一个或多个条件排序
	[limit {[offset,]row_count | row_countOFFSET offset}]; --指定查询的记录从哪条至哪条
```

**数据库中表达式**

```sql
select version();  --查询系统版本 （函数）
select 100*3-1 as '计算结果';  --用于计算 （表达式）
select `max`+1 as '修改后' from t1;  --列数据全部加一显示
```



## 4.1别名as-连接concat-去重distinct

> 关键字

| 关键字       | 含义       | 用法                                                         |
| ------------ | ---------- | ------------------------------------------------------------ |
| as           | 取别名     | **select** [列1] **as** [新名] **from** 表名 **as** [新表名] |
| concat       | 连接       | **select concat**  ([字符],[列名])  **from** 表名            |
| concat_ws    | 多字段连接 | **select concat_ws**  ([连接符],[列名1],[列名2])  **from** 表名 |
| group_concat | 纵向拼接   | **select group_concat**  列名  **from** 表名                 |
| distinct     | 去重       | **select distinct** 列名  **from** 表名                      |

 **别名 -as**

```sql
--给列取别名
select `id` as '学号' from t1;

--给表取别名
select * from t1 as t;
```

**连接-concat**

```sql
--连接学号和id
select concat('学号:',id) from t1;
```

**多字段连接-concat_ws**

```mysal
select concat_ws(':',id,name,pwd) from t1;
```

**去重-distinct**

```sql
--去除相同的id
select distinct id from t1;
```





## 4.2where条件子句

作用：检索数据中符合条件的值

搜索条件由一个或多个表达式组成   结果布尔值

> **运算符**

| 运算符              | 语法                   | 描述            |
| ------------------- | ---------------------- | --------------- |
| and   &&            | A and B      A&&B      | 逻辑与          |
| or     \|\|         | A or B          A\|\|B | 逻辑或          |
| not    ！           | not A           !A     | 逻辑非          |
| between ... and ... | between A and B        | [A,B]    AB区间 |

> **比较运算符**

| 运算符      | 语法            | 描述                                            |
| ----------- | --------------- | ----------------------------------------------- |
| is null     | A is null       | 如果操作符为空，返回真                          |
| is not null | A is not null   | 如果操作符不为空，返回真                        |
| like        | A like B        | sql匹配，如果A匹配到B，返回真                   |
| in          | A in(a,b,c)     | A在a,b,c其中某一个，返回真  (相当于a or b or c) |
| not in      | A not in(a,b,c) | A不在a,b,c中，返回真                            |
|             |                 |                                                 |



### 4.2.1模糊查询 -like

condition表示参数 SQL LIKE子句中，使用%字符来表示任意字符，如果没有使用任何%，那么此时LIKE相当于=

```sql
SELECT * FROM 表名 WHERE 条件 LIKE 条件;
```

实例：搜索表中带孙的人 timi_adc表   hero_name名字属性

```sql
SELECT * FROM timi_adc WHERE hero_name LIKE '%孙%';
```

实例：_占位，有几个表示占几位 下例表示三个字中，后两个字为尚香的

```sql
SELECT * FROM timi_adc WHERE hero_name LIKE '_尚香';
```

实例：查询名字里面没有孙的数据

```sql
SELECT  * FROM timi_adc WHERE hero_name NOT LIKE '%孙%';
```

==注意：==

- %孙%  表示这个字符串含孙
- 孙%  表示这个字符以孙开头
- %孙  表示这个字符串以孙结尾
- _     一个表示一位

---

### 4.2.2精确查询 -in/not in

```sql
SELECT * FROM table_name WHERE column IN (condtionA,condtionB);
```

实例:查询fever属性值位为T0 和T3的数据 IN可以简化语法     等价与SELECT * FROM timi_adc WHERE fever = 'T0' OR fever = 'T3';

```sql
SELECT  * FROM timi_adc WHERE fever IN ('T0', 'T3');
```

实例: NOT IN 就是否定这个条件 就是查询非T0的所有数据   注意：即使只有一个属性 也不能省略括号

```sql
SELECT  * FROM timi_adc WHERE fever NOT IN ('T0');
```





## 4.3结果去空格及字符串替换-trim

 数据库记录的是用户输入的数据，用户输入时的数据通常不是我们所预期的，有时候会包含空格等不需要字符从而产生脏数据，为了保持数据的格式正确，我们会经常使用TRIM函数来清理数据语法非常简单，就是把需要去除空格的数据放在TRIM ()函数的括号里

> 去空格TRIM      语法：TRIM (str)

```sql
--  实例  INSERT语句添加有空格的数据  SELECT查询并去除结果的空格（并不能修改原数据）
INSERT INTO timi_adc VALUES( 20,'   鲁班七号', 'T1  ', 0.5111,0.2300,0.0944,now(),now())
SELECT trim(hero_name),trim(fever) FROM timi_adc WHERE id = 20;
```

> TRIM函数可以加上LEADING来只除去前面的空格，或者加上TRAILING来只除去后面的空格，如果都不加，默认BOTH

```sql
TRIM( BOTH|LEADING|TRAILING removed_str FROM str);
```

> TRIM函数可以删除指定的字符串内容，如果不加，默认删除空格

```sql
--实例 去除id为21的数据中fever尾部的Q
SELECT TRIM(TRAILING 'Q' FROM fever)FROM timi_adc WHERE id = 21;
```

可以把找到的某个字符串替换成另一个字符串，但是这个操作也可以由UPDATE完成 

```sql
UPDATE table_name 
SET colunm_name = REPLACE(column_name,string_find,string_to_replace)
WHERE conditions;
```





## 4.4排序-ORDER BY

> 对结果排序         以field_name参数来排序  排序默认升序【ASC】（一般不写） 【 DESC】逆序
>

```sql
SELECT * FROM table_name ORDER BY field_name;
```

> 实例：升序
>

```sql
SELECT * FROM timi_adc ORDER BY win_rate;
```

> 实例：逆序
>

```sql
SELECT * FROM timi_adc ORDER BY win_rate DESC;
```

> 实例：逆序输出前三行 先排序后取行
>

```sql
SELECT * FROM timi_adc ORDER BY win_rate DESC LIMIT 3;
```



## 4.5返回指定行(分页)-LIMIT

> 返回指定行  parameter是LIMIT语句参数
>

```sql
SELECT * FROM table_name LIMIT parameter;
```

> 实例 :查询timi_adc表中第x-y行
>

```sql
SELECT  * FROM  timi_adc   LIMIT 5, 6;
```

> 实例 :查询timi_adc表中第0-y行
>

```sql
SELECT  * FROM  timi_adc   LIMIT 6;
```

> 实例 :查询timi_adc表中第x行
>

```sql
SELECT  * FROM  timi_adc   LIMIT 5, 1;
```



## 4.6分组过滤-group by...having...

分组不能使用where过滤，而是要使用hving

```sql
select `subjectName`,avg(stuResult)as '平均分'  --stuResult分数列求平均    subjectName课程名
from stu s join sturesult r                --连接学生表和分数表
on s.resultId=r.resultId                   --条件：学生表中课程号等于分数表中课程号
group by r.resultName                      --通过什么字段分组
having 平均分>80;                           --过滤条件 
```









## 4.7连表查询 -join ...on...

> 左连接
>

```sql
/*JOIN是关键查询的关键词，基础结构是 TableA JOIN TableB 即表A和表B的关联查询
LEFT 表示左连接  左连接就是返回左表的所有数据，即使右表没有匹配的数据（此时右表会以NULL形式匹配数据）
ON 是关键查询的条件
*/
SELECT * FROM TableA  LEFT  JOIN TableB ON condition;
```

> 右连接
>

```sql
SELECT * FROM TableA RIGHT JOIN TableB ON condition;
```

> 内连接

```sql
/*INNER 可以省略不写 左右连接都是外连接*/

/*查询同时拥有两表共有属性的数据（满足A同时满足B）*/
SELECT * FROM Table_A  INNER JOIN Table_B ON Table_A.id = Table_B.student_id;


/*查询A中和B完全没有关系的数据（满足A同时不满足B）*/
SELECT * FROM Table_A LEFT JOIN Table_B ON Table_A.id = Table_B.student_id
WHERE Table_B.student_id IS NULL;
```

> 多表连接

```sql
/*
在实际应用中，会对三张以上表查询
会选择一张表为主表，以它为基准，进行查询
*/
SELECT * FROM TableA  LEFT JOIN TableB ON conditionA
                      LEFT JOIN TableC ON conditionB
```





## 4.8 联合查询 union

将两张表纵向拼接，要求：字段数目必须相同；

```mysql
select * from TableA union select * from TableB;
```

union可以不直接接表明，使用null代替列名(TableA有几列，null就有几个)

```sql
select * from TableA union select null,null;
```





## 4.9子查询与嵌套查询

```mysql
SELECT * FROM TableA where id in(SELECT uid FROM TableB );
```









# 5.Mysql函数

## 5.1常用函数

> 数学运算

```sql
select abs(-9);  --绝对值
select ceiling(9.4); --向上取整
select floor(9.4);   --向下取整
select radn();   --0-1随机数
select sign(-9);  --判断符号 0-0 正负数返回±1
```

> 字符串函数

```sql
select char_length('werr'); --字符串长度
select concat('ww','22'); --拼接字符串
select lower('qwe'); --小写转换大写
select upper('WW');  --大写转换小写
select reverse('qwer');  --字符串反转
```

> 日期时间函数

```sql
select current_date() --获取当前日期
select curdate()  --获取当前日期
select now()  --获取当前时间
select localtime() --本地时间
select year(now()) --当前年   year()  month()  day()
```



## 5.2聚合函数（统计函数）

| 函数名称  | 描述   |
| --------- | ------ |
| count（） | 计数   |
| sum（）   | 求和   |
| avg（）   | 平均值 |
| max（）   | 最大值 |
| min（）   | 最小值 |

> **count**

```sql
SELECT COUNT(seat_address) FROM`mtime_hall_dict_t`;   -- 指定列名去查，是会忽略null值

-- count(*)和count(1)是不会忽略null值
-- 查询条件中没有索引时，count(*)比count(1)查询速度要快些。
-- 查询条件中有索引时，count(1)比count(*)查询速度要快些。
SELECT COUNT(1) FROM`mtime_hall_dict_t`;
SELECT COUNT(*) FROM`mtime_hall_dict_t`;
```

> **sun  avg max min**

```sql
select sum(result) as '总分' from stu;  --查总分
select avg(result) as '平均分' from stu;  --查平均分
select max(result) as '最高分' from stu;  --查平均分
select min(result) as '最低分' from stu;  --查平均分
```



# 6.元数据库information_schema

![image-20240318132423487](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240318132423487.png)

> 查询所有数据库名

```mysql
select schema_name from information_schema.schemata;
```

> 查询某一数据库下的表名

```mysql
select table_name from information_schema.tables where table_schema="数据库名";
```

> 查询某一数据库中某一表的字段名

```mysql
select column_name from information_schema.columns where ctable_schema="数据库名" and table_name="表名";
```

---



# 7.远程管理

> 1.查询mysql用户的可登录位置 (host)

```mysql
select user,password,host from mysql.user;
```

> 2.授权 -格式：grant 授权内容 on  库名.表名 to 用户名@登录主机ip  identified by 密码;

```mysql
grant all on  T.* to 'root'@'192.168.1.1' identified by '123456';
```

> 3.撤权-格式：revoke 撤权内容 on 库名.表名 from  用户名@登录主机ip

```mysql
revoke all on  T.* from 'root'@'192.168.1.1';
```

---



# 8.安全模式重置密码

> 条件：

- 必须是Linux的root账户
- 必须先停止mysql的数据库工作
- 以安全模式启动mysql

---

```sh
systemctl stop mariadb.service  #停止
mysqld_safe --skip-grant-table &   #安全模式启动
mysql -uroot   #此时无需密码进入
```

```mysql
update mysql.user set password=password('123456') where host='localhost' and user='root'; #修改密码
```

重启并登录；

---





# 9.数据库md5密码加密

> 加密

```sql
create table `userpwd`(
	`id` int(10) not null,
    `name` varchar(50) not null,
    `pwd` varchar(50)not null,
    primary key(`id`)
)engine=innodb default charset=utf8;

--明文密码
insert into userpwd values (1,'www','12345'),(2,'qqq','12345');

--md5加密
update userpwd set pwd=md5(pwd); 

插入时加密
insert into userpwd values (3,'eee',md5('12345'))
```

> 效验

```sql
--将用户传入的密码，进行md5加密，然后再对比数据库中已加密的值
select * from userpwd
where `name`='www' and pwd=md5('12345');
```



# 数据库备份

```sql
#备份数据库(在DOS执行，即cmd)命令行
mysqldump -u 用户名 -p -B 数据库1 数据库2 数据库n >【路径】文件名.sql

#恢复数据库（进入Mysql命令行再执行）
Source 文件名.sql


#备份数据库中的表
mysqldump -u 用户名 -p 数据库 表1 表2 表n >【路径】文件名.sql
```





# 课程内表数据创建语句

```sql
CREATE TABLE timi_adc(
  id INT (10) NOT NULL,
  hero_name VARCHAR (20) NOT NULL,
  fever VARCHAR(10) NOT NULL,
  win_rate DOUBLE NOT NULL,
  appearance_rate DOUBLE NOT NULL,
  ban_rate DOUBLE NOT NULL,
  gmt_created datetime,
  gmt_modified datetime,
  PRIMARY KEY (id)
) ENGINE = InnoDB DEFAULT CHARSET = utf8;
INSERT INTO
  timi_adc
VALUES
  (1, '后羿', 'T0', 0.4995, 0.3290, 0.0108, now(), now());
INSERT INTO
  timi_adc
VALUES
  (2, '鲁班七号', 'T0', 0.5062, 0.3030, 0.044, now(), now());
INSERT INTO
  timi_adc
VALUES
  (3, '狄仁杰', 'T2', 0.5082, 0.1000, 0.0016, now(), now());

INSERT INTO
  timi_adc
VALUES
  (4, '虞姬', 'T1', 0.5111, 0.2300, 0.0944, now(), now()),
  (5, '伽罗', 'T0', 0.5261, 0.1150, 0.6212, now(), now()),
  (6, '成吉思汗', 'T3', 0.5251, 0.0310, 0.002, now(), now()),
  (7, '黄忠', 'T1', 0.5150, 0.1810, 0.0264, now(), now()),
  (8, '孙尚香', 'T0', 0.4969, 0.3150, 0.0212, now(), now()),
  (9, '李元芳', 'T1', 0.4948, 0.1600, 0.0072, now(), now()),
  (10, '艾琳', 'T3', 0.4935, 0.001, 0, now(), now()),
  (11, '百里守约', 'T2', 0.4771, 0.095, 0.0448, now(), now()),
  (12, '蒙犽', 'T2', 0.4682, 0.077, 0.152, now(), now()),
  (13, '马可波罗', 'T2', 0.4678, 0.1270, 0.0088, now(), now()),
  (14, '公孙离', 'T2', 0.4644, 0.0630, 0.0228, now(), now());
DROP Table if EXISTS user; /* user如果存在则删除 */

CREATE TABLE user ( 
`id` VARCHAR (40)NOT NULL,
`login_name` VARCHAR (20) NOT NULL,
`password` VARCHAR(50) NOT NULL,
`mobile` VARCHAR(20) NOT NULL,
`email` VARCHAR(50) ,
`name` VARCHAR(50) NOT NULL,
`gender` VARCHAR(10) NOT NULL,
`gmt_created` datetime ,
`gmt_modified` datetime ,
PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP Table if EXISTS questionnaire;

CREATE TABLE questionnaire ( 
`id` VARCHAR (40)NOT NULL,
`title` VARCHAR (40) NOT NULL,
`description` TEXT NOT NULL,
`status` VARCHAR(20) NOT NULL,
`content` TEXT NOT NULL,
`author` VARCHAR(40) NOT NULL,
`gmt_created` datetime ,
`gmt_modified` datetime ,
PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

DROP Table if EXISTS reply;

CREATE TABLE reply ( 
`id` VARCHAR (40)NOT NULL,
`ques_id` VARCHAR (40) NOT NULL,
`ques_index` int(20) NOT NULL,
`user_id` VARCHAR(40) NOT NULL,
`content` TEXT NOT NULL,
`gmt_created` datetime ,
`gmt_modified` datetime ,
PRIMARY KEY ( `id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO
  user (
    id,
    gmt_created,
    gmt_modified,
    login_name,
    `password`,
    mobile,
    email,
    name,
    gender
  )
VALUES
  (
    "9ea0409f-c220-48b6-8874-7fd5451acac4",
    now(),
    now(),
    "帅子张三",
    "woshizhangsan",
    "13426498073",
    null,
    "张三",
    "male"
  ),(
"2ec231fe-2e3c-41ce-8782-a2b1af3c5323",
now(),
now(),
"妖艳李四",
"woshilisi",
"13449898073",
"1019837689@qq.com",
"李四",
"female"
  ),
  ("63e882ba-a7cd-443e-85cc-efda1507df56",
  now(),
  now(),
  "强壮王五",
  "woshiwangwu",
  "13758980765",
  null,
  "王五",
  "male"
  ),(
"119ba44f-e85d-47cc-a864-03eefcc9bf7a",
now(),
now(),
"橘子",
"woshijuzi",
"18901345890",
"xixue@126.com",
"橘右京",
"male"
  ),
  (
"b308f450-eee6-4def-8967-9d7c09dbebca",
now(),
now(),
"不知好歹",
"woshibuzhihaodai",
"17897634890",
"fengdie@sina.com",
"不知火舞",
"female"
  )

INSERT INTO questionnaire
(id,title,`description`,`status`,content,author,gmt_created,gmt_modified)
VALUES(
"110d5051-36df-47b0-a768-0be2e69318eb",
"这是一张调查你对于公司的一些想法的问卷",
"尊敬的女士/先生： 您好！为了了解小区安保满意度状况，我们受XX单位/机构的委托正在XX小区进行网上调查。非常感谢您能够作为该小区的代表参加调查，提供您的看法与意见，希望能够得到您的大力支持与合作。本调查不记名，数据由后台统一处理。能倾听您的意见，我们感到十分荣幸。谢谢！",
"inuse",
'[{"title":"您的职位","type":"singleChoice","option":[{"title":"技术","score":0},{"title":"设计","score":0},{"title":"市场","score":0},{"title":"运营","score":0},{"title":"销售","score":0},{"title":"行政","score":0}]},{"title":"您的工作年数","type":"text","option":[{"title":"","score":0}]},{"title":"我的领导对于有想法和意见的员工会鼓励","type":"singleChoice","option":[{"title":"非常不同意","score":-4},{"title":"比较不同意","score":-2},{"title":"一般","score":0},{"title":"非常同意","score":2},{"title":"非常同意","score":4}]},{"title":"我满意公司配备的办公设备","type":"singleChoice","option":[{"title":"非常不同意","score":-2},{"title":"比较不同意","score":-1},{"title":"一般","score":0},{"title":"非常同意","score":1},{"title":"非常同意","score":2}]}]',
"b308f450-eee6-4def-8967-9d7c09dbebca",
now(),now()
)

INSERT INTO reply(
id,ques_id,ques_index,user_id,content,gmt_created,gmt_modified
)
VALUES
(
'0539bdb9-8c40-4982-be72-00674e3ea41e',
'110d5051-36df-47b0-a768-0be2e69318eb',
'1',
'63e882ba-a7cd-443e-85cc-efda1507df56',
'技术',
now(),
now()

),
(
'259e2e48-7bed-405b-803f-c4a17b935932',
'110d5051-36df-47b0-a768-0be2e69318eb',
'2',
'110d5051-36df-47b0-a768-0be2e69318eb',
'十年',
now(),
now()
)
```



子查询后需要的表

```sql
create database if not exists `school`;
-- 创建一个school数据库
use `school`;-- 创建学生表
drop table if exists `student`;
create table `student`(
	`studentno` int(4) not null comment '学号',
    `loginpwd` varchar(20) default null,
    `studentname` varchar(20) default null comment '学生姓名',
    `sex` tinyint(1) default null comment '性别，0或1',
    `gradeid` int(11) default null comment '年级编号',
    `phone` varchar(50) not null comment '联系电话，允许为空',
    `address` varchar(255) not null comment '地址，允许为空',
    `borndate` datetime default null comment '出生时间',
    `email` varchar (50) not null comment '邮箱账号允许为空',
    `identitycard` varchar(18) default null comment '身份证号',
    primary key (`studentno`),
    unique key `identitycard`(`identitycard`),
    key `email` (`email`)
)engine=InnoDB default charset=utf8;




-- 创建年级表
drop table if exists `grade`;
create table `grade`(
	`gradeid` int(11) not null auto_increment comment '年级编号',
  `gradename` varchar(50) not null comment '年级名称',
    primary key (`gradeid`)
) engine=innodb auto_increment = 6 default charset = utf8;



-- 创建科目表
drop table if exists `subject`;
create table `subject`(
	`subjectno`int(11) not null auto_increment comment '课程编号',
    `subjectname` varchar(50) default null comment '课程名称',
    `classhour` int(4) default null comment '学时',
    `gradeid` int(4) default null comment '年级编号',
    primary key (`subjectno`)
)engine = innodb auto_increment = 19 default charset = utf8;



-- 创建成绩表
drop table if exists `result`;
create table `result`(
	`studentno` int(4) not null comment '学号',
    `subjectno` int(4) not null comment '课程编号',
    `examdate` datetime not null comment '考试日期',
    `studentresult` int (4) not null comment '考试成绩',
    key `subjectno` (`subjectno`)
)engine = innodb default charset = utf8;


-- 插入学生数据 其余自行添加 这里只添加了2行
insert into `student` (`studentno`,`loginpwd`,`studentname`,`sex`,`gradeid`,`phone`,`address`,`borndate`,`email`,`identitycard`)
values
(1000,'123456','张伟',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011234'),
(1001,'123456','赵强',1,3,'13800002222','广东深圳','1990-1-1','text111@qq.com','123456199001011233'),
(1002,'123456','张伟2',0,1,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011235'),
(1003,'123456','张伟3',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011236'),
(1004,'123456','张伟4',0,3,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011237'),
(1005,'123456','张伟5',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011238'),
(1006,'123456','张伟6',0,1,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011239'),
(1007,'123456','张伟7',0,3,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011212'),
(1008,'123456','张伟8',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011434'),
(1009,'123456','张伟9',0,1,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011634'),
(1010,'123456','张伟10',0,3,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011534'),
(1011,'123456','张伟11',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011734'),
(1012,'123456','张伟12',0,2,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001013234'),
(1013,'123456','张伟13',0,1,'13800001234','北京朝阳','1980-1-1','text123@qq.com','123456198001011834');



-- 插入成绩数据  这里仅插入了一组，其余自行添加
insert into `result`(`studentno`,`subjectno`,`examdate`,`studentresult`)
values
(1000,1,'2013-11-11 16:00:00',85),
(1000,2,'2013-11-12 16:00:00',70),
(1000,3,'2013-11-11 09:00:00',68),
(1000,4,'2013-11-13 16:00:00',98),
(1000,5,'2013-11-14 16:00:00',58),
(1001,1,'2013-11-11 16:00:00',81),
(1001,2,'2013-11-12 16:00:00',71),
(1001,3,'2013-11-11 09:00:00',61),
(1001,4,'2013-11-13 16:00:00',91),
(1001,5,'2013-11-14 16:00:00',53),
(1002,1,'2013-11-11 16:00:00',55),
(1002,2,'2013-11-12 16:00:00',60),
(1002,3,'2013-11-11 09:00:00',88),
(1002,4,'2013-11-13 16:00:00',98),
(1002,5,'2013-11-14 16:00:00',78),
(1003,1,'2013-11-11 16:00:00',45),
(1003,2,'2013-11-12 16:00:00',60),
(1003,3,'2013-11-11 09:00:00',78),
(1003,4,'2013-11-13 16:00:00',18),
(1003,5,'2013-11-14 16:00:00',58),
(1004,1,'2013-11-11 16:00:00',95),
(1004,2,'2013-11-12 16:00:00',60),
(1004,3,'2013-11-11 09:00:00',48),
(1004,4,'2013-11-13 16:00:00',58),
(1004,5,'2013-11-14 16:00:00',98),
(1005,1,'2013-11-11 16:00:00',75),
(1005,2,'2013-11-12 16:00:00',90),
(1005,3,'2013-11-11 09:00:00',88),
(1005,4,'2013-11-13 16:00:00',58),
(1005,5,'2013-11-14 16:00:00',78),
(1006,1,'2013-11-11 16:00:00',65),
(1006,2,'2013-11-12 16:00:00',70),
(1006,3,'2013-11-11 09:00:00',78),
(1006,4,'2013-11-13 16:00:00',88),
(1006,5,'2013-11-14 16:00:00',48),
(1007,1,'2013-11-11 16:00:00',45),
(1007,2,'2013-11-12 16:00:00',60),
(1007,3,'2013-11-11 09:00:00',78),
(1007,4,'2013-11-13 16:00:00',88),
(1007,5,'2013-11-14 16:00:00',88),
(1008,1,'2013-11-11 16:00:00',95),
(1008,2,'2013-11-12 16:00:00',50),
(1008,3,'2013-11-11 09:00:00',38),
(1008,4,'2013-11-13 16:00:00',48),
(1008,5,'2013-11-14 16:00:00',48),
(1009,1,'2013-11-11 16:00:00',55),
(1009,2,'2013-11-12 16:00:00',60),
(1009,3,'2013-11-11 09:00:00',48),
(1009,4,'2013-11-13 16:00:00',97),
(1009,5,'2013-11-14 16:00:00',58),
(1010,1,'2013-11-11 16:00:00',89),
(1010,2,'2013-11-12 16:00:00',70),
(1010,3,'2013-11-11 09:00:00',68),
(1010,4,'2013-11-13 16:00:00',97),
(1010,5,'2013-11-14 16:00:00',58),
(1011,1,'2013-11-11 16:00:00',84),
(1011,2,'2013-11-12 16:00:00',75),
(1011,3,'2013-11-11 09:00:00',66),
(1011,4,'2013-11-13 16:00:00',97),
(1011,5,'2013-11-14 16:00:00',58),
(1012,1,'2013-11-11 16:00:00',85),
(1012,2,'2013-11-12 16:00:00',74),
(1012,3,'2013-11-11 09:00:00',65),
(1012,4,'2013-11-13 16:00:00',96),
(1012,5,'2013-11-14 16:00:00',57),
(1013,1,'2013-11-11 16:00:00',88),
(1013,2,'2013-11-12 16:00:00',76),
(1013,3,'2013-11-11 09:00:00',67),
(1013,4,'2013-11-13 16:00:00',97),
(1013,5,'2013-11-14 16:00:00',59);


-- 插入年级数据
insert into `grade` (`gradeid`,`gradename`) values(1,'大一'),(2,'大二'),(3,'大三'),(4,'大四'),(5,'预科班');


-- 插入科目数据
insert into `subject`(`subjectno`,`subjectname`,`classhour`,`gradeid`)values
(1,'高等数学-1',110,1),
(2,'高等数学-2',110,2),
(3,'高等数学-3',100,3),
(4,'高等数学-4',130,4),
(5,'C语言-1',110,1),
(6,'C语言-2',110,2),
(7,'C语言-3',100,3),
(8,'C语言-4',130,4),
(9,'Java程序设计-1',110,1),
(10,'Java程序设计-2',110,2),
(11,'Java程序设计-3',100,3),
(12,'Java程序设计-4',130,4),
(13,'数据库结构-1',110,1),
(14,'数据库结构-2',110,2),
(15,'数据库结构-3',100,3),
(16,'数据库结构-4',130,4),
(17,'C#基础',130,1);

```













































