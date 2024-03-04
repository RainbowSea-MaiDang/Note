

# ###########javaSE#######################

# 字符串函数

### 获取字符串长度  lenght

 返回类型：int

 作用：获取字符串长度

 用法：`   int a=b.lenght();`

---

### 获取字符  charAt

返回类型：String

作用：获取字符串内某一下标对应的值

用法：`char a=b.charAt(下标);`

---

### 字符串相同比较 equals

equals("被比较的字符串")；

返回类型：boolean

作用：判断两字符串是否相同

用法：`boolean bool=str.equals("java");`

---

### 字符串大小比较 CompareTo

返回类型：int    ascill差值  大正同零小负

作用：判断两字符串大小关系，按位依次比较

用法：`int ct=str.CompareTo("java");`

---

### 字符串输出 toString

返回类型：String

作用：将当前对象以字符串的形式返回

用法：`System.out.println(date.toString());`

---

### 去除字符  trim

返回类型：String

作用：移除字符串两侧的空白字符或其他预定义字符

用法：`String newa=a.trim(); //去除字符串a左右的空格`

---

### 查找字符  indexof

返回类型：int          正确返回下标，错误返回-1

作用：返回所查字符的下标

用法1：`int index = str.indexOf("要查找的字符串");//返回字符串在str的下标`

用法2：`index = str.indexOf("要查找的字符串", 开始查找的下标);`

结合：`int index = str.indexOf("Java");  //第一次返回的索引`

​         ` index = str.indexOf("Java", index + 4);  //index+4跳过第一次的索引下标`

---

### 字符串拼接  substring

substring(开始索引，结束索引)；

返回类型：String      包含开始索引，不包含结束索引  无结束索引即默认打印开始索引后的全部

作用：返回当前字符串中一个连续的片段

用法1：`String newStr = str.substring(4);`

用法2：`String newStr = str.substring(4，7);`

---

### 字符串开始内容判断  startsWith

返回类型：boolean

作用：检查给定的字符串是否以指定字符串的字符开头

用法：`boolean bool=url.startsWith("字符串");`

---

### 字符串结束内容判断 endsWith

返回类型：boolean

作用：检查给定的字符串是否以指定字符串的字符结尾

用法：` boolean bool=url.endsWith("字符串");`

---

### 字符串替换 replaceAll

replaceAll("要替换的值","新值")

返回类型：String     失败返回原字符串

作用：在字符串中用一些字符替换另一些字符，只返回新字符串，原字符串不变

用法：` String newStr = str.replaceAll("Java","Python");`

---

### 字符串分割 split

split("用以分割字的符串")；

返回类型：Array             '.'   '|'   '*'  这三类要加上"\\"

作用：将文本数据按某个字符分割成数组

用法：`String[] data = text.split("\n");`

---

### 字母转换

全大写：toUpperCase()；

全小写：toLowerCase()；

返回类型：String

作用：将字符串进行大小写转换

用法：`String enName = text.toUpperCase();`

---

### 字符串数字转换

字符串转化数字：Integer.parseInt("字符串")；

用法：`int a = Integer.parseInt("100");`

数字转字符串：String.valueOf(数字)；

 用法：`String str = String.valueOf(a);`

住：数字转字符串也可以：`String str = ""+100;`

---





# 序列化与反序列化

### JSON对象序列化

> 基本格式：
>

1.必须是对象{}或数组[ ]

> 语法规则：

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1668167953243-9e07c0d2-d37a-4c2a-bf9b-31aaf528a405.png)

> 值类型：
>

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1668167977400-96660c19-c6c7-40b0-b85b-17b8e950a1e6.png)

> 值可以是数组对象，就意味着数据和对象可以任意嵌套、任意深度
>
> 如果需要处理LocalDateTime的json数据，不管是序列化还是反序列化，都需要在定义的字段上添加注解：
>

```cpp
@JsonDeserialize(using = LocalDateTimeDeserializer.class)
@JsonSerialize(using = LocalDateTimeSerializer.class)
@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")
```

> 注意：该注解需要Jackson库：

```xml
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.12.4</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jsr310</artifactId>
            <version>2.12.6</version>
        </dependency>
```



### 序列化

> 字符串集合序列化

```java
List<String> Str=new ArrayList<>();
Str.add("hello");
Str.add("world");
ObjectMapper mapper=new ObjectMapper();  //创建Jackson的核心对象ObjectMapper
//import com.fasterxml.jackson.core.type.TypeReference;
try {
    String jsonstr = mapper.writeValueAsString(Str);  //调用writeValueAsString，将指定的对象转换成json
    System.out.println(jsonstr);
}catch (Exception e){
    System.out.println(e);
}
```

> 单个对象序列化{ }

```cpp
User user=new User();
user.setUserName("tom");
user.setPassword("tom123");
user.setGmtCreated(LocalDateTime.now());
ObjectMapper mapper=new ObjectMapper(); 
try {
    String jonsUser = mapper.writeValueAsString(user); 
    System.out.println(jonsUser);
}catch (Exception e){
    System.out.println(e);

}
```

> 集合对象序列化[ ]

```cpp
List<User> users = new ArrayList<>();
User user=new User();
user.setUserName("tom");
user.setPassword("tom123");
user.setGmtCreated(LocalDateTime.now());
users.add(user);
ObjectMapper mapper=new ObjectMapper();
try {
    String jonsUsers = mapper.writeValueAsString(users);
    System.out.println(jonsUsers);
}catch (Exception e){
    System.out.println(e);
}
```



### 反序列化

**将json文件反序列化为User对象**

> 单对象反序列化：{ }

```cpp
ObjectMapper mapper=new ObjectMapper();
try {
    String content = FileUtils.readFileToString(new File("./data/users.json"), "utf-8");//将指定的文件夹中的内容读取出来以String的形式来显示 

    User user = mapper.readValue(content, User.class);
    System.out.println(user.getUserName());
} catch (IOException e) {
    e.printStackTrace();
}
```

**将json文件反序列化为List<User>集合**

> 多对象反序列化[{ },{ }]

```cpp
ObjectMapper mapper=new ObjectMapper();
try {
    String content = FileUtils.readFileToString(new File("./data/users.json"), "utf-8");
    List<User>users=mapper.readValue(content, new TypeReference<List<User>>() {
});//将Json字符串反序列化为List<User>集合
    for (User user : users) {
        System.out.println(user.getUserName());
    }
} catch (Exception e) {
    e.printStackTrace();
}
```



### 将JSON文件读取到集合

> 使用static代码块：
>

```cpp
static{
    //代码
}
```

> static代码块特点：优先执行，只执行一次

---

> 将json文件中的数据读取到集合

```cpp
static{
    if (usersFile.exists()) {//判空
        try {
            String conent = FileUtils.readFileToString(usersFile, "utf-8");//将字符串写入到文件当中
            List<User> users1 = mapper.readValue(conent, new TypeReference<List<User>>() {
        });
            users.addAll(users1); //将集合数据添加到集合
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

> 判断输入数据是否以及存在，存在则return

```cpp
for (User user : users) {
    if(user.getUserName().equals(userNameText)){
        notification.setText("username already reg");
        notification.open();
        return;
    }
}
```



### 反序列化-对象集合-对象数组

json字符串转化为对象集合

```java
public static  List<SongList> songList=new ArrayList<SongList>();
 songList= JSONArray.parseArray(content,SongList.class);
```

json字符串转化为对象数组

```java
SongList[] lists = JSON.parseObject(jsonString, SongList[].class);
```





# 文件读、写、异常

### 实例化

实例化：`File file = new File("路径");`

计算文件大小（字节数）：`long size = file.length();`

配置Apache commons-io

Apache commons-io 是为了简化java Io的操作，可以很轻松的读文件

找到工程文件里的pom.xml文件，在<dependencies>节点里配置如下内容：

```plain
<dependency>
<groupId>commons-io</groupId>
<artifactId>commons-io</artifactId>
<version>2.10.0</version>
</dependency>
```

注：<dependencies>是配置依赖的

### 文件读

con=FileUtils.readFileToString(file,"utf-8"); //将指定的文件夹中的内容读取出来以String的形式来显示 

con=FileUtils.readLines(file,"utf-8"); //按行读

```cpp
//实例化一个文件类型的文件，把指向的文件对象（./data/users.txt）存放到实例化的对象里面。
File nameFile = new File("./data/users.txt");
try {
    //以字符串形式去读取utf-8编码的nameFile里面的文件，存放到定义好的content对象里
    String content = FileUtils.readFileToString(nameFile,"utf-8");
    System.out.println(content);
} catch (IOException e) {
    e.printStackTrace();
}
}
File usersFile = new File("./data/users.txt");
        List<String>users = new ArrayList<>();
        try {
					//按行读取文件，存放到users集合里面
            users = FileUtils.readLines(usersFile,"utf-8");
        } catch (Exception e) {
            e.printStackTrace();
        }
      	//定义一个User类型的集合
        List<User>users1 = new ArrayList<>();
        User user;
      	//遍历users集合
        for (String s : users) {
            user = new User();
          	//每一次遍历把遍历到的内容用split分割成字符串，存放到定义的字符串t里面
            String[] t= s.split(" ");
          	//user集合按位取得字符串里的内容
            user.setUserName(t[0]);
            user.setPassword(t[1]);
            //读取时间
          	user.setGmtCreated(LocalDateTime.parse(strings[2]));
          	//把本次循环里的user集合添加到users1集合里
            users1.add(user);
        }
        	//通过遍历打印users1里面所有用户名
      	for (User user1 : users1) {
            System.out.println(user1.getUserName());
        }
```



### 文件写

```
FileUtils.writeStringToFile(接受的文件,传输的内容,格式);
```

将文件以String形式写出`FileUtils.writeValueAsString(文件)`

将字符串存储为文件，实现永久存储

```cpp
try {
    String conent = mapper.writeValueAsString(users);//转化为json
    File file=new File("./data/users.json");   //打开文件
    FileUtils.writeStringToFile(file,conent,"utf-8");//写入
} catch (Exception e) {
    e.printStackTrace();
}
```



### 异常

```cpp
try
    {
        // 程序代码
    }catch(ExceptionName e1){
        //Catch 块
    }
```

捕获异常快捷键：alt+回车

```cpp
File file=new File("./data/users.txt");
String con=null; 
try{
    con= FileUtils.readFileToString(file,"utf-8");    //必须捕获异常

}catch(Exception e){
    e.printStackTrace();
};
System.out.println(con);
}
```





# 组件

- TextField   用于处理输入框对象

- Button   用于处理按钮行为的对象
- Route   用于处理页面地址的对象
- VerticalLayout  用于处理页面布局的对象



```cpp
垂直布局类：VerticalLayout
水平布局类：HorizontalLayout
文本框输入类：TextField
按钮类：Button
输入框上方文字：.setLabel();
输入框内部提示文字：.setPlaceholder();
输入框内部输入的内容：.setValue();
按钮内部文字输入方法：setText
通知类：Notification
通知类的显示方法：.open
通知类的文本输入方法：.setText
通知类的延时方法：.setDuration
```

## Vaadin

### 输入框组件TextTield

声明：com.vaadin.flow.component.textfield.TextField

实例化：`TextField field = new TextField();`

添加用布局组件，add可以添加任意子组件： `add(field);`

### 布局组件 OrderdLayout

垂直布局声明：com.vaadin.flow.component.orderedlayout.VerticalLayout

水平布局声明：com.vaadin.flow.component.orderedlayout.HorizontalLayout



输入框上有字：`field.setLabel(String label)`

输入框中有提示字：`field.setPlaceholder(String placeholder)`

输入框中有默认值：`field.setValue(String valu`



```cpp
public class Todo extends VerticalLayout {//继承与垂直布局类
    public Todo() {
        TextField userNameField = new TextField();//创建输入框
        TextField passWordField = new TextField();
        String userName ="UserName";
        String passWord ="Password";
        userNameField.setLabel(userName);//输入框上的文字
        passWordField.setLabel(passWord);//输入框上的文字
        userNameField.setPlaceholder("please input userName");//输入框内的提醒
        passWordField.setPlaceholder("please input password");//输入框内的提醒
        add(userNameField,passWordField);//添加窗口
    }
}
```

## button按钮

声明：com.vaadin.flow.component.button.Button

创建一个保存按钮对象并添加信息：Button addButton = new Button("提示信息");

添加提示信息也可以这样：addButton.setText("提示信息");

添加：add(addButton)

## Lambda闭包

给 loginButton 添加一个点击事件：loginButton.addClickListener(click->{});    //click任意



```cpp
 Button loginButton = new Button("Login");//创建按钮并定义按钮名称

        loginButton.addClickListener(click->{// 给 loginButton 添加一个点击事件

            String text = userNameField.getValue();//获取输入框里的内容赋值给text
            String text1 = passwordField.getValue();


        System.out.println(text+"/"+text1+"login"+"fail");

      	add(loginButton);//添加按钮

        });
```

## 逻辑语句

用于登录事件执行后的账户密码判断

```cpp
loginButton.addClickListener(click -> {

    String userNameText = userNameField.getValue();

    if ("admin".equals(userNameText)){
        System.out.println("用户名正确");
    }

});
```

## Notification界面提示

声明：com.vaadin.flow.component.notification.Notification

实例化：`Notification no=new Notification();`

显示的提示内容：`no.setText("success");`

显示时长设置（1000毫秒=1秒）： `no.setDuration(3000);`

显示提示框： `no.open();`

```cpp
  Notification notification = new Notification();
  notification.setDuration(3000);
  notification.setText("success");
  notification.open();
```

## 注解@Route("")

支持多界面，“”中填写地址

```cpp
@Route("/reg.html")
```



# 包装类

![image-20230603195750164](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230603195750164.png)



## 包装类和基本类型的转换

> 装箱

Java将原始类型值转换成对应的包装类型，如将int的变量转换成Integer对象，这个过程叫做装箱。

自动装箱时编译器调用valueOf将基本类型值转换成引用类型。

> 拆箱

将Integer引用类型转换成int类型值，这个过程叫做拆箱

自动拆箱时，编译器通过调用类似intValue()，doubleValue()这类的方法将对象转换成原始类型值。

---

**手动装箱**

```java
int i=1;
Integer integer = new Integer(i);

//或者
Integer integer1 = Integer.valueOf(i);
```

**手动拆箱**

```java
int i1 = integer1.intValue();
```

---

**自动装箱**

```java
int i=1;
 Integer integer=i;   //其底层使用的是Integer.valueOf方法  jdk5以后支持
```

自动拆箱

```java
  int n=integer;     //其底层使用的是 integer1.intValue方法
```



## 包装类的互转

> Integer-->String

```java
Integer i = 100;
//法一
String str1 = i + "";
//法二
String str2 = i.toString();
//法三
String str3 = String.valueOf(i);
```

> String -->Integer-->

```java
 String str="123";
//法一
Integer i1=new Integer(str);  //构造器
//法二
Integer i2=Integer.parseInt(str); //自动装箱
```





## 面试题：Intefer创建机制

> 下列输出结果？

```java
Integer i1=new Integer(1);
Integer i2=new Integer(1);
System.out.println(i1==i2);  //false   两个对象比较 ==判断的是引用


Integer i3=1;
Integer i4=1;
System.out.println(i3==i4);  //true    其底层用的是 Integer.valueOf()


Integer i5=128;
Integer i6=128;
System.out.println(i5==i6);    //false  其底层用的是 Integer.valueOf() 
```

> 原因   --Integer.valueOf()

```java
//这是valueOf源码  This method will always cache values in the range -128 to 127
public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
```

可以看到，valueOf方法有一个值判断，如果不在-128 to 127，则new一个对象。 



## String详解

![image-20230604140957296](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230604140957296.png)

- String实现了Serializable接口 可以串行化 -即可以在网络传输

- String被final修饰，不能被改变（地址而不是字符内容，每次修改都是产生一个新的String）

- String 有属性private final byte[] value; 用于存放字符串内容 

  

  

  ### String面试题

  > 题一：判断下面代码输出结果
  
  ```java
  Person p1=new Person();
  p1.setName("he");
  
  Person p2=new Person();
  p2.setName("he");
  
  System.out.println(p1.getName().equals(p2.getName())); //true  比较的是内容
  System.out.println(p1.getName()==p2.getName());//true   指向的都是常量池中同一个字符串 (地址相同)
  System.out.println(p1.getName()=="he");//true    指向同一个常量池字符串  (地址相同)
  ```

  > 内存图

  ![image-20230604153029850](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230604153029850.png)

  

  ---

  > 题二：以下语句创建了几个对象
  
  ```java
  String str="he";
  str="hehe";   //两个 每次修改都会创建新的String 对象的引用改变了
  ```

  > 内存图 

  ![image-20230604153636599](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230604153636599.png)
  
  

---

> 题三：创建了几个对象

```java
String a="hello"+"abc";

//只有一个
//String a="hello"+"abc";  编译器优化等价于 String a="helloabc";
```

---

> 题四： 创建了几个对象

```java
String a="hello";
String b="abc";
String c=a+b;  //三个 
/*String c=a+b；实际上进行了如下操作：
1.先创建一个StringBuilder sb=StringBuilder()
2.执行 sb.append("hello");
3.执行 sb.append("abc");
4.String c=sb.toString()
最后实际上是 c指向堆种的对象(String)value[] ->池中“helloabc"
*/
```

> 内存图

![image-20230604155013024](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230604155013024.png)

注意：

- String c=”hello“+”abc";常量相加  看的是池
- String c=a+b; 变量相加 是在堆中



---

## StringBuffer



> 创建方法

```java
//创建一个大小为16的 char[] ，用于存放字符内容
StringBuffer stringBuffer1=new StringBuffer();

//通过构造器指定 char[] 大小
 StringBuffer stringBuffer2=new StringBuffer(50);

//通过给一个Strintg 创建StringBuffer  char[] 大小就是 String.length（）+16
 StringBuffer stringBuffer3=new StringBuffer("hello");
```



### StringBuffer转换

> StringBuffer---->String

```java
StringBuffer stringBuffer=new StringBuffer("hello");

//法一
String s = stringBuffer.toString();
//法二
String s1=new String(stringBuffer);
```

> String---->StringBuffer

```java
String str="hello";

//法一
StringBuffer stringBuffer1=new StringBuffer(str);
//法二
StringBuffer stringBuffer2 = new StringBuffer().append(str);
```



### StringBuffer增删改查

> 增

```java
StringBuffer stringBuffer=new StringBuffer("hello");

stringBuffer.append(" ");
stringBuffer.append("world").append(10).append(true);
System.out.println(stringBuffer);  //结果：hello world10true    
```

> 删

```java
stringBuffer.delete(0,5); //删除索引为>=start && <end处的字符（0-4）
```

> 改(替换)

```java
stringBuffer.replace(0,5,"你好");  //替换0-4处字符为你好
```

> 查（查找指定子串第一次出现的索引）

```java
int indexOf = stringBuffer.indexOf("world");
```

> 插入（在指定位置插入,原位置字符自动后移）

```java
stringBuffer.insert(0,"hello"); 
```



### StringBuffer面试题

> 题目一：将空String转换为StringBuffer，会输出什么

```java
String str=null;

//StringBuffer stringBuffer=new StringBuffer(str); 注意:使用构造器会报错，因为构造器设置@NotNull

stringBuffer.append(str);  

System.out.println(stringBuffer); //null
System.out.println(stringBuffer.length());  //4

```

> 原因------>源码

```java
//  stringBuffer.append源码 若传入值为null，则调用父类append
public synchronized StringBuffer append(String str) {
        toStringCache = null;
        super.append(str);
        return this;
    }

//其父类 AbstractStringBuilder的append源码  若值为null 则调用appendNull方法
    public AbstractStringBuilder append(String str) {
        if (str == null) {
            return appendNull();
        }
        int len = str.length();
        ensureCapacityInternal(count + len);
        putStringAt(count, str);
        count += len;
        return this;
    }

//appendNull方法源码
    private AbstractStringBuilder appendNull() {
        ensureCapacityInternal(count + 4);
        int count = this.count;
        byte[] val = this.value;
        if (isLatin1()) {
            val[count++] = 'n';
            val[count++] = 'u';
            val[count++] = 'l';
            val[count++] = 'l';
        } else {
            count = StringUTF16.putCharsAt(val, count, 'n', 'u', 'l', 'l');
        }
        this.count = count;
        return this;
    }
```



## StringBuilder

和StringBuffer用法完全一致





# 数组 Arrays

## 遍历 toString

> 可以使用toString遍历数组

```java
int[] i = {1, 2, 3, 4};

System.out.println(Arrays.toString(i));
```

> toString源码

```java
    public static String toString(int[] a) {
        if (a == null)
            return "null";
        int iMax = a.length - 1;
        if (iMax == -1)
            return "[]";
        
        StringBuilder b = new StringBuilder();
        b.append('[');
        for (int i = 0; ; i++) {
            b.append(a[i]);
            if (i == iMax)
                return b.append(']').toString();
            b.append(", ");
        }
    }
```



---

## 排序 sort

> Arrays.sort方法排序(默认排序升)

```java
int[] i = {1, 2, 3, 4,-5,-3,0};
Arrays.sort(i); //排序
System.out.println(Arrays.toString(i)); //[-5, -3, 0, 1, 2, 3, 4]
```

> 定制排序（排序升降）

```java
        Integer[] arr={1, 2, 3, 4,-5,-3,0};

        Arrays.sort(arr,new Comparator(){
            @Override
            public int compare(Object o1, Object o2) {
                Integer i1= (Integer) o1;
                Integer i2= (Integer) o2;
                return i1-i2;
            }
        });
        System.out.println(Arrays.toString(arr));
```

> 源码分析

```java
//（1）执行
Arrays.sort(arr,new Comparator());
//(2)最终到了
private static <T> void binarySort(T[] a, int lo, int hi, int start,Comparator<? super T> c) {
    ····
     while (left < right) {
                int mid = (left + right) >>> 1;
                if (c.compare(pivot, a[mid]) < 0)
                    right = mid;
                else
                    left = mid + 1;
            }   
    ····    
}
//(3)执行到  binarySort方法的代码，会根据动态绑定机制 c.compare()执行我们传入的匿名内部类compare()
new Comparator(){
            @Override
            public int compare(Object o1, Object o2) {
                Integer i1= (Integer) o1;
                Integer i2= (Integer) o2;
                return i1-i2;
            }
        }
//(4)public int compare(Object o1, Object o2) 返回值是否大于小于0会影响排序的结果

```

---



## 二叉查找 binarySearch

> 前提：数组有序

```java
Integer[] arr={1, 2, 3, 4};

int i1 = Arrays.binarySearch(arr, 3);
System.out.println(i1);
```





## 拷贝 copyOf 

> 从arr数组中，拷贝arr.length个元素到arr1
>
> 如果拷贝长度大于arr.length  就在新数组后面加null  拷贝长度小于零报异常

```java
Integer[] arr={1, 2, 3, 4,-5,-3,0};
        
Integer[] arr1=Arrays.copyOf(arr,arr.length);
```



## 数组元素替换 fill 

> 使用100 去填充arr

```java
Integer[] arr={1, 2, 3, 4,-5,-3,0};

Arrays.fill(arr,100);
System.out.println(Arrays.toString(arr)); //[100, 100, 100, 100, 100, 100, 100]
```









# 日期时间 Date

## 获取时间

```java
//获取当前时间
Date date = new Date();
System.out.println(date);

//通过毫秒数获取时间
Date date = new Date(1008666);
System.out.println(date);
```



## 将当前时间转换为字符串

```java
//创建SimpleDateFormat对象设置格式
SimpleDateFormat simpleDateFormat=new SimpleDateFormat("YYYY年MM月dd日 hh:mm:ss E");
String format = simpleDateFormat.format(new Date()); //调用format将当前日期转换为字符串
System.out.println(format);
```



## 将格式化的字符串转换成Data

```java
String str="2023年06月07日 09:46:13 周三";

SimpleDateFormat simpleDateFormat=new SimpleDateFormat("YYYY年MM月dd日 hh:mm:ss");
Date parse = simpleDateFormat.parse(str);    //转换的date是国外格式   Sun Jan 01 09:46:13 CST 2023

 //如果想输出自定义格式，再使用simpleDateFormat.format转换就可以了
String format = simpleDateFormat.format(parse);
System.out.println(format);
```

> 注意：1.在将String转换为date，使用的SimpleDateFormat格式要和String格式一样，否则抛出转换异常
>
> ​			2.在将String转换为date，转换的date是国外格式



# 日历

```java
//Calendar是一个抽象类，并且构造器是private  只能getInstance获取实例，不能new

Calendar instance = Calendar.getInstance();//创建日历类对象
System.out.println(instance);
/*会输出大量字段：java.util.GregorianCalendar[time=1686104901715,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=19,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2023,MONTH=5,WEEK_OF_YEAR=23,WEEK_OF_MONTH=2,DAY_OF_MONTH=7,DAY_OF_YEAR=158,DAY_OF_WEEK=4,DAY_OF_WEEK_IN_MONTH=1,AM_PM=0,HOUR=10,HOUR_OF_DAY=10,MINUTE=28,SECOND=21,MILLISECOND=715,ZONE_OFFSET=28800000,DST_OFFSET=0]*/
```

> 获取日历对象的某个字段

```java
System.out.println("年"+instance.get(Calendar.YEAR));
System.out.println("月"+instance.get(Calendar.MONTH));
System.out.println("日"+instance.get(Calendar.DAY_OF_MONTH));
System.out.println("明日"+instance.get(Calendar.DAY_OF_MONTH)+1);

//Calendar没有专门的格式化方法，需要程序员直接组合
System.out.println(instance.get(Calendar.YEAR)+"年"+
                   instance.get(Calendar.MONTH)+"月"+
                   instance.get(Calendar.DAY_OF_MONTH)+"日");
```

> 注意：如果想以24小时制显示时间，Calendar.HOUR 改为Calendar.HOUR_OF_DAY





# 第三代日期时间LocalDateTime

日期：yyyy-MM-dd 

时间：HH:mm:ss 

带毫秒的时间：HH:mm:ss.SSS 

日期和时间：yyyy-MM-dd'T'HH:mm:ss 

带毫秒的日期和时间：yyyy-MM-dd'T'HH:mm:ss.SSS





## 返回当前时间 now

用法：`LocalDate now = LocalDate.now();// 得到当前的完整日期（不包括时间）`

​         ` System.out.println(now.toString());// 打印出日期`

得到当前年：`int year = time.getYear();`

得到当前月： `int month = time.getMonth().getValue();`

得到当前日：`int day = time.getDayOfMonth();`

得到当前周：` int dayOfWeek = time.getDayOfWeek().getValue();`

得到当前完整时间：`LocalDateTime loc=LocalDateTime.now(); //日期+时间`



## 获取时间

```java
LocalDateTime localDateTime=LocalDateTime.now();
System.out.println(localDateTime);
```



## 将当前时间转换为日期

```java
LocalDateTime localDateTime=LocalDateTime.now();
DateTimeFormatter dateTimeFormatter=DateTimeFormatter.ofPattern("YYYY年MM月dd日 hh:mm:ss");
String format = dateTimeFormatter.format(localDateTime);
System.out.println(format);
```







## 计算时间日期

> 天数加减  plusDays(天数)          minusDays(天数)

```java
LocalDate leaveTime = time.plusDays(days); //加days天
LocalDate leaveTime=time.minusDays(days);   //减去days天
```

> 月数加减    plusMonths(月数)         minusMonths(月数)

```java
LocalDate leaveTime = time.plusMonths(mons);//加mons天
LocalDate leaveTime=time.minusMonths(mons);//减mons天
```

> 年数加减   plusYears(年数)          minusYears(年数)

```java
LocalDate leaveTime = time.plusYears(years);  //加years年
LocalDate leaveTime=time.minusYears(years);   //减years年
```

> 周数加减    plusWeek(周数)         minusWeek(周数)

```java
LocalDate leaveTime = time.plusWeek(weeks); //加weeks周
LocalDate leaveTime=time.plusWeek(weeks);  //减weeks周
```



## 两个日期的判断

> 返回boolean

```java
boolean bool=time1.isBefore(time2); //之前

boolean bool=time1.isAfter(time2);  //之后

boolean bool=time1.isEqual(time2);  //当天
```



# 集合

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230609101530653.png" alt="image-20230609101530653" style="zoom:50%;" />

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230609101604149.png" alt="image-20230609101604149" style="zoom:50%;" />

集合分为单列集合Collection 和双列集合Map

---





## Collection接口遍历元素-迭代器

Iterator对象称为迭代器，主要用于遍历Collection集合中的元素，所有实现Collection接口的集合类都有iterator方法

Iterator仅用于遍历集合，本身并不存放对象

**如果要二次遍历，需要重置Iterator 即新创一个**

```java
ArrayList list=new ArrayList<>();
list.add(new Book("java基础","余胜军"));
list.add(new Book("数据结构","jacker"));

        Iterator iterator = list.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println(next);
        } 
//book{name='java基础', author='余胜军'}
//book{name='数据结构', author='jacker'}
```



## Collection接口遍历元素-增强for循环

增强for循环可以代替Iterator迭代器

增强for循环就是简化的Iterator(其底层就是Iterator)，本质一样，只能用于遍历集合和数组.

```java
for (Object o : list) {
    System.out.println(o);
}
```



## List

List添加基础数据类型时，会有一个自动装箱的过程，即会把基础类型转换成对应的包装类

> 常用方法

```java
//add  添加单个元素
list.add("w");
list.add("b");
list.add(10); //自动装箱为包装类Integer

//addAll 添加多个元素
ArrayList list1=new ArrayList<>();
list1.add("ll");
list.addAll(list1);  //所有Collection的子类都可以加入 返回bool
list.addAll(0，list1);  //所有Collection的子类都可以加入 从下标0开始将list1所有元素插入 返回bool


//size 获取元素个数
System.out.println(list.size());

//isEmpty 判断是否为空
System.out.println(list.isEmpty());


//remove 删除指定元素
list.remove(0); //删除第一个元素
list.remove("w"); //删除指定元素

//removeAll 删除多个元素 返回bool
list.removeAll(list1);   //所有Collection的子类


//clear 清空
list.clear();


//contains 查找元素是否存在 返回bool
System.out.println(list.contains("w"));

//containsAll 查找多个元素是否存在
list.containsAll(list1);  //所有Collection的子类



//indexOf 返回首次出现字符的下标
System.out.println(list.indexOf("java基础"));

//lastIndexOf 返回最后出现字符的下标
System.out.println(list.lastIndexOf("java基础"));


//set 替换指定位置字符 索引必须存在
list.set(0,"数据结构");

//subList 返回指定的子集合 【 ）
System.out.println(list.subList(0, 2));
```



> ArrayList底层结构：

ArrayList底层是Object数组。若是无参构造创建，则初始容量为0，第一次添加则扩容到10，再次扩容则是1.5倍。若是指定大小构造，则初始容量为指定大小，再次扩容也是1.5倍。

ArrayList 线程不安全



> Vector 【V ke te】

Vector底层是Object数组。若是无参构造创建，则初始容量为10，再次扩展是2倍。若是指定大小构造，再次扩容直接2倍。

Vector 线程安全



> LinkedList

LinkdList底层是双向循环链表，可以添加任意元素，可重复

LinkedList线程不安全



## Set

Set无序不可重复，最多允许一个null对象，无索引，只能使用迭代器取得所有元素，逐一遍历 

插入多个null不会报错，只是加入失败

Set有两个子类 HashSet  TreeSet



> HashSet

对象加入hashSet时，hashSet会先计算对象的hashCode值判断对象加入的位置，如果发现有值，则调用equals方法来检测两个对象是否相同，如果相同就加入失败，如果不同，就散列到其他位置，这样减少了equals的次数，提高了执行速度

- 如果两个对象相等，则hashCode一定相同，反之不成立
- qeuals方法被重写，则hashCode方法也必须重写
- hashCode的值会转化为索引值

**--则 未重写equals的类可以new多个相同内容对象加入HashSet ，String就不可以new多个相同内容对象加入HashSet**

```java
HashSet hashSet=new HashSet<>();
hashSet.add(new Book("111","111"));//ok
hashSet.add(new Book("111","111")); //ok

hashSet.add(new String("111"));//ok
hashSet.add(new String("111"));//no
```

**hashSet底层是hashMap**



> TreeSet

有序（在未作任何处理时无序）

使用无参构造器创建TreeSet时，是无序的

使用TreeSet提供的构造器，可以传入一个比较器，并指定排序规则





## Map

Map用于保存具有映射关系的数据

Map 中key不允许重复，velue可以重复     （key不允许重复原因和set一样，要计算hashCode值 ，所以也是无序的 ）

Map中 hashMap允许null值    HashTable不允许null值

hashMap 线程不安全 ，hashTable线程安全

---

> Map原理 

```
k-v 最后是 HashMap$Node node=newNode(hash,key,value,null)
k-v为了方便程序员的遍历，还会创建EntrySet集合，该集合存放的元素类型Entry ，而一个Entry对象就有 k，v
EntrySet<Entry<k,v>> 即：transient Set<Map.Entry<k,v>> entrySet;
entrySet中，定义的类型是Map.Entry ,但实际上还是存的HashMap$Node

---把HashMap$Node对象存放到entrySet 是为了方便遍历
```

> Map遍历

```java
Map<String, Integer> buy=new HashMap<>();
buy.put("苹果手机", 2);
buy.put("智能手表", 1);

Set<Map.Entry<String, Integer>> entries = buy.entrySet(); //转化为Set集合
for (Map.Entry<String, Integer> entry : entries) { //增强for遍历
     System.out.println(entry.getKey()+":"+entry.getValue());
    }
```



> HashMap

HashMap基于哈希表实现，通过使用键的hashCode()来确定键值对的存储位置，无序不可重复

HashMap线程不安全；

HashMap允许key和value为null（k为null只能有一个），  HashTable不允许；



> HashTable

底层和HashMap一样，基于哈希表实现，无序不可重复

HashTable线程安全；

HashTable不允许k-v为null



> treeMap

TreeMap基于红黑树实现，它根据键的自然顺序或者Comparator  【kan pai er te】来组织键值对 ，自然有序不可重复

treeMap线程不安全；

treeMap不允许k为null，但允许v为null





# 泛型

泛型，即“参数化类型”。

泛型的作用：在类声明时通过一个标识表示类中某个属性的类型以及方法的返回类型

- 代码更加简洁【不用强制转换】
- 程序更加健壮【只要编译时期没有警告，那么运行时就不会抛出ClassCastException的异常】
- 可读性和稳定性【在编写集合的时候，就限定了类型】

---



> ​	往集合添加数据并遍历时

```java
List list=new ArrayList();
```

传统方法的缺点：

不能对加入到集合的数据类型进行约束 

遍历时，需要类型转化，如果集合数据量大，效率低

---

使用泛型：

```java
List<Book> list=new ArrayList<Book>();
```

对加入集合的数据类型进行约束，非Book类加入即报错



---

泛型的作用：在类声明时通过一个标识表示类中某个属性的类型以及方法的返回类型

```java
class Book<E>{
    private E name;  //E表示name的数据类型，该数据类型在定义Book对象时指出，即在编译期间确定E是什么类型
    private E author;
    
    public E getName() {
        return name;
    }    
}

//定义
Book<String> book=new B<String>();
```







# java绘图

Component类提供两个和绘图相关最重要的方法：

- paint(Graphics g) 绘制组件的外观
- repaint() 刷新组件的外观



**画圆案例**

> 先定义一个MyPanel，继承 JPanel 类，画图形            【Panel -画板】  【paint-颜料】 【Graphics-绘画】

```java
//画板类
public class MyPanel extends JPanel {
    
    //绘画方法
    @Override
    public void paint(Graphics g) {
        //调用父类的方法完成初始化
        super.paint(g); 
        
        //画一个圆 x坐标，y坐标(都是距左上角的像素数),宽度，高度
        g.drawOval(10,10,100,100);        
    }

}
```

> 主程序 继承JFrame        【 JFrame-窗口】

```java
//窗口
public class DrawCircle extends JFrame {

    //定义一个画板
    private MyPanel mp = null;

    public static void main(String[] args) {
        //构造
        new DrawCircle();
    }

    public DrawCircle() {
        //初始化面板
        mp = new MyPanel();
        //把面板放入窗口
        this.add(mp);
        //设置窗口大小
        this.setSize(400, 400);
        //设置可视化
        this.setVisible(true);
        //设置叉掉窗口，则退出程序
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

> 问题：只实例化了MyPanel，并未调用paint方法，为什么paint方法会执行？
>
> 原因：当组件第一次在屏幕显示时，程序会自动调用paint方法来绘制组件
>
>  在以下情况paint方法将会被调用：
>
> - 窗口最小化后再最大化
> - 窗口大小发生改变
> - repaint函数被调用



---

## Graphics类绘制方法

Graphics类可以理解为画笔，为我们提供了各种绘制图形的方法

```java
//画直线 起点(x,y) -终点(x,y)
drawLine(int x1,int y1,int x2,int y2)

//画矩形边框 距左上角的距离(x,y)
drawRect(int x,int y,int width,int height)
    
//画椭圆边框
drawOval(int x,int y,int width,int height)
    
//填充矩形
fillRect(int x,int y,int width,int height)
    
//填充椭圆
fillOval(int x,int y,int width,int height)
    
//设置画笔的字体
setFont(Font font)
---g.setFont(new Font("隶书",Font.BOLD,50));  【字体名字，是否粗体，大小】

    
//设置画笔的颜色
setColor(Color c)  
---g.setColor(Color.BLACK);    
    
    
//画图片
drawImage(Image img,int x,int y,...)
    
    
//画字符串
drawString(String str,int x,int y)
```

> 画图片   drawImage(Image img,int x,int y,...)   【图片，坐标x,坐标y,分辨率x,分辨率y，this】

```java
//先获取图片   （固定写法）
Image image = Toolkit.getDefaultToolkit().getImage(Paint.class.getResource("/.bg.png"));

//画图片
drawImage(image,10,10,1080,960,this)
```

---

**实例-绘制坦克**

![image-20230610191646363](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230610191646363.png)







# java事件处理机制

**演示小球通过键盘上下左右控制移动轨迹**

> 先定义一个MyPanel，继承 JPanel 类，画图形, 再实现KeyListener 接口 事务处理 用于获取键盘信息

```java
//继承 JPanel类 绘画 实现 KeyListener 接口 事务处理
public class MyPanel extends JPanel implements KeyListener {
    //坐标
	private static int x=10;
	private static int y=10;

    //绘画
    @Override
    public void paint(Graphics g) {
        super.paint(g);
        g.fillOval(x, y, 30, 30);
    }

    //有字符输出，该方法会触发
    @Override
    public void keyTyped(KeyEvent e) {
    }
    
    //当键盘键按下，该方法触发
    @Override
    public void keyPressed(KeyEvent e) {
        System.out.println((char)e.getKeyCode()+"键被按下");
        //根据按下不同键，来处理移动
        if(e.getKeyCode()==KeyEvent.VK_DOWN){ //KeyEvent.VK_DOWN向下箭头
            y++;
        }
        if(e.getKeyCode()==KeyEvent.VK_UP){ //KeyEvent.VK_UP 向上
            y--;
        }
        if(e.getKeyCode()==KeyEvent.VK_LEFT){//KeyEvent.VK_LEFT 向左
            x--;
        }
        if(e.getKeyCode()==KeyEvent.VK_RIGHT){//KeyEvent.VK_RIGHT 向右
            x++;
        }
        //面版重绘
        this.repaint();
    }

    //当键盘键释放（松开），该方法触发
    @Override
    public void keyReleased(KeyEvent e) {
    }
}
```

> 主程序 继承JFrame

```java
//窗口
public class BallMove extends JFrame {
    //定义画板
	MyPanel myPanel=null;

public BallMove(){
    //初始化面板
    myPanel = new MyPanel();
    //把面板放入窗口
    this.add(myPanel);
    //设置窗口监听键盘事件 ，即可以监听面板myPanel发生的键盘事件
    this.addKeyListener(myPanel);
    //设置窗口大小
    this.setSize(400, 400);
    //设置可视化
    this.setVisible(true);
    //设置叉掉窗口，则退出程序
    this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
    public static void main(String[] args) {
        new BallMove();
    }
}
```

> 注意点：
>
> 绘画类要继承JPanel 且实现KeyListener 
>
> 在执行了KeyListener 中事务方法时，要调用 this.repaint() 方法重绘
>
> 主体窗口要设置监听 this.addKeyListener()



---





# IO 文件

## 文件的创建

> **创建文件对象相关方法**
>
> new File(String pathname)  //根据路径构建一个File对象
>
> new File(File parent,String child)  //根据父目录文件+子路径构建
>
> new File(String parent,String child)  //根据父目录+子路径构建

---

**方式一**  根据路径构建一个File对象

```java
        String filePath = "D:\\news1.txt";
        //构建File对象
        File file = new File(filePath);

        try {
            //创建文件
            file.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            System.out.println("文件创建失败");
        }
```

**方式二**  根据父目录文件+子路径构建

```java
        //构建File对象作为父目录
        File file = new File("D:\\");

        String fileName = "news2.txt";
        //构建完整的File
        File fileNow=new File(file,fileName);

        try {
            //创建文件
            fileNow.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            System.out.println("文件创建失败");
        }
```

**方式三**  根据父目录+子路径构建

```java
		String filePath="D:\\";

        String fileName = "news3.txt";

        File fileNow=new File(filePath,fileName);
        
        try {
            //创建文件
            fileNow.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            System.out.println("文件创建失败");
        }
```

> 注意
>
> File fileNow=new File(); 并不会直接创建文件，这只是构建出一个java的File对象 只有执行 fileNow.createNewFile(); 才能创建对象

---



## 常用文件操作-获取文件信息

```java
        File fileNow=new File("D:\\news1.txt");

        System.out.println("文件名=" + fileNow.getName());
        System.out.println("文件路径="+fileNow.getPath());
        System.out.println("文件绝对路径"+fileNow.getAbsolutePath());
        System.out.println("文件父目录="+fileNow.getParent());
        System.out.println("文件大小（字节）"+fileNow.length());
        System.out.println("文件是否存在(bool)"+fileNow.exists());
        System.out.println("判断是不是一个文件（bool）"+fileNow.isFile());
        System.out.println("判断是不是一个目录（bool）"+fileNow.isDirectory());
```



## 目录操作及文件删除

mkdir 创建一级目录  mkdirs 创建多级目录  delete 删除空目录或文件

> 判断文件是否存在，存在则删除，否则就创建

```java
        File fileNow=new File("D:\\news1.txt");

        if(!fileNow.exists()){
            System.out.println("文件不存在");
            
            try {
                fileNow.createNewFile();
                System.out.println("文件创建成功");
            } catch (IOException e) {
                System.out.println("文件创建失败");
            }
            
        }else {
            System.out.println("文件存在");
            
            if(fileNow.delete()){
                System.out.println("文件删除成功");
            }
            else {
                System.out.println("文件删除失败");
            }
            
        }
```

> 判断目录是否存在，存在就删除，不存在则创建   mkdir

```java
        File fileNow=new File("D:\\news1");

        if(!fileNow.exists()){
            System.out.println("目录不存在");

            if (fileNow.mkdir()) {
                System.out.println("目录创建成功");
            }else {
                System.out.println("目录创建失败");
            }

        }else {
            System.out.println("目录存在");
            if(fileNow.delete()){
                System.out.println("目录删除成功");
            }
            else {
                System.out.println("目录删除失败");
            }
        }
```

> 判断多级目录是否存在，存在就删除，不存在则创建   mkdirs

```java
File fileNow=new File("D:\\news1\\news2");

        if(!fileNow.exists()){
            System.out.println("目录不存在");

            if (fileNow.mkdirs()) {
                System.out.println("目录创建成功");
            }else {
                System.out.println("目录创建失败");
            }

        }else {
            System.out.println("目录存在");
            if(fileNow.delete()){
                System.out.println("目录删除成功");
            }
            else {
                System.out.println("目录删除失败");
            }
        }
```

---





## IO原理及其分类

I/O 是Input/Output的缩写  用于处理数据传输

Java程序中，对于数据的输入输出操作以 流(stream)的方式进行

java.io包下提供各种“流”类和接口，用于获取不同种类的数据，并通过方法输入或输出数据

---

**输入输出**

输入input：读取外部数据（磁盘）到程序（内存）

输出output：将程序（内存）数据输出到磁盘

---

**流的分类**

按操作数据单位不同分为：字节流（8 bit 二进制文件）字符流（按字符 文本文件）

按数据流的流向不同分为：输入流、输出流

按流的角色不同分为：节点流、处理流/包装流

| 抽象基类 | 字节流       | 字符流 |
| -------- | ------------ | ------ |
| 输入流   | InputStream  | Reader |
| 输出流   | OutputStream | Writer |

Java的IO流共涉及40多个类，实际上非常规则，都是从如上4个抽象基类派生的

由这四个类派生出来的子类名称都是以其父类名作为子类后缀名



---

## 字节输入输出流

InputStream抽象类是所有类字节输入流的超类

**InputStream常用的子类：**

1. FileInputStream  文件输入流
2. BufferedInputStream  缓冲字节输入流
3. ObjectInputStream   对象字节输入流 

---

> FileInputStream  (字节输入流     文件---->程序   ) 

```java
//  read（）单字节读取
	public static void main(String[] args) {
        int readData = 0;
        FileInputStream fileInputStream = null;

        try {
            //创建FileInputStream 对象，用于读取文件
            fileInputStream = new FileInputStream("D:\\news1.txt");

            //循环读取 read方法每次从该输入流读取一个字节的数据，如果返回-1，表示读取完毕
            while ((readData = fileInputStream.read()) != -1) {
                //转换为char输出
                System.out.println((char) readData);
            }
        } catch (IOException e) {
            System.out.println(e);
        } finally {
            //释放资源 close
            try {
                fileInputStream.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }

-----------------------------------------------------------------------------------------------
//read（byte[] b）多字节读取
     public static void main(String[] args) {
        byte[] b = new byte[8];
        FileInputStream fileInputStream = null;

        try {
            //创建FileInputStream 对象，用于读取文件
            fileInputStream = new FileInputStream("D:\\news1.txt");
            int readDataLength = 0;
            //循环读取 read(byte[] b)方法每次从该输入流读取8个字节的数据，如果返回-1，表示读取完毕
            while ((readDataLength = fileInputStream.read(b)) != -1) {
                //转换为String输出
                System.out.print(new String(b, 0, readDataLength));
            }
        } catch (IOException e) {
            System.out.println(e);
        } finally {
            //释放资源 close
            try {
                fileInputStream.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
```

---

> FileOutputStream (字节输出流   程序--->文件) 

```java
 public static void main(String[] args) {

        //创建FileOutputStream 对象
        FileOutputStream fileOutputStream = null;


        try {
            //打开文件一（会覆盖原文件数据） 没有自动创建
            // fileOutputStream = new FileOutputStream("D:\\news5.txt");
            //打开文件二 （不覆盖原有数据，在其后追加）
            fileOutputStream = new FileOutputStream("D:\\news5.txt", true);

            //写入一个字符
            fileOutputStream.write('a');

            //写入字符串   getBytes把字符串转换为字节数组
            fileOutputStream.write("bcde".getBytes());

        } catch (Exception e) {
            System.out.println(e);
        } finally {
            try {
                //释放资源
                fileOutputStream.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }

    }
```



## 文件拷贝

思路：1.创建文件输入流，将文件读取到程序中

​           2.创建文件输出流，将程序中文件输出到指定位置

​            3.可以一边读，一边写

```java
    public static void main(String[] args) {

        //创建输入流对象
        FileInputStream fileInputStream = null;
        //创建FileOutputStream 对象
        FileOutputStream fileOutputStream = null;
        //创建byte数组，用于设置一次读取字节数
        byte[] bytes = new byte[1024];

        try {
            //指定输入流文件
            fileInputStream = new FileInputStream("D:\\news1.txt");
            //指定输出流文件
            fileOutputStream = new FileOutputStream("D:\\news11.txt", true);
            //用于记录读取长度
            int readDataLength = 0;

            //输入流输入到程序
            while ((readDataLength = fileInputStream.read(bytes)) != -1) {
                //输出流输出到文件  必须这个方法，不可以直接fileOutputStream.write(bytes);
                fileOutputStream.write(bytes, 0, readDataLength);
            }
        } catch (Exception e) {
            System.out.println(e);
        } finally {
            try {
                //释放资源
                fileOutputStream.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }

    }
```



## 字符输入输出流

**只要以Reader、Writer为后缀的都是字符流**

> **FileReader输入流：**
>
> - new FileReader(File / String);   创建
> - read（）每次读取单个字符返回，到文件末尾返回-1
> - read（char[ ]） 批量读取多个字符到数组返回，到文件末尾返回-1
> - new String（char[ ]）将char[ ]转换成String
> - new String（char [ ],off ,len）将char[ ]的指定部分转换成String

```java
    public static void main(String[] args) {

        int readData = 0;
        char buf[]=new char[8];
        FileReader fileReader = null;

        try {
            //FileReader 对象，用于读取文件
            fileReader = new FileReader("D:\\news1.txt");

            //循环读取 read(buf)，如果返回-1，表示读取完毕
            while ((readData = fileReader.read(buf)) != -1) {
                //可以直接输出  new String(buf,0,readData)是避免最后一次取出不足8位
                System.out.println(new String(buf,0,readData));
            }
        } catch (IOException e) {
            System.out.println(e);
        } finally {
            //释放资源 close
            try {
                fileReader.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
```



---

> **FileWriter 输出流：**
>
> - new FileWriter( File / String)    覆盖模式写入文件
> - new FileWriter(File / String , true)  追加模式写入文件
> - writer(int)  写入单个字符
> - writer(char [ ]) 写入指定数组
> - writer(char[ ],off,len) 写入指定数组的指定部分
> - writer(string) 写入整个字符串
> - writer(string,off,len) 写入字符串的指定部分
>
> 相关API ：String类--- toCharArray：将String转换为char[ ]

```java
public static void main(String[] args) {

        //创建FileWriter 对象
        FileWriter fileWriter = null;

        try {
            //打开文件一（会覆盖原文件数据） 没有自动创建
            // fileWriter = new FileWriter("D:\\news5.txt");
            //打开文件二 （不覆盖原有数据，在其后追加）
            fileWriter = new FileWriter("D:\\news5.txt", true);

            //写入一个字符
            fileWriter.write('a');
            //写入字符串   getBytes把字符串转换为字节数组
            fileWriter.write("bcde");
            //写入数组
            char[] chars = {1, 2};
            fileWriter.write(chars);
            //写入指定数组的指定部分
            fileWriter.write(chars, 0, 1);
            //写入字符串的指定部分
            fileWriter.write("abcd", 0, 2);

        } catch (Exception e) {
            System.out.println(e);
        } finally {
            try {
                //释放资源
                fileWriter.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
```





## 节点流与处理流

- 节点流可以从一个特定的数据源读写数据，如FileReader、FileWriter
- 处理流（也叫包装流）是连接已存在的流（节点流或处理流）之上，为程序提供更为强大的读写能力，如**BufferedReader**、**BufferedWriter**

![image-20230707143425481](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230707143425481.png)

> 节点流与处理流的区别与联系：
>
> 节点流是底层流（低级流），可以直接跟数据源连接，处理流包装节点流使用了修饰器设计模式，不直接与数据源连接
>
> 处理流包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入输出
>
>  
>
> 处理流的功能：
>
> 性能提高 --主要以增加缓冲的方式提高输入输出效率
>
> 操作便捷 --处理流提供一系列便捷方法来一次输入输出大批量数据

---





## 处理流字符输入输出

> **BufferedReader**

```java
    public static void main(String[] args) throws IOException {

        //创建BufferedReader   FileReader将文件转换为字符流
        BufferedReader bufferedReader=new BufferedReader(new FileReader("D:\\\\news5.txt"));

        //readLine 按行读取   当返回null，表示读取结束
        String read=null;
        while (( read=bufferedReader.readLine())!=null){
            System.out.println(read);
        }

        //关闭资源
        bufferedReader.close();
    }
```

> **BufferedWriter**

```java
   public static void main(String[] args) throws IOException {

        //创建BufferedWriter   FileWriter将文件转换为字符流  true表追加（默认覆盖）
        BufferedWriter bufferedWriter=new BufferedWriter(new FileWriter("D:\\\\news5.txt",true));

        //写入
        bufferedWriter.write("hello");
        //需要插入换行符表输出结束
        bufferedWriter.newLine();

        //关闭资源
        bufferedWriter.close();
    }
```





## 处理流字节输入输出

> **BufferedInputStream**

```java
   public static void main(String[] args) throws IOException {

        //创建BufferedInputStream 对象   FileInputStream转换为字节流
        BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("D:\\\\news5.txt"));

        //IO读取
        byte[] bytes = new byte[1024];
        int readLen = 0;
        while ((readLen = bufferedInputStream.read(bytes)) != -1) {
            //转换为String输出
            System.out.println(new String(bytes,0,readLen));

        }

        //关闭资源
        bufferedInputStream.close();
    }
```

> **BufferedOutPutStream**

```java
    public static void main(String[] args) throws IOException {

        //创建BufferedOutputStream对象
        BufferedOutputStream bufferedOutputStream=new BufferedOutputStream(new FileOutputStream("D:\\\\news5.txt",true));

        //写入
        bufferedOutputStream.write('a');

        //关闭资源
        bufferedOutputStream.close();
    }
```





## 对象处理流-序列反序列

对象处理流的意义：在保存一个数据的同时，保存这个数据的类型

通俗说就是保存一个dog类型的数据，在读取时，也是以dog形式读出。就是能将基本数据类型或对象进行序列化和反序列化操作

> **序列化和反序列化**
>
> 1. 序列化就是在保存数据时，保存数据的值和数据类型	
> 2. 反序列化就是在恢复数据时，恢复数据的值和数据类型
> 3. 需要让某个对象支持序列化机制，必须让其类是可序列化的，为了让某个类是可序列化的，该类必须实现两个接口之一：**Serializable** （标记接口，其内没有任何方法，常用）、Externalizable（继承于Serializable 有方法需要实现）

---

**ObjectOutputStream 提供序列化功能**

**ObjectInputStream 提供反序列化功能**

> ObjectInputStream（InputStream）
>
> ObjectInputStream（）

---

**ObjectOutputStream实例**：保存一个Dog对象到data.dat文件中

```java
public class DogObjectOutputStream {

    public static void main(String[] args) throws IOException {
        //创建 ObjectOutputStream 对象 序列化
        ObjectOutputStream objectOutputStream=new ObjectOutputStream(new FileOutputStream("D:\\data.dat",true));

        //序列化数据到目标文件 自动装箱
        objectOutputStream.writeInt(100);   //int--->Integetr  (实现了Serializable)
        objectOutputStream.writeChar('a');   //char--->Character (实现了Serializable)
        objectOutputStream.writeUTF("你好");    //String (实现了Serializable)
        objectOutputStream.writeBoolean(true);//boolean--->Boolean (实现Serializable)
        objectOutputStream.writeDouble(10.5);   //double--->Double (实现Serializable)

        //保存一个java对象
        objectOutputStream.writeObject(new Dog("haha",5));//Dog实现了Serializable

        //关闭资源
        objectOutputStream.close();
    }
}
//必须实现Serializable 否则报错
class Dog implements Serializable{
     String name;
     int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

**ObjectInputStream 实例**读取出Dog对象

```java
public class DogObjectInputStream {
    
  public static void main(String[] args) throws IOException, ClassNotFoundException {
      
        //创建ObjectInputStream 对象 反序列化
        ObjectInputStream objectInputStream=new ObjectInputStream(new FileInputStream("D:\\data.dat"));

        //读取：反序列化顺序必须与序列化的顺序一致（什么顺序保存的就什么顺序读出）
        System.out.println(objectInputStream.readInt());  
        System.out.println(objectInputStream.readChar());
        System.out.println(objectInputStream.readUTF());
        System.out.println(objectInputStream.readBoolean());
        System.out.println(objectInputStream.readDouble());

        //读Dog对象 注意必须要有Dog类才能调用Dog方法
        Object o = objectInputStream.readObject();
        System.out.println(o.toString());

        Dog dog= (Dog) o;
        System.out.println(dog.getName());
    }
}
```

> **注意事项：**
>
> 1. 读写顺序要一致
> 2. 要求实现序列化和反序列化对象，需要实现Serializable
> 3. 序列化的类中建议添加SerialVersionUID，为了提高版本的兼容性
> 4. 序列化对象时，默认将里面所有属性都进行序列化，除static和transient修饰的成员
> 5. 序列化对象时，要求里面属性的类型也需要实现序列化接口
> 6. 序列化具备可继承性，也就是如果某类实现了序列化，则其所有子类也默认实现了序列化



​	

## 转换流

**处理纯文本数据时，使用字符流效率更高，且可以有效解决中文乱码**

**可以在使用时指定编码格式（utf-8、gbk 等）**

---

**InputStreamReader**

> Reader的子类，可以将InputStream（字节流）转换（包装）成Reader（字符流）

```java
        //将 FileInputStream 转换成 InputStreamReader 并指定编码
        InputStreamReader inputStreamReader=new InputStreamReader(new FileInputStream("D:\\data.dat"),"utf-8");

        //将 InputStreamReader 传入BufferedReader
        BufferedReader bufferedReader=new BufferedReader(inputStreamReader);

        //读取
        String str=bufferedReader.readLine();

        //关闭资源（只需关闭外层）
        bufferedReader.close();
```

**OutputStreamWriter**

> Writer的子类，实现将OutputStream（字节流）转换（包装）成Writer（字符流）

```java
        //将 FileOutputStream 转换成 OutputStreamWriter 并指定编码
        OutputStreamWriter outputStreamWriter = new OutputStreamWriter(new FileOutputStream("D:\\data.dat"), "utf-8");

        //将 OutputStreamWriter 传入 BufferedWriter
        BufferedWriter bufferedWriter = new BufferedWriter(outputStreamWriter);

        //io写入
        bufferedWriter.write(100);

        //关闭资源（只需关闭外层）
        bufferedWriter.close();
```





## 读写配置文件

**配置文件**

```properties
# classfullpath 表类的全限定名；methood 表类方法
classfullpath=com.wang.Cat
methood=hi
```

**读配置文件**

```java
//Properties类可以读写配置文件
 Properties properties=new Properties();
//读
 properties.load(new FileInputStream("src\\re.properties"));
//获取
 String classfullpath=properties.get("classfullpath").toString();
 System.out.println(classfullpath);
```

**写配置文件**

```java
```











# 网络

## 网络协议

**五类互联网网络地址**

![image-20230706095823352](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230706095823352.png)

---



**TCP/IP分层**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230706100001059.png" alt="image-20230706100001059" style="zoom: 67%;" />

> 数据进入协议栈时的封装过程 当成为以太网帧就可以通过物理层传输，对方获取以太网帧后会反向解码
>
> TCP/IP分层：
>
> <img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230706100334171.png" alt="image-20230706100334171" style="zoom:50%;" />	





##  InetAddress

**常用方法**  都需要抛出异常

> 获取本机InetAddress对象  --- getLocalHost
>
> 获取指定主机名/域名获取Ip地址对象 --- getByName
>
> 获取InetAddress对象的主机名 ---getHostName
>
> 获取InetAddress对象的地址 ---getHostAddress

---

```java
//获取本机InetAddress对象
InetAddress inetAddress=InetAddress.getLocalHost();
System.out.println(inetAddress);  //DESKTOP-NAQRCQR/192.168.31.1
```

```java
//指定主机名获取InetAddress对象
InetAddress inetAddress=InetAddress.getByName("DESKTOP-NAQRCQR");
System.out.println(inetAddress);  //DESKTOP-NAQRCQR/192.168.31.1
```

```java
//指定域名获取InetAddress对象
InetAddress inetAddress=InetAddress.getByName("www.baidu.com");
System.out.println(inetAddress); //www.baidu.com/180.101.50.188
```

```java
// 通过InetAddress对象 获取InetAddress对象的主机名和地址
InetAddress inetAddress=InetAddress.getByName("www.baidu.com");

String hostName=inetAddress.getHostName();
System.out.println(hostName); //www.baidu.com

String address=inetAddress.getHostAddress();
System.out.println(address); //14.119.104.189
```





## Socket

Socket--英语解释：插孔

- 套接字（Socket）开发网络应用程序被广泛采纳，成为事实上的标准。
- 通信两端都要有Socket，是两台机器通信的端点
- 网络通信实际上就是Socket间的通信
- Socket允许程序把网络连接当成一个流，数据在两个Socket间通过IO传输
- 一般主动发起通信的应用程序属于客户端，等待通信请求为服务端

**示意图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230706154019064.png" alt="image-20230706154019064" style="zoom:50%;" />

---

### TCP字节流通信

1. 编写一个服务端，和客户端
2. 服务端在9999端口监听
3. 客户端连接服务端，发送数据，并接收服务端返回的数据，再退出
4. 服务端接收到客户端发出的数据，然后返回自己的数据，再退出

> **客户端**

```java
public class SocketTcpClient {
    public static void main(String[] args) throws IOException {
        //连接服务端（ip，端口）这里因为服务器是本地模拟，所以ip为本机的host.连接成功返回Socket
        Socket socket=new Socket("192.168.8.107",9999);

        //通过socket.getOutputStream 得到和socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //通过输出流，写入数据到数据通道
        outputStream.write("hello Server".getBytes());
        //设置输出结束标记
        socket.shutdownOutput();

        
        //通过socket.getInputStream 接受服务器返回的数据
        InputStream inputStream = socket.getInputStream();
        //IO读取
        byte buf[]=new byte[1024];
        int readLen=0;
        while ((readLen=inputStream.read(buf))!=-1){
            System.out.println(new String(buf,0,readLen));
        }


        //关闭资源（必须）
        outputStream.close();
        socket.close();
    }
}
```

> **服务器**

```java
public class ScoketTcpServer {
    public static void main(String[] args) throws IOException {
        //在本机9999端口监听，等待客户端连接
        ServerSocket serverSocket=new ServerSocket(9999);
        //当没有客户端连接9999端口时，程序会阻塞，等待连接
        System.out.println("服务端正在等待连接......");

        //当有客户端连接，则返回Socket对象，程序继续执行
        Socket socket=serverSocket.accept();

        //通过socket.getInputStream 读取客户端写入数据通道的数据
        InputStream inputStream = socket.getInputStream();
        //IO读取
        byte buf[]=new byte[1024];
        int readLen=0;
        while ((readLen=inputStream.read(buf))!=-1){
            System.out.println(new String(buf,0,readLen));
        }
        
        

        //通过socket.getOutputStream 得到和socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //通过输出流，写入数据到数据通道
        outputStream.write("hello Client".getBytes());
        //设置输出结束标记（非常重要，不设置结束标记，就无法判断输出释放结束，程序会等待）
        socket.shutdownOutput();


        //关闭服务
        inputStream.close();
        socket.close();
        serverSocket.close();
    }
}
```



### TCP字符流通信

**要求：**

1. 编写一个服务端，和客户端
2. 服务端在9999端口监听
3. 客户端连接服务端，发送数据，并接收服务端返回的数据，再退出
4. 服务端接收到客户端发出的数据，然后返回自己的数据，再退出

**思路:**	

1. 客户端使用socket.getOutputStream();   服务端使用socket.getInputStream();
2. 客户端将OutputStream-->Writer             服务端InputStream ->Reader
3. 客户端使用转换流                                       服务端使用转换流

​		OutputStreamWriter                                 InputStreamReader

​	4.设置写入结束标记(换行符，表写入结束)  writer.newLine   



> **客户端**   只需要修改输出流的核心代码

```java
//通过socket.getOutputStream 得到和socket对象关联的输出流对象
OutputStream outputStream = socket.getOutputStream();

//通过输出流，写入数据到数据通道  OutputStreamWriter将OutputStream的字符流转换为字节流
BufferedWriter bufferedWriter=new BufferedWriter(new OutputStreamWriter(outputStream));
bufferedWriter.write("hello,server");

//设置结束标记(插入一个换行符表写入结束) 对方必须使用readline读入
bufferedWriter.newLine();
//使用字符流需要手动刷新，否则数据不会写入到数据通道
bufferedWriter.flush();
```

> **服务端** 只需要修改输入流的核心代码

```java
//通过socket.getInputStream 读取客户端写入数据通道的数据
InputStream inputStream = socket.getInputStream();

//IO读取  通过InputStreamReader将inputStream转换为字符流
BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(inputStream));
//读出
String str=bufferedReader.readLine();
System.out.println(str);
```



### 网络上传文件到服务器

**结构图：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230712153340629.png" alt="image-20230712153340629" style="zoom: 50%;" />

>  **客户端代码**

```java
public class SocketTcpClient {
    public static void main(String[] args) throws IOException {
        //连接服务端（ip，端口）这里因为服务器是本地模拟，所以ip为本机的host.连接成功返回Socket
        Socket socket = new Socket("192.168.8.107", 9999);

        //读取本地文件
        FileInputStream fileInputStream = new FileInputStream("D:\\abc.jpg");
        byte[] bytes = streamToByteArray(fileInputStream);

        //发送到服务器
        //通过socket.getOutputStream 得到和socket对象关联的输出流对象
        OutputStream outputStream = socket.getOutputStream();
        //通过输出流，写入数据到数据通道
        outputStream.write(bytes);
        //结束
        socket.shutdownOutput();


        //获取服务器返回的数据
        InputStream inputStream = socket.getInputStream();
        String s = streamToString(inputStream);
        System.out.println(s);


        //关闭资源（必须）
        fileInputStream.close();
        outputStream.close();
        inputStream.close();
        socket.close();
    }


    /**
     * 功能：将输入流转换为byte[] ，即可以把文件的内容读到byte[]
     *
     * @param is
     * @return
     */
    public static byte[] streamToByteArray(InputStream is) throws IOException {
        //创建输出流对象
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();

        //IO读取
        byte[] b = new byte[1024];
        int len;
        while ((len = is.read(b)) != -1) {
            byteArrayOutputStream.write(b, 0, len);
        }

        //转换为数组
        byte[] array = byteArrayOutputStream.toByteArray();

        //关闭资源
        byteArrayOutputStream.close();
        return array;
    }


    /**
     * 功能：将输入流转换成String ，即把读到的文件内容以String形式返回
     *
     * @param is
     * @return
     */
    public static String streamToString(InputStream is) throws IOException {

        //IO读取  通过InputStreamReader将inputStream转换为字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(is));

        //读出
        String str = bufferedReader.readLine();
        return str;
    }
}
```

> **服务器代码**

```java
public class ScoketTcpServer {
    public static void main(String[] args) throws IOException {
        //在本机9999端口监听，等待客户端连接
        ServerSocket serverSocket = new ServerSocket(9999);
        //当没有客户端连接9999端口时，程序会阻塞，等待连接
        System.out.println("服务端正在等待连接......");
        //当有客户端连接，则返回Socket对象，程序继续执行
        Socket socket = serverSocket.accept();

        //读取客户端写入数据通道的数据
        InputStream inputStream = socket.getInputStream();
        //Io读出
        byte[] bytes = streamToByteArray(inputStream);

        //将数据写入到指定路径
        FileOutputStream fileOutputStream = new FileOutputStream("./src/abc.jpg");
        fileOutputStream.write(bytes);


        //向客户端回复信息
        OutputStream outputStreamString = socket.getOutputStream();
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(outputStreamString));
        bufferedWriter.write("收到图片");
        //将内容刷新到数据通道，并设置写入结束
        bufferedWriter.flush();
        socket.shutdownOutput();

        //关闭服务
        fileOutputStream.close();
        inputStream.close();
        bufferedWriter.close();
        outputStreamString.close();
        socket.close();
        serverSocket.close();
    }

    /**
     * 功能：将输入流转换为byte[] ，即可以把文件的内容读到byte[]
     *
     * @param is
     * @return
     */
    public static byte[] streamToByteArray(InputStream is) throws IOException {
        //创建输出流对象
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();

        //IO读取
        byte[] b = new byte[1024];
        int len;
        while ((len = is.read(b)) != -1) {
            byteArrayOutputStream.write(b, 0, len);
        }

        //转换为数组
        byte[] array = byteArrayOutputStream.toByteArray();

        //关闭资源
        byteArrayOutputStream.close();
        return array;
    }


    /**
     * 功能：将输入流转换成String ，即把读到的文件内容以String形式返回
     *
     * @param is
     * @return
     */
    public static String streamToString(InputStream is) throws IOException {

        //IO读取  通过InputStreamReader将inputStream转换为字符流
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(is));

        //读出
  
        String str = bufferedReader.readLine();
        return str;
    }
}

```



### URL下载网络资源

```java
ublic class UrlDown {
    public static void main(String[] args) throws Exception {
        //下载地址
        URL url = new URL("https://i0.hdslb.com/bfs/banner/8bb2303e3b3338d4a056e99581f811f268d57444.png");
        
        //openConnection连接到这个资源  HTTP  (强转为http)
        HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
        InputStream inputStream = urlConnection.getInputStream(); 
        FileOutputStream fos = new FileOutputStream("1.png");
        byte[] buffer = new byte[1024];
        int len;
        while ((len=inputStream.read(buffer))!=-1){
            fos.write(buffer,0,len);//写出数据
        }
        fos.close();
        inputStream.close();
        urlConnection.disconnect();//断开连接
    }
}
```



### TCP连接的秘密

当客户端连接到服务端后，实际上客户端也是通过一个端口和服务端进行通讯的，这个端口是随机的，由TCP/IP来分配。

**示意图：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230713090450561.png" alt="image-20230713090450561" style="zoom:80%;" />

**程序连接时查询端口信息netstat：**

![image-20230713091311895](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230713091311895.png)









# 反射

反射是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为 Java 语言的反射机制





## 为什么需要反射

> 实例：根据配置文件 re.properties 指定信息，创建Cat对象并调用方法hi

```properties
# classfullpath 表类的全限定名；methood 表类方法
classfullpath=com.wang.Cat
methood=hi
```

> 这样的需求在学习框架的时候特别多，即通过外部文件配置，在不修改源代码的情况下，来控制程序，符合ocp开闭原则
>
> 开-功能扩展  ；闭-源码修改功能关闭

---



## 反射机制

**以上功能使用反射机制实现**

```java
        //读取配置文件
        Properties properties = new Properties();
        properties.load(new FileInputStream("src\\re.properties"));
        String classfullpath = properties.get("classfullpath").toString();  //类全限定名
        String methoodName = properties.get("methood").toString();  //类方法名

        //使用反射机制
        //(1)加载类，返回Class类型的对象 cls
        Class cls = Class.forName(classfullpath);
        //(2)通过cls得到你加载的类  com.wang.Cat
        Object obj = cls.newInstance();
        //(3)通过cls得到你加载的类 com.wang.Cat 的method方法对象
        Method method = cls.getMethod(methoodName);
        //(4)通过method方法对象 实现调用方法
        method.invoke(obj);//传统方法 对象.方法()  ==>反射机制 方法.invoke(对象)
```



## 反射原理



反射(Reflection) 允许程序在执行期间借助于ReflectionAPI取得任何类的内部信息；

加载完类后，在堆中会产生一个Class类型的对象（一个类只有一个Class对象），这个对象包含类的完整结构信息，通过这个对象得到类的结构。这个对象就像一面镜子，透过这个镜子看到类的结构，所以形象称之为反射。

**原理图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230721115856411.png" alt="image-20230721115856411" style="zoom:80%;" />



## 反射相关类

```java
java.lang.Class   //代表一个类，Class对象表示某个类加载后在堆中的对象
java.lang.reflect.Method  //代表类的方法
java.lang.reflect.Field   //代表类的成员变量
java.lang.reflect.Constructor //代表类的构造方法
```

演示：

```java
        //(1)加载类，返回Class类型的对象 cls
        Class cls = Class.forName("com.wang.Cat");

        //(2)通过cls得到你加载的类  com.wang.Cat
        Object obj = cls.newInstance();
        //(3)通过cls得到你加载的类 com.wang.Cat 的method方法对象
        Method method = cls.getMethod("hi");
        //(4)通过method方法对象 实现调用方法
        method.invoke(obj);//传统方法 对象.方法()  ==>反射机制 方法.invoke(对象)
        //(5)通过cls得到你加载的类的Field成员变量对象 得到公有成员变量字段 注意，.getField不能得到私有属性
        Field ageField = cls.getField("age");
        System.out.println(ageField.get(obj).toString());  //==>反射 属性.get(对象)
        //(6)通过cls得到你加载的类的 Constructor 构造方法对象，Constructor表构造器
        //无参构造
        Constructor constructor = cls.getConstructor(); //()中可以指定构造器参数类型，返回无参构造
        System.out.println(constructor);
        //有参构造
        Constructor constructor1 = cls.getConstructor(String.class); //指定构造器参数类型 形参类型.class
        System.out.println(constructor1);
```



## 反射优缺点及优化

优点：可以动态创建和使用对象（也是框架的底层核心），使用灵活，没有反射机制，框架技术就失去了底层支撑

缺点：使用反射基本是解释执行，对执行速度有影响

---

**优化-关闭访问检查**

> Method和Field、Constructor对象都有setAccessible()方法
>
> setAccessible方法作用是启动和禁用访问安全检查的开关
>
> 参数值为true表示反射的对象在使用时取消访问检查，提高反射效率
>
> 参数值为f'alse表示反射的对象执行访问检查

```java
        //(1)加载类，返回Class类型的对象 cls
        Class cls = Class.forName("com.wang.Cat");
        //(2)通过cls得到你加载的类  com.wang.Cat
        Object obj = cls.newInstance();
        //(3)通过cls得到你加载的类 com.wang.Cat 的method方法对象
        Method method = cls.getMethod("hi");

        //(4)反射优化
        method.setAccessible(true);

        //(5)通过method方法对象 实现调用方法
        method.invoke(obj);//传统方法 对象.方法()  ==>反射机制 方法.invoke(对象)
```



## Class类

1. Class也是类，因此也继承Object类
2. Class类对象不是new出来的，而是系统创建的
3. 对于某个类的Class类对象，在内存中只有一份，因为类只加载一次（被synchronized修饰）
4. 每个类的实例都会记得自己是由哪个Class实例生成的
5. 通过Class可以完整的得到一个类的完整结构，通过一系列API
6. Class对象是存放在堆里的
7. 类的字节码二进制数据，是放在方法堆区的，有的地方称为元数据（包括方法代码、变量名、方法名、访问权限等）

---

**有Clss对象的类型**

1. 外部类，成员内部类，静态内部类，局部内部类，匿名内部类
2. 接口 interface
3. 数组 arrays
4. 枚举 enum
5. 注解 annotation
6. 基本数据类型
7. void

---

**Class类常用方法：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230724090051062.png" alt="image-20230724090051062" style="zoom: 67%;" />

 	

```java
        //获取到Car类对应的Class对象 <?>表示不确定的java类型
        Class<?> cls = Class.forName("com.wang.Cat");
        //输出cls  显示cls对象是哪个类的Class对象(不是具体类，不能强转)
        System.out.println(cls);  //com.wang.Cat
        //输出cls运行类型
        System.out.println(cls.getClass()); //java.lang.Class
        //得到包名
        System.out.println(cls.getPackage().getName()); //com.wang
        //得到全类名 （全限定名）
        System.out.println(cls.getName()); //com.wang.Cat
        //通过cls创建对象实例 输出信息
        Cat cat = (Cat) cls.newInstance();
        System.out.println(cat); //等价cat.toString() 结果 Cat{name='cat', age='10'}
        //通过反射获取某个属性（仅公有）
        Field age = cls.getField("age"); //括号内只能填公有属性名 “公有属性名” 私有报错
        System.out.println(age.get(cat)); //10
        //通过反射获取所有属性(仅公有)
        Field[] fields = cls.getFields();
        for (Field field : fields) {
            System.out.println(field.get(cat));
        }
        //通过反射给属性赋值
        age.set(cat, "20");
        System.out.println(age.get(cat)); //20
```





## 获取Class对象六种方式

> 方式一：
>
> 前提：若已知一个类的全类名，且该类在路径下，可通过Class类的静态方法forName()获取
>
> 场景：多用于配置文件，读取类全路径，加载类

```java
Class<?> cls = Class.forName("com.wang.Cat");
```

> 方式二：
>
> 前提：若已知具体的类，通过类的Class获取，该方式最为安全可靠，程序性能最高
>
> 场景：多用于参数传递，比如通过反射得到对应构造器对象

```java
Class cls = Cat.class;
```

> 方式三：
>
> 前提：若已知某个类的实例，调用该实例的getClass()方式获取Class对象
>
> 场景：通过创建好的对象，获取Class对象

```java
Class cls = cat.getClass();
```

> 方式四：
>
> 前提：
>
> 场景：通过类加载器来获取类的Class对象

```java
//先得到类加载器
ClassLoader classLoader = cat.getClass().getClassLoader();
//通过类加载器得到Class对象
Class cls = classLoader.loadClass("com.wang.Cat");
```

> 方式五：
>
> 前提：基本数据类型
>
> 场景：基本数据类型获取Class对象

```java
//Class cls=基本数据类型.Class;
Class cls = int.class;
```

> 方式六：
>
> 前提：包装类
>
> 场景：包装类获取Class对象

```java
//Class cls=包装类.TYPE;
Class cls = Integer.TYPE;
```



---





## 类加载流程

反射机制是java实现动态语言的关键，也就是通过反射实现类动态加载

静态加载：编译时加载相关的类，如果没有则报错，依赖性强

动态加载：运行时加载需要的类，如果运行时不用该类，则不报错，降低依赖性

---

**类加载流程图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230725090450121.png" alt="image-20230725090450121" style="zoom: 67%;" />

---

**类加载三个阶段完成的任务**

- **加载**：将类的class文件读入内存，并为之创建一个java.lang.class对象。此过程由类加载器完成。
- **连接**：将类的二进制数据合并到JRE中。

​				**验证**：对文件安全进行效验；

​                **准备**：对静态变量进行默认初始化，并分配内存空间；

​                **解析**：将符号引用转换成直接引用；

- **初始化**：JVM负责对类进行初始化，这里主要是指静态成员。





## 类加载阶段



**加载阶段**

> JVM在该阶段主要目的是将字节码从不同数据源（可能是class文件、也可能是jar包、甚至网络）转化为二进制字节流加载到内存中，并生成一个代表该类的java.lang.Class对象。



**连接阶段-验证**

> 1. 目的是为了确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身安全。
> 2. 包括：文件格式验证（是否以魔数oxcafebabe开头）、元数据验证、字节码验证和符号引用验证
> 3. 可以考虑使用 -Xverify：none参数来关闭大部分类验证措施，缩短虚拟机类加载时间



**连接阶段-准备**

> JVM会在该阶段对静态变量，分配内存并默认初始化（对应数据类型的默认初始值，如0、0L、null、false等）。这些变量所使用的n内存都将在方法区进行分配。
>
> ```java
>     //n1是实例属性，不是静态变量，因此在准备阶段，不会分配内存
>     //n2是静态变量，准备阶段分配内存，n2默认初始化0; 想获得20这值要在类加载最后阶段初始化中获得
>     //n3是static final 是常量，一旦赋值不可变，准备阶段n3值就是30
>     public int n1=10;
>     public static int n2=20;
>     public static final int n3=30;
> ```



**连接阶段-解析**

> 虚拟机将常量池内的符号引用替换为直接引用的过程
>
> 

**初始化**

> - 到初始化阶段，才真正开始执行类中定义的Java程序代码，此阶段是执行<clinit>()方法的过程。
> - <clinit>()方法是由编译器按语句在源文件中出现的**顺序**，依次自动收集类中所有静态变量的赋值动作和静态代码块中的语句	，并进行合并
> - 虚拟机会保证一个类的<clinit>()方法在多线程环境中被正确加锁、同步，如果多个线程同时区初始化一个类，那么只有一个线程会去执行这个类的<clinit>()方法，其他线程都需要阻塞等待，直到活动线程执行<clinit>()方法完毕
>
> ```java
> class B{
>     static {
>         System.out.println("B静态代码块");
>         num=10;
>     }
>     static int num=20;
> }
> //分析
> //1.加载阶段：加载B类，并生成B的class对象
> //2.连接阶段:num=0
> //3.初始化阶段：依次自动收集类中的所有静态变量的赋值动作和静态代码块中语句，并合并 注意是按顺序收集合并
>     /*
>     * clinit(){
>     *      System.out.println("B静态代码块");
>     *       num=10;
>     *       num=10;
>     *
>     * }
>     */
> ```





## 反射获取类结构信息

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230725111612715.png" alt="image-20230725111612715" style="zoom:67%;" />

> Cat类

```java
public class Cat implements i1 {
    public  String name="cat";
    String age="10";
    protected String height="100cm";
    private String weight="30kg";

    public void m1(){}
    void m2(){}
    protected void m3(){}
    private void m4(){}
}
```

> 测试类

```java
public class todo {
    public static void main(String[] args) throws Exception {

        //获取到Car类对应的Class对象 <?>表示不确定的java类型
        Class<?> cls = Class.forName("com.wang.Cat");
        //getName() 获取全类名
        System.out.println(cls.getName()); //com.wang.Cat
        //getSimpleName() 获取简单类名
        System.out.println(cls.getSimpleName()); //Cat
        //getFields() 获取所有public修饰的属性，包含本类及父类
        Field[] fields = cls.getFields();
        for (Field field : fields) {
            System.out.println(field.getName()); //name
        }
        //getDeclaredFields() 获取本类中所有属性
        Field[] declaredField = cls.getDeclaredFields();
        for (Field field : declaredField) {
            System.out.print(field.getName() + " ");//name age height weight
        }
        System.out.println();
        //getMethods() 获取所有public修饰的方法 ，包含本类及父类
        Method[] methods = cls.getMethods();
        for (Method method : methods) {
            System.out.print(method.getName() + " "); //m1 wait wait wait equals toString hashCode getClass notify notifyAll
        }
        System.out.println();
        //getDeclaredMethods() 获取本类所有方法
        Method[] declaredMethods = cls.getDeclaredMethods();
        for (Method declaredMethod : declaredMethods) {
            System.out.print(declaredMethod.getName() + " "); //m2 m1 m3 m4
        }
        System.out.println();
        //getConstructors() 获取所有public修饰的构造器，包含本类
        Constructor<?>[] constructors = cls.getConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.print(constructor.getName()); //com.wang.Cat
        }
        System.out.println();
        //getPackage() 返回包类型
        System.out.println(cls.getPackage()); //package com.wang
        //getSuperclass() 以class形式返回父类信息(父类的class对象)
        Class<?> superclass = cls.getSuperclass();
        System.out.println(superclass); //class java.lang.Object
        //getInterfaces() 以class形式返回接口信息
        Class<?>[] interfaces = cls.getInterfaces();
        for (Class<?> anInterface : interfaces) {
            System.out.print(anInterface + " ");//interface com.wang.i1
        }
        System.out.println();
        //getAnnotations() 返回注解信息
        Annotation[] annotations = cls.getAnnotations();
        for (Annotation annotation : annotations) {
            System.out.print(annotation + " ");
        }
```





## 反射暴破-创建实例

方式一：调用类中的public修饰的无参构造器

方式二：调用类中的指定构造器

---

**Class类相关方法**

newInstance： 调用类中无参构造器，获取对应类的对象

getConstructor(Class...class):根据参数列表，获取对应的构造器对象

getDecalaredConstructor(Class...class):根据参数列表，获取对应的所有构造器对象

---

**Constructor类相关方法**

setAccessible：暴破

newInstance(Object...obj):调用构造器

---

> 实例一：通过反射创建某类对象，分别通过公有无参、公有有参、私有有参构造

```java
/**
 * Cat类
 */
public class Cat {
    private String name = "cat";
    private String age = "10";

    public Cat() {
    }
    public Cat(String name) {
        this.name = name;
    }
    private Cat(String name, String age) {
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                ", age='" + age + '\'' +
                '}';
    }
}

/**
 * 测试类
 */
public class todo {
    public static void main(String[] args) throws Exception {
        //获取到Car类对应的Class对象 <?>表示不确定的java类型
        Class<?> cls = Class.forName("com.wang.Cat");

        //通过public无参构造器创建实例
        Object o = cls.newInstance();
        System.out.println(o); //Cat{name='cat', age='10'}

        //通过public有参构造器创建实例  getConstructor返回一个构造器
        Constructor<?> constructor = cls.getConstructor(String.class);
        //通过构造器创建实例
        Object dog = constructor.newInstance("Dog");
        System.out.println(dog);  //Cat{name='Dog', age='10'}

        //通过private有参构造器创建实例 私有构造器需要通过getDeclaredConstructor返回构造器
        Constructor<?> declaredConstructor = cls.getDeclaredConstructor(String.class, String.class);
        //暴破，若不添加则报错，私有不能直接创建实例。 【暴力破解】，使用反射可以访问私有构造器/属性/方法
        declaredConstructor.setAccessible(true);
        //创建实例
        Object pig = declaredConstructor.newInstance("Pig", "30");
        System.out.println(pig);//Cat{name='Pig', age='30'}
```







## 反射暴破-操作属性

- 根据属性名获取Field对象:   Field field=class对象.getDeclardeField(属性名);
- 暴破:  field.setAccessible(true);
- 访问:   field.set(obj,值);        System.out.println(field.get(obj));
- 注意：如果是静态属性，则set的参数obj可以写null 即 field.set(null,值); 

---

> 实例一：反射操作属性

```java
        //获取到Car类对应的Class对象 <?>表示不确定的java类型
        Class<?> cls = Class.forName("com.wang.Cat");
        //创建对象
        Object obj = cls.newInstance();
        //使用反射得到public name对象 getField可以拿到公有属性
        Field name = cls.getField("name");
        name.set(obj,"Dog");
        System.out.println(obj);//Cat{name='Dog', age='10'}

        //使用反射得到privaet age对象 getDeclaredField可以拿到任意权限属性
        Field age = cls.getDeclaredField("age");
        //暴破 私有属性不能直接操作，必须爆破
        age.setAccessible(true);
        age.set(obj,"30");
        System.out.println(obj);//Cat{name='Dog', age='30'}

        //获取属性值
        System.out.println(name.get(obj));//Dog
        System.out.println(age.get(obj));//30
```





## 反射暴破-操作方法

根据方法名和参数列表获取Method方法对象： Method method = class对象.getDeclaredMethod("方法名"，参数.class);

获取对象： Object obj = class对象.newInstance();

暴破： method.setAccessible(true);

访问：Object invoke = method.invoke(obj,实参列表);

注意：如果是静态方法，则invoke()的参数obj可以写为null

---

```java
        //获取到Car类对应的Class对象 <?>表示不确定的java类型
        Class<?> cls = Class.forName("com.wang.Cat");
        //获取对象
        Object obj = cls.newInstance();
        //根据方法名和参数列表获取Method方法对象 getMethod获取公有方法 m1公有
        Method methodM1 = cls.getMethod("m1",String.class);
        //访问
        Object invoke = methodM1.invoke(obj,"Dog");
        System.out.println(obj); //Cat{name='Dog', age='10'}

        //根据方法名和参数列表获取Method方法对象 getDeclaredMethod获取所有方法 m2私有
        Method  methodM2 = cls.getDeclaredMethod("m2", String.class);
        //私有方法需要暴破
        methodM2.setAccessible(true);
        //访问
        Object invoke1 = methodM2.invoke(obj, "30");
        System.out.println(obj); //Cat{name='Dog', age='30'}
```



# #####################################



# Lambda

Lambda的本质: 作为函数式接口的实例

Lambda表达式只适用于函数式接口

**AIt+回车**直接将匿名内部类转换为Lambda

**为什么要使用Lambda表达式**

- 避免匿名内部类定义过多
- 可以让代码看起来更简洁
- 去掉没有意义的代码，只留下核心逻辑



**Lambda表达式基本结构**

```java
f -> { }
/** 
*f 是参数变量  非固定 f类型是系统根据上下文自动识别
*-> 是语法符号
*{ } 是语句块
**/
```



## Lambda表达式演变（推导）

**首先定义一个函数式接口**

```java
interface ILike{
    void lambda();
}
```

**对比实现类、静态内部类、局部内部类、匿名内部的实现及调用**

```java
//2.实现类
class Like implements ILike{
    @Override
    public void lambda() {
        System.out.println("I like lambda01");
    }
}
public class TestLambda {
    //3.静态内部类
    static class Like2 implements ILike {
        @Override
        public void lambda() {
            System.out.println("I like lambda02");
        }
    }
    public static void main(String[] args) {
        //调用实现类
        ILike like = new Like();
        like.lambda();
        
        //调用静态内部类
        like = new Like2();
        like.lambda();
        
        //4.局部内部类
        class Like3 implements ILike{
            @Override
            public void lambda() {
                System.out.println("I like Lambda03");
            }
        }
         //调用局部内部类
        like = new Like3();
        like.lambda();
        
        //5.匿名内部类,没有类的名称，必须借助接口或者父类
        like = new ILike() {
            @Override
            public void lambda() {
                System.out.println("I like Lambda04");
            }
        };
         //调用匿名内部类
        like.lambda();
    }
}
```

**显然匿名内部类更简洁，那么在匿名内部类的基础上进行简化**

```java
public class TestLambda2 {
    public static void main(String[] args) {
        //匿名内部类
        Ilove Love = new Ilove() {
            @Override
            public void love(int a) {
                System.out.println("i love you " + a);
            }
        };
        
        Love.love(1);
        
        //lambda简化
        Ilove ilove =(int a)->{System.out.println("i love you " + a);};
        ilove.love(2);
        
        //去掉参数类型
        ilove = (a)->{
            System.out.println("i love you " + a);
        };
        
        //去掉小括号
        ilove = a ->{System.out.println("i love you " + a);};
        
        //去掉大括号
        ilove = a -> System.out.println("i love you " + a);
    }
    
interface Ilove{
    void love(int a);
}
}
```

  ==**总结：**==

-    只能有一行时简化称为一行，否则{}包裹
-    必须是函数式接口（只有一个方法）
-    多个参数，参数类型一起操作，要么都保留，要么都删除



---





## 有类型参数与无类型参数		

**无类型参数实例**

```java
List<Student> students = new ArrayList<Student>();
students.add(new Student(111, "bbbb", "london"));
students.add(new Student(131, "aaaa", "nyc"));
students.add(new Student(121, "cccc", "jaipur"));

// 实现升序排序
Collections.sort(students, (student1, student2) -> {
  // 第一个参数的学号 vs 第二个参数的学号
  return student1.getRollNo() - student2.getRollNo();
});

//逆序 反减就行了
Collections.sort(students, (student1, student2) -> {
  return student2.getRollNo() - student1.getRollNo();
});

students.forEach(s -> System.out.println(s));
```

**注意：**

箭头（->）前表示参数变量，有 **多个参数** 的时候，必须使用小括号包裹：`()`

```java
(student1, student2) -> {}
```

箭头（->）前表示参数变量，**没有参数** 的时候，必须使用小括号：`()`

```java
() -> {}
```

箭头（->）后的执行语句 **只有一条** 时，可以不加大括号 `{}` 包裹

```java
s -> System.out.println(s);
```



---

**有类型参数实例**

```java
fruits.forEach((Fruit f) -> {
  System.out.println(f.getName());
});
```

**注意：**

使用有类型参数时，即使只有一个参数，也必须使用小括号：`()`包裹

```java
(Fruit f) -> {}
```









## 引用外部变量

Lambda表达式`{}`内的执行语句,除了能引用参数变量外，还可以引用外部变量

```java
List<Fruit> fruits = Arrays.asList(......);
String message = "水果名称：";

fruits.forEach(f -> {
  System.out.println(message + f.getName());
});
```

**注意**

- 规范一：Lambda表达式引用的局部变量不允许被修改。即使修改代码写在表达式后面也不可以。甚至不可以在表达式内部修改
- 规范二：Lambda表达式的参数不能与局部变量同名。







## 双冒号（::）操作符

​        Java 8 支持了一种新的语法：双冒号 “`::`”，这也是一种 Lambda 写法 ，是与 Lambda 表达式相关的一个重要特性。



只有一条执行语句的 *Lambda* 表达式：

```java
List<String> names = Arrays.asList("zhangSan", "LiSi", "WangWu");

names.forEach(n -> {
  System.out.println(n);
});
```

可以进一步简化为：

```java
names.forEach(System.out::println);
```

`::` 语法干脆省略了参数变量，所以读这段代码需要相互对照、并且自行脑补

这段代码的重点是使用 `::` 时，系统每次遍历取得的元素（`n`），会 **自动** 作为参数传递给 `System.out.println()` 方法打印输出

​	`System.out::println`等同于` n -> {System.out.println(n);}`

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-1-5-1.svg)



---

**用法一：静态方法调用**

使用`System.out::println`代替` n -> {System.out.println(n);}`，简化代码

```java

```



---

**用法二：非静态方法调用**

`print()` 方法不再标识为 `static`,于是需要实例对象来调用

```java
//LambdaTest是类名
fruits.forEach(new LambdaTest()::print);
```

简写了

```java
LambdaTest lt = new LambdaTest();
fruits.forEach(lt::print);
```



---

**用法三：多参数**

升序案例：

```java
Collections.sort(students, (student1, student2) -> {
  // 第一个参数的学号 vs 第二个参数的学号
  return student1.getRollNo() - student2.getRollNo();
});
```

就碰到了多参数的情况。如果把比较的过程定义成一个方法：

```java
private static int compute(Student s1, Student s2) {
  ... ...
  ... ...
}
```

那么，排序过程就可以简写为：

```java
Collections.sort(students, SortTest::compute);
//SortTest是类名   compute是比较方法名
```

**注意**，系统会 自动获取上下文的参数，并按上下文定义的 **顺序** 传递给指定的方法。所谓 *顺序* 就是 *Lambda* 表达式 `()` 中的顺序。



---

**用法四：父类方法**

我们在《Java面向对象》学过，`super` 关键字的作用是在子类中引用父类的属性或者方法。那么同样，`::` 语法也可以用 `super` 关键字调用父类的**非静态方法**。

```java
import java.util.Arrays;
import java.util.List;

public class LambdaTest extends LambdaExample {
  public static void main(String[] args) {
    List<Fruit> fruits = Arrays.asList(
            new Fruit("香蕉"),
            new Fruit("苹果"),
            new Fruit("梨子"),
            new Fruit("西瓜"),
            new Fruit("荔枝")
    );

    LambdaTest at = new LambdaTest();
    at.print(fruits);
  }

  public void print(List<Fruit> fruits){
    fruits.forEach(super::print);
    }
}

class LambdaExample {
    public void print(Fruit f){
        System.out.println(f.getName());
    }
}
```









## Lambda操作多线程

原匿名内部类：

```java
new Thread(new Runnable(){
    @Override
    public void run() {
       System.out.println("run");
    }
}).start();
```

现Lambda表达式

```java
new Thread(()-> System.out.println("run")).start();
```







# 流 Stream



- Java 8 的新特性：`Stream`（中文称之为：流）也是很常见且常用的，主要优点是提升开发效率，使代码更干净、简洁
- `Stream` 的主要作用是对集合（`Collection`）中的数据进行各种操作，增强了集合对象的功能。
- `Stream` 是一个接口（`interface`），当然也有多个实现类。但 Java 是面向接口编程的，我们暂时不用关心具体有哪些实现类，先学会使用 `Stream` `API`。(在接口中提供了操作数据的方法，通常我们叫作 `API`)



这里大家需要先了解两件事：

- 与我们在《Spring Web全栈》第二章第四节中学习的用于操作文件的 `InputStream` 完全不同，是完全不同的概念。不要混淆
- `Stream` 经常与 `Lambda` 表达式 配合使用

---

**流的方法作用**

```java
//创建操作
.stream() //将数据转化为流
    
    //中间操作
    .distinct() //去重
    .filter()  //过滤
    .
    
    //终结操作
    
    

```





## 创建流与迭代流

**方式一：直接创建**

```java
import java.util.stream.Stream;

Stream<String> stream = Stream.of("苹果", "哈密瓜", "香蕉", "西瓜", "火龙果");
```

**方式二：由数组转化**

```java
String[] fruitArray = new String[] {"苹果", "哈密瓜", "香蕉", "西瓜", "火龙果"};
Stream<String> stream = Stream.of(fruitArray);
```

**方式三：由集合转化**

```java
List<String> fruits = new ArrayList<>();
fruits.add("苹果");
fruits.add("哈密瓜");
fruits.add("香蕉");
fruits.add("西瓜");
fruits.add("火龙果");
Stream<String> stream = fruits.stream();
```

**注意：** 无论是哪种方式创建，一定要清楚的知道：由于源数据（集合或数组）的数据是有序的，所以流中的元素也是有序排队的。



---

**迭代流**

我们知道集合类提供了 `forEach()` 方法可以遍历集合中的元素。很巧的是，`Stream` 提供的迭代方法也叫做 `forEach()`

```java
Stream<String> stream = Stream.of("苹果", "哈密瓜", "香蕉", "西瓜", "火龙果");
stream.forEach(System.out::println);
```

**注意**：为了能让系统自动识别 Lambda 表达式的参数类型，也必须使用泛型语法指定 `Stream` 中对象的类型。





## 流数据过滤（条件判断）filter

数据过滤即剔除不需要的数据，如输出学生成绩高于80的学生，那么低于80的就是不需要的数据



**传统代码写法：**

```java
List<Pupil> pupils = new ArrayList<>();
// 这里假设小学生数据对象已经存入了

// 有资格的小学生集合
List<Pupil> qualified = new ArrayList<>();
for (Pupil pupil : pupils) {
    // 统计是否满足条件
    if (pupil.getAverageScore() >= 80) {
        qualified.add(pupil);
    }
}

// 打印符合条件的小学生姓名
for (Pupil pupil : qualified) {
    System.out.println(pupil.getName());
}
```

**java8新特性-流写法：**

```java
List<Pupil> pupils = new ArrayList<>();
// 这里假设小学生数据对象已经存入了

pupils.stream()  //转化为流
    .filter(pupil -> pupil.getAverageScore() >= 80)
    .forEach(pupil -> {System.out.println(pupil.getName());});
```

**filter() 方法** : 从方法名我们可以理解其功能：对流中的数据对象进行过滤。

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-2-3-2.svg)

方法参数是一个 Lambda 表达式，箭头后面是条件语句，判断数据需要 **符合** 的条件。

也就是说，使用 Lambda 表达式告诉过滤器，需要那些 **符合** 条件的数据（把不符合条件的数据过滤掉）。

> 注意：这里的 Lambda 表达式略有不同。
>
> 箭头后的过滤条件语句（非可执行的语句）。传统代码中，条件语句写在 () 中的，所以新特性条件语句可以用 () 而不能用 {} 哦
>
> 等同于 pupil -> ((pupil.getAverageScore() >= 80) && (pupil.getViolationCount() < 1))







## 流的设计思想



数据流的操作过程，可以看做一个管道，管道由多个节点组成，每个节点完成一个操作。

数据流输入这个管道，按照 **顺序** 经过各个节点。上节课的案例中，最后完成输出到 console。

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-2-4-1.svg)

> 案例中，`.filter().forEach()` 组成了一个管道，每个方法都是管道的一个节点。方法调用的顺序构成了管道的节点顺序。



对比普通 Java 代码，`Stream` 的显著特点是：编程的重点，不再是对象的运用，而是数据的计算。

如果使用普通的 Java 代码，重点是使用对象完成各种各样的逻辑，加上语法代码也比较多，导致整个代码比较繁复。

使用了 `Stream API`，系统会自动完成很多操作，加上大幅度简化了语法，开发者的注意力重点就变为捋清楚数据计算的步骤，不用太关心变量类型、变量赋值、对象转换等。编程的重点更加清晰。

Stream 的这种变化，特征是：函数式风格。即弱化了面向对象的严格、完整的语法，重心变为通过函数完成数据计算。

> 记住 函数式 这个词

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-2-8-1.svg)

大家在练习过程中，务必对比代码，不仅要学会运用 `Stream API`，更要思考和理解 `Stream` 的特点。







## 流数据映射(修改数据) map

`map()` 方法通常称作**映射**，其作用就是用新的元素替换掉流中原来**相同位置**的元素。相当于每个对象都经历一次转换。

`map()` 方法可以改变流中的数据类型

`map()` 方法的参数是一个 *Lambda* 表达式，在语句块中对流中的每个数据对象进行计算、处理，最后用 `return` 语句返回的对象，就是转换后的对象。

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-2-5-1.svg)

**优点**

- 映射后的对象类型，可以与流中原始的对象类型不一致。
- 在流中，可以用字符串替换原来的整数。这就极大的提供了***灵活性***、***扩展性***，让流的后继操作可以更方便。



**代码实例一 -计算一组数字中每个数字的平方数**

```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 7, 63, 2, 3, 5);

numbers.stream()
    .map(num -> {
        return num * num;
    })
    .forEach(System.out::println);
```

**特例写法**

少数情况下，如果替换语句简单、系统能自动识别需要返回的值，代码可以简写为：

```java
.map(num -> num * num)  //不建议
```



**代码实例二 -多条件需要判断时**

```java
 .map(pupil -> {
              if (pupil.getAverageScore() > 85) {
                  pupil.setMessage(pupil.getName() + "同学您的成绩优秀，恭喜入围");
              } else {
                  pupil.setMessage(pupil.getName() + "同学您的成绩优良，恭喜入围");
              }
              return pupil;
          })
```





---







## 流数据排序 sorted



**Lambda表达式排序**

```java
// 实现升序排序
Collections.sort(students, (student1, student2) -> {
  // 第一个参数的学号 > 第二个参数的学号
  return student1.getRollNo() - student2.getRollNo();
});
```

**流操作排序**

```java
students.stream()
    // 实现升序排序
    .sorted((student1, student2) -> {
        return student1.getRollNo() - student2.getRollNo();
    })
    .forEach(System.out::println);
```

`sorted()` 顾名思义，就是完成排序的方法。把排序规则写成一个 Lambda 表达式传给此方法即可。

> 核心的排序规则 Lambda 表达式是一样的。

**参数顺序**    无论是 *Lambda 表达式* 写法，还是 *Stream API* 写法，参数 `(student1, student2)` 中的 *student1* 指代后一个元素，*student2* 指代前一个元素。不要被变量名迷惑了哦



**特例写法**   少数情况下，如果排序计算语句简单、系统能自动识别需要返回的值，代码可以简写为：

```java
.sorted((student1, student2) -> student1.getRollNo() - student2.getRollNo())
```









## 流数据摘取 limit



**流操作完成一组数字中取最大的前三个数**

```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 7, 63, 2, 3, 5);

numbers.stream()
    .sorted((n1, n2) -> n2 - n1)
    .limit(3)
    .forEach(System.out::println);
```

`limit()` 方法的作用是返回流的 **前** `n` 个元素，当然 `n` 不能为负数。 不是摘取任意位置哦，只能是流开头的.





## 流合并（计算）reduce



**流操作整数完成一组数据的求和**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = numbers.stream()
    .reduce((a, b) -> a + b)
    .get();
System.out.println("1-10求和 : " + sum);
```

- `reduce()` 方法的作用，是合并了所有的元素，***终止*** 计算出一个结果。注意这里终止的意思，就是流已经到达终点结束了，不能再继续流动了。
- `reduce()` 方法的返回值是一个比较复杂的对象，需要调用 `get()` 方法返回最终的整数值。同理，`get()` 方法返回值的类型，也是系统自动根据流中元素类型推定的。

`reduce()` 方法的参数就稍微有点**复杂**了（重点理解）：

- `a` 在第一次执行计算语句 `a + b` 时，指代流的第一个元素；然后充当缓存作用以存放本次计算结果。此后执行计算语句时，`a` 的值就是上一次的计算结果并继续充当缓存存放本次计算结果。
- `b` 参数第一次执行计算语句时指代流的第二个元素。此后依次指代流的每个元素。



**实例： 计算平均分**

```java
        List<Student> students = new ArrayList<>();
        students.add(new Student("赵祯", 92));
        students.add(new Student("曹丹姝", 60));
  
        int classScore = students.stream()
            .map(s -> {  
                return s.getMidtermScore();  //先用map改变流中数据类型
            })
            .reduce((s1, s2) -> s1 + s2)  
            .get();

        System.out.println("三年二班期中考试平均分：" + (int)(classScore/students.size()));
```



---

​	

**流操作对象完成平均分计算**

```java
  List<Student> students = new ArrayList<>();
        students.add(new Student("赵祯", 92, 92));
        students.add(new Student("曹丹姝", 60, 75));

        Student reduce = students.stream()
          .reduce(new Student(" ", 0, 0),//如果不new一个新对象，会出现bug，第一个对象会充当了缓存角色，正确性被破坏
                 (a, b) -> {
                        a.setMidtermScore(a.getMidtermScore() + b.getMidtermScore());
                        a.setLastScore(a.getLastScore() + b.getLastScore());
                        return a;});
	System.out.println("三年二班期中考试平均分：" + (reduce.getMidtermScore()/students.size()));           		System.out.println("三年二班期末考试平均分：" + (reduce.getLastScore()/students.size()));	

```

`reduce()` 方法的参数变为了两个：

- 第一个参数，是作为*缓存角色*的对象
- 第二个参数，是Lambda表达式，完成计算，格式是一样的。
  - 那么 `a` 变量不再指代流中的第一个元素了，专门指代*缓存角色*的对象，即方法第一个参数对象。
  - `b` 变量依次指代流的每个元素，包括第一个元素。
  - `a`、`b` 职责非常清晰了。

对照下图理解 `a`、`b` 参数的功能变化：

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-3-2-1.svg)

`reduce()` 方法的返回值同样发送了变化，**返回**作为*缓存角色*的对象，即第一个参数。

> **不用**再调用一次 `get()`





## 流收集 collect



`forEach()` 方法和 `reduce()` 方法都是流的终点哦。本节再来学习一种属于终点的流操作：收集。

在实际工作中，整体功能如果比较复杂的话，使用流对集合进行计算后，可能并不想输出和合并，而是把结果元素放在一个新的集合中，待进一步使用。例如，新的集合可以传递给 Thymeleaf 模板等等。

**实例：找到一组数字最大的三个数字放入新集合，用-组成字符串输出**

```java
List<Integer> numbers = Arrays.asList(3, 2, 2, 7, 63, 2, 3, 5);

List<String> numResult = numbers.stream()
    .sorted((n1, n2) -> n2 - n1)   
    .limit(3)
    .map(a -> "" + a)
    .collect(Collectors.toList());

String string = String.join("-", numResult);
System.out.println("字符串是: " + string);
```

- `collect()` 方法的作用就是收集元素。

- `Collectors.toList()` 是一个静态方法，作为参数告诉 `collect()` 方法存入一个 `List` 集合。

> ​		  所以 `collect()` 方法的返回值类型就是 `List`。
>
> ​		 `java.util.stream.Collectors` 是流工具包中提供的收集器。

- 为了能够把最终结果转换为字符串打印，调用了 `map()` 方法把流中原来的整数映射为字符串（`"" + a`），所以 `collect()` 方法的返回值类型就是 `List<String>`，而不是 `List<Integer>`。







## 并行流 parallelStream

串行：每个节点依次执行，下一个节点必须等上一个节点执行完毕。串行工作模式无法发挥多核cpu的优势

并行：利用多线程，变成同时执行



使用并行流的代码就是不再调用`stream()` 方法，改为调用 `parallelStream()` 方法即可。其它的计算方法是一样的。

`parallelStream()` 以并行的方式执行任务，同时也支持流的收集、合并等计算。结合下图理解与串行运算的不同：

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-3-4-1.svg)



**注意：有如下几点不适合并行计算：**

流中的每个数据元素之间，有逻辑依赖关系的时候，不适合使用并行计算。

因为并行计算使用了多线程，每个线程独立输出数字，而线程的输出时机，是由 *CPU* 动态决定的，无法确定。

所以，逻辑上要求数字必须按书写的前后顺序（数字之间有逻辑顺序）输出时，就不能使用并行计算。



---





# 设计模式



## 单例模式

***单例*** 设计模式：保证只有一个实例对象的方式

**保证一个类仅有一个实例 --方法：把构造函数设为私有。当把构造函数设为私有后，除了类自己，其他任何类都不能实例化其对象**

```java
public class ClassMaster {
  private String id;
  // 班主任名称
  private String name;

  // 唯一实例 ClassMaster自己实例化自己
  private static ClassMaster instance = new ClassMaster();

  private ClassMaster() {
  }
}
```

`ClassMaster` 类中定义一个 `ClassMaster` 类型的变量，赋值为 `new` 出来的自己的实例。

> 要注意：**必须**使用 `static` 修饰符，否则会造成死递归的严重的错误。

也就是说，不允许其他类实例化 `ClassMaster`（私有化构造方法）、只有自己能实例化一个唯一的自己（private static），所以可以保证 `ClassMaster` 的实例是全局唯一的。



**类`new` 出一个实例的目的，是要给其他类使用的。所以还需要增加一个方法，允许其他类访问这个单例的实例。**

```java
public class ClassMaster {
  private String id;
  // 班主任名称
  private String name;

  // 唯一实例 （私有的静态实例）
  private static ClassMaster instance = new ClassMaster();

    //（私有的构造方法）
  private ClassMaster() {
  }

  // 外部类可以通过这个方法访问唯一的实例   （公共静态访问方法）
  public static ClassMaster getInstance() {
    return instance;
  }
    
    //方法
    public void print(){   
         System.out.println("  ");
    }
}
```



---

**Spring中的单例模式**

任何**自动**注入实例对象，默认只有一个实例对象，是单例的。例如：可能多个 `Service` 和 `Control` 等都需要用到用户服务，那么这些类中都会定义：

```java
@Autowired
private UsersService usersService;
```

**Spring** 会保证只生成一个 `UsersServiceImpl` 实例，注入到多个 `Service` 或 `Control` 中，不会为每个 `Service` 或 `Control` 分别 `new` 出多个 `UsersServiceImpl` 实现类的实例。

虽然我们写 `Service` 服务的时候没有像写 `ClassMaster` 代码一样使用私有的构造方法，但 **Spring** 也应用了 ***单例*** 的 ***思想*** 来减少不必要的消耗。

---

**总结**

单例模式不仅仅一段代码，它更是一种思想。

我们可以编码来实现；Spring 作为框架在管理各个 *bean* 过程中，也用到、实现了这个思想。

虽然具体实现编码有不同，但大家都用这种思想解决了一类问题。









## 简单工厂模式（静态）

学习视频：https://www.bilibili.com/video/BV1mc411h719?p=3&vd_source=2f0cee9ab04c26aacbb64624794caaac

所谓工厂，就是生产物品的。程序中的工厂，就是生产实例对象的。

**实现简工厂的两个步骤：**

- 从具体的产品类抽象出接口。工厂应该生产一种产品，不应该生产某一个产品
- 把生产实例的过程，收拢到工厂类中实现



**实例：简单工厂生产对应的不同水果**

```java
public class FruitFactory {
    public static Fruit getFruit(Customer customer) {
        Fruit fruit = null;
        if ("sweet".equals(customer.getFlavor())) {
            fruit = new Watermelon();
        } else if ("acid".equals(customer.getFlavor())) {
            fruit = new Lemon();
        } else if ("smelly".equals(customer.getFlavor())) {
            fruit = new Durian();
        }
        return fruit;
    }
}
```

工厂仍然要实现功能，完成“根据不同条件创建不同对象”需求。

工厂的主要优点在于 ***职责明确*** 。餐馆、甜品店等需要水果的地方只需要告诉工厂顾客的口味，获得工厂生产的水果，但不需要知道具体是什么水果。餐馆和甜品店的责任是上菜，生产的责任交给工厂。

---

**命名**

一般来说，工厂类命名为 `XXXXFactory`，以 `Factory` 作为后缀可以提高辨识度，易于理解这个类的作用。

工厂类中的方法，依据实际情况而定，并没有特别的约定。方法名、输入参数、返回值，都是要根据实际需求确定的。

> 方法名是自由命名的。大家如果没有特别好的创意，建议选用 `get`、`create`、`make` 或 `build` 作为前缀

---

**重点**

理解简单工厂设计模式，重点还是要理解这种思想，以及适用的场景。

使用简单工厂完成功能开发时，重点就是要明确 ***什么条件*** 下创建 ***什么实例对象*** 的需求逻辑。







## 抽象工厂模式



简单工厂主要是把多个产品抽象，使用一个工厂创建；

抽象工厂的主要作用是把多个工厂进一步抽象；

---



<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-4-4-1.svg" alt="j5-4-4-1.svg" style="zoom:67%;" />

**工厂接口**

工厂接口（`SnacksFactory`）即规定工厂应该提供什么样的产品，所以包含了所有工厂的方法：

```java
public interface SnacksFactory {
    // 取得水果
    public Fruit getFruit(Customer customer);
    // 取得饮料
    public Drink getDrink(Customer customer);
}
```

但水果工厂不提供饮料，可实现工厂接口后又必须实现`getDrink()` 方法，这时候直接返回 `null` 即可。

```java
public class FruitFactory implements SnacksFactory {
    public Drink getDrink(Customer customer) {
        return null;
    }
}
```



---

**工厂的工厂**

`SnacksFactoryBuilder` 称之为 生产工厂的工厂 ，工厂用来生成产品实例，`SnacksFactoryBuilder` 用来生成工厂实例。

```java
public class SnacksFactoryBuilder {   
    public SnacksFactory buildFactory(String choice) {  //注意：非静态
        if (choice.equalsIgnoreCase("fruit")) {
            return new FruitFactory();
        } else if (choice.equalsIgnoreCase("drink")) {
            return new DrinkFactory();
        }
        return null;
    }
}
```

从简单工厂到抽象工厂，完成了对产品的抽象和对工厂的抽象。

**注意：**

`SnacksFactoryBuilder` 的 `buildFactory()` 方法并不是 `static` 的。

因为复杂场景下尽量不要使用类（static）方法，实例方法可以被继承，扩展性较好，应该优先使用实例方法。

> 《Java语言入门》课程中把 static 方法称之为静态方法，没有 static 的方法叫对象方法。实际上，**静态方法** = **类方法**，**对象方法** = **实例方法**，只是叫法不同罢了。

---

抽象工厂实例的UML图：

![image-20230508210337229](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230508210337229.png)







## 工厂模式结合Spring工程

工厂模式中不提倡定义`static`方法



在使用Spring框架的时候，可以为`SnacksFactoryBuilder`加上`@Component`注解，可以让框架管理实例

```java
//工厂生产者
@Component
public class SnacksFactoryBuilder {  
    public SnacksFactory buildFactory(String choice) {

    }
}
```

任何需要使用工厂的地方，只需要使用`@Autowired`注解让框架自动注入实例

```java
@Service
public class XxxxxServiceImpl implements XxxxxService {
    @Autowired
    private SnacksFactoryBuilder snacksFactoryBuilder;
}
```

这样可以让工厂模式的代码与Spring互为一体，扩展性更好、更易于维护。







## 观察者模式



观察者模式的核心是要知道观察什么，什么对象发生了什么变化需要通知。

```java
import java.util.Observable;
public class xxxx extends Observable {
    
}
```

Observable类是java提供的，继承了就是表示是核心的、需要被观察的类。  xxx是被观察者

---

**定义 JDK 实现的观察主体**

```java
public class WeatherData extends Observable {
    // 城市
    private String cityName;
    // 时间
    private String time;
    // 温度
    private String temp;

    // 城市固定了就不变了
    public WeatherData(String cityName) {
        this.cityName = cityName;
    }

    // 打印天气信息
    public String toString() {
        return cityName + "，" + LocalDate.now().toString() + " " + time + "，气温：" + temp + "摄氏度。";
    }
//get手动生成 
    
    
    /**
     * 修改   （一个城市的气温在某个时刻发生了变化）
     */
    public void changeTemp(String time, String temp) {
        if(time == null || temp == null) {
            // 输入数据为空是有问题的，不处理
            return;
        }

        // 与原数据不同，说明发生了变化
        if(!time.equals(this.time) || !temp.equals(this.temp)) {
            // 标记变化
            super.setChanged();
            this.time = time;
            this.temp = temp;
            // 发出通知，参数是额外的信息
            super.notifyObservers("温度变化已通知");
        }
    }
}
```

- 在 `changeTemp()` 中，如果天气数据与原来不同，则会标记变化并发出通知。
- 父类 `Observable` 提供的方法 `setChanged()` 就是标记被观察者对象发送了变化。
- 父类 `Observable` 提供的方法 `notifyObservers()` 就是发出通知；如果需要发送额外（不在被观察者对象里的）的信息，在参数中传入信息对象，可以是 **任意对象** ，需要自己根据具体的需求场景而定。如果不想发送额外信息，可以写为super.notifyObservers(null)



---

**观察者**     观察者需要实现 `Observer` 接口，也是 Java 提供的，实现此接口表示作为观察者。

```java
public class WeatherObserver implements Observer {
    private String name;

    @Override
    public void update(Observable o, Object arg) {
        System.out.print(this.name + "观察到天气变化为：");
        System.out.print(o.toString());
        System.out.println(" " + arg);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    
}
```

作为观察者，实现 `Observer` 接口后，要自己实现 `update()` 方法，方法签名是接口中定义好的，属于固定写法。

- 第一个参数就是被观察者对象，被观察者对象都需要继承自 Observable
- 第二个参数就是额外的信息，具体说就是调用 `super.notifyObservers()` 是传入的参数对象；传入什么对象，arg 的值就是什么对象

如果不想发送额外信息，写为 super.notifyObservers(null) ，那么这里 arg 值就是 null ，注意避免空指针异常哦。

`update()` 方法的作用就是接收通知。实际上，系统在 `super.notifyObservers()` 发出通知后，及调用所有观察者的 `update()` 方法，完成通知的过程。



---

**调用**

```java
public class WeatherTest {
    public static void main(String[] args) {
        // 在天气变化后发邮件的观察者
        WeatherObserver w1 = new WeatherObserver();
        w1.setName("天气邮件观察者");

        // 在天气变化后发短信的观察者
        WeatherObserver w2 = new WeatherObserver();
        w2.setName("天气短信观察者");

        // 城市天气数据
        WeatherData weatherData = new WeatherData("余杭");
        // 添加观察者
        weatherData.addObserver(w1);
        weatherData.addObserver(w2);

        // 气温变化
        weatherData.changeTemp("11:08", "32.8");
        // 气温变化
        weatherData.changeTemp("14:46", "29.3");
    }
}
```

观察者可以有多个。观察者对象与被观察者对象谁先 `new` 出来都可以，但是必须先调用 `addObserver()` 方法把观察者对象实例添加到被观察者（天气数据）实例中，然后再调用自定义的 `changeTemp()` 方法变更天气，才能触发自动通知。



---

UML图：

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/20230510145524.png" style="zoom: 80%;" />



---



# ###############JUC######################



# 进程与线程

![image-20230426191021252](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230426191021252.png)





# 线程创建

**线程创建三种方式：**

- Thread class         --->继承 Thread 类
- Runnable 接口     ---->实现 Runnable 接口
- Callable 接口        ---->实现 Callable 接口

---

**创建线程方式一：继承Thread类，重写run()方法，调用start开启线程**

- 子类继承Thread类具备多线程能力
- 启动线程：子类对象.start()
- 不建议使用：避免OOP单继承局限性

```java
//总结，线程开启不一定立即执行，由cpu调度执行
public class Demo1 extends Thread{
    @Override
    public void run() {
        //run 方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("我在看线程代码！");
        }
    }
    
    public static void main(String[] args) {
        //main线程，主线程
        //创建一个线程对象
        Demo1 testThread1 = new Demo1();
        //调用start（）方法主线程和创建的线程交替进行
        testThread1.start();
        //调用run（）方法会按顺序执行线程
        //testThread1.run();
        for (int i = 0; i < 2000; i++) {
            System.out.println("我在学习多线程！");
        }
    }
}
```

**创建线程方式二：实现Runnable接口，重写run方法**

- 实现接口Runnable具有多线程能力
- 启动线程：传入目标对象+Thread对象.start()
- 推荐使用：避免单继承局限性，灵活方便，方便同一个对象被多个线程使用

```java
//执行线程需要丢入runnable接口实现类，调用start方法
public class Demo3 implements Runnable{
    @Override
    public void run() {
    //run 方法线程体
        for (int i = 0; i < 200; i++) {
            System.out.println("我在看线程代码！");
        }
    }
    
    public static void main(String[] args) {
        //main线程，主线程
        //创建一个runnable接口的实现类对象
        Demo3 testThread3 = new Demo3();
        //创建线程对象，通过线程对象来开启我们的线程，代理
        new Thread(testThread3).start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("我在学习多线程！");
        }
    }
}
```

**创建线程方式三：实现Callable接口，重写call方法**

Runnable接口的run方法是没有返回值的，但有时候我们希望某个任务在执行完毕后返回一个结果，那么可以实现Callable接口。

Callable优势：

- 可以定义返回值
- 可以抛出异常

Thread类不接受Callable对象，需要使用FutureTask类来执行Callable任务

实质：`new Thread(new FutureTask(callable)).start();`

```java
public class Demo4 {
    public static void main(String[] args) {
        
        Callable1 callable1=new Callable1();
        //创建FutureTask实例执行Callable
        FutureTask futureTask=new FutureTask(callable1);
        //启动Callable
        futureTask.run();
        

        try {
            //获取线程执行结果
            String str= (String) futureTask.get();
            System.out.println(str);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        } catch (ExecutionException e) {
            throw new RuntimeException(e);
        }
    }
}

class Callable1 implements Callable{
    @Override
    public Object call() throws Exception {

        return "hehe";
    }
}
```

> 注意：run方法只是一个普通方法不会启动线程，start() 方法调用的run才是线程 。
>
> start方法源码：

```java
cat.start();

//(1) 其调用的是 start0 方法
public synchronized void start(){
  start0();  
}

//(2) start0是本地方法，最底层了，无法再追进  是JVM调度的，底层由C/C++实
private native void start0();

//可以理解为真正实现多线程效果的是start0 调用的run方法
```





# 线程状态

![image-20230512120727996](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230512120727996.png)

官方文档：

**六大状态**：创建、可运行（可运行分就绪和运行）、阻塞、等待、超时等待、死亡

![image-20230613162606539](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230613162606539.png)



```java
NEW      //创建
RUNNABLE //运行
BLOCKED  //阻塞
WAITING  //等待(一直等)
TIMED_WAITING //超时等待（等一段时间）
TERMINATED  // 终止
```



# 线程设置（基础）

## 线程停止

- 不推荐使用JDK提供的stop()、destroy()方法。【已废弃】
- 推荐线程自己停止下来
- 建议使用一个标志位进行终止变量,当flag=false，则终止线程运行。

```java
public class Demo10 implements Runnable{
    //1.设置一个标志位
    private  boolean flag = true;
    @Override
    public void run() {
        int i = 0;
        while (flag){
            System.out.println("run...Thread"+i++);
        }
    }
    //2.设置一个公开的方法停止进程，转换标志位
    public void stop(){
        this.flag=false;
    }
    //主方法调用
    public static void main(String[] args) {
        Demo10 testStop = new Demo10();
        new Thread(testStop).start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if (i==900){
                //调用stop方法切换标志位，让线程停止
                testStop.stop();
                System.out.println("线程该停止了");
            }
        }
    }
}
```





## 线程休眠 sleep

- sleep(时间)指定当前线程阻塞的毫秒数
- sleep存在异常InterruptedException
- sleep时间达到后线程进入就绪状态
- sleep可以模拟网络延时，倒计时等
- 每一个对象都有一个锁，sleep不会释放锁
- **调用Interrupt方法可以中断休眠，提前执行**

```java
//模拟倒计时
Date startTime = new Date(System.currentTimeMillis());//获取系统时间
        try {
           Thread.sleep(1000);
           System.out.println(new SimpleDateFormat("HH:mm:ss").format(startTime));
           startTime = new Date(System.currentTimeMillis());//更新当前时间
        } catch (InterruptedException e) {
           e.printStackTrace();
        }
```





## 线程礼让 yield

- 礼让线程，让当前正在执行的线程暂停，但不阻塞
- 将线程从运行状态转为就绪状态
- 让cpu重新调度，礼让不一定成功!看CPU心情

```java
public class Demo12 {
    public static void main(String[] args) {
        MyYield myYield = new MyYield();
        new Thread(myYield,"小明").start();
        new Thread(myYield,"小亮").start();
    }
}
class MyYield implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"线程开始");
        Thread.yield();  //礼让
        System.out.println(Thread.currentThread().getName()+"线程结束");
    }
}
//Thread.currentThread().getName() 获 取当前正在执行的线程的名字
```





## 线程强制执行 join

join就是阻塞当前线程，等join的线程执行完后，进入就绪状态

```java
//测试join方法（插队)
public class Demo13 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("线程vip来了"+i);
        }
    }
    
    
    public static void main(String[] args) throws InterruptedException{
        Demo13 testJoin = new Demo13();
        Thread thread = new Thread(testJoin);
        thread.start();
        for (int i = 0; i < 500; i++) {
            if (i==200){
                thread.join();//插队
            }
            System.out.println("main"+i);
        }
    }
}
```





## 线程唤醒与等待

在 Java 当中，实现线程之间进行通讯和配合执行的功能有三个方法：

- wait() / wait(long timeout)：让线程进入等待状态。
- notify()：唤醒当前对象上一个休眠的线程。
- notifyAll()：唤醒当前对象上的所有线程。

---

- wait()：释放锁，线程进入休眠状态等待唤醒
  例： `object.wait();` 释放object对象的锁并且本线程进入休眠状态，等待其他获得object对象的锁的线程执行notify()/notifyAll()方法进行唤醒。
- wait(long timeout)：指定等待的毫秒数
  如果一个线程调用共享对象的该方法挂起后，没有在指定的timeout ms 内被其他线程调用该共享变量的notify()或者 notifyAll() 方法唤醒，那么该函数还是会因为超时而返回。如果将 timeout置为0则和wait方法效果一样，因为在 wait()方法内部就是调用了 wait(0)。

---

```java
public class Demo4 {
    public static void main(String[] args) {
        Object o = new Object();

        //等待线程
        Runnable runnableWait = new Runnable() {
            @Override
            public void run() {
                while (true) {
                    synchronized (o) {
                        try {
                            System.out.println(Thread.currentThread().getName() + "进入等待....");
                            o.wait();
                            System.out.println(Thread.currentThread().getName() + "已获取唤醒通知");
                            System.out.println(Thread.currentThread().getName() + "已执行一次");
                        } catch (InterruptedException e) {
                            throw new RuntimeException(e);
                        }
                    }}}
        };

        //唤醒线程
        Runnable runnableNotify = new Runnable() {
            @Override
            public void run() {
                synchronized (o) {
                    System.out.println(Thread.currentThread().getName() + "执行唤醒");
                    o.notify();
                    System.out.println(Thread.currentThread().getName() + "已执行唤醒");
                }
            }
        };
        //启动线程
        new Thread(runnableWait).start();
        new Thread(runnableNotify).start();
    }
}

```



## 优先级

- Java提供一个线程调度器来监控程序中启动后进入就绪状态的所有线程，线程调度器按照优先级决定应该调度哪个线程来执行。
- 线程的优先级用数字表示，范围从1~10.
- Thread.MIN_PRIORITY = 1;
- Thread.MAX_PRIORITY = 10;
- Thread.NORM_PRIORITY = 5;
- 使用以下方式改变或获取优先级
- getPriority()/.setPriority(int xxx)

```java
public class demo15 {
    public static void main(String[] args) {
        MyPriority myPriority = new MyPriority();
        Thread t1 = new Thread(myPriority);
        Thread t2 = new Thread(myPriority);
        Thread t3 = new Thread(myPriority);
       
        //设置优先级
        t1.setPriority(2);
        t2.setPriority(NORM_PRIORITY);
        t3.setPriority(4);

        t1.start();
        t2.start();
        t3.start();
    }
}

class MyPriority implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
    }
}
```





## 守护线程

守护线程是为所有非守护线程提供服务的线程，

如果想主线程结束后，子线程也结束，只需要将子线程设置为守护线程 setDaemon(true);

常见的守护线程：垃圾回收机制

---



- 线程分为用户线程和守护线程
- 虚拟机必须确保用户线程执行完毕
- 虚拟机不用等待守护线程执行完毕
- 如,后台记录操作日志,监控内存,垃圾回收等待

```java
public class Demo16 {
    public static void main(String[] args) {
        God god = new God();
        You2 you2 = new You2();
        Thread thread =new Thread(god);
        thread.setDaemon(true);//默认是false表示是用户线程，正常的线程都是用户线程
        thread.start();//上帝守护线程启动
        new Thread(you2).start();
    }
}

class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("上帝保佑着你！");
        }
    }
}

class You2 implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 36500; i++) {
            System.out.println("你开心的活着！");
        }
        System.out.println("Goodbye World!");
    }
}
```



# 线程同步机制

**线程同步**

- 并发:同一个对象被多个线程同时操作

  处理多线程问题时，多个线程访问同一个对象，并且某些线程还想修改这个对象。这时候我们就需要线程同步。线程同步其实就是一种等待机制，多个需要同时访问此对象的线程进入这个对象的等待池形成队列，等待前面线程使用完毕，下一个线程再使用

由于同一进程的多个线程共享同一块存储空间，在带来方便的同时，也带来了访问冲突问题，为了保证数据在方法中被访问时的正确   性,在访问时加入**锁机制synchronized** ，当一个线程获得对象的排它锁，独占资源，其他线程必须等待，使用后释放锁即可.存以下问题:

- 一个线程持有锁会导致其他所有需要此锁的线程挂起；
- 在多线程竞争下，加锁。释放锁会导致比较多的上下文切换和调度延时，引起性能问题；
- 如果一个优先级高的线程等待一个优先级低的线程释放锁会导致优先级倒置，引起性能问题。

---



## 线程安全问题

多个线程操作同一个资源的时候，发生了冲突的现象，就叫做线程不安全

**如何保证线程安全：**

- **Synchronize**关键字：保证只有一个线程拿到锁，进入同步代码块操作共享资源，临界区内的代码对外是不可分割的，不会被线程切换打断，保证了原子性 （**本质就是排队，先进先出**）
- **volatile**关键字：被volatile关键字修饰的变量，一旦被线程修改，其他线程锁保持的该变量的缓存就会失效，需要从内存中获取最新值，也叫做MESI缓存一致性
- **atomic**原子类：一种乐观锁，用atomic原子类代替基本数据类型，无论原子更新哪种类型，都要遵循比较和替换原则，即要比较的更新值是否等于期望值，是则更新，不是则失败，保证了原子性

![image-20230513105337436](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230513105337436.png)

**线程不安全案例**

```java
//不安全的买票
//线程不安全，有小于等于0的数出现，
public class Demo17 {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();
        new Thread(buyTicket,"眉笔的我").start();
        new Thread(buyTicket,"欧皇的你").start();
        new Thread(buyTicket,"可恶的黄牛党").start();
    }
}

class BuyTicket implements Runnable{
    private int ticketNums=10;//票数
    boolean flag = true;//外部停止方式
    @Override
    public void run() {
        while (flag){
            try {
                buy();//买票
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    
    private void buy() throws InterruptedException {
        if (ticketNums<=0){//判断是否有票
            flag=false;
            return;
        }
        Thread.sleep(100);//模拟延迟
        System.out.println(Thread.currentThread().getName()+"买到了第"+ticketNums--+"张票");
    }
   
}
```

以上代码会使得取到的票号有小于等于0的数出现。

解及该问题有三种办法：

- 同步块
- 同步方法
- 同步锁



---





## 同步方法**与**同步块 

**同步方法**

- 由于我们可以通过private关键字来保证数据对象只能被方法访问,所以我们只需要针对方法提出一套机制，这套机制就是synchronized关键字，它包括两种用法∶synchronized方法和synchronized块.
- synchronized方法控制对“对象”的访问﹐每个对象对应一把锁,每个synchronized方法都必须获得调用该方法的对象的锁才能执行，否则线程会阻塞，方法一旦执行﹐就独占该锁，直到该方法返回才释放锁﹐后面被阻塞的线程才能获得这个锁,继续执行
- 缺陷:若将一个大的方法申明为synchronized将会影响效率

---

- 同步方法

```java
//不安全的买票案例修改
public class Demo17 {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();
        new Thread(buyTicket, "眉笔的我").start();
        new Thread(buyTicket, "欧皇的你").start();
        new Thread(buyTicket, "可恶的黄牛党").start();
    }
}


class BuyTicket implements Runnable {
    private int ticketNums = 10;//票数
    boolean flag = true;//外部停止方式
    @Override
    public void run() {
        while (flag) {
            try {
                Thread.sleep(100);//模拟延迟
                buy();//买票
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    //synchronized同步方法，锁的是this
    private synchronized void buy() {
        if (ticketNums <= 0) {//判断是否有票
            flag = false;
            return;
        }
        System.out.println(Thread.currentThread().getName() + "买到了第" + ticketNums-- + "张票");
    }
}
```

`synchronized` 解决了车票余量错乱、以及余量可能相同的问题。使用 `synchronized` 的方法意味着满足了两个线程安全的特性：

1. **原子性**：方法全部执行并且执行的过程不会被任何因素打断。
2. **可见性**：当多个线程访问同一个变量时，一个线程修改了这个变量的值，其他线程能够立即看得到修改的值。

但是 `synchronized` 为了实现这两个特性，也是要付出代价是的：性能可能不高。因为方法加锁，同时只有一个线程竞争成功能继续执行，其它很多线程是持续等待、响应慢的。所以 `synchronized` 不能滥用，比较适合的场景是：

1. 写操作的场景。例如用户修改个人信息、点赞、收藏、下单等。
2. 尽量精确锁住最小的代码块，把最关键的写操作抽象成独立的方法加锁。不建议给大段的方法加锁。

---

**同步块**

- 同步块:synchronized (Obj ){ }
- Obj称之为同步监视器
  - obj可以是任何对象,但是推荐使用共享资源作为同步监视器
  - 同步方法中无需指定同步监视器﹐因为同步方法的同步监视器就是this ,就是这个对象本身，或者是class[反射中讲解]
- 同步监视器的执行过程
  1．第一个线程访问，锁定同步监视器﹐执行其中代码．
  2．第二个线程访问，发现同步监视器被锁定﹐无法访问．
  3．第一个线程访问完毕,解锁同步监视器.

```java
//不安全的买票案例修改
public class Demo17 {
    public static void main(String[] args) {
        BuyTicket buyTicket = new BuyTicket();
        new Thread(buyTicket, "眉笔的我").start();
        new Thread(buyTicket, "欧皇的你").start();
        new Thread(buyTicket, "可恶的黄牛党").start();
    }
}

class BuyTicket implements Runnable {
    private int ticketNums = 10;//票数
    Object obj = new Object(); //同步监视器

    @Override
    public void run() {
        while (true) {
            synchronized (obj) {
                if (ticketNums <= 0) {//判断是否有票
                    break;
                }
                System.out.println(Thread.currentThread().getName() + "买到了第" + ticketNums-- + "张票");
            }

            try {
                Thread.sleep(100);//模拟延迟
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

> 如果是 static 静态方法，则不能直接使用this ，要锁类本身，即xxx.Class

```java
 //synchronized同步静态方法
private static void buy() {
synchronized (BuyTicket.Class) { //锁类本身
    if (ticketNums <= 0) {//判断是否有票
        break;
        }
    }
```





## 同步锁 Lock

**synchronized 与Lock的对比**

- Lock是显式锁（手动开启和关闭锁，别忘记关闭锁) synchronized是隐式锁，出了作用域自动释放
- Lock只有代码块锁,synchronized有代码块锁和方法锁
- 使用Lock锁，JVM将花费较少的时间来调度线程，性能更好。并且具有更好的扩展性（提供更多的子类)
- 优先使用顺序:Lock >同步代码块（已经进入了方法体，分配了相应资源)>同步方法（在方法体之外)

---

```java
public class Demo21 {
    public static void main(String[] args) {
        TestLock testLock = new TestLock();
        new Thread(testLock,"线程1").start();
        new Thread(testLock,"线程2").start();
        new Thread(testLock,"线程3").start();
    }
}
class TestLock implements Runnable{
    int ticketNum=10;
    
    //定义lock锁
    private final ReentrantLock lock =new ReentrantLock();
    @Override
    public void run() {
        while (true){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            lock.lock();//加锁
            if (ticketNum>0){
                System.out.println(Thread.currentThread().getName()+"获得了第"+ticketNum--+"张票");
            }else {
                lock.unlock();//解锁
                break;
            }
            lock.unlock();//解锁
        }
    }
}
```







## 乐观锁

`java.util.concurrent` 是 Java 系统提供的并发编程包，尝试使用 `java.util.concurrent.atomic.AtomicInteger` 让车票余量能够安全的递减。

```java
public class Ticket {
    private AtomicInteger count = new AtomicInteger(30);

    public void sell() {
        int newCount = 0;
        if (count.get() > 0) {
            newCount = count.decrementAndGet();
        }
        System.out.println(Thread.currentThread().getName() + "：还剩下 " + newCount + " 张票");
    }

    public int getCount() {
        return count.get();
    }
}
```

**解决的问题：**

- sell（）不再加锁，解决了车票余量重复的问题

> `AtomicInteger` 虽然是一个类，但等同于一个整数（就像 Integer 是 int 的对象）。
>
> 调用 `new AtomicInteger()` 构造函数实例化   对象的时候，可以指定任意的整数值。
>
> 不同的是，`AtomicInteger` 提供了不使用 `synchronized` 就能保证数据操作原子性的方法。例如 `decrementAndGet()`方法是     
>
> 三个操作的组合（取得当前值-->减一 --->return新值），多线程情况下也不会出现数值重复的错误，证明这三个操作是密不可分
>
> 的、线程间没有互相干扰打断，保证了数据的正确性。这就是类名 *Atomic* － **原子性**的含义。
>
> 线程间都是基于**最新的**结果进行减一的运算，所以不会重复，这样是 **可见性** 的体现。
>
> `count.decrementAndGet()` 代替了使用 `synchronized` 时，整数 `count--`

**没有解决的问题：**

- 仍然会出现负数车票
- Console打印的顺序也可能错误。

> 这是因为条件判断语句、操作语句、打印信息语句组合起来，就不具备原子性了，因为 `sell()`    不加锁，多条语句执行时就可能被其它线程打断了。所以必须给 `sell()` 整体加 `synchronized` 才能保证多条语句整体的原子性：
>
> public synchronized void sell() {}

---

**注意：**

```java
private static AtomicInteger count = new AtomicInteger(10);

//（取得当前值-->减一 --->return新值）   代替了使用 `synchronized` 时，整数 `count--`
count.decrementAndGet();

//（取得当前值-->加一 --->return新值）   代替了使用 `synchronized` 时，整数 `count++`
count.incrementAndGet();
```



---





## 死锁

多个线程各自占有一些共享资源﹐并且互相等待其他线程占有的资源才能运行﹐而导致两个或者多个线程都在等待对方释放资源﹐都停止执行的情形﹒某一个同步块同时拥有“**两个以上对象的锁**”时﹐就可能会发生“死锁”的问题．

产生死锁的四个必要条件:

- 互斥条件:一个资源每次只能被一个进程使用。
- 请求与保持条件:一个进程因请求资源而阻塞时，对已获得的资源保持不放
- 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
- 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

---

**死锁案例**

```java
public class Demo20 {
    public static void main(String[] args) {
        Makeup girl1 =new Makeup(0,"灰姑娘");
        Makeup girl2 =new Makeup(1,"白雪公主");
        girl1.start();
        girl2.start();
    }
}

class Lipstick{
}
class Mirror{
}

class  Makeup extends Thread{
    //需要的资源只有一份，用static来保证只有一份
    static Lipstick lipstick =new Lipstick();
    static Mirror mirror = new Mirror();
    int choice;//选择
    String girlName;//使用化妆品的女人
    
    Makeup(int choice,String girlName){
        this.choice=choice;
        this.girlName=girlName;
    }
    @Override
    public void run() {
        //化妆
        try {
            makeup();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    private void makeup() throws InterruptedException {//有死锁的makeup方法
        if (choice==0){
            synchronized (lipstick){
                System.out.println(this.girlName+"获得口红的锁");
                Thread.sleep(1000);
                synchronized (mirror){
                    System.out.println(this.girlName+"获得镜子的锁");
                }
            }
        }else {
            synchronized (mirror){
                System.out.println(this.girlName+"获得镜子的锁");
                Thread.sleep(2000);
                synchronized (lipstick){
                    System.out.println(this.girlName+"获得口红的锁");
                }
            }
        }
    }
    
    /*private void makeup() throws InterruptedException {//无死锁的makeup方法
        if (choice == 0) {
            synchronized (lipstick) {
                System.out.println(this.girlName + "获得口红的锁");
                Thread.sleep(1000);
            }
            synchronized (mirror) {
                System.out.println(this.girlName + "获得镜子的锁");
            }
        } else {
            synchronized (mirror) {
                System.out.println(this.girlName + "获得镜子的锁");
                Thread.sleep(2000);
            }
            synchronized (lipstick) {
                System.out.println(this.girlName + "获得口红的锁");
            }
        }
    }*/
}
```



---



# 线程通信



## 企业中的Lock与syn的使用

企业开发中，资源类是干净的，不会继承或实现 Thread 、Runnable  这样是为了降低耦合

> syn：

```java
public class test01 {

    public static void main(String[] args) {
        //创建资源
        Ticket ticket=new Ticket();

        //多线程执行 (正常操作：)
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 20; i++) ticket.sale();
            }
        },"A").start();

        //多线程执行 (lambda：)
        new Thread(() -> {
            for (int i = 0; i < 20; i++) ticket.sale();
        },"B").start();


    }
}

//资源类，只有属性和方法 （卖票） OOP
class Ticket{

    private int number=10;

    //卖票 synchronized
    public synchronized void sale(){
        if(number>0)
            System.out.println(Thread.currentThread().getName() + "卖出了第" + (number--) + "张票，" + "剩余" + number);
    }
}
```

> Lock

```java
public class test01 {

    public static void main(String[] args) {
        //创建资源
        Ticket ticket=new Ticket();
        //多线程执行 (正常操作：)
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 20; i++) ticket.sale();
            }
        },"A").start();
        //多线程执行 (lambda：)
        new Thread(() -> {
            for (int i = 0; i < 20; i++) ticket.sale();
        },"B").start();

    }


}

//资源类，只有属性和方法 （卖票） OOP
class Ticket{

    private int number=10;
    Lock lock=new ReentrantLock();

    //卖票 Lock 必须try。。catch。。finally
    public  void sale(){
        lock.lock(); //加锁
    try {
        if(number>0)
            System.out.println(Thread.currentThread().getName() + "卖出了第" + (number--) + "张票，" + "剩余" + number);
    }catch (Exception e){
        e.printStackTrace();
    }
    finally {
        lock.unlock(); //解锁
    }
    }
}
```



## 企业中应用（生产消费问题）

等待通知 生产者生产，消费者消费

三大步骤：1.判断是否等待  2.业务代码   3.通知

> synchronized版本

```java
public class test02 {
    public static void main(String[] args) {
        //资源
        Product product=new Product();
        
        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    product.inProduct();
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }
        },"生产者").start();

        new Thread(()->{
            for (int i = 0; i < 10; i++) {
                try {
                    product.deProduct();
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }
        },"消费者").start();

    }
}


//资源类，产品
class Product{

    private int productId=0;

    //生产
    public synchronized void inProduct() throws InterruptedException {
        if(productId!=0){  //if判断只能判断一次，多线程情况会造成虚假唤醒，建议使用while
            //等待
            this.wait();
        }
        //业务
        productId++;
        System.out.println(Thread.currentThread().getName()+"=>"+productId);

        //通知
        this.notifyAll();

    }

    //消费
    public synchronized void deProduct() throws InterruptedException {
        if(productId==0){  //if判断只能判断一次，多线程情况会造成虚假唤醒，建议使用while
            //等待
            this.wait();
        }

        //业务
        productId--;
        System.out.println(Thread.currentThread().getName()+"=>"+productId);
        //通知
        this.notifyAll();

    }
    }
```

> 上诉代码问题存在：只有两个线程时，安全。如果4个线程，本方法则不安全；
>
> 原因：if判断（if只会判断一次）改为while即可解决

---

> Lock版
> 		注意：Lock锁中，Codition取代了传统的wait和notify。成为了新的对象监视器
>
> ```java
>     Lock lock=new ReentrantLock(); //创建Lock
>     Condition condition= lock.newCondition(); //通过lock创建 Condition （可以创建多个）
>     condition.await();  //等待
>     condition.signalAll(); //唤醒全部
> ```
>
> 

```java
public class test02 {
    public static void main(String[] args) {
        Product product = new Product();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) product.inProduct();
        }, "生产者").start();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) product.deProduct();
        }, "消费者").start();


    }}

//资源类，产品
class Product {

    private int productId = 0;

    //锁
    Lock lock = new ReentrantLock();
    Condition condition = lock.newCondition();

    //生产
    public void inProduct() {
        lock.lock(); //加锁
        try { //全部业务丢入try

            while (productId!=0) {
                //等待
                condition.await();
            }

            //业务
            productId++;
            System.out.println(Thread.currentThread().getName() + "=>" + productId);

            //通知
            condition.signalAll();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();//解锁
        }
    }

    //消费
    public void deProduct() {
        lock.lock(); //加锁
        try { //全部业务代码
            while (productId==0) {
                //等待
                condition.await();
            }

            //业务
            productId--;
            System.out.println(Thread.currentThread().getName() + "=>" + productId);
            //通知
            condition.signalAll();

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();//解锁
        }
    }
}
```



## Condition 实现精准唤醒

> 线程A 执行后唤醒 线程B；线程B 执行后唤醒 线程C

```java
public class test02 {
    public static void main(String[] args) {
        Product product = new Product();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) product.A();
        }, "A").start();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) product.B();
        }, "B").start();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) product.C();
        }, "C").start();

    }

}



//资源类，产品
class Product {

    private int productId = 0;

    Lock lock = new ReentrantLock();
    Condition condition_A = lock.newCondition();
    Condition condition_B = lock.newCondition();
    Condition condition_C = lock.newCondition();


    public void A() {
        lock.lock(); //加锁
        try { //全部业务丢入try

            while (productId!=0) {
                // A等待
                condition_A.await();
            }

            //业务
            productId = 1;
            System.out.println(Thread.currentThread().getName() + "=>" + productId);

            //通知 唤醒指定线程B
            condition_B.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();//解锁
        }
    }


    public void B() {
        lock.lock(); //加锁
        try { //全部业务代码

            while (productId!=1) {
                //等待
                condition_B.await();
            }


            //业务
            productId = 2;
            System.out.println(Thread.currentThread().getName() + "=>" + productId);
            
            //通知C
            condition_C.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();//解锁
        }
    }

    public void C() {
        lock.lock(); //加锁
        try { //全部业务代码

            while (productId!=2) {
                //等待
                condition_C.await();
            }


            //业务
            productId = 0;
            System.out.println(Thread.currentThread().getName() + "=>" + productId);
            
            //通知A 完成循环
            condition_A.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();//解锁
        }
    }
}
```



# 并发下的集合

CopyOnWrite -写入时复制。简称COW ，是计算机次序设计领域的一种优化策略



## CopyOnWriteArrayList

由于ArrayList线程不安全，多个线程调用的时候，虽然读取是固定的位置，但写入的时候，可能会存在一种覆盖操作；

解决方法：在写入的时候复制一个数组，写完再插入（类似于快照）；

CopyOnWriteArrayList 比 Vector 效率高； 前者Lock  后者syn

---

> **ArrayList**
>
> 运行错误信息：Exception in thread "73" java.util.ConcurrentModificationException   并发修改异常

```java
public class Test03 {
    public static void main(String[] args) {
        List list=new ArrayList();

        for (int i = 0; i <= 100; i++) {
            new Thread(() -> {
                list.add(UUID.randomUUID().toString().substring(0, 5));
                System.out.println(list);
            }, String.valueOf(i)).start();
        }
    }
}
```

> **CopyOnWriteArrayList** 
>
> 被Lock修饰 安全

```java
public class Test03 {
    public static void main(String[] args) {

        List list = new CopyOnWriteArrayList();

        for (int i = 0; i <= 100; i++) {
            new Thread(() -> {
                list.add(UUID.randomUUID().toString().substring(0, 5));
                System.out.println(list);
            }, String.valueOf(i)).start();
        }

    }
}
```

---



## CopyOnWriteArraySet

> **CopyOnWriteArraySet**
>
> 和上面的List相同

```java
public class Test03 {
    public static void main(String[] args) {

        Set set=new CopyOnWriteArraySet();

        for (int i = 0; i < 100; i++) {
            new Thread(()->{
                set.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(set);
            }).start();
        }
    }
}
```

---



## CopyOnWriteHashMap

 同上，不再缀叙.....



# 常用的辅助工具类

## 减法计数 CountDownLatch

允许一个或多个线程等待，直到在其他线程中执行的一组操作完成；

用于计数；

>  countDownLatch.countDown(); //减一操作
>
>  countDownLatch.await();  //等待计数器归零，然后再向下执行

```java
public class Test03 {
    public static void main(String[] args) throws InterruptedException {
        //总数是6
        CountDownLatch countDownLatch = new CountDownLatch(6);

        //线程模拟学生离校
        for (int i = 1; i <= 6; i++) {
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"==>离校");
                countDownLatch.countDown(); //减一操作
            }).start();
        }
        
        countDownLatch.await();  //等待计数器归零，然后再向下执行

        System.out.println("关门");
    }
}
```



## 加法计数 CyclicBarrier

> CyclicBarrier cyclicBarrier = new CyclicBarrier(7,()->{ }); //创建
>
> cyclicBarrier.await();  //等待

```java
public class Test03 {
    /**
     *收集7龙珠
     */
    public static void main(String[] args) throws InterruptedException {

        //召唤龙珠的线程 （前数量，后runnable接口）
        CyclicBarrier cyclicBarrier = new CyclicBarrier(7,()->{
            System.out.println("召唤神龙");
        });

        for (int i = 1; i <= 7; i++) {
            final int tmp=i; //因为lambda 不能直接操作到i
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"收集到第"+tmp+"颗");

                try {
                    cyclicBarrier.await();//等待
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                } catch (BrokenBarrierException e) {
                    throw new RuntimeException(e);
                }

            }).start();
        }
        
    }
}
```



## 限流 Semaphore

信号量控制

> semaphore.acquire();   //获得  假设已经满了所设定的限制数量，则等待被释放
>
>  semaphore.release();  //释放 将当前的信号量释放+1
>
> 作用：多个共享资源互斥的使用，并发限流，控制最大线程数

```java
public class Test03 {
    /**
     *停车位 六辆车 三个停车位
     */
    public static void main(String[] args) throws InterruptedException {
        //线程数量: 停车位 限流3位
        Semaphore semaphore = new Semaphore(3);

        //停车
        for (int i = 1; i <= 6; i++) {
            new Thread(()->{
                // semaphore.acquire(); 得到/抢到 停车位
                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName()+"===>抢到车位");
                    TimeUnit.SECONDS.sleep(2); //停顿
                    System.out.println(Thread.currentThread().getName()+"===>离开车位");
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }finally {
                    semaphore.release(); //释放 (离开车位)
                }
            }).start();

        }
        
    }
}
```



# 读写锁 ReadWriteLock

读可以被多个线程同时读； 写只能被一个线程去写；

> private ReadWriteLock lock=new ReentrantReadWriteLock(); //读写锁（共享锁与排它锁）
>
> lock.writeLock().lock(); //加写锁
>
> lock.writeLock().unlock();//解锁
>
> lock.readLock().lock(); //加读锁
>
>  lock.readLock().unlock();//解锁

```java
public class Test04 {
    public static void main(String[] args) {
        ReadWriteLockDemo readWriteLockDemo=new ReadWriteLockDemo();

        //写入
        for (int i = 0; i < 5; i++) {
            final int tmp=i; //lambda不能直接找到i
            new  Thread(()->{
                readWriteLockDemo.put(tmp+"",tmp);
            },String.valueOf(i)).start();
        }

        //读取
        for (int i = 0; i < 5; i++) {
            final int tmp=i; //lambda不能直接找到i
            new  Thread(()->{
                readWriteLockDemo.get(tmp+"");
            },String.valueOf(i)).start();
        }

    }

}


class ReadWriteLockDemo{

    //存储  volatile关键字作用是，使系统中所有线程对该关键字修饰的变量共享可见
    private volatile Map<String, Object> map=new HashMap<>();
    //读写锁（共享锁与排它锁）
    private ReadWriteLock lock=new ReentrantReadWriteLock();

    //写操作,只希望同时仅有一个线程写
    public void put(String key,Object value){
        lock.writeLock().lock(); //加写锁
        try {
            System.out.println(Thread.currentThread().getName()+"写入==> "+key+"...");
            map.put(key,value);
            System.out.println(Thread.currentThread().getName()+"写入==> "+key+"...成功");
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            lock.writeLock().unlock();//解锁
        }
    }

    //读操作，所有人都可以读
    public void get(String key){
        lock.readLock().lock(); //加读锁
        try {
            System.out.println(Thread.currentThread().getName()+"读取==> "+key+"...");
            Object o = map.get(key);
            System.out.println(Thread.currentThread().getName()+"读取==> "+key+"...成功");
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            lock.readLock().unlock();//解锁
        }
    }
}

```







# 阻塞队列 BlockingQueue

![image-20240128094737017](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240128094737017.png)



> 使用环境：

多线程并发处理，A调用B；线程池

---

> BlockingQueue的来源

![image-20240128095026727](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240128095026727.png)

---

> 四组API

|     方式     | 无返回值，抛出异常 | 有返回值,不抛出异常 | 阻塞等待 | 超时等待 |
| :----------: | :----------------: | :-----------------: | :------: | :------: |
|     添加     |        add         |        offer        |   put    |  offer   |
|     移除     |       remove       |        poll         |   take   |   poll   |
| 检测队首元素 |      element       |        peek         |    -     |    -     |

> 代码
>

```java
public class Test05 {

    public static void main(String[] args) throws InterruptedException {
        //addAndRemove();
        //offerAndPoll();
        //putAndTake();
        //offerAndPollToTime();

    }

    /**
     * 无返回值，抛出异常
     * 当添加数据大于队列容量，抛出队列已满异常 IllegalStateException: Queue full
     * 当删除数据大于队列容量，抛出没有元素异常 NoSuchElementException
     * 当队列为空，查看队首元素抛出没有元素异常 NoSuchElementException
     */
    public static void addAndRemove() {
        //队列的大小 2
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(2);
        System.out.println(blockingQueue.add("a"));//T
        System.out.println(blockingQueue.add("b"));//T
        System.out.println(blockingQueue.add("c")); //队列已满，抛出异常

        System.out.println("===============================");
        System.out.println(blockingQueue.remove());//T
        System.out.println(blockingQueue.remove());//T
        System.out.println(blockingQueue.remove()); //没有元素，抛出异常

        System.out.println("===============================");
        System.out.println("队首元素：" + blockingQueue.element()); //查看队首元素
    }

    /**
     * 有返回值，不抛出异常
     * 当添加数据大于队列容量，抛出队列已满异常 IllegalStateException: Queue full
     * 当删除数据大于队列容量，抛出没有元素异常 NoSuchElementException
     */
    public static void offerAndPoll() {
        //队列的大小 2
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(2);
        System.out.println(blockingQueue.offer("a"));//T
        System.out.println(blockingQueue.offer("b"));//T
        System.out.println(blockingQueue.offer("c"));// F 队列已满

        System.out.println("===============================");
        System.out.println(blockingQueue.poll());//a
        System.out.println(blockingQueue.poll());//b
        System.out.println(blockingQueue.poll());// null 没有元素

        System.out.println("===============================");
        System.out.println("队首元素：" + blockingQueue.peek()); //查看队首元素
    }

    /**
     * 等待，一直阻塞
     */
    public static void putAndTake() throws InterruptedException {
        //队列的大小 2
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(2);
        blockingQueue.put("a");
        blockingQueue.put("b");
        blockingQueue.put("c"); //队列没有位置，一直阻塞，知道有位置放进去

        System.out.println("===============================");
        System.out.println(blockingQueue.take());//a
        System.out.println(blockingQueue.take());//b
        System.out.println(blockingQueue.take());//队列没有元素，一直阻塞，知道取出数据
    }


    /**
     * 超时等待
     */
    public static void offerAndPollToTime() throws InterruptedException {
        //队列的大小 2
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(2);
        blockingQueue.offer("a");
        blockingQueue.offer("b");
        blockingQueue.offer("c", 2, TimeUnit.SECONDS);// 等待超过2秒结束

        System.out.println("===============================");
        blockingQueue.poll();
        blockingQueue.poll();
        blockingQueue.poll(2, TimeUnit.SECONDS);// 等待超过2秒结束
    }

}
```



# 同步队列 SynchronousQueue

没有容量(容量为0)，进去一个元素，必须等待取出来后，才能再放进去一个元素；

put、take；

---



```java
public class Test06 {
    public static void main(String[] args) {
        synchronousQueueDemo synchronousQueueDemo=new synchronousQueueDemo();

        //存
            new Thread(()->{
                for (int i = 0; i < 10; i++) {
                    synchronousQueueDemo.put(i+"");
                }
            },"T1").start();
        
        //取    
            new Thread(()->{
                for (int i = 0; i < 10; i++) {
                    synchronousQueueDemo.take();
                }
            },"T2").start();
            
    }
}

class synchronousQueueDemo {

    //同步队列
    SynchronousQueue synchronousQueue = new SynchronousQueue();

    //存
    public void put(String v)  {
        try {
            System.out.println(Thread.currentThread().getName()+" put "+v);
            synchronousQueue.put(v);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }

    //取
    public void take()  {
        try {
            TimeUnit.SECONDS.sleep(3);
            System.out.println(Thread.currentThread().getName()+" take ");
            synchronousQueue.take();
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```





































# 三大特性

- 可见性：当一个线程修改了某些线程共享变量的值，其他线程能够立即得知这个修改。
- 有序性：保证指令不会受cpu指令并行优化的影响(即程序执行的顺序按照代码的先后顺序执行)。
- 原子性：一个操作或者一系列操作，要么全部执行成功，要么全部执行失败。

---



## 可见性 Volatile 

**Volatile 刷新主内存过程**

![image-20230513094831202](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230513094831202.png)

**实例**

```java
public class Demo4 extends Thread{
    volatile int i = 0;
        @Override
        public void run() {
            i = 100;
            System.out.println(i);
        }


    public static void main(String[] args) {
        Demo4 demo4 = new Demo4();
        demo4.start();
        int j=1;
        while(demo4.i==0){
            System.out.println("执行了"+(j++) +"次，未改变初始值"+ demo4.i);
        }
        System.out.println("主线程执行完毕");
    }
}
```

根据执行结果得出结论：添加了volatile关键字更快修改i的值



## 有序性 Volatile

有序性-happens-before原则：(8条)

- 程序次序规则：一个线程内，按照代码顺序，书写在前面的操作系统先行发生于书写在后面的操作；
- 锁定规则：一个unLock操作先行发生于后面对同一个锁的lock操作；
- volatile变量规则：对一个变量的写操作先行于发生于后面对这个变量的读操作；



**指令重排案例**

1. 定义static int a、b、x、y;变量，初始化都为0
2. main中一直循环
3. 开启两个线程：第一个线程a=1；x=b； 第二个线程b=1；y=a；
4. 启动两个线程，并使用join
5. 增加volatile观察结果

```java

```



## 原子性 atomic

```

```









# 8.并发容器

**并发**：在方法调用的时候（就是所谓任务），需要等待返回取得返回值是同步，不等待而继续执行程序代码就是异步。采用异步方式，能够支持多个任务并行执行，这种机制称为并发

- **CompletableFuture**是一个异步任务编排、调度框架，以更优雅的方式实现组合式异步编程。
- 基本的多线程编程不利于任务的管理（包括编排、调度等），在 Java8 时代，使用新的 CompletableFuture技术可以让多线程并发编程更优雅。



## 8.1单步骤

**实例一**：学生注册，在注册同时打印欢迎信息

```java
//学生
public class Student {
    private int id;
    privaet String name;
    //get、set
}
```

```java
//注册
public class Register {
    private static AtomicInteger count = new AtomicInteger(0);//保证id唯一
     // 注册学号
	public Student regId(Student student) {
    	student.setId(count.incrementAndGet());
    	return student;
 	 }  
}
```

```java
//并行注册
public class StudentIDTest {
  public static void main(String[] args) {
    // 构建学生集合
    List<Student> studentList = new ArrayList<>();
    for (int i = 1; i <= 10; i++) {
      Student s = new Student();
      s.setName("学生" + i);
      studentList.add(s);
    }

    Register reg = new Register();

    studentList.forEach(s -> {
      CompletableFuture.supplyAsync(
          // 每个学生都注册学号
          () -> reg.regId(s)
        )
        // 学号注册完毕后，打印欢迎消息
        .thenAccept(student -> {
          System.out.println("你好 " + student.getName() + ", 欢迎来到春蕾中学大家庭");
        });
    });

    System.out.println("mission complate");
  }
}
```

- `CompletableFuture.supplyAsync()` 方法运行一个异步任务并且返回结果，所以 `regId()` 方法必须有返回值。

- `Register` 虽然没有实现 `Runnable` 接口，但系统会自动优化：把作为 `supplyAsync()` 方法参数的整个 `() -> reg.regId(s)` 表达式语句包装在另一个对象中；这个对象是 JDK 内置的，它实现了 `Runnable` 接口，在这个对象中执行表达式语句。所以实际上，`supplyAsync()` 方法的作用是**：在一个单独的线程中执行 `reg.regId(s)` 语句**，本质上就是多线程编程。
- 在注册完毕以后，使用 `thenAccept()` 方法完成后继的任务步骤。`thenAccept()` 方法的参数（`student`）就是前置任务的返回结果，系统会在前一个任务完成后，**自动**执行 `student -> {}` 后继任务。所以本质上，后继任务也是多线程方式执行的。`thenAccept()` 方法通常用于任务链的末尾。

> 一般情况下，不建议一个大任务的所有步骤都集中在 `supplyAsync()` 里实现，分步骤更好

---



## 8.2 多步骤

**实列二：多步骤任务(部分并发执行代码)**

```java
//并行注册
public class StudentIDTest {
  public static void main(String[] args) {

     //注册类
    Register reg = new Register();

    studentList.forEach(s -> {
      CompletableFuture.supplyAsync(
          // 每个学生都注册学号
          () -> reg.regId(s)
          //审核学生
        ).thenApply(stu -> {
                reg.examine(stu);
                return offer;
        // 学号注册完毕后，打印欢迎消息
       }).thenAccept(student -> {
          System.out.println("你好 " + student.getName() + ", 欢迎来到春蕾中学大家庭");
        });
    });

    System.out.println("mission complate");
  }
}
```

- 只需要调用 `CompletableFuture` 类的 `thenApply()` 方法即可。
- `supplyAsync()` 用于**开头**，`thenAccept()` 用于**末尾**，各自调用一次即可。中间有多个步骤，可以调用多次 `thenApply()` 。
- 由于末尾也要用到 `student` 实例对象，所以位于中间的 `thenApply()` 方法，总是要 `return`

![j5-5-7-1.svg](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/j5-5-7-1.svg)

对于多个任务之间是并行的，使用多线程同时执行多个任务；

对于一个任务的多个步骤，是串行的，必须执行完前一个步骤才能执行下一个；

---



## 8.3返回值及返回类型

`supplyAsync()` 是静态方法，返回值是 `CompletableFuture` 实例对象，再调用 `thenApply()` 或 `thenAccept()` 实例方法，返回的也是 `CompletableFuture` 实例对象。

```java
CompletableFuture<Void> cf = CompletableFuture.supplyAsync(() -> reg.regId(s))
  .thenApply(student -> {
    return dis.assignClasses(student);
  })
  .thenAccept(student -> {
     System.out.println("姓名：" + student.getName() + "，学号：" + student.getId() + "，班级号：" + student.getClassId());
  });
```

返回的是仍是 `CompletableFuture` 实例对象，所以定义变量的类型就是 `CompletableFuture` 。

但可以用泛型 `CompletableFuture<>` 表示其中包含的数据具体是什么类型。

因为本案例末尾调用了 `thenAccept()`，其 *Lambda* 表达式没有 `return` 语句，表示 `CompletableFuture` 实例对象***不包含***数据，所以泛型写为 `CompletableFuture<Void>`。

---

**返回 CompletableFuture 类型**

如果没有调用 `thenAccept()` 方法，以 `thenApply()` 或 `supplyAsync()` 结尾的话，例如代码：

```java
CompletableFuture<Student> cf = CompletableFuture.supplyAsync(() -> reg.regId(s))
  .thenApply(student -> {
    return dis.assignClasses(student);
  });
```

因为 `thenApply()` 的 *Lambda* 表达式返回的是 `Student` 对象，所以 `CompletableFuture` 实例对象包含的是 `Student` 数据，于是泛型写为 `CompletableFuture<Student>`

> 这几个方法返回的是 `CompletableFuture` 实例，但其中包含什么类型的数据取决于 *Lambda* 表达式返回值的类型，如果没有返回值，则用 `<Void>` 表示。







## 8.4扩展知识点：main() 方法的问题

目前我们的程序，都是通过 `main()` 方法执行的。如果学生人数较多，例如 *2000* 个，所有注册线程的运行就没有那么快完毕了。

问题是，可能线程任务还没执行完毕，`main()` 方法就执行完毕，导致程序运行结束退出了。

要解决这个问题，返回值就有用了。我们先把每个学生的入学任务实例对象（`CompletableFuture<Void>`），收集起来（装入集合），然后等待所有的线程执行完毕。

```java
List<CompletableFuture> cfs = new ArrayList<>();
studentList.forEach(s -> {
  CompletableFuture<Void> cf = CompletableFuture.supplyAsync(() -> reg.regId(s))
    .thenApply(student -> {
        return dis.assignClasses(student);
    }).thenAccept(student -> {
        System.out.println("姓名：" + student.getName() + "，学号：" + student.getId() + "，班级号：" + student.getClassId());
    });

  cfs.add(cf);
});

try {
  // 等待所有的线程执行完毕
  CompletableFuture.allOf(cfs.toArray(new CompletableFuture[] {})).get();
} catch (Exception e) {
  e.printStackTrace();
}
```

`CompletableFuture.allOf()` 是静态方法，作用就是收集所有的任务实例对象。因为 `allOf()` 方法只支持数组不支持集合，所以需要把集合转换成数组（`cfs.toArray(new CompletableFuture[] {})`）。当然，你可以一开始就定义数组来收集任务实例对象，因为学生的个数可以通过 `studentList.size()` 取得。`allOf()` 方法的返回值也是 `CompletableFuture` 实例对象。再调用类方法 `get()`，其作用就是等待所有的任务线程（`allOf()` 收集的）都执行完毕，再继续执行。

**需要强调的是**：

- 在 *SpringBoot* 等服务端运行 `supplyAsync()` 异步任务编排的时候，就没有必要可以使用 `get()` 方法等待所有线程任务执行完毕了。因为服务端往往是常驻程序，不像 `main()` 方法执行完毕就退出程序了。
- `get()` 方法造成了 `main()` 方法等待，所以是同步的；通过 `CompletableFuture` 编排的任务，不会造成 `main()`方法等待，所以是异步。





## 8.5拓展知识点：原子操作布尔值

`java.util.concurrent.atomic.AtomicInteger` 能够以原子的方式操作整数

 `java.util.concurrent.atomic.AtomicBoolean` 能够以原子的方式操作布尔值。

布尔值只有 **true**/**false** 两个值，`AtomicBoolean` 使用起来就很简便了。

`AtomicBoolean` 是 `boolean` 的包装类，`AtomicBoolean` 的实例等同于一个布尔值：

- `new AtomicBoolean(true)` 等同于 **true**
- `new AtomicBoolean(false)` 等同于 **false**

---

**实例对象取得基础类型的布尔值，可以调用 `get()` 方法：**

```java
AtomicBoolean ab = new AtomicBoolean(true);
boolean value = ab.get();
```

**实例对象调用 `compareAndSet()` 方法，就能以原子的方式修改值：**

`compareAndSet(true, false)` 判断当前值为 **true** 时，修改为 **false**，然后返回成功或失败。这是三个步骤哦。

- 修改成功后，方法返回 `true` 。
- 如果当前值不是 **true** ，则不修改，返回值为 `false`，表示操作失败

> `compareAndSet()` 实际上就是保证了整个修改操作的三个步骤的原子性，不会因为多线程出现错乱。

***再次强调***：`compareAndSet()` 方法返回值表示**修改操作**成功或失败，跟方法参数值无关。



**初始化AtomicInteger数组**

```java
private static AtomicBoolean[] PLACES = {
        new AtomicBoolean(float),
        new AtomicBoolean(float)
}; //初始化，存两个float的数组
```





# 9.线程池

使用`Runnable` 接口开发多线程程序，更符合面向对象的习惯，但是随之而来的问题是，对象太多。

在现实中，如果有一千位同学入学，就意味着程序要额外 `new Thread(register)` 一千次。对象除了创建需要消耗计算机 CPU、内存等资源，对象还会被销毁（系统自动做的），销毁也是要消耗资源的。

那么能不能做一些优化，做到复用 `Thread` 对象，不必每次都创建新对象呢？答案是有的：Java 提供了 ***线程池*** 技术。

---

**线程池基本概念**

所谓 线程池，顾名思义，就像一个池子，里面装满了线程，随用随取。线程可以被 复用，一个线程，可以执行 A 任务，也可以执行 B 任务，于是线程不再频繁创建和销毁。

> `new Thread(register)` 意味着一个线程对象只能执行一个任务，而线程池让线程与任务分离，不再紧密绑定。

线程池的另一个重要概念是，线程池并不是无限大的（因为计算机的CPU、内存等资源毕竟有限），所以线程池中存在的线程数也是 **有限** 的，这就意味着能同时运行的任务数是 **有限** 的，其它过剩的任务就需要 **排队** 。待任务完成、有空闲的线程后，才能继续执行任务。

**典型的线程池案例-银行业务办理：**

![image-20230514092841896](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230514092841896.png)

---

## 9.1线程池实现

**通过ThreadPoolExecutor构建线程池服务**

```java
public static void main(String[] args) {
    ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(
        3,     //创建几个线程 一般两位数
        5,     //线程池最大容量 通常不超过200
        1L,    //多长时间不用自动销毁 想立即回收则0，一般30
        TimeUnit.SECONDS,  //时间单位（这里是秒）
        new ArrayBlockingQueue<>(3),  //等待队列容量[也可以使用自定义的等待队列]
        Executors.defaultThreadFactory(), //线程工厂（通过线程工厂才能创建线程对象）[也可以使用自定义线程工厂]
        new ThreadPoolExecutor.AbortPolicy());  //拒绝策略（当线程池和等待队列都满了，开启拒绝策略，本方法抛出异常）

	//测试
     for (int i = 0; i < 7; i++) {         
         threadPoolExecutor.execute(()->{    
             System.out.println(Thread.currentThread().getName()+"====>正在办理业务");  
             });
        }
}
```

**创建自定义线程工厂**

- `BasicThreadFactory` 需要依赖一个库，这个库也是经常会使用的工具库：

```xml
<dependency>
  <groupId>org.apache.commons</groupId>
  <artifactId>commons-lang3</artifactId>
  <version>3.10</version>
</dependency>
```

- 自定义线程工厂

```java
  private static final ThreadFactory namedThreadFactory = new BasicThreadFactory.Builder()
    .namingPattern("studentReg-pool-%d") //定义线程名字的格式，相当于线程模板，根据需求修改“studentReg”，%d自动编号
    .daemon(true)   //设置线程为守护线程，即后台线程，当所有非守护线程都执行完毕时，JVM会自动退出
    .build();       //构建ThreadFactory对象
```

**创建等待队列**

```java
private static final BlockingQueue<Runnable> workQueue = new LinkedBlockingQueue<Runnable>(1024);
//CPU核多内存大一般2048，性能一般则1024
```

---

**使用线程池运行任务**

```java
 List<Offer> offers = getOffers();
offers.forEach(offer->{
    //创建Runnable 对象
    Publisher publisher=new Publisher(offer);
    // 传入 Runnable 对象，运行任务
    threadPoolExecutor.execute(publisher);
    });
}
```







## 9.2线程池与并发容器的选择

**问题：**多线程编程到底要用什么？并发容器？还是线程池？



实际上 `CompletableFuture` 内部也用到了线程池，是把任务放入内部的**默认线程池**里执行的。

```java
CompletableFuture.supplyAsync(
    () -> reg.regId(s)
  )
```

也可以指定线程池来运行任务：

```java
CompletableFuture.supplyAsync(
    () -> reg.regId(s),
    EXECUTOR_SERVICE //supplyAsync的第二个参数，传入我们构建好的线程池对象。那么任务就是用指定的线程池而不是默认的
  )
```



> ### 技术升级
>
> 线程池也可以运行任务，但是不利于编排，只是把实现了 `Runnable` 接口的任务对象扔进线程池运行。
>
> *Java* 系统的升级进化历程：
>
> ```
> 基础多线程
> ↓
> 线程池
> ↓
> 并发容器
> ```
>
> 如果一家企业技术升级较慢，还处于 **Java 6** 时代，那么多线程编程用***线程池***就够了；如果一家企业技术升级较快，已经使用 **Java 8** ，那就要用并发容器了。
>
> ### 指定线程池的场景
>
> 在学习阶段，一般来说，直接使用 `supplyAsync(() -> {})` 就够了。在企业中，遇到任务并发度高、任务量大、任务执行慢的情况下，就需要指定线程池，严格控制线程任务了。
>
> 或者一开始使用 `CompletableFuture`默认线程池，当发现任务执行满、任务堆积的问题时，就要考虑指定线程池，并调整线程池参数。

































