







# 5.各类注解详解

**jdk内置注解**

```java
@Override                   /* 检测被该注解标注的方法是否继承自父类（接口）  如果父类没有，则报错*/
@Deprecated                 /*该注解标注的内容已过时，但可以继续用（引用时会有斜线）*/
@SuppressWarnings("all")    /*压制警告 让所有警告不显示*/
```

---

**Spring注解**

类级别的注解： 如@Component、@Repository、@Controller、@Service以及JavaEE6的@ManagedBean和@Named注解，都是添加在类上面的类级别注解。

类内部的注解： 如@Bean、@Autowire、@Value、@Resource以及EJB和WebService相关的注解等，都是添加在类内部的字段或者方法上的类内部注解。



- 声明bean的注解

```java
@Component    //组件，通用的注解方式

@Service      //在业务逻辑层使用（service层）

@Repository   //在数据访问层使用（dao层） 需要在Spring中配置扫描地址,然后生成Dao层的Bean才能被注入到Service层中

@Mapper       //在数据访问层使用（dao层）不需要配置扫描地址，通过xml里面的namespace里面的接口地址，生成了Bean后注入到                    Service层中

@Controller    //在表现层使用，控制器的声明（C）
```

- 注入bean的注解

```java
@Autowired     //使用在字段或方法上，用于根据类型byType注入引用数据

@Value         //使用在字段或方法上，用于注入普通数据

@Qualifier     //使用在字段或方法上，结合@Autowired 根据名称注入

@Resource       //使用在字段或方法上，根据类型或名称进行注入
```

- java配置类相关注解

```java
@Configuration      //声明当前类为配置类，相当于xml形式的Spring配置（类上）

@Bean                //注解在方法上，声明当前方法的返回值为一个bean，替代xml中的方式（方法上）示把此方法返回的对象实例注                        册成为bean

@Configuration       //声明当前类为配置类，其中内部组合了@Component注解，表明这个类是一个bean（类上）

@ComponentScan       //用于对Component进行扫描，相当于xml中的（类上）

@WishlyConfiguration //为@Configuration与@ComponentScan的组合注解，可以替代这两个注解
```

- 启动类注解

```java
@PostConstruct   		    //在Bean启动后自动执行被标注的方法

@SpringBootApplication      //加了@SpringBootApplication的注解的类是启动类 默认扫描启动类所在包及其包下子包进行解                                 析，如果有与启动类所在包平级的其他包，并不会扫描，也不会实例化

@ComponentScan({"fm.service", "fm.app"})  //若不是Spring Boot启动类，可以使用独立注解@ComponentScan，作用相同，                                           用于指定多个待扫描包
```



- 业务逻辑层相关注解

```
```

- 数据访问层相关注解

```java
```

- 表现层相关注解

```java
@Controller
@RequestMapping     //用于映射web请求，包括访问路径和参数。

@GetMapping         //与@RequestMapping效果一样，支持某样http method 更安全

@RequestParam("id")   //url参数

@ResponseBody        //支持将返回值放到response内，而不是一个页面，通常用户返回json数据。


@RequestBody          //允许request的参数在request体中，而不是在直接连接的地址后面。（放在参数前）

@PathVariable          //用于接收路径参数，比如@RequestMapping(“/hello/{name}”)声明的路径，将注解放在参数前，即                          可获取该值，通常作为Restful的接口实现方法。

@RequestParam(value="pageNum",required = false) int pageNum  //非必须传递参数 如果是int必须写为Integer
    
    
@RestController         //所有方法不渲染Thymeleaf页面，而是都返回数据，等同于@Controller加上@ResponseBody
```



- 数据效验注解

```java
@NotNull  //不允许为null对象

@AssertTrue  //是否为ture

@Size   //约定字符串长度

@Min  //字符串最小长度

@Max   //字符串最大长度

@Email  //是否是邮箱格式

@NotEmpty  //不允许为空和null，可判断字符串、集合

@NotBlank  //不允许为null和空格
```



```java
@EnableSpringHttpSession   /*开启session*/

```

**自定义注解格式**

```java
/*格式*/
元数据
public @interface 注解名称{}


/*注解本质就是一个接口，该接口默认继承Annotation：*/
public interface 注解名 extends java.lang.annotation.Annotation{}

/*属性：接口中的抽象方法
       要求：1.属性的返回值类型只能是基本数据类型、String、枚举、注解、以上类型的数组
            2.定义了属性，在使用时需要给属性赋值，如果只有一个属性需要赋值，则属性名可以不写
 */

/*@Override注解的实际格式*/
@Target(ElementType.METHOD) //作用于类的方法上
@Retention(RetentionPolicy.SOURCE)//纯注释作用
public @interface Override{    
}
```





---

## 5.1元注解

元注解是用来修饰其他自定义注解的

**Target 元注解**

- java.lang.annotation.Target 自身也是一个注解，它只有一个数组属性，用于设定该注解的目标范围，比如说可以作用于类或方法等。因为是数组，所以可以同时设定多个范围

- 如果某个Annotation的Target设定为METHOD，那么就只能在方法的前面引用它，其他地方都不行，其它Target值也类似规则

```java
ElementType.TYPE    //可以作用于类、接口类、枚举类上
ElementType.FIELD   //可以作用于类的属性上
ElementType.METHOD  //可以作用于类的方法上
ElementType.PARAMETER //可以作用于类的参数上

/*如果想同时作用于类和方法上，就可以如下*/
@Target({ElementType.TYPE,ElementType.METHOD})
```

Target实例

```java
/*注意以下实例中的注解都包含有Target*/
/* ElementType.TYPE  */
@Service  /*实例化当前对象，存入Spring容器，以messageServiceImpl为名称*/
public class MessageServiceImpl implements MessageService{
    public String getMessage() {
         return "Hello World!";
    }
}

/* ElementType.METHOD */
public class MessageServiceImpl implements MessageService{
    @ResponseBody
    public String getMessage() {
         return "Hello World!";
    }
}

/* ElementType.FIELD  */
public class MessageServiceImpl implements MessageService{
    @Autowired
    private WorkspaceService workspaceService;
}

/* ElementType.PARAMETER */
public class MessageServiceImpl implements MessageService{
    public String getMessage(@RequestParam("msg")String msg) {
         return "Hello "+msg;
    }
}
```



---

**Retention 元注解**

- `java.lang.annotation.Retention`自身也是一个注解，用于声明该注解的生命周期，就是在java编译、运行的哪个环节有效，它的值定义在java.lang.annotation.RetentionPolicy枚举类中，有三个值：

​          SOURCE      纯注释作用

​          CLASS         在编译阶段有效

​          RUNTIME   在运行时有效

```java
/*在运行期间有效   一般都定义为RUNTIME*/
@Retention(RetentionPolicy.RUNTIME)
```



---

**Documented元注解**

- java.lang.annotation.Documented自身也是一个注解，作用是将注解元素包含到javaDoc文档中
- 如果一个注解@B，被@Documented标注，那么被@B修饰的类，生成文档时，会显示@B。如果@B没有被@Documented标准，最终生成的文档中就不会显示@B。

```java
@Documented
```



---

**interface 元注解**

- @interface就是声明当前的java类型是Annotation,固定语法

```java
public @interface 注解名称{
}
```



---

**Annotation属性**

Annotation的属性有点像类的属性一样，它约定了属性的类型（基础类型）和属性名称（默认value），default代表的是默认值

```java
String value() default "";

String value() default -1; //-1代表不存在
```

- Annotation也是java类，一样需要import
- @Service 也可以写为  @Service(value="Demo")
- 又由于value 是默认属性名称，可以缩写，所以也可以写为 @Service("Demo")

```java
import org.springframework.stereotype.Service;
@Service
public class Demo {
}
```

- Annotation属性是可以有多个
- @AliasFor("name") 是别名的意思（这个属性用这个别名也可以访问到）

```java
@Target(ElementType.PARAMETER)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface RequestParam {
    @AliasFor("name")   
    String value() default "";

    @AliasFor("value")
    String name() default "";

    boolean required() default true;
    String defaultValue() default ValueConstants.DEFAULT_NONE;
}
```







## 5.2Spring注解原理-Bean实例化

注解本质是XML配置 注解的作用是简化Bean配置

![image.png](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1680694937215-5df1503e-386a-4f5f-953a-02fcbffb6a4c.png)

---



### 5.2.1Component -bean标签

当Bean不在某一层（既不属于业务层，也不是web层又不是dao层），又需要Spring进行维护，所以使用Component



**基本Bean注解，主要是使用注解的方式替代原有的xml的`<bean>`标签及其标签属性的配置**

```xml
<bean id="" name="" class="" scope="" lazy-init="" init-method="" destroy-method=""
abstract="" autowire="" factory-bean="" factory-method=""></bean>
```

**使用@Component注解替代`<bean>`标签**

![image-20230416144125798](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230416144125798.png)

==相当于：==

```java
//<bean id="userDao" class="com.tihema.dao.impl.UserDaoImpl">
@Component
public class UserDaoImpl implements UserDao{
    
}
```







### 5.2.2Bean标签属性注解@Scope@Lazy@PostConstruct/Destroy

**使用@Component注解代替`<bean>`标签**

![](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230416144255476.png)







### 5.2.3Component的衍生注解@Repository@Services@Controller

由于JavaEE开发是分层的，为了每层Bean标识的注解语义化更加明确，@Component又衍生如下三个注解

![image-20230416144456959](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230416144456959.png)

```java
@Repository("userDao")
public class UserDaoImpl implements UserDao{}

@Service("userService")
public class UserServiceImpl implements UserService{}

@Controller("userService")
public class UserController{}
```



### 5.2.4依赖注入的相关注解 @Autowired@Value@Resource@Qualifier

Bean依赖注入的注解，主要是使用注解的方式替代xml的`<property>`标签完成属性的注入操作

```xml
<bean id="" name="" class="" >
	<property name="" value=""/>
    <property name="" ref=""/>
</bean>
```

**Spring主要提供如下注解，用于在Bean内部进行属性注入的**

![image-20230416145114551](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230416145114551.png)

---

**Value**

```java
@Value("zhangsan")
private String username;

@Value("list")
public void setUsername(String username){
    this.username=username;
}
```

---

**Autowired**

@Autowired 根据类型进行注入，如果有同一类型的Bean有多个，尝试根据名字进行二次匹配，匹配不成功再报错

```java
@Autowired
public void xxx(UserDao userDao){
    this.userDao=userDao;
}


@Autowired
public void xxx(List<UserDao> userDaoList){
    this.userDaoList=userDaoList;
}
```

---

**Qualifier**

配合Autowired使用 指定注入名字为userDao的Bean

```java
@Autowired
@Qualifier("userDao")
private UserDao userDao;
```

---

**Resource**

相当于Autowired+Qualifier 不常用 

```java
@Resource(name="userDao")
private UserDao userDao;
```







### 5.2.5 配置类相关注解@ Configuration

- @Configuration注解标识的类为配置类，代替原有xml配置文件，该注解第一个作用是标识该类是一个配置类，第二个作用是具备@Component作用
- @ComponentScan组件扫描配置，代替原有xml文件中的`<context:component-scan base-package=""/>`

```java
//标注当前类是配置类 代替xml文件+@Component  
@Configuration
//等同于 <context:component-scan base-package="com.ithema"/>
@ComponentScan({"com.ithema"})
//等同于 <context:property-placeholder location="classpath:jdbc.properties"/>
@PropertySource("classpath:jdbc.properties")
public class ApplicationContextConfig{   
}
```

base-package的配置方式：

​	指定一个或多个包名：扫描指定包及其子包下使用注解的类

​	不配做包名：扫描当前@ComponentScan注解配置类所在包及其子包下的类





### 5.2.6Boot启动类相关注解

**Boot启动方式确定扫包范围注解**

- 本方法一般不用

```java
@EnableAutoConfiguration
@ComponentScan("com.youkeda.comment")
public class CommentApplication {

	public static void main(String[] args) {
		SpringApplication.run(CommentApplication.class, args);
	}
}
```

- 一般使用

```java
/**
*@SpringBootApplication 组合了
*                       @EnableAutoConfiguration
*                       @ComponentScan
**/
@SpringBootApplication
public class CommentApplication {
	public static void main(String[] args) {
		SpringApplication.run(CommentApplication.class, args);
	}

}
```







# 7.文件系统SpringResource-读取-封装

工程文件的三种情况

```java
文件在本地，例如d:/mywork/a.doc     //可以用file
文件在工程目录下，例如mywork/toutiao.png   //可以用file
文件在工程的src/main/resources目录下  //不可以用file，需要classpath，并需要三方库commons-io
```

**classpath**：

- 在java内部，一般把文件路径称为classpath，所以读取内部文件就是从classpath中获取，classpath指定的文件不能解析成file对象，但可以解析为InputStream，借助java IO就可以读出
- classpath类似虚拟目录，它的根目录'/'开始代表的是src/main/java目录或者src/main/java目录

---

**读取**：

配置读文件所需要的三方库commons-io依赖

```xml
<dependency>
  <groupId>commons-io</groupId>
  <artifactId>commons-io</artifactId>
  <version>2.6</version>
</dependency>
```

classpath读取文件实例:

- 接口定义方法

```java
public interface FileService {
    String getContent(String name);
}
```

- 实现类中实现

```java
@Service
public class FileServiceImpl implements FileService {
    @Autowired
    private ResourceLoader loader;  
    @Override
    public String getContent(String name) {
        try {
            /*InputStream是输入流
                getResource(name)接收一个表示文件路径的参数，返回一个url对象，该对象表示的是name指向的文件资源
               getInputStream()获取输入流
               IOUtils.toString（）将实体流转化为字符串*/
            InputStream in = loader.getResource(name).getInputStream();
            return IOUtils.toString(in,"utf-8");
        } catch (IOException e) {
           return null;
        }
    }
}
```

- 测试

​           实例：工程目录src/main/resources/data/urls.txt

```java
  FileService fileService = context.getBean(FileService.class);
  String content = fileService.getContent("classpath:data/urls.txt");
  System.out.println(content);
```

​              实例：工程目录mywork//readme.md

```java
String content2 = fileService.getContent("file:mywork/readme.md");
System.out.println(content2);
```

​             实例：加载远程文件

```java
String content3 = fileService.getContent("https://www.zhihu.com/question/34786516/answer/822686390");
System.out.println(content3);
```

---





# 13.Spring Data

## 13.1Mongodb安装-启动-配置

**优客达平台安装**

```shell
#要先配置好docker

#docker安装mongodb
sudo docker run -itd --name mongo -p 27017:27017 mongo

#验证登录
sudo docker exec -it mongo mongosh admin

#创建practice数据库，同时完成创建和切换
use practice

#查询所有数据库
show dbs

#查询数据库中集合 （需先进入数据库）
show collections

#查看集合所有数据（需先进入数据库）
db.news.find()

#删除数据库 （需先进入数据库）
db.dropDatabase()

#删除集合（需先进入数据库）
db.名字.drop()




```



---

**本地安装**

- windows本地安装：https://www.yuque.com/yangzhi-odbdk/npye9n/zq27ovwovf2e7un5/edit
- windows使用mongodb命令：https://blog.51cto.com/u_15101587/2624026
- mongodb操作命令：https://blog.csdn.net/qq_34093387/article/details/128330637

**windows本地常用命令**

```shell
启动：   mongo 或mongod --dbpath=..\data\db
进入：    mongo --host=127.0.0.1 --port=27017
创建practice数据库：    use practice
	
查看所有数据库：    show dbs
切换到不同数据库：    use userdb
查看所有集合(表)    show tables  和   show collections
```





## 13.2Spring Data Mongodb配置

可以通过网页https://start.spring.io/创建 增加一个Spring Data Mongodb选项就行了

如果已经创建好了，也可以手动添加依赖：

```xml
<!--Spring Data Mongodb依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

修改src/main/resources/application.properties文件增加配置项：

```properties
# 购买的云服务器的公网 IP
spring.data.mongodb.host=192.168.0.1
# MongoDB 服务的端口号
spring.data.mongodb.port=27017
# 创建的数据库及用户名和密码
spring.data.mongodb.database=practice
```

注意：如果本地电脑用本地数据库就是127.0.0.1；如果是远程电脑用本地数据库就是本地数据库所在的电脑ip；

因为MongoDB的配置文件默认是本地ip访问，所以需要改配置文件	mongodb/config.conf

```properties
# network interfaces
net:
  port: 27017
  bindIp: 0.0.0.0
```







## 13.3Spring Data CRUD-增删改查

- 对数据库的操作一定要在@service类中（即service接口即实现类），不能放@Controller类（即Control控制类）中且@Controller类可以调用@service类方法，反之不可，这是SpringMVC经典架构设计理念
- @service类主要用于不异变的核心业务逻辑
- @Controller类与前端页面紧密配合，调用@service服务读写数据，从而响应前端请求

---

**新增数据-mongoTemplate.insert（"要添加的数据"）**

==mongoTemplate.insert(); 返回类型由添加的数据决定，添加什么就返回什么==



实现类中实现

```java
@Autowired   
private MongoTemplate mongoTemplate;  //注入mongodb的实例MongoTemplate

//传入数据添加并返回
public Song add(Song song) {
    return mongoTemplate.insert(song); //添加的数据是什么类型，返回的就是什么类型
  }
```

控制类中调用

```java
@Autowired   
private SongService songService; //注入接口实例

 @RequestMapping("add")
    public Map add(){
     //调用Impl里的增加方法, 返回map到网页
     Map map=new HashMap();
     Song song=new Song();
     song.setSubjectId("s001");
     song.setLyrics("...");
     song.setName("成都");
     
    Song song1=songService.add(song);

     map.put("song1",song1);
     return map;
    }
```



---

**查询数据-mongoTemplate.findById("查询的主键","查询的类名.class")**

==mongoTemplate.findById(id, Song.class); 返回类型由查询的数据决定，查询什么就返回什么==



实现类中实现

```java
public Song get(String id) {
    return mongoTemplate.findById(id, Song.class); 返回类型由查询的数据决定，查询什么就返回什么
  }
```

控制类中调用     传入id，通过实现类获取实例

```java
@Autowired   
private SongService songService; //注入接口实例
 
    public Map get(@RequestParam String id){
     //调用Impl里的增加方法, 返回map到网页    
    Map map=new HashMap();
    Song song=songService.get(id);  

     map.put("song",song);
     return map;
    }

```



---

**修改数据-mongoTemplate.updateFirst("查询对象","要修改数据","要修改的对象的类**

- 修改数据包括两步：修改哪条数据，修改为什么值 --即修改条件和修改字段
  Criteria类  条件对象
  Query  查询对象

1.先使用条件对象 Criteria 构建条件对象实例 再构建查询对象Query
2.使用修改对象Update的方法 .set设置需要修改的字段
3.调用mongoTemplate.updateFirst(query, updateData, Song.class)方法完成修改
    参数1：查询对象
    参数2：要修改数据
    参数3：要修改的对象的类



实现类中实现

```java
public boolean modify(Song song) {
    //修改传输过来的song
  Criteria criteria=Criteria.where("id").is(song.getId());
  Query query = new Query(criteria);

// 把歌名修改为 “new name”  修改语句
Update updateData = new Update();
updateData.set("name", "new name");

// 执行修改，修改返回结果的是一个对象
UpdateResult result = mongoTemplate.updateFirst(query, updateData, Song.class);
// 修改的记录数大于 0 ，表示修改成功
System.out.println("修改的数据记录数量：" + result.getModifiedCount());

return  result!=null&&result.getModifiedCount()>0;
}
```

控制类中调用   传入要修改的数据id 和要修改的数据 通过实现类实现并返回boolean

```java
@Autowired   
private SongService songService; //注入接口实例

    public Map mod(String id，String name){
     //调用Impl里的增加方法, 返回map到网页
    Map map=new HashMap();
        Song song=new Song();
        song.setId(id);
        song.setName(name);
    boolean result=songService.modify(id);
     map.put("modify",result);
     return map;
    }
```

---

**删除数据-mongoTemplate.remove("要删除数据")**

实现类中实现

```java
public boolean delete(String songId) {   
 Song song = new Song();
 song.setId(songId);
// 执行删除
DeleteResult result = mongoTemplate.remove(song);
// 删除的记录数大于 0 ，表示删除成功
System.out.println("删除的数据记录数量：" + result.getDeletedCount());
return  result!=null&&result.getDeletedCount()>0;
}
```

控制类中调用  传入要删除的数据id，通过实现类完成并返回boolean

```java
@Autowired   
private SongService songService; //注入接口实例

    public Map del(@RequestParam String id){
     //调用Impl里的增加方法, 返回map到网页
    Map map=new HashMap();
    boolean result=songService.delete(id);

     map.put("delete",result);
     return map;
    }
```

传入一个对象，这个对象相当于在remove里是这样的  {id:xxx}

- remove方法可以接受一个对象类型的参数，表示删除id为xxx的数据字段

![Clipboard - 2023年4月20日晚上8点54分](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/Clipboard%20-%202023%E5%B9%B44%E6%9C%8820%E6%97%A5%E6%99%9A%E4%B8%8A8%E7%82%B954%E5%88%86.png)

---







## 13.4**Spring Data Query-条件查询**



**条件查询-mongoTemplate.find(“查询对象实例”, “查询对象类名.class”);**

```java
/*构建单一条件查询对象*/
Criteria criteria = Criteria.where("条件字段名").is("条件值");
Query query = new Query(criteria);


/*构建组合条件查询对象  根据或（or）、且（and）的关系组合，多子条件组合总条件*/
Criteria criteria=new Criteria();
criteria.orOperator(criteria1, criteria2);
Query query = new Query(criteria);



/*多层组合*/
public List<Song> list(Song songParam) {
    // 总条件
    Criteria criteria = new Criteria();
    // 可能有多个子条件
    List<Criteria> subCris = new ArrayList();
    if (StringUtils.hasText(songParam.getName())) {//StringUtils.hasText()判断是否为空
      subCris.add(Criteria.where("name").is(songParam.getName()));
    }

    if (StringUtils.hasText(songParam.getLyrics())) {
      subCris.add(Criteria.where("lyrics").is(songParam.getLyrics()));
    }

    if (StringUtils.hasText(songParam.getSubjectId())) {
      subCris.add(Criteria.where("subjectId").is(songParam.getSubjectId()));
    }

    // 必须至少有一个查询条件
    if (subCris.isEmpty()) {//判断长度
      LOG.error("input song query param is not correct.");
      return null;
    }

    // 三个子条件以 and 关键词连接成总条件对象，相当于 name='' and lyrics='' and subjectId=''
    criteria.andOperator(subCris.toArray(new Criteria[]{}));

    // 条件对象构建查询对象
    Query query = new Query(criteria);
    // 仅演示：由于很多同学都在运行演示程序，所以需要限定输出，以免查询数据量太大
    query.limit(10);
     //因为多条件查询，所以可能是多对象，需要集合存储
    List<Song> songs = mongoTemplate.find(query, Song.class);

    return songs;
}
```







# 14.Spring Data-分页

分页是查询中最常用功能，为了防止一次查询的数据量太大而影响性能



**分页-PageRequest.of("页码0开始","每页数量")**

```java
/*
查询支持分页：只需要调用ageRequest.of()方法构建一个分页对象，然后注入查询对象中
分页需要的查询结果、查询总数，才可以计算总共页数，才能实现完整分页功能

调用count(query, XXX.class)方法查询总数。参数1：查询条件  参数2：查询什么对象
根据结果、分页条件、总数构建分页器对象
*/

// 总数
long count = mongoTemplate.count(query, Song.class);
// 构建分页器
Page<Song> pageResult = PageableExecutionUtils.getPage(songs, pageable, new LongSupplier() {
    @Override
    public long getAsLong() {
        return count;
    }
});
```



---

**条件查询-分页返回实例**

 实现类

```java
public Page<Song> list(Song songParam) {
    // 作为服务，要对入参进行判断，不能假设被调用时，入参一定正确
    if (songParam == null) {
    LOG.error("input song data is not correct.");
    return null;
}
 // 总条件
Criteria criteria = new Criteria();
// 可能有多个子条件
List<Criteria> subCris = new ArrayList();
if (StringUtils.hasText(songParam.getName())) {
    subCris.add(Criteria.where("name").is(songParam.getName()));
}

if (StringUtils.hasText(songParam.getLyrics())) {
    subCris.add(Criteria.where("lyrics").is(songParam.getLyrics()));
}

if (StringUtils.hasText(songParam.getSubjectId())) {
    subCris.add(Criteria.where("subjectId").is(songParam.getSubjectId()));
}

// 必须至少有一个查询条件
if (subCris.isEmpty()) {
    LOG.error("input song query param is not correct.");
    return null;
}

// 三个子条件以 and 关键词连接成总条件对象，相当于 name='' and lyrics='' and subjectId=''
criteria.andOperator(subCris.toArray(new Criteria[]{}));

// 条件对象构建查询对象
Query query = new Query(criteria);
// 仅演示：由于很多同学都在运行演示程序，所以需要限定输出，以免查询数据量太大
query.limit(10);
List<Song> songs = mongoTemplate.find(query, Song.class);

Pageable pageable = PageRequest.of(0 , 20);
query.with(pageable);
long count = mongoTemplate.count(query, Song.class);
Page<Song> pageResult = PageableExecutionUtils.getPage(songs, pageable, new LongSupplier() {
    @Override
    public long getAsLong() {
        return count;
    }
});
return pageResult;
}
```

控制类

```java
public Map list(String subjectId, String name, String lyrics) {
    Map returnData = new HashMap();
    Song queryParam = new Song();
    queryParam.setSubjectId(subjectId);
    queryParam.setLyrics(lyrics);
    queryParam.setName(name);
    Page<Song> songResult = songService.list(queryParam);
    List<Song> songs = songResult.getContent();
    returnData.put("songResult", songs);
    return returnData;
}
/*注：还有个实例在用户注册登录实战里，该实例描述如何取出查询后返回结果的第一个值*/
```





# ############Maven##################



# 工程化工具Maven

**注意：Maven所有xml配置必须放在 src/main/resources + 类的全路径 下**

Maven仓库地址：https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient/3.1

Maven是一个项目管理和构建自动化工具

![image.png](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1678452359241-37ee472a-3a7f-4df9-8f79-cafca774c27b.png)

# Maven安装

**Maven安装**：https://www.bilibili.com/video/BV16Q4y127BZ/

**Maven命令**

```shell
mvn clean compile 
#编译命令
#Maven会自动扫描src/maign/java 下的代码并完成编译工作，执行时，会在根目录下
#生成target/classes目录（存放所有class） 
    
mvn clean package
#编译并打包命令
#这个命令是compile和package的集合，会先执行compile命令，然后再执行jar打包命令，
#这个的结果是把所有java文件和资源打包成一个jar（jar是java的压缩格式）


mvn clean install
#执行安装命令
#先执行compile编译命令，再执行jar打包命令，然后执行install安装到本地的Maven仓库目录
#这个目录是${user_home}/.m2  （即电脑登录用户的个人目录）


mvn compile exec:java -Dexec.mainClass=${main}
#这个命令是在compile执行完成后，执行运行java的命令
#具体执行哪个java由 '-Dexec.mainClass=${main}'参数指定
#例如想执行com.youkeda.Test类：
#mvn compile exec:java -Dexec.mainClass=com.youkeda.Test
```





# Maven 配置文件pom.xml



![image.png](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1678452576930-b911feb3-1cef-4e4a-bb55-cc3d4d6444bb.png)

一个java项目所有的配置都放在POM文件中，大致有如下行为：

- 定义项目的类型、名字
- 管理依赖关系
- 定制插件

---

**Maven坐标**

```xml
<groupId>com.youkeda.course</groupId>
<artifactId>app</artifactId>
<packaging>jar</packaging>
<version>1.0-SNAPSHOT</version>
```

- **groupld**   

  ​     类似于文件夹，它的命名和java的包一致，这里一般只用小写的英文字面和字符'.'
  ​	一般一个公司都会设置自己的groupld，以防重名

- **artifactId**

  类似于文件名，在一个groupld内是唯一的，不能使用中文或特殊符号，只能使用小写字母和'.' '-' '_'

- **packaging**

  Maven工程执行完后会把整个工程打包成packaging指定的文件格式，默认是jar

  packaging有如下格式：jar   war     ear     pom

- **version**

  遵守软件工程对版本号的约定

  工程一般两个状态：

  测试阶段：SNAPSHOT      例子：[version]-SNAPSHOT

  发布后：  RELEASE       例子：[version]-RELEASE

  一般用三个数字表示版本号：x.x.x

  第一位是主版本号：一般是团队约定来的

  第二位是新增功能：是多少就代表了新增了多少次功能的行为

  第三位是bugfix后的版本：bugfix是修改bug，是几就修复了几次

---

**Maven属性配置**

```xml
<properties>
    <java.version>1.8</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.target>${java.version}</maven.compiler.target>
</properties>
```

- **格式**：在<properties>标签内
- **java.version** 

​         代表设置一个参数

- **maven.compiler.source** 

​         指定Maven编译时候源代码JDK版本，${java.version}是一个动态值
${key}这个语法会动态找到key这个参数配置的值

- **project.build.sourceEncoding**

  指定工程代码源文件的文件编码格式，一般情况下，都设置为UTF-8

- maven.compiler.target

  这个参数作用是按照这个值来进行编译源代码

---

**Maven依赖管理**

```xml
<dependencies>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.62</version>
    </dependency>
</dependencies>
```

- **dependency**   标签的内容其实就是Maven坐标，所以说只要有坐标我们就可以建立依赖
- **dependencies**  标签中可以添加多个依赖
- **间接依赖**：如果一个remote工程依赖okhttp库，而当前工程locale依赖了remote工程， 这时候locale工程也会自动依赖okhttp

---

**Maven插件**

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
        </plugin>
    </plugins>
</build>
```

**maven-compiler-plugin** 用于执行maven compile

插件体系让Maven这个工具变得高度可定制，可以无缝的支撑工程化能力

maven插件其实也是存放在中央仓库的坐标，也是一切都是jar





# 查看自己引入的依赖关系图

![image-20230815152343762](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230815152343762.png)





# 常用的Maven库依赖集合

Maven仓库地址：https://mvnrepository.com/artifact/commons-httpclient/commons-httpclient/3.1

```xml
<!--以下所有依赖，都必须在 <dependencies> 标签中配置-->


		<!--Spring开发的基本包  建立Spring容器框架必须引入-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.6.RELEASE</version>
        </dependency>

		<!-- spring开发切面编程需要的 aspects 包  切面编程时必须引入 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.2.6.RELEASE</version>
        </dependency>


        <!--spring-jdbc Spring框架中的模块，提供了对Java数据库连接的支持。Spring框架Jdbc操作数据库必须导入-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.6.RELEASE</version>
        </dependency>
        <!--mysql-connector-java mysql的驱动，用于连接和操作MySQL数据库 只要操作mysql必须导入，该包中包含了c3p0-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.11</version>
        </dependency>
 		 <!--spring-orm  Spring 框架中的一个模块，提供了对 对象关系映射（ORM）的支持 该包中包含了spring-tx-->
   		 <dependency>
       	 	<groupId>org.springframework</groupId>
        	<artifactId>spring-orm</artifactId>
        	<version>5.3.8</version>
   		 </dependency>
		<!--c3p0 用于管理数据库连接池。它提供了高性能、可配置的连接池，并支持连接池的自动监控和管理-->
    	<dependency>
        	<groupId>com.mchange</groupId>
       		<artifactId>c3p0</artifactId>
       	 	<version>0.9.1.2</version>
        </dependency>
		<!-- spring-tx 是Spring 框架中的一个模块，提供了对事务的支持。-->
   		 <dependency>
       		 <groupId>org.springframework</groupId>
       		 <artifactId>spring-tx</artifactId>
       		 <version>5.3.8</version>
    	</dependency>


        <!-- Spring Web  SpringMVC必须引入，可以在项目中使用SpringWeb提供的控制器、请求映射、视图解析器等-->
		<!--也是使用controller层各项请求注解必须要引入的包-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>5.3.9</version>
        </dependency>

		<!--客户端Http请求 处理xml数据的依赖-->
		<dependency>
			<groupId>com.fasterxml.jackson.dataformat</groupId>
			<artifactId>jackson-dataformat-xml</artifactId>
		</dependency>





<!--#############################以下是常用的 Spring Boot 工程需要引入的#################################-->

		<!--SpringBoot父工程 告诉Maven在构建过程中使用指定的SpringBoot Starter Parent作为父项目-->
		<!--创建spring boot项目必须写 注意：不在dependencies标签中 -->
		<parent>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-parent</artifactId>
			<version>3.1.2</version>
			<relativePath/> 
		</parent>

		<!--导入web项目场景启动器：会自动导入和web开发相关的所有依赖[jar/库]-->
		<!--将springboot、spring、springmvc、tomcat、日志、json都引入-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>







        <!--链接Spring Boot和MyBatis，构建基于Spring Boot的MyBatis应用程序-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.2</version>
        </dependency>
        <!--MySQL提供的JDBC驱动包，用于JDBC连接MySQL数据库-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>









<!--#####################################以下是常用的第三方库##########################################-->

        <!--读取配置文件的第三方库-->
        <dependency>
            <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
            <version>2.6</version>
        </dependency>



```





# ############Spring##################



# Spring容器介绍

**简介：**

> - Spring是一个开源免费的框架 , 容器 .
> - Spring是一个针对bean的生命周期进行管理的轻量级的框架 , 非侵入式的 .
> - 控制反转 IoC , 面向切面 Aop
> - 对事物的支持 , 对框架的支持
> - 解决企业应用开发的复杂性
>
> ***Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器（框架）\***

**底层结构图：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230731105452820.png" alt="image-20230731105452820" style="zoom: 50%;" />

> **Bean 实例化基本流程：**
>
> Spring容器在进行初始化时，会将xml配置的<bean>的信息封装成一个BeanDefinition对象，所有的BeanDefinition存储到一个名为beanDefinitionMap的Map集合中去，Spring框架在对该Map进行遍历，使用反射创建Bean实例对象，创建好的Bean对象存储在一个名为singletonObjects的Map集合中，当调用getBean方法时则最终从该Map集合中取出Bean实例对象返回

---

**Maven工程项目的Spring依赖**

```xml
<!--spring5依赖-->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>5.2.6.RELEASE</version>
</dependency>
```

---

实例化

```java
@ComponentScan
public class Application {
    public static void main(String[] args) {
        /*启动容器 ，并自动加载包Application下的Bean（在Bean内且引用Spring注解的类）*/
        ApplicationContext context = new AnnotationConfigApplicationContext(Application.class);
        /*从容器中获取msgService服务*/
        MessageService msgService = context.getBean(MessageService.class);
        
        System.out.println(msgService.getMessage());
    }
}
```

---



# 基于xml的Bean配置

> **导入Spring开发ioc的基本包(也可以选择配置Maven)**

- **spring-expression-5.3.8.jar**
- **spring-core-5.3.8.jar**
- **spring-context-5.3.8.jar**
- **spring-beans-5.3.8.jar**

> 导入spring写日志需要的包

- **commons-logging-1.1.3.jar**

----

> 配置javaBean

完整的<bean >标签

```xml
<bean id="" name="" class="" scope="" lazy-init="" init-method="" destroy-method=""
abstract="" autowire="" factory-bean="" factory-method=""></bean>
```



## 根据类型或Id获取Bean

**java类代码**

```java
public class Monster {
    private String name;
    private String skill;
    
    //get、set 有参无参构造 toString省略
}
```

**xml配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">

    <!--
    1.配置Monster对象的JavaBean
    2.在本xml中可以配置多个Bean
    3.bean表示一个java对象

    class属性用于指定类的全路径 ->spring底层使用反射创建（故java对象必须要有无参构造器）
    id属性表示该bean在spring容器中的id。通过id可以获取到该对象
    <property name="name" value="悟空"/>用于给该对象的属性赋值
    -->
    <bean class="com.wang.spring.bean.Monster" id="monster01">
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>
    
</beans>
```

**java测试**

```java
public class test {
    @Test
    public void getMonster(){
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //根据id获取Bean：通过getBean() 获取id对应的对象 
        Object monster01 = ioc.getBean("monster01");
        
        //根据类型获取Bean： 类型获取需要保证同一类型的bean只能有一个
        Object monster02 = ioc.getBean( Monster.class);
        System.out.println((Monster)monster01);

        //也可以直接获取 Monster 的bean，无需强转
        Monster monster011 = ioc.getBean("monster01", Monster.class);
        System.out.println(monster011);
    }
}
```

---





## 根据构造器配置Bean

**XML配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">

    <!--
    1.constructor-arg标签可以指定使用构造器的参数
    2.index表示构造器的第几个参数，从0开始
    3.除了可以通过index，还可以通过name、Type来指定参数方式（原理：类构造器参数列表不能有完全相同的类型、顺序）
	<constructor-arg value="八戒" name="name"/>
    <constructor-arg value="钉耙" type="java.lang.String"/>
    -->
    <bean class="com.wang.spring.bean.Monster" id="monster02">
        <constructor-arg value="八戒" index="0"/>
        <constructor-arg value="钉耙" index="1"/>
    </bean>
</beans>
```

**java测试**

```java
public class test {
    @Test
    public void getMonster(){

        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取 Monster 的bean，无需强转
        Monster monster02 = ioc.getBean("monster02", Monster.class);
        System.out.println(monster02);
    }
}
```

**注意：本方法会调用无参构造器和有参构造器**故无参有参都要有

---





## 根据P名称空间配置Bean

**XML**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/util https://www.springframework.org/schema/util/spring-util.xsd">

    <!--
    1.选择p，alt+enter  会自动添加 xmlns:p
    -->
    <bean class="com.wang.spring.bean.Monster" id="monster03"
          p:name="唐僧"
          p:skill="锡杖">
    </bean>
</beans>
```

java测试同上

---



## ref 引入/注入其他Bean对象（依赖注入）

> 在Spring的Ioc容器，可以通过ref（Reference：引入参考）来实现Bean对象的相互引用

**java类代码**

```java
package com.wang.spring.dao;
public class MonsterDaoImpl {
    //构造器
    public MonsterDaoImpl() {
        System.out.println("monsterDaoImpl 构造器被执行");
    }
    //方法
    public void add(){
        System.out.println("monsterDaoImpl add方法被执行");
    }
}
```

```java
package com.wang.spring.server;
import com.wang.spring.dao.MonsterDaoImpl;
public class MonsterServerImpl {
    private MonsterDaoImpl monsterDao;
    //add方法
    public void add(){
        System.out.println("MonsterServer add方法被执行");
        //调用 MonsterDaoImpl 的add方法
        monsterDao.add();
    }

    //get、set
    public MonsterDaoImpl getMonsterDao() {
        return monsterDao;
    }
    public void setMonsterDao(MonsterDaoImpl monsterDao) {
        this.monsterDao = monsterDao;
    }
}

```

****

**XML配置**

```xml
    <!--配置 MonsterDaoImpl 对象-->
    <bean id="monsterDao" class="com.wang.spring.dao.MonsterDaoImpl"></bean>

    <!--配置 MonsterServer 对象
     1. ref="monsterDaoImpl" 表示 MonsterServerImpl对象，其属性monsterDao引用的是id=monsterDao 的对象
     2.这里就体现出spring容器的依赖注入
     3.spring容器是作为一个整体执行，所以对配置的顺序没有要求
    -->
    <bean id="monsterServer" class="com.wang.spring.server.MonsterServerImpl">
        <property name="monsterDao" ref="monsterDao"/>
    </bean>
```

**Java测试**

```java
public class test {
    @Test
    public void getMonster(){

        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取 MonsterServerImpl 的bean，无需强转
        MonsterServerImpl monsterServer = ioc.getBean("monsterServer", MonsterServerImpl.class);
        monsterServer.add();
    }
}

/**测试结果：
 * monsterDaoImpl 构造器被执行
 * MonsterServer add方法被执行
 * monsterDaoImpl add方法被执行
 */
```

---



## 引入/注入内部Bean对象

> 在spring的Ioc容器中，可以直接配置内部bean

**Jvav类代码同上**

**xml配置**

```java
    <!--配置 MonsterServer 对象 使用内部配置的bean-->
    <bean id="monsterServer" class="com.wang.spring.server.MonsterServerImpl">
        <!--自己配置一个内部的bean 表示属性monsterDao的值是 MonsterDaoImpl对象-->
        <property name="monsterDao" >
            <bean class="com.wang.spring.dao.MonsterDaoImpl"/>
        </property>
    </bean>
```

**java测试代码同上**



---



## 引入/注入集合、数组

​	**Java类代码**

```java
public class Master {
    private String name;
    private List<Monster> monsterList;
    private Map<String, Monster> monsterMap;
    private Set<Monster> monsterSet;
    private String[] monsterName;

    // 这 个 Properties 是 Hashtable 的 子 类 , 是 key-value的形式
    // 这 里 Properties key和value都是String
    private Properties pros;

    
    
    //构造方法和get/set及toString ......
}
```

> **给list集合属性注入值**

```xml
<!-- 给集合属性注入值-->
    <bean id="master" class="com.wang.spring.bean.Master">
        <!--给普通string属性注入值-->
        <property name="name" value="吴承恩"/>
        
        <!--给list注入值 注入了俩个-->
        <property name="monsterList">
            <list>
                <ref bean="monster01"/>
                <ref bean="monster02"/>
            </list>
        </property>
        
    </bean>
```

---

> **给Map集合属性注入值**

```xml
    <bean id="master" class="com.wang.spring.bean.Master">
        <property name="monsterMap">
            <map>
                <!-- map 里面是一对一对的entry 每个entry都是一个k-v -->
                <entry>
                    <key>
                        <value>monster_map01</value>
                    </key>
                    <ref bean="monster01"/>
                </entry>

                <entry>
                    <key>
                        <value>monster_map02</value>
                    </key>
                    <ref bean="monster02"/>
                </entry>
            </map>
        </property>
    </bean>
```

---

> **给Set属性注入值**

```xml
    <bean id="master" class="com.wang.spring.bean.Master">
        <property name="monsterSet">
            <set>
                <ref bean="monster01"/>
                <ref bean="monster02"/>
            </set>
        </property>
    </bean>
```

---

> **给数组属性注入值**

```xml
    <bean id="master" class="com.wang.spring.bean.Master">
        <property name="monsterName">
            <array>
                <value>齐天大圣</value>
                <value>天蓬元帅</value>
            </array>
        </property>
    </bean>
```

---

> **给Properties属性注入值**

```xml
    <bean id="master" class="com.wang.spring.bean.Master">
        <!-- Properties属性结构k-v kv都是String-->
        <property name="pros">
            <props>
                <!-- key="userName"定义k  root是v-->
                <prop key="userName">root</prop>
                <prop key="paswword">123456</prop>
            </props>
        </property>
    </bean>
```



## 通过util名称空间创建list

> 在spring的Ioc容器中，可以通过util名称空间创建list集合

**用本方法是为了代码复用**

**xml配置**

```xml
    <!--util是为了代码复用 类似于java的方法-->
    <util:list id="list">
        <ref bean="monster01"/>
        <ref bean="monster02"/>
    </util:list>


    <bean class="com.wang.spring.bean.Master" id="master">
        <!--引用定义的util-->
        <property name="monsterList" ref="list"/>
    </bean>
```



## 级联属性赋值

> spring的Ioc容器，可以直接给对象属性的属性赋值，即级联属性赋值

对象属性的属性---给A类对象的B类属性 的 属性赋值	

```xml
	<!--配置Dept对象-->
	<bean id="dept" class="com.hspedu.spring.beans.Dept"/>
	
	<!--配置 Emp对象-->
	<beanid="emp"class="com.hspedu.spring.beans.Emp"> 
        <property name="name" value="jack"/> 
        <property name="dept"ref="dept"/> 
        <!--给Dept类的属性赋值-->
        <property name="dept.name" value="Java 开发部"/>
	</bean>
```





## 通过静态工厂获取Bean

**java类-静态工厂代码**

```java
public class MyBeanFactory {
    private static final Map<String, Monster> monsterMap = new HashMap<>();
    //创建实例
    static {
        monsterMap.put("monster_01", new Monster("悟空", "金箍棒"));
        monsterMap.put("monster_02", new Monster("八戒", "九齿钉耙"));

    }
    //  获取实例的方法
    public static Monster getMonster(String key){
        return monsterMap.get(key);
    }
}
```

**xml配置**

```xml
 <!--通过静态工厂来获取bean对象
    1.配置monster对象
    2.class 是静态工厂全路径
    3.factory-method 表示是指定静态工厂哪个方法返回对象
    4.<constructor-arg value="monster_01"/>   value 是指定要返回哪个静态工厂的对象  若value不变，则获取的对象也不变
    -->
    <bean id="monsterFactory" class="com.wang.spring.bean.MyBeanFactory" factory-method="getMonster">
            <constructor-arg value="monster_01"/>
        </bean>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        Monster monster01= ioc.getBean("monsterFactory", Monster.class);
        System.out.println(monster01);
```





## 通过实例工厂获取Bean

**java类-实例工厂代码**

```java
public class MyBeanFactory {
    private  final Map<String, Monster> monsterMap = new HashMap<>();
    //创建实例
     {
        monsterMap.put("monster_01", new Monster("悟空", "金箍棒"));
        monsterMap.put("monster_02", new Monster("八戒", "九齿钉耙"));

    }
    //  获取实例的方法
    public  Monster getMonster(String key){
        return monsterMap.get(key);
    }
}
```

**xml配置**

```xml
    <!--配置实例工厂对象-->
    <bean id="monsterFactory" class="com.wang.spring.bean.MyBeanFactory"/>

    <!--通过实例工厂，配置monster对象
    1.factory-bean 指定使用哪个实例工厂对象返回bean
    2.factory-method 指定使用实例工厂对象的哪个方法返回bean
    3.<constructor-arg value="monster_01"/>  value 是指定要返回实例工厂的哪个monster对象-->
    <bean id="myBeanFactory" factory-bean="monsterFactory" factory-method="getMonster">
        <constructor-arg value="monster_01"/>
    </bean>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        Monster monster01= ioc.getBean("myBeanFactory", Monster.class);
        System.out.println(monster01);
```



## 通过FactoryBean获取对象 [重点]

**java代码**

```java
//实现FactoryBean接口 <Monster>是类型
public class MyFactoryBean implements FactoryBean<Monster> {
    //配置时指定获取的对象的key值
    private String key;

    //初始化
    private Map<String,Monster> monsterMap=new HashMap<>();
    {
        monsterMap.put("monster_01", new Monster("悟空", "金箍棒"));
        monsterMap.put("monster_02", new Monster("八戒", "九齿钉耙"));
    }

    //获取对象
    @Override
    public Monster getObject() throws Exception {
        return this.monsterMap.get(key);
    }
    //获取对象类型
    @Override
    public Class<?> getObjectType() {
        return Monster.class;
    }
    //是否单例
    @Override
    public boolean isSingleton() {
        return true;
    }
    
//get、set方法
}
```

**xml配置**

```xml
    <!-- 配置monster对象 通过FactoryBean
    1.class 指定使用的FactoryBean
    2.key表示就是MyFactoryBean 属性key
    3.value就是你要获取的对象对应的key （初始化在hashMap中的对象）-->
    <bean id="myFactoryBean" class="com.wang.spring.bean.MyFactoryBean">
        <property name="Key" value="monster_01"/>
    </bean>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        Monster monster01= ioc.getBean("myFactoryBean", Monster.class);
        System.out.println(monster01);
```



## Bean配置信息重用(继承)

**xml配置**

```xml
    <!-- 配置Monster对象
    1.如果bean指定了 abstract="true" 表示该bean对象是被用于继承 且本bean不能被获取/实例化-->
    <bean id="monsterAbstract" class="com.wang.spring.bean.Monster" abstract="true">
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>

    <!--配置Monster对象 继承于monsterAbstract
	1.parent 指定继承的bean-->
    <bean id="monster" class="com.wang.spring.bean.Monster" parent="monsterAbstract"/>
```





## Bean的单例和多实例

> 在spring的Ioc容器中，默认是安装单例创建的，即配置一个bean对象猴，ioc容器只会创建一个bean实例。
>
> 如果我们希望ioc容器配置的某个bean对象，是以多个实例形式创建的，则可以通过 scope="prototype" 来指定

**xml配置**

```xml
    <!-- 配置Monster对象
    1.  scope 默认是="singleton"单例 。若scope设为="prototype"则多实例
     2.若bean设置为单例的 当程序员执行getBean时，返回的是同一个对象
     3.若bean设置为多时例的 当程序员执行getBean时，每次返回的都是新对象-->
    <bean id="monsterAbstract" class="com.wang.spring.bean.Monster" scope="prototype" >
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>
```

> bean配置默认是单例的，在启动容器时，默认就会创建
>
> 当设置为多实例后，该bean是在getBean时才创建
>
> 如果是单例，同时希望在getBean时才创建 ，可以指定懒加载 lazy-init="true" （默认是false）

**xml配置**

```xml
    <!--懒加载-->
    <bean id="monsterAbstract" class="com.wang.spring.bean.Monster" scope="singleton" lazy-init="true" >
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>
```



## Bean的生命周期

**bean对象创建是由JVM机完成的，然后执行以下方法：**

1. 执行构造器
2. 执行set方法
3. 调用bean的初始化方法（需要配置）
4. 使用bean
5. 当容器关闭时，调用bean的销毁方法（需要配置）

---

**Java类代码**

```java
public class House {
    private String name;
    
    //初始化
    public void init() {
        System.out.println("House 的初始化方法init被执行");
    }

    //销毁
    public void destory() {
        System.out.println("House 的销毁方法destory被执行");
    }

    //省略一系列有参、无参构造；get、set方法；tostring方法；
}
```

**xml配置**

```xml
    <!--配置bean的初始化方法和销毁方法 演示bean生命周期
    1.init-method="init" 指定bean的初始化方法，在setter方法后执行
    2.destroy-method="destory" 指定bean销毁方法，在容器关闭时执行
    3.初始化和销毁方法执行的时机，由spring容器来控制-->
    <bean class="com.wang.spring.bean.House" id="house"
          init-method="init"
          destroy-method="destory">
        <property name="name" value="汤臣一品"/>
    </bean>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        House house = ioc.getBean("house", House.class);
        System.out.println(house);

        /*
         * 关闭容器
         * 1.ioc的编译类型为ApplicationContext 运行类型为 ClassPathXmlApplicationContext
         * 2.ApplicationContext没有close方法，所以无法直接调用
         * 3.又因 ClassPathXmlApplicationContext 实现了 ConfigurableApplicationContext
         * 4.ConfigurableApplicationContext 有close方法，故将ioc强转后调用close
         */
        ((ConfigurableApplicationContext) ioc).close();

/** 执行结果
 * House 的无参构造被调用           --执行构造
 * House 的setName被调用           --执行setter
 * House 的初始化方法init被执行      --执行初始化
 * House{name='汤臣一品'}          --使用bean
 * House 的销毁方法destory被执行     --销毁
 */
```





## Bean后置处理器

> 在spring容器中，可以配置bean的后置处理器
>
> 该处理器/对象会在bean**初始化方法调用前**和**初始化方法调用后**被调用   ---AOP
>
> 程序员可以在后置处理器中编写自己的代码

****

**java后置处理器代码**

```java
// 配置Bean后置处理器 需要实现BeanPostProcessor接口
public class MyBeanPostProcessor implements BeanPostProcessor {

    /**
     * 什么时候调用：在init初始化方法之前
     * @param bean  传入的、在ioc容器中创建/配置的bean
     * @param beanName 传入的、在ioc容器中创建/配置的bean 的Id
     * @return 程序员对传入的bean进行修改/处理后 返回
     * @throws BeansException
     */
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessBeforeInitialization 被调用");
        
        //判断如果类型是House 将其name改为中南海 （改的是所有的House）
        if(bean instanceof House){
            ((House)bean).setName("中南海");
        }
        return bean;
    }

    /**
     * 什么时候调用：在init初始化方法之后
     * @param bean  传入的、在ioc容器中创建/配置的bean
     * @param beanName 传入的、在ioc容器中创建/配置的bean 的Id
     * @return 程序员对传入的bean进行修改/处理后 返回
     * @throws BeansException
     */
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessAfterInitialization 被调用");
        return bean;
    }
}
```

**xml配置**

```xml
    <!--配置house对象-->
    <bean class="com.wang.spring.bean.House" id="house" init-method="init" destroy-method="destory">
        <property name="name" value="汤臣一品"/>
    </bean>

    <!--配置后置处理器对象 MyBeanPostProcessor
    1.当我们在xml中配置后置处理器对象，这时后置处理器就会作用在该容器的对象中（xml中所以创建的bean）-->
    <bean class="com.wang.spring.bean.MyBeanPostProcessor" id="myBeanPostProcessor"/>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        House house = ioc.getBean("house", House.class);
        System.out.println(house);
		//销毁
        ((ConfigurableApplicationContext) ioc).close();

/** 执行结果
 House 的无参构造被调用
 House 的setName被调用
 postProcessBeforeInitialization 被调用
 House 的初始化方法init被执行
 postProcessAfterInitialization 被调用
 House{name='中南海'}
 House 的销毁方法destory被执行
 */
```





## 通过配置文件properties配置Bean

**properties文件**

```properties
#属性文件有中文时，需要转换为unicode码 否则乱码
#name=悟空
name=\u609f\u7a7a
#skill=金箍棒
skill=\u91d1\u7b8d\u68d2
```

**xml配置**

```xml
    <!--指定属性的配置文件
    1.location="classpath:myproperties.properties" 表示指定的属性配置文件 要携带classpath
    -->
    <context:property-placeholder location="classpath:myproperties.properties"/>


    <!-- 配置Monster文件
    1.通过 指定属性的配置文件 给Monster对象赋值
    2.这时我们的属性值通过${属性名} 这里的属性民是 properties文件中的k
    -->
    <bean class="com.wang.spring.bean.Monster" id="monster">
        <property name="name" value="${name}"/>
        <property name="skill" value="${skill}"/>
    </bean>
```





## 自动装配Bean

> 自动装配 需要配置  
>
> 1. **autowire="byType"   类型自动装配   --容器中不能同时存在两个相同类型bean对象**
> 2. **autowire="byName" 名字自动装配  --会根据这个对象的属性的setXxx()中的Xxx来找容器中对象的Id**

**java代码**

```java
package com.wang.spring.dao;
public class MonsterDaoImpl {   
    //有参无参构造器
}



//----------MonsterServerImpl中有MonsterDaoImpl类型的属性--------------------------------------------
package com.wang.spring.server;
public class MonsterServerImpl {
    private MonsterDaoImpl monsterDao;
    
    //get、set
}
```

**xml配置**

```xml
    <!--配置MonsterDaoImpl对象-->
    <bean class="com.wang.spring.dao.MonsterDaoImpl" id="monsterDao"/>


    <!--配置 MonsterServerImpl 对象
    1.autowire="byType" 表示在创建MonsterServerImpl时，通过类型给对象的属性自动完成赋值
    2.比如MonsterServerImpl 对象有 private MonsterDaoImpl monsterDao;
    就会在容器中去找 有没有 MonsterDaoImpl 类型对象，如果有，自动装配。
    3.如果是按照类型自动装配，则容器中不能同时存在两个MonsterDaoImpl类型对象-->
    <bean class="com.wang.spring.server.MonsterServerImpl" id="monsterServer" autowire="byType"/>
```

**java测试**

```java
        //创建容器 ApplicationContext  该容器和容器配置文件关联
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        //直接获取bean
        MonsterServerImpl monsterServer = ioc.getBean("monsterServer", MonsterServerImpl.class);
		//输出属性值 若没自动装配则null 若有自动装配 则输出对象哈希值
        System.out.println(monsterServer.getMonsterDao());  //com.wang.spring.dao.MonsterDaoImpl@6cc558c6
```







## Spring EL表达式配置Bean

**java代码**

```java
package com.wang.spring.bean;

public class SpELBean {
    private String name;
    private Monster monster;
    private String monsterName;
    private String crySound;
    private String bookName;
    private Double result;

    //自定义方法
    public String cry(String sound) {
        return "发出 " + sound + "叫声...";
    }
    public static String read(String bookName) {
        return "正在看 " + bookName;
    }
    
    //省略了有参无参构造、getset方法、toString方法
}
```

**xml配置**

```xml
    <!-- spring el表 达 式-->
    <bean id="spELBean" class="com.wang.spring.bean.SpELBean">
        <!--sp el给字面量 -->
        <property name="name" value="吴承恩"/>
        <!-- sp el 引用其它bean -->
        <property name="monster" value="#{monster01}"/>
        <!-- sp el 引用其它bean的属性值 -->
        <property name="monsterName" value="#{monster02.name}"/>
        <!-- sp el 调用普通方法赋值-->
        <property name="crySound" value="#{spELBean.cry('喵喵的..')}"/>
        <!-- sp el 调用静态方法赋值-->
        <property name="bookName" value="#{T(com.wang.spring.bean.SpELBean).read(' 西游记')}"/>
        <!-- sp el 通过运算赋值-->
        <property name="result" value="#{89*1.2}"/>
    </bean>

	<!--省略了 id为 monster01 和 monster02 的对象-->
```









# 基于注解的Bean配置

注解本质是XML配置 注解的作用是简化Bean配置

> **导入包(也可以选择配置Maven)**

-  **spring-aop-5.3.8.jar**

---



## 配置文件自动扫描包

> 在xml文件中添加

```xml
    <!--配置自动扫描的包,注意需要加入context名称空间
    1. base-package 指定一个或多个包名,扫描指定包及其子包下使用注解的类-->
    <context:component-scan base-package="com.wang.spring.annotation"/>
```

> **也可以使用注解**
>
> 1. **@Configuration**  标注当前类是配置类 ，代替xml文件+@Component
> 2. **@ComponentScan({"xxx"})**  配置文件包扫描路径,等同于  **<context:component-scan  base-package="xxx"/>**
> 3. **@PropertySource("classpath:xxx")**  指定属性文件 ,等同于  <context:property-placeholder location="classpath:xxx"/>

```java
@Configuration
@ComponentScan({"com.ithema"})
@PropertySource("classpath:jdbc.properties")
public class ApplicationContextConfig{   
}
```

---

> **xml配置扫描包注意事项**：

- 必须在 Spring 配置文件中指定"自动扫描的包"，IOC 容器才能够检测到当前项目中哪些类被标识了注解， 注意到导入context名称空间

```xml
<!-- 配置自动扫描的包  可以使用通配符*来指定 ，比如 com.hspedu.spring.* 表示-->
<context:component-scanbase-package="com.hspedu.spring.component"/>
```

- Spring的IOC容器不能检测一个使用了@Controller注解的类到底是不是一个真正的控 制器。注解的名称是用于程序员自己识别当前标识的是什么组件。其它的@Service @Repository 也是一样的道理 [也就是说spring的IOC容器只要检查到注解就会生成对象， 但是这个注解的含义spring 不会识别，注解是给程序员编程方便看的]

- 只扫描满足要求的类 【使用的少，不想扫描，不写注解就可以】

```xml
<!--resource-pattern="User*.class":  表示只扫描 com.hspedu.spring.component 包下 User开头的类 -->
<context:component-scan base-package="com.hspedu.spring.component" resource-pattern="User*.class"/>
```

- 排除哪些类 【如果希望排除某个包/子包下的某种类型的注解，可以通过exclude-filter 指定】 

```xml
<!--exclude-filter 指定要排除的哪些类
    type 指定要排除的方式  type="annotation"表示按照注解来排除
	expression 指定要排除的注解的全路径-->
<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Service"/>
</context>
```

- 指定自动扫描哪些注解类【按照自己的方式指定要扫描的注解的类】

```xml
<!--
	1.use-default-filters="false" 表示不再使用默认的过滤机制
	2.context:include-filter 表示只扫描指定的注解的类 
	3.type 指定方式  type="annotation"表示按照注解来指定
	4.expression 指定要扫描的注解的全路径-->
<context:component-scan base-package="com.hspedu.spring.component" use-default-filters="false"> 			<context:include-filter type="annotation" expression="org.springframework.stereotype.Service"/> 		<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/> </context:component-scan>
```

- 指定注解类Id 【**默认是类名首字母小写**，但也可以使用value属性手动指定Id】

```java
@Controller(value="userAction01")
@Controller("userAction01")
```







## 组件注解

**基于注解的方式配置bean，主要是项目开发中的组件，比如Controller、Service、Dao**

**使用@Component注解代替`<bean>`标签**

当Bean不在某一层（既不属于业务层，也不是web层又不是dao层），又需要Spring进行维护，使用Component

> **组件注解的形式有：**
>
> 1. **@Component**     表示当前注解标识的是一个组件，等同于  **<bean id=" " class=" ">**  **其下三个注解都是其衍生注解**
> 2. **@Controller**      表示当前注解表示的是一个控制器，通常用于Servlet (web层）
> 3. **@Service**     表示当前注解标识的是一个处理业务逻辑的类，通常用于Service类
> 4. **@Repository** 标识当前注解标识的是一个持久化层的类，通常用于Dao类

```java
@Component  //等同于<bean id="userDao" class="com.tihema.dao.impl.UserDaoImpl">
public class UserDaoImpl implements UserDao{}

@Repository("userDao") 
public class UserDaoImpl implements UserDao{}

@Service("userService")
public class UserServiceImpl implements UserService{}

@Controller("userService")
public class UserController{}
```



## 引入注入注解

**Bean依赖注入的注解，主要是使用注解的方式替代xml的`<property>`标签完成属性的注入操作**

> 1. **@Value**  使用在字段或方法上注入普通数据
> 2. **@Autowired**   使用在字段或方法上，根据类型注入引入数据
> 3. **@Qualifier**  使用在字段或方法上，结合 @Autowired，根据名称注入
> 4. **@Resource**  使用在字段或方法上，根据类型或名称注入 【常用】

**Value注解**

```java
@Value("zhangsan")   //等同于 <property name="username" value="zhangsan"/>
private String username;

@Value("list") 
public void setUsername(String username){
    this.username=username;
}
```

**Autowired 注解** 【根据类型进行注入，如果有同一类型的Bean有多个，尝试根据名字进行二次匹配，匹配不成功再报错  **过时**】

```java
@Autowired   //等同于 <bean class=" " id=" " autowire="byType"/>
public void xxx(UserDao userDao){
    this.userDao=userDao;
}

@Autowired
public void xxx(List<UserDao> userDaoList){
    this.userDaoList=userDaoList;
}
```

**Qualifier注解** 【配合Autowired使用 指定注入名字为userDao的Bean】

```java
@Autowired
@Qualifier("userDao")  //等同于  <property name="userDao"> <qualifier value="userDao" /> </property>
private UserDao userDao;
```

**Resource注解**【 相当于Autowired+Qualifier   **常用**】

```java
@Resource(name="userDao")  //名字匹配
private UserDao userDao;

@Resource(type=UserDao.class)  //类型匹配（类型必须唯一）
private UserDao userDao;

@Resource    //先根据名字注入，如果匹配不上，再根据类型注入，再匹配不成功则报错
private UserDao userDao;
```



## Bean标签属性注解

**注意：在使用本标签时，必须在组件注解下**

> **bean标签属性注解：**
>
> 1. **@Scope**  类或被@Bean标注的方法上使用，标注bean为单例或多例【singleton/prototype】，等同于 <bean scope=" "/> 
> 2. **@Lazy**  类或被@Bean标注的方法上使用，标注bean是否延迟加载【true/false】，等同于 <bean lazy-init=" "/>
> 3. **@PostConstruct** 在方法上使用，标注bean实例化后执行的方法【即初始化方法】，等同于 <bean init-method=" "/>
> 4. **@PreDestory** 在方法上使用，标注bean销毁前执行方法,等同于 <bean destroy-method=" "/>

**Scope注解**【默认 singleton，即单例】

```java
@Component
@Scope("prototype") //等同于 <bean id=" " class=" " scope="prototype" >
public class User{}

@Component
@Scope//等同于 <bean id=" " class=" " scope="singleton" >
public class User{}
```

**Lazy注解**【默认false，即非延迟加载，容器启动立即实例化】

```java
@Component
@Lazy(true)  //等同于 <bean id="" class=" " lazy-init="true" >
public class MyBean {}
```

**PostConstruct注解** 【标注初始化方法，容器实例化立即执行，类似于静态代码块】

```java
@PostConstruct  //等同于 <bean init-method="init">
public void init() {}
```

**PreDestory注解** 【标注bean销毁后执行的方法，容器销毁后执行】

```java
@PreDestory  //等同于  <bean destroy-method="destory">
public void destory() {}
```



## Boot启动类注解

> **Boot启动方式确定扫包范围注解**：
>
> 1. **@EnableAutoConfiguration**   该注解会根据现有的类路径下的配置和约定，自动加载和配置所需的bean和其他组件
> 2. **@ComponentScan(" ")**   指定要扫描的组件的基础包路径。它会自动扫描并注册带有特定注解的**组件**
> 3. **@SpringBootApplication**   该注解等同于@EnableAutoConfiguration+@ComponentScan(" ") 

- 本方法一般不用

```java
@EnableAutoConfiguration  
@ComponentScan("com.youkeda.comment") //等同于<context:component-scan base-package="com.youkeda.comment"/>
public class CommentApplication {
	public static void main(String[] args) {
		SpringApplication.run(CommentApplication.class, args);
	}
}
```

- 一般使用

```java
/**
*@SpringBootApplication 组合了
*                       @EnableAutoConfiguration
*                       @ComponentScan
**/
@SpringBootApplication
public class CommentApplication {
	public static void main(String[] args) {
		SpringApplication.run(CommentApplication.class, args);
	}
}
```





## 【重点】 注解配置Bean的机制模拟

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/%7B159FBACB-8199-4413-A574-BB1749D8FCAD%7D.png.jpg" alt="{159FBACB-8199-4413-A574-BB1749D8FCAD}.png" style="zoom: 50%;" />

> 模拟Ioc容器工作流程（简易）

```java
package com.wang.spring.annotation;

import com.wang.spring.mybean.ComponentScan;

import org.springframework.stereotype.Component;
import org.springframework.stereotype.Controller;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;

import java.io.File;
import java.net.URL;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

/**
 * @author: 汪邦龙
 * @version: 1.0
 * @date: 2023/8/6 10:20
 * 模拟Ioc容器
 */
public class ApplicationContext {
    //接收传入的class对象
    private Class configClass;

    //ioc容器 ,用于存放反射后创建的对象
    private ConcurrentHashMap<String, Object> ioc = new ConcurrentHashMap<>();


    //构造：用于接收传入的配置类class，得到配置类配置的要扫描的包
    public ApplicationContext(Class configClass) {
        this.configClass = configClass;
        System.out.println("this.configClass=" + configClass);

        //获取要扫描的包
        //1.先得到配置了配置的 @ComponentScan("com.wang.spring.annotation") 注意此处ComponentScan是自定义的
        ComponentScan componentScan =
                (ComponentScan) this.configClass.getDeclaredAnnotation(ComponentScan.class);
        //2.通过componentScan得到value ==>即要扫描的包
        String path = componentScan.value();
        System.out.println("要扫描的包-path=" + path);

        //得到要扫描包下的所有.class文件
        //1.先得到类加载器（只有得到类加载器才能得到out根目录）
        ClassLoader classLoader = ApplicationContext.class.getClassLoader();
        //2.通过类加载器获取到要扫描包的url  注：getResource("") 只能写路径斜杠分隔，不能点分隔
        path = path.replace(".", "/");
        URL resource = classLoader.getResource(path);
        System.out.println("resource=" + resource);
        //3.将要加载的.class 路径下文件进行遍历
        File file = new File(resource.getFile());
        //4.判断是否是目录
        if (file.isDirectory()) {
            File[] files = file.listFiles();
            for (File file1 : files) {
                String absolutePath = file1.getAbsolutePath();
                System.out.println("absolutePath=" + absolutePath);
                //此时获取 C:\Users\admin\...\com\wang\spring\annotation\UserServiceImpl.class


                //需要得到 com.wang.spring.annotation.UserServiceImpl.class
                //1.过滤，只允许.class文件进入
                if (absolutePath.endsWith(".class")) {
                    //2.获取到类名
                    String className =
                            absolutePath.substring(absolutePath.lastIndexOf("\\") + 1, 
                                    absolutePath.indexOf(".class"));
                    System.out.println("className=" + className);
                    //3.获取类全限定名
                    String classFullName = path.replace("/", ".") + "." + className;
                    System.out.println("classFullName=" + classFullName);


                    //判断该 .class文件是不是需要注入到容器 即判断是否有组件注解
                    try {
                        //1.得到该类的class对象
                        Class<?> aClass = Class.forName(classFullName);
                        //2.判断
                        if (aClass.isAnnotationPresent(Component.class) ||
                                aClass.isAnnotationPresent(Controller.class) ||
                                aClass.isAnnotationPresent(Service.class) ||
                                aClass.isAnnotationPresent(Repository.class)) {


                            //可以反射创建对象，放入容器了
                            Class<?> aClass1 = Class.forName(classFullName);
                            Object o = aClass1.newInstance();
                            ioc.put(className, o);
                        }
                    } catch (Exception e) {
                        throw new RuntimeException(e);
                    }
                }
            }
        }
    }

    //输出ioc容器中的数据
    public void getIocHashMap() {
        for (Map.Entry<String, Object> stringObjectEntry : ioc.entrySet()) {
            System.out.println("ioc=" + " k: " + stringObjectEntry.getKey() + " v: " + stringObjectEntry.getValue());
        }
    }
}
```

**测试**

```java
public class test {
    public static void main(String[] args) {
        //传入 SpringConfig 配置类 拿到配置类的class
        ApplicationContext ioc=new ApplicationContext(SpringConfig.class);
        ioc.getIocHashMap();
    }
}
```



# 输出容器所有Bean

```java
	ApplicationContext ioc=new ApplicationContext(SpringConfig.class);	

	String[] beanDefinitionNames = ioc.getBeanDefinitionNames();
		for (String beanDefinitionName : beanDefinitionNames) {
			System.out.println("beanDefinitionName="+beanDefinitionName);
		}
```







# 面向切面AOP

AOP底层支撑----动态代理+反射+动态绑定......

> **导入AOP编程需要的包**

- **com.springsource.net.sf.cglib-2.2.0.jar**
- **com.springsource.org.aopalliance-1.0.0.jar**
- **com.springsource.org.aspsctij.weaver-1.6.8.RELEASE.jar**
- **spring-aspects-5.3.8.jar**

---



## 动态代理【重要】

动态代理解决思想：在调用方法时，使用反射机制，根据方法去决定调用哪个对象方法。

 代理模式是一种设计模式，提供了对目标对象额外的访问方式，即通过代理对象访问目标对象，这样可以在不修改原目标对象的前提下，提供额外的功能操作，扩展目标对象的功能

静态代理： 在编译时就已经实现，编译完成后代理类是一个实际的class文件

动态代理： 在运行时动态生成的，即编译完成后没有实际的class文件，而是在运行时动态生成类字节码，并加载到JVM中

---

**使用JDK动态代理的步骤：**

1. 创建接口，定义目标类要完成的功能（也就是目标接口，你要通过代理执行的目标类）
2. 创建接口的实现类
3. 通过Proxy类的newProxyInstance方法来实例化我们需要的类
4. 创建InvocationHandler接口的实现类，在invoke方法中完成代理类的功能
5. 使用Proxy类的静态方法，创建代理对象

---

> 1.创建接口

```java
/**
 * 接口，该接口有run方法
 */
public interface Vehicle {
    public void run();
}
```

> 2.创建接口的实现类

```java
/**
 * 实现子类
 */
public class Car implements Vehicle{
    @Override
    public void run() {
        System.out.println("这是Car第一句");
        System.out.println("这是Car第二句");
        System.out.println("这是Car第三句");
    }
}
```

> 创建一个返回代理对象的类
>
> 3.通过Proxy类的newProxyInstance方法来实例化我们需要的类
>
> 4,.创建InvocationHandler接口的实现类，在invoke方法中完成代理类的功能

```java
/**
 * 该类可以提供一个方法，返回一个代理对象
 */
public class VehicleProxyProvider {
    //定义一个属性 用于接受传过来的对象
    //target_vehicle 表示真正要执行的对象 要求这个对象的类实现Vehicle接口
    private Vehicle target_vehicle;

    //构造器
    public VehicleProxyProvider(Vehicle target_vehicle) {
        this.target_vehicle = target_vehicle;
    }

    //编写一个方法，返回代理对象
    public Vehicle getProxy() {

        //第一步：得到类加载器
        ClassLoader classLoader = target_vehicle.getClass().getClassLoader();

        //第二步骤：得到将来要代理的对象（被执行的对象）的接口信息
        Class<?>[] interfaces = target_vehicle.getClass().getInterfaces();

        //第三步：创建调用处理器对象 InvocationHandler   反射包下面 java.long.ref
        /*
         * 1.invoke 方法是将来执行我们 target_vehicle的 方法时，会调用到
         * 2.Object proxy 表示代理对象
         * 3.Method method 通过代理对象调用方法时，的哪个方法  代理对象.run()
         * 4.Object[] args 表示在调用方法时（代理对象.run(xxx)） 传入的参数xxx
         * 5.rterun 表示代理对象.run(xxx) 执行后的结果
         * */
        InvocationHandler invocationHandler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println("invoke方法 第一句");
                //这里是反射技术 方法.对象
                Object invoke = method.invoke(target_vehicle, args);
                System.out.println("invoke方法 最末句");
                return invoke;
            }
        };

		//第四步：通过Proxy类的newProxyInstance方法来实例化我们需要的类,并作为方法返回
        /* 
        public static Object newProxyInstance(ClassLoader loader,
                                          Class<?>[] interfaces,
                                          InvocationHandler h)

        1.Proxy.newProxyInstance() 可以返回一个代理对象
        2.ClassLoader loader 类的加载器
        3.Class<?>[] interfaces 将来要代理的对象（被执行的对象）的接口信息
        4.InvocationHandler h 调用处理器对象  有一个非常重要的方法invoke
        */
        Vehicle proxy = (Vehicle) Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);
        
        return proxy;
    }

}
```

> 测试类
>
> 5.使用Proxy类的静态方法，创建代理对象

```java
/**
 * 测试
 */
public class TestVehicle {
    @Test
    public void proxyRun() {
        //创建对象
        Vehicle vehicle = new Car();
        //创建VehicleProxyProvider对象 将要代理的对象 vehicle传入
        VehicleProxyProvider vehicleProxyProvider = new VehicleProxyProvider(vehicle);

        //获取代理对象，该对象可以代理执行方法
        //1.proxy 编译类型Vehicle 运行类型 代理类型（Car）
        Vehicle proxy = vehicleProxyProvider.getProxy();
        proxy.run();
        
    }
}
/** 执行结果
 * invoke方法 第一句
 * 这是Car第一句
 * 这是Car第二句
 * 这是Car第三句
 * invoke方法 最末句
 */
```



## AOP编程

AOP思想：创建一个切面类，切面类的任意方法 可以插入到任意类的任意方法的位置（方法执行前、后、异常、finally），如图：

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230810112104086.png" alt="image-20230810112104086" style="zoom:67%;" />

> - 当我们需要为分散的对象引入公共行为的时候，面向对象则显得无能为力，例如日志、事务功能往往水平的分散在所有对象层次中，在面向对象设计中，它导致了大量代码重复，不利于各个模块的重用。
>
> - AOP将程序中的交叉业务逻辑封装成一个切面，然后注入到目标对象中去。Aop可以对某个对象或某些对象的功能进行增强，使得可以在执行某个方法之前额外做一些事情，执行之后又额外做一些事情。

![image-20230810112343298](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230810112343298.png)

----

**AOP编程说明**

> 1.需要引入核心的aspect包
>
> 2.在切面中声明通知方法
>
> ​	1).前置通知：@Before
>
> ​	2).返回通知：@AfterReturning
>
> ​	3).异常通知：@AfterThrowing       --发生了异常才调用
>
> ​	4).后置通知：@After                        --在finally中执行，也叫最终通知
>
> ​	5).环绕通知：@Around

---

> 接口

```java
/**
 * service接口
 */
public interface SmartAnimalableService {
    public float getSum(float f1, float f2);
    public float getSub(float f1, float f2);

}
```

> 子类

```java
/**
 * @Component 注入到容器
 */
@Component
public class SmartDog implements SmartAnimalableService {
    @Override
    public float getSum(float f1, float f2) {
        System.out.println("SmartDog.getSum = " + (f1 + f2));
        return f1 + f2;
    }
    @Override
    public float getSub(float f1, float f2) {
        System.out.println("SmartDog.getSub = " + (f1 - f2));
        return f1 - f2;
    }
}
```

> 切面

```java
/**
 * 切面类
 * @Component 表注入容器
 * @Aspect 表这是一个切面类
 */
@Aspect
@Component
public class SmartAnimalAspect {

    //前置 方法名字不重要，自己自定义的
    //1. @Before(value ="execution( )") 指定切入到哪个类的哪个方法 格式：访问修饰符 返回类型 全限定名.方法名(参数列表类型)
    //2. JoinPoint joinPoint 在底层执行时，由AspectJ切面框架，会给该切入方法传入一个连接点对象JoinPoint
    @Before(value ="execution(public float com.wang.spring.aop.SmartDog.getSum(float,float ))")
    public void before(JoinPoint joinPoint){
        //通过连接点对象，可以获取方法签名(方法的参数的顺序和类型)
        Signature signature = joinPoint.getSignature();
        //通过方法签名获取数据并输出
        System.out.println("aop-方法执行前-日志-方法名-"+signature.getName() +"参数"+ Arrays.asList(joinPoint.getArgs()));

    }
}
```

> xml

```xml
    <!--配置自动扫描的包,注意需要加入context名称空间 也可以在测试类上添加 @ComponentScan("com.wang.spring.aop ") 代替xml配置-->
    <context:component-scan base-package="com.wang.spring.aop"/>

    <!--开启基于注解的AOP功能 也可以在切面类上添加 @EnableAspectJAutoProxy 代替xml配置 -->
    <aop:aspectj-autoproxy/>
```

> 测试

```java
    @Test
    public void test() {
        ApplicationContext ioc = new ClassPathXmlApplicationContext("beans.xml");
        
        //如果是通过全注解完成的aop，则可以使用以下：
        //ApplicationContext ioc = new AnnotationConfigApplicationContext("com.wang.spring.aop")
        SmartAnimalableService bean = ioc.getBean(SmartAnimalableService.class);

        bean.getSum(2, 3);
    }
```

注意：

- SmartAnimalableService bean = ioc.getBean(SmartAnimalableService.class);  通过接口类型获取注入的对象--就是代理对象
- 切面方法要非静态方法
- @Before(value="execution(*com.hspedu.aop.proxy.SmartDog.*(..))") 切入表达式的更多配置，比如使用模糊配置
- @Before(value="execution(**.*(..))")  表示所有访问权限，所有包的下所有有类的所方法，都会被执行该前置通知方法
-  当 spring 容器开启了<aop:aspectj-autoproxy/>, 我们获取注入的对象, 需要以接口的类型来获取, 因为你注入的对象.getClass() 已经是代理类型 了
-  当 spring 容器开启了 <aop:aspectj-autoproxy/>, 我们获 取注入的对象, 也可以通过id来获取, 但是也要转成接口类型.
- @Before(value="execution(*com.proxy.SmartDog() || com.towproxy.SmartDog())")  配置多个

---



## 切入表达式

切入点表达式，作用：通过表达式的方式定位一个或多个具体的连接点

> 语法格式

```java
execution([权限修饰符] [返回类型] [全类名/简单类名].[方法名]([参数列表]))
```

|   表达式   | execution( * com.wang.spring.aop.SmartDog.*(..))             |
| :--------: | :----------------------------------------------------------- |
|    含义    | SmartDog 接口中声明的所有方法。                                                                                                                                                        第一个”\*"表示任意修饰符及任意返回值。                                                                                                                                                           第二个”\*“表任意方法。                                                                                                                                                                                      ”.."表匹配任意数量、类型的参数。                                                                                                                                                                          若目标类、接口、切面类在同一包，可写简单类名。 |
| **表达式** | **execution(public * com.wang.spring.aop.SmartDog. * (.. ))** |
|    含义    | SmartDog 接口中声明的所有公共方法。                          |
| **表达式** | **execution(* String com.wang.spring.aop.SmartDog. * (.. ))** |
|    含义    | SmartDog 接口中声明的所有返回值为String的方法。              |
| **表达式** | **execution(public String com.wang.spring.aop.SmartDog. * (String, .. ))** |
|    含义    | SmartDog 接口中声明的所有第一个参数为String，返回值为String的公共方法。 |
| **表达式** | **execution(public String com.wang.spring.aop.SmartDog. * (String, String ))** |
|    含义    | SmartDog 接口中声明的所有两个参数都是String，返回值为String的公共方法。 |
| **表达式** | **execution(* * . add (.. ) \|\| * * . sub (.. ) )**         |
|    含义    | 在AspectJ中，切入点表达式可以用”&&“，”\|\|“，”！“等操作符结合                                                                                                  "&&"同时满足多个条件。匹配同时满足条件A和B的切入点：within(com.example..*) && execution(* doSomething(..))          "!"对条件进行取反。匹配不满足条件A的切入点：!within(com.example.util..*) |



## 返回通知获取结果

> 返回通知：即把showSuccessEndLog方法切入到目标方法执行完毕后的地方
>
> 1.如果希望目标方法执行的结果返回给切入方法，可以增加一个属性，比如 returning = "ref" 同时在切入方法增加形参 Object ref

```java
    @AfterReturning(value ="execution(public float com.wang.spring.aop.SmartDog.getSum(float,float ))",
                    returning = "ref")
    public  void showSuccessEndLog(JoinPoint joinPoint,Object ref){
        System.out.println(ref);
    }
```



## 异常通知获取异常信息

> 异常通知：即把 showExceptionLog 方法切入到目标方法执行发生异常的catch{}
>
> 1.如果希望获取异常信息，可以增加一个属性 throwing = "thr" 同时在切入方法增加形参 Exception thr

```java
    @AfterThrowing(value ="execution(public float com.wang.spring.aop.SmartDog.getSum(float,float ))",
                   throwing = "thr")
    public  void showExceptionLog(JoinPoint joinPoint,Exception thr){
        
        System.out.println(thr);
    }
```



## 环绕通知

了解-后续补充

```java
```





## 切入点表达式重用

> 定义一个切入点，在后面使用时可以直接引用，提高复用性

```java
	//定义一个切入点
	@Pointcut(value = "execution(public float com.wang.spring.aop.SmartDog.getSum(float,float ))")
    public void myPointCat(){}

	//使用
    @AfterThrowing(value ="myPointCat()",throwing = "thr")
    public  void showExceptionLog(JoinPoint joinPoint,Exception thr){
        
        System.out.println(thr);
    }
```





## XML配置AOP

java代码和上面AOP编程代码一致,去除注解

主要看xml配置

```xml
    <!--    配置一个切面类对象bean-->
    <bean id="smartAnimalAspect" class="com.wang.spring.aop.SmartAnimalAspect"/>


    <!--    配置为切面类-->
    <aop:config>
        <!--配置统一切入点-->
        <aop:pointcut id="myPointCut" expression="execution(public float com.wang.spring.aop.SmartDog.getSum(float,float))"/>

        <!--指定切面对象 配置前置通知，有返回异常的异常通知
        1.order 当存在多个切面，order属性可以控制切面的执行顺序。order值越小，优先级越高，即该切面会被先执行
        2.method 是切面类的方法
        3.pointcut-ref 表示要插入的切入点
        4.throwing 代表获取异常的返回值 其他通知有其他的写法 将结果返回给 method="showExceptionLog"-->
        <aop:aspect ref="smartAnimalAspect" order="1">
            <!--配置前置通知-->
            <aop:before method="before"  pointcut-ref="myPointCut"/>
            <!--有返回异常的异常通知-->
            <aop:after-throwing method="showExceptionLog" throwing="thr" pointcut-ref="myPointCut"/>
            
        </aop:aspect>
    </aop:config>

```





# JdbcTemplate 操作数据库

当程序员使用Spring框架做项目时，Spring提供了一个操作数据库(表)功能强大的类JdbcTemplate。我们可以提供ioc容器来配置一个JdbcTemplate对象，使得完成对数据库表各种操作。

JdbcTemplate是Spring提供的访问数据库的技术，可以将JDBC的常用操作封装为模板对象

---

## JdbcTemplate 配置环境

> 1.导入 spring-jdbc  、mysql-connector-java 、spring-orm 的Maven依赖

> 2.创建 Spring 配置文件    src/main/resources/jdbc.properties

```properties
jdbc.username=root
jdbc.password=123456
#8以上是 com.mysql.cj.jdbc.Driver 8以下是 com.mysql.jdbc.Driver
jdbc.driver=com.mysql.cj.jdbc.Driver
#高版本有SSL,这里useSSL=false将SSL关闭,serverTimezone=GMT%2B8设置字符集
jdbc.url=jdbc:mysql://localhost:3306/wbldb?serverTimezone=GMT%2B8&useSSL=false
```

> 3.在 src/main/resources/ +包名下创建 JdbcTemplate.xml文件 (本次无java实例，直接resources下创建即可)

```xml
    <!--    引入外部配置文件-->
    <context:property-placeholder location="classpath:jdbc.properties"/>

    <!--    配置数据源对象- dataSource  mysql-connector-java 包下的数据源-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
    </bean>

    <!--   配置jdbcTemplate对象, spring-jdbc包下，用于对数据库操作 -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!--  给jdbc对象配置dataSource属性-->
        <property name="dataSource" ref="dataSource"/>
    </bean>
```

> 4.测试

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");
        
        //获取jdbcTemplate对象，通过 jdbcTemplate 操作数据库
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);
       
        System.out.println(jdbcTemplate);
    }
```



## 通过 jdbcTemplate 添加数据

> 测试

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);
        
        //方式1
        jdbcTemplate.update("INSERT INTO monster VALUES(700, '红孩儿', '喷火')");
        
        //方式二
        String sql="INSERT INTO monster VALUES(?, ?, ?)";
        jdbcTemplate.update(sql,800,"大圣","闹天宫");
    }
```



## 通过 jdbcTemplate 修改数据

> 测试

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        //修改数据
        String sql="UPDATE monster SET name=?,skill=? WHERE id=?";
        jdbcTemplate.update(sql,"八戒","吃东西",600);
    }
```





## 通过 jdbcTemplate 批量处理

> 批量添加数据

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        String sql="INSERT INTO monster VALUES(?, ?, ?)";
        //准备参数
        List<Object[]> objects = new ArrayList<>();
        objects.add(new Object[]{"1001","吴锦","效率"});
        objects.add(new Object[]{"1002","王五","低能"});
        //添加
        jdbcTemplate.batchUpdate(sql,objects);
    }
```



## 查询结果封装为对象/集合

> 对象

```java
public class Monster {
    private Integer monsterId;
    private String monsterName;
    private String monsterSkill;
    
    //省略了get、set、无参有参构造、toString方法
}
```

> 查询结果封装为对象

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        String sql = "SELECT id AS monsterId, name AS monsterName, skill AS monsterSkill FROM monster WHERE id=?";

        //使用 RowMapper 接口来对返回的数据进行一个封装 ==》底层使用的反射-->setter
        RowMapper<Monster> rowMapper = new BeanPropertyRowMapper<>(Monster.class);

        //查询并以对象形式返回
        Monster monster = jdbcTemplate.queryForObject(sql, rowMapper,1001);
        System.out.println(monster);
    }
```

> 查询结果封装为对象集合

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        String sql = "SELECT id AS monsterId, name AS monsterName, skill AS monsterSkill FROM monster WHERE id>?";
        //使用 RowMapper 接口来对返回的数据进行一个封装 ==》底层使用的反射-->setter
       RowMapper<Monster> rowMapper = new BeanPropertyRowMapper<>(Monster.class);
        //查询输出
        List<Monster> query = jdbcTemplate.query(sql, rowMapper,100);
        for (Monster monster : query) {
            System.out.println(monster);
        }
    }
```



## 查询结果返回某一行一列

> 例如只想查询id为100的妖怪的名字

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        //通过 jdbcTemplate 对数据库数据进行操作
        JdbcTemplate jdbcTemplate = ioc.getBean("jdbcTemplate", JdbcTemplate.class);

        //只查询某一行列的数据
        String sql = "SELECT  name  FROM monster WHERE id>?";
        String name = jdbcTemplate.queryForObject(sql, String.class, 1001);

        System.out.println(name);
    }
```





## 具名参数

 使用Map传入具名参数完成操作，比如添加 螃蟹精.   :name 就是具名参数形式需要使 用NamedParameterJdbcTemplate 类

> 1.在xml中增加配置

```xml
    <!--配置 NamedParameterJdbcTemplate 支撑具名参数-->
    <bean id="namedParameterJdbcTemplate" 
          class="org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate">
        <!--  这里需要关联数据源,通过构造器设置-->
        <constructor-arg name="dataSource" ref="dataSource"/>
    </bean>
```

> 2.测试

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        NamedParameterJdbcTemplate namedParameterJdbcTemplate =
                ioc.getBean("namedParameterJdbcTemplate", NamedParameterJdbcTemplate.class);

        String sql="INSERT INTO monster VALUES(:id, :name,:skill)";

        //创建map  k和sql语句的具名参数一致 用于匹配
        HashMap<String, Object> map = new HashMap<>();
        map.put("id",1003);
        map.put("name","吴亦凡");
        map.put("skill","牢饭");
        
        // 添加
        namedParameterJdbcTemplate.update(sql,map);
    }
```



## 封装具名参数

使用 sqlparametersoruce 来封装具名参数

```java
    public static void main(String[] args) throws SQLException {

        ApplicationContext ioc = new
                ClassPathXmlApplicationContext("classpath:com/wang/spring/jdbc/JdbcTemplate.xml");

        NamedParameterJdbcTemplate namedParameterJdbcTemplate =
                ioc.getBean("namedParameterJdbcTemplate", NamedParameterJdbcTemplate.class);

        String sql="INSERT INTO monster VALUES(:id, :name,:skill)";

        //封装具名参数
        Monster monster = newMonster(900, "狐狸精", "狐媚之术"); 
        SqlParameterSource source = new BeanPropertySqlParameterSource(monster); 
        
        // 添加
        namedParameterJdbcTemplate.update(sql, source); 
    }
```











# 事务

后续补充.........













# ############SpringMVC##############

 **Spring MVC 是java Web的实现框架**



- **MVC : 模型(dao,service) 视图(jsp) 控制器(Servlet)**，是一种软件设计规范。（Servlet重点 : **转发，重定向**）

- 是将业务逻辑、数据、显示分离的方法来组织代码。

- MVC主要作用是**降低了视图与业务逻辑间的双向偶合**。

- MVC不是一种设计模式，**MVC是一种架构模式**。当然不同的MVC存在差异。

  ---

  **Model（模型）：**数据模型，提供要展示的数据，因此包含数据和行为，可以认为是领域模型或JavaBean组件（包含数据和行为），不过现在一般都分离开来：Value Object（数据Dao） 和 服务层（行为Service）。也就是模型提供了模型数据查询和模型数据的状态更新等功能，包括数据和业务。

  **View（视图）：**负责进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西。

  **Controller（控制器）：**接收用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。 也就是说控制器做了个调度员的工作。

  ---

  **Controller：控制器**

  > 1. 取得表单数据
  > 2. 调用业务逻辑
  > 3. 转向指定的页面

  **Model：模型**

  > 1. 业务逻辑
  > 2. 保存数据的状态

  **View：视图**

  > 1. 显示页面

# Spring MVC 介绍

Spring MVC只是Spring处理WEB层请求的一个模块/组件，Spring MVC的基石是Servlet。

Spring Boot包含很多组件/框架，Spring就是其核心之一。故也包含Spring MVC。

> Spring Boot  >Spring > Spring MVC

---

> Spring MVC 需要引入Spring Web

```xml
        <!-- Spring Web  SpringMVC必须引入，可以在项目中使用SpringWeb提供的控制器、请求映射、视图解析器等-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>5.3.9</version>
        </dependency>
```

---

> Spring MVC 的控制层使用的注解 -spring Web注解

```java
@Controller
@RequestMapping     //用于映射web请求，包括访问路径和参数。

@GetMapping         //与@RequestMapping效果一样，支持某样http method 更安全

@RequestParam("id")   //url参数

@ResponseBody        //支持将返回值放到response内，而不是一个页面，通常用户返回json数据。


@RequestBody          //允许request的参数在request体中，而不是在直接连接的地址后面。（放在参数前）

@PathVariable          //用于接收路径参数，比如@RequestMapping(“/hello/{name}”)声明的路径，将注解放在参数前，即                          可获取该值，通常作为Restful的接口实现方法。

@RequestParam(value="pageNum",required = false) int pageNum  //非必须传递参数 如果是int必须写为Integer
    
    
@RestController         //所有方法不渲染Thymeleaf页面，而是都返回数据，等同于@Controller加上@ResponseBody
```

---



# Spring MVC 入门



后续补充.........



# ############Mybatis##############

# Mybaits介绍

- MyBatis 是一款优秀的**持久层框架**
- Mybatis就是帮助程序员将数据存入数据库中 , 和从数据库中取数据 .
- MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集的过程
- MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 实体类 【Plain Old Java Objects,普通的 Java对象】映射成数据库中的记录。
- Mybatis官方文档 : http://www.mybatis.org/mybatis-3/zh/index.html

- 持久层 ：完成持久化工作的代码块  ——> dao层 【DAO (Data Access Object) 数据访问对象】

- 视图层：渲染页面   ——>  controller

- 业务逻辑层：——> service







# 创建MyBatis工程配置Mysql

==方法一==：通过网站创建集成MyBayis：https://start.spring.io/

- 添加Spring Web 依赖

- 添加MyBatis Framework 依赖

- 添加MySQL Driver 依赖

  ![网站生成Spring](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/%E7%BD%91%E7%AB%99%E7%94%9F%E6%88%90Spring.PNG)

  

==方法二==：

如果有现有的Spring Boot工程，可以直接在pom里集成

```xml
<!--链接Spring Boot和MyBatis，构建基于Spring Boot的MyBatis应用程序-->
<dependency>
<groupId>org.mybatis.spring.boot</groupId>
<artifactId>mybatis-spring-boot-starter</artifactId>
<version>2.1.2</version>
</dependency>
<!--MySQL提供的JDBC驱动包，用于JDBC连接MySQL数据库-->
<dependency>
<groupId>mysql</groupId>
<artifactId>mysql-connector-java</artifactId>
<scope>runtime</scope>
</dependency>
```



---

 配置Mysql连接：



- 购买云数据库教程 [https://style.youkeda.com/newcoursep4/d1/d1-1/%E9%98%BF%E9%87%8C%E4%BA%91%E8%B4%AD%E4%B9%B0.mp4](https://style.youkeda.com/newcoursep4/d1/d1-1/阿里云购买.mp4)

- 配置数据库教程https://style.youkeda.com/coursevideo/d1/d3fix.mp4

  

- 配置数据源-application.properties

```properties
spring.datasource.url=jdbc:mysql://mysql数据库地址:数据库端口/数据库名称?serverTimezone=GMT%2B8
spring.datasource.username=用户名
spring.datasource.password=密码
	

#serverTimezone=GMT%2B8 用于设置数据库的时区为中国区域，这样查询出来的时间
#和平时时间一致。这是数据源标准写法
#必须要配置数据源，这样项目才知道要连接哪个数据库
#一定要清楚自己购买的数据库地址，端口，用户名，密码


spring.datasource.url=jdbc:mysql://rm-bp13g4yc4o27d44q8oo.mysql.rds.aliyuncs.com:3306/wbldb?serverTimezone=GMT%2B8
spring.datasource.username=gly0601
spring.datasource.password=@Gly0601

#如果是本地mysql
spring.datasource.url=jdbc:mysql://localhost:3306/wbldb?serverTimezone=GMT%2B8
spring.datasource.username=root
spring.datasource.password=123456
```

```properties
#mybatis.mapper-locations 用于指定MyBatis Mapper XML文件路径 一般和DAO包路径一致
#当我们配置好后，系统启动时，MyBatis框架会自动扫描工程下指定路径，并完成路径下所有xml加载
#多个路径可以用逗号隔开 *是所有的意思
#
mybatis.mapper-locations=classpath:com/youkeda/comment/dao/*.xml
```

```properties
#数据源连接池  数据库操作就无需每次都去连接数据库，只是复用连接，从而完成性能提升
spring.datasource.druid.stat-view-servlet.enabled=true    //#是否启用StatViewServlet（监控页面）默认值为false
spring.datasource.druid.stat-view-servlet.url-pattern=/druid/*   
spring.datasource.druid.stat-view-servlet.login-username=druid
spring.datasource.druid.stat-view-servlet.login-password=druid
spring.datasource.druid.stat-view-servlet.allow=
spring.datasource.druid.stat-view-servlet.deny=
```

```properties
#将值为null字段的json过滤掉，使其不输出到网页
spring.jackson.deserialization.fail-on-unknown-properties=false
spring.jackson.default-property-inclusion=non_null
```











# 领域模型及数据库访问接口

==注意 DO类就是日常说的POJO类   DAO层就是日常的Mapper层==

```text
ORM对象的关系映射:

数据库的表（table） --> 类（class）
记录（record，行数据）--> 对象（object）
字段（field）--> 对象的属性（attribute）
```

- DO对象规则

1. 所有的ORM框架都要有一个Java对象来映射数据库的表，并且一一对应，一般把这类对象称为DO对象,对象名称的规范是表名+DO

2. DO对象包规范：xxx.xxx.dataobject 包下

例如：user表对应的Java对象就是userDO 存放在com.youkeda.user.dataobject包下

![](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1679644967490-4d6ccd46-64f2-4aef-b59e-326a807438d3.png)

---

- 数据库访问接口层 Mapper/DAO

1. 在java工程化中，一般把数据层的服务称为DOA层，DAO层会包含对数据库操作的接口和实现类，MyBatis只需要定义接口就可以完成数据的增删改查

2. DOA接口包规范：xxx.xxx.dao 包下

---

==实例：==

- 创建DAO接口

```java
/*创建接口，用于完成增删改查操作 需要@Mapper注解
 @Mapper注解是由Mybatis框架中定义的一个描述数据层接口的注解用于告诉sprigng框架此接口的实现类由Mybatis负责创建，并将其实现类对象存储到spring容器中
*/
@Mapper
public interface UserDAO {

}
```

- 创建控制类用于处理用户请求的web服务

```java
/*完成DAO定义后，Spring启动会自动加载这个接口，这里直接注入接口即可*/
@Controller
public class UserController {
    @Autowired
    private UserDAO userDAO;
   
}
```







# MyBatis注解方式-CRUD

==步骤：==

1. 在DOA中添加接口方法

2. 在控制类使用

---



**插入-INSERT**

```java
/*
插入：通过传入一个DO对象完成插入
INSERT INTO 表名 （表列属性）VALUES（#{DO对象属性}）
#{DO对象变量名}实际是执行了userDO.getUserName()方法来获取UserName值

插入数据要添加@Options主键否则插入不了主键
Options参数：
         useGeneratedKeys  设置为true 代表允许数据库使用自增主键
         keyColumn   设置表的主键字段名称，一般是id
         keyProperty   	设置DO模型的主键字段，一般是id
*/

//DAO中：

@Mapper
public interface UserDAO {
@Insert("INSERT INTO user (user_name, pwd,nick_name,avatar,gmt_created,gmt_modified) VALUES(#{userName}, #{pwd}, #{nickName}, #{avatar},now(),now())")
@Options(useGeneratedKeys = true, keyColumn = "id", keyProperty = "id")
int insert(UserDO userDO);
}


//控制类中：
 @PostMapping("/user")
  @ResponseBody
  public UserDO save(@RequestBody UserDO userDO) {
    userDAO.insert(userDO);
    return userDO;
  }
```

---



**删除-DELETE**

```java
/*
删除：通过传入的主键 通过WHERE条件判断进行删除
*/

//DAO中：
@Mapper
public interface UserDAO {  
@Delete("delete from user where id=#{id}")
int delete(@Param("id") long id);
}


//控制类中：
 @GetMapping("/user/del")
    @ResponseBody
    public boolean delete(@RequestParam("id") Long id) {
        return userDAO.delete(id) > 0; //通过返回值是否大于0判断是否删除成功
    }
```

---



**修改-UPDATE**

```java
/*
修改：通过传入的对象，并使用WHERE条件判断传入对象的id对数据库进行修改
修改必须对修改时间进行修改，且不能对创建时间进行修改
*/

//DAO中：
@Update("update user set nick_name=#{nickName},gmt_modified=now() where id=#{id}")
    int update(UserDO userDO);


//控制类中:
    @PostMapping("/user/update")
    @ResponseBody
    public UserDO update(@RequestBody UserDO userDO) {
        userDAO.update(userDO);
        return userDO;
    }
```

---



**查询SELECT**

- 无参查询

  ```java
  /*
  无参查询：无需传入，直接查询表中数据
  可能返回多对象，使用list 也可以使用指定行返回单个对象
  */
  
  //DAO中：
  @Select("SELECT id,user_name as userName,pwd,nick_name as nickName,avatar,gmt_created as gmtCreated,gmt_modified as gmtModified FROM user")
    List<UserDO> findAll();
  
  
  //控制类中：
    @GetMapping("/users")
    @ResponseBody
    public List<UserDO> getAll() {
      return userDAO.findAll();
    }
  ```

- 有参查询

  ```java
  /*
  有参查询：通过传入的参数，使用WHERE条件语句与数据库数据进行判断，并返回符合的数据
  */
  
  @Select("select id,user_name as userName,pwd,nick_name as nickName,avatar,gmt_created as gmtCreated,gmt_modified as gmtModified  from user  where user_name=#{userName} limit 1")
    UserDO findByUserName(@Param("userName") String name);
  
  
    @GetMapping("/user/findByUserName")
    @ResponseBody
    public UserDO findByUserName(@RequestParam("userName") String userName) {
      return userDAO.findByUserName(userName);
    }
  ```










# MyBatis XML配置

## XML开发顺序

1. 创建DO对象
2. 创建DAO接口，配置@Mapper注解
3. 创建XML文件，完成resultMap配置
4. 创建DAO接口方法
5. 创建对应的XML语句



==注意：XML配置文件要和其对应的Mapper（即DAO）类放一起resources下要用/隔开，不能用点==

一个DOA类对应一个xml文件 xml文件路径存放在resources目录下（没有则自己创建）

例如UserDAO.xml存放在：src/main/resources/com/youkeda/comment/dao/UserDAO.xml

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1681274370239-9a1a03d2-4f5a-4b9e-a0b6-3a1a101a3e79.png)



**XML文件规范-顺序不能错误**

```xml
/*头信息 固定格式*/

/*Mapper根节点   namespace-命名空间 一绑定mapper对应的DAO接口全称*/

/*resultMap在Mapper根节点内  用于处理表和DO对象的属性映射，确保表中每个字段都有属性可以匹配
 id -唯一标示，一般命名规则是xxxResultMap  用于后续SQL方法通过id调用环境
 type -对应的DO类的全限定名
*/

/*resultMap子节点：
id -设置数据库主键字段信息，column属性对应是表的字段名称  property对应DO属性名称
resullt -设置数据库其他字段信息  column属性对应表的字段名称 property对应DO属性名称
*/


<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.youkeda.comment.dao.UserDAO">

<resultMap id="userResultMap" type="com.youkeda.comment.dataobject.UserDO">
    <id column="id" property="id"/>
    <result column="user_name" property="userName"/>
    <result column="pwd" property="pwd"/>
  </resultMap>
</mapper>
```







## 配置解析（补充）

- mybatis-config.xml 系统核心配置文件
- MyBatis 的配置文件包含了会深深影响 MyBatis 行为的设置和属性信息。
- 能配置的内容如下

```xml
configuration（配置）
    properties（属性）
    settings（设置）
    typeAliases（类型别名）
    typeHandlers（类型处理器）
    objectFactory（对象工厂）
    plugins（插件）
    environments（环境配置）
        environment（环境变量）
            transactionManager（事务管理器）
            dataSource（数据源）
    databaseIdProvider（数据库厂商标识）
    mappers（映射器）
<!-- 注意元素节点的顺序！顺序不对会报错 -->
```





### 环境配置（多套数据库时使用）

配置MyBatis的多套运行环境，将SQL映射到多个不同的数据库上，必须指定其中一个为默认运行环境（通过default指定） default指向哪个 id就是在使用哪个环境

子元素节点：**environment**

- 具体的一套环境，通过设置id进行区别，id保证唯一！

  

子元素节点：**数据源（dataSource）**

- dataSource 元素使用标准的 JDBC 数据源接口来配置 JDBC 连接对象的资源。

- 数据源是必须配置的。

- 有三种内建的数据源类型 【`type="[UNPOOLED|POOLED|JNDI]"）`】

  unpooled： 这个数据源的实现只是每次被请求时打开和关闭连接。

  pooled： 这种数据源的实现利用“池”的概念将 JDBC 连接对象组织起来 , 这是一种使得并发 Web 应用快速响应请求的流行处理方式。

  jndi：这个数据源的实现是为了能在如 Spring 或应用服务器这类容器中使用，容器可以集中或在外部配置数据源，然后放置一个 JNDI 上下文的引用

```xml
<environments default="development">
    
  <environment id="development">
      
    <dataSource type="POOLED">
      <property name="driver" value="${driver}"/>
      <property name="url" value="${url}"/>
      <property name="username" value="${username}"/>
      <property name="password" value="${password}"/>
    </dataSource>
      
  </environment> 
</environments>
```



### 属性动态替换

在配置项db.properties中配置Mysql 

```properties
spring.datasource.url=jdbc:mysql://rm-bp13g4yc4o27d44q8oo.mysql.rds.aliyuncs.com:3306/wbldb?serverTimezone=GMT%2B8
spring.datasource.username=gly0601
spring.datasource.password=@Gly0601
```

在xml中引入

```xml
<properties resource="db.properties"/>
```

就可以使`<dataSource>`标签中的`value="${driver}" `获取到值

也可以在内部添加属性配置

```xml
<properties resource="db.properties">
property name="driver" value="Driver"/>
</properties>
```

- 可以直接引入外部文件
- 可以在其中添加一些属性配置
- 如果两个文件有同一字段，优先外部配置文件



### 映射文件(核心配置中注册绑定Mapper XML)

- 映射器 : 定义映射SQL语句文件
- 既然 MyBatis 的行为其他元素已经配置完了，我们现在就要定义 SQL 映射语句了。但是首先我们需要告诉 MyBatis 到哪里去找到这些语句, Java 在自动查找这方面没有提供一个很好的方法，所以最佳的方式是告诉 MyBatis 到哪里去找映射文件

```xml
<!--每一个Mapper.XML都需要在MyBatis核心配置文件中注册!-->
<mappers>
  <mapper resource="com/mybatis/dao/PostMapper.xml"/>
</mappers>
```









### 结果集映射

```xml
<resultMap id="UserMap" type="User">
    <!-- id为主键 -->
    <id column="id" property="id"/>
    <!-- column是数据库表的列名 , property是对应实体类的属性名 -->
    <result column="name" property="name"/>
    <result column="pwd" property="password"/>
</resultMap>


<select id="selectUserById" resultMap="UserMap">
    select id , name , pwd from user where id = #{id}
</select>
```

---

 

**映射子对象**association

按照查询进行嵌套处理就像SQL中的子查询



方案一按照结果进行嵌套处理    就像SQL中的联表查询

- 如果Comment对象里包含一个子对象属性User 其属性名为author
- resultMap的子节点association可以聚合其他模型
- association配置：【property 对应表的字段名         javaType对应java对象】

```xml
<!--
按查询结果嵌套处理
思路：
    1. 直接查询出结果，进行结果集的映射
-->
<resultMap id="commentModelResultMap" type="com.youkeda.comment.model.Comment">
    <id column="id" property="id"/>
    <result column="ref_id" property="refId"/>

    <!--关联对象property 关联对象在Student实体类中的属性-->
    <association property="author" javaType="com.youkeda.comment.model.User">
        <id property="id" column="user_id"/>
        <result column="user_name" property="userName"/>
        <result column="nick_name" property="nickName"/>
        <result column="avatar" property="avatar"/>
    </association>

</resultMap>
```



---



方案二按照查询进行嵌套处理      就像SQL中的子查询

​         给接口添加方法

```java
//获取所有学生及对应老师的信息
public List<Student> getStudents();
```

​        配置sql语句

```xml
    <!--
    需求：获取所有学生及对应老师的信息
    思路：
        1. 获取所有学生的信息
        2. 根据获取的学生信息的老师ID->获取该老师的信息
        3. 思考问题，这样学生的结果集中应该包含老师，该如何处理呢，数据库中我们一般使用关联查询？
            1. 做一个结果集映射：StudentTeacher
            2. StudentTeacher结果集的类型为 Student
            3. 学生中老师的属性为teacher，对应数据库中为tid。
               多个 [1,...）学生关联一个老师=> 一对一，一对多
            4. 查看官网找到：association – 一个复杂类型的关联；使用它来处理关联查询
    --> 
<select id="getStudents" resultMap="StudentTeacher">
      select * from student
    </select>

    <resultMap id="StudentTeacher" type="Student">
        <!--association关联属性  property属性名 javaType属性类型 column在多的一方的表中的列名-->
        <association property="teacher"  column="tid" javaType="Teacher" select="getTeacher"/>
    </resultMap>
    <!--
    这里传递过来的id，只有一个属性的时候，下面可以写任何值
    association中column多参数配置：
        column="{key=value,key=value}"
        其实就是键值对的形式，key是传给下个sql的取值名称，value是片段一中sql查询的字段名。
    -->
    <select id="getTeacher" resultType="teacher">
        select * from teacher where id = #{id}
    </select>
</mapper>
```



---

**映射集合**

方法一按结果进行嵌套查询

```xml
<!--按结果进行嵌套查询-->
<select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid, s.name sname , t.name tname, t.id tid
        from student s,teacher t
        where s.tid = t.id and t.id=#{id}
    </select>

    <resultMap id="TeacherStudent" type="Teacher">
        <result  property="name" column="tname"/>
        
        <!--复杂的属性，我们需要单独的处理 对象：association  集合：collection
         javaType="" 指定属性的类型
         集合中的泛型信息，我们使用ofType获取-->
        <collection property="students" ofType="Student">
            <result property="id" column="sid" />
            <result property="name" column="sname" />
            <result property="tid" column="tid" />
        </collection>
    </resultMap>
```



方法二按照查询嵌套处理

```xml
<select id="getTeacher2" resultMap="TeacherStudent2">
  select * from teacher where id = #{id}
</select>
<resultMap id="TeacherStudent2" type="Teacher">
    <!--column是一对多的外键 , 写的是一的主键的列名-->
    <collection property="students" javaType="ArrayList" ofType="Student" column="id" select="getStudentByTeacherId"/>
</resultMap>
<select id="getStudentByTeacherId" resultType="Student">
    select * from student where tid = #{id}
</select>
```



---

**结果集映射总结**：

- 关联-association 【多对一】

- 集合-collection    【一对多】

- JavaType  &  ofType

  - javaType 用来指定实体类中属性的类型

  - ofType 用来指定映射到list或者集合中的pojo类型，泛型中的约束类型









### 日志Log4j

- Log4j是Apache的一个开源项目
- 通过使用Log4j，我们可以控制日志信息输送的目的地：控制台，文本，GUI组件….
- 我们也可以控制每一条日志的输出格式；
- 通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就是，这些可以通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

**使用步骤**

1. 导入log4j包

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

2. 配置文件编写

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file
#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/kuang.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

3. setting设置日志实现

```xml
<settings>
    <setting name="logImpl" value="LOG4J"/>
</settings>
```

4. 在程序中使用Log4j进行输出！

```java
//注意导包：org.apache.log4j.Logger
static Logger logger = Logger.getLogger(MyTest.class);
    logger.info("info：进入selectUser方法");
    logger.debug("debug：进入selectUser方法");
```











## 日期时间参数处理

使用注解@DateTimeFormat     作用是把字符串转化为日期类型

```java
/*日期时间型参数：*/
  @RequestParam("time")
    @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    LocalDateTime time
```



**实例**

```java
@GetMapping("/user/search")
    @ResponseBody
    public List<UserDO> search(@RequestParam("keyWord") String keyWord,
    @RequestParam("time")
    @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss")
    LocalDateTime time) {
        return userDAO.search(keyWord, time);
    }
```

```java
@DateTimeFormat(pattern="M月d日")
private Date myDate;
```









# MyBatis XML方式CRUD

resultMap   返回一个集合  返回多个

resultType   返回类型  返回一个



**查询-Select**

- select标签是mybatis中最常用的标签之一

- select语句有很多属性可以详细配置每一条SQL语句

  - id

    - 命名空间中唯一的标识符
    - 接口中的方法名与映射文件中的SQL语句ID 一一对应

  - parameterType

    - 传入SQL语句的参数类型 。【万能的Map，可以多尝试使用】

  - resultType

    - SQL语句返回值类型。【完整的类名或者别名】

      

在DAO接口中添加方法

```java
//无参查询
List<UserDO> findAll();

//有参条件查询
UserDO findByUserName(@Param("userName") String name);
```

在XML中添加Select

```xml
<select id="findAll" resultMap="userResultMap">
select * from user
</select>

<select id="findByUserName" resultMap="userResultMap">
select * from user where user_name=#{userName} limit 1
</select>
```

在视图层添加

```java
/*
@RequestParam注解解决前端与后端参数不一致的问题。将请求参数和控制器方法的形参创建映射关系。
*/
@GetMapping("/user/findByUserName")
@ResponseBody
public UserDO findByUserName(@RequestParam("userName") String userName) {
    return userDAO.findByUserName(userName);
}

@GetMapping("/user/findAll")
@ResponseBody
public List<UserDO> findAll() {
    return userDAO.findAll();
}

```



---



**插入-Insert**

在DAO接口中添加方法

```java
@Mapper
public interface UserDAO {
    int add(UserDO userDO);
}
```

在XML中添加Insert

```xml
  <insert id="add" parameterType="com.youkeda.comment.dataobject.UserDO" >
    INSERT INTO user (user_name, pwd, nick_name,avatar,gmt_created,gmt_modified)
    VALUES(#{userName}, #{pwd}, #{nickName}, #{avatar},now(),now())
  </insert>
```

在视图层添加

```java
/* 
当传递过来的是json数据时，需要使用@RequestBody注解接收
*/

@PostMapping("/user")
@ResponseBody
public UserDO save(@RequestBody UserDO userDO) {
    userDAO.add(userDO);
    return userDO;
}
```



---



**修改-Update**

在DAO接口中添加方法

```java
@Mapper
public interface UserDAO {
    int update(UserDO userDO);
}
```

在XML中添加Update

```xml
<update id="update" parameterType="com.youkeda.comment.dataobject.UserDO">
update user set nick_name=#{nickName},gmt_modified=now() where id=#{id}
</update>
```

在视图层添加

```java
@PostMapping("/user/update")
@ResponseBody
public UserDO update(@RequestBody UserDO userDO) {
    userDAO.update(userDO);
    return userDO;
}
```



---



**删除Delete**

在DAO接口中添加方法

```java
/* 
@Param注解的作用是给参数命名，参数命名后就可以通过 #{xxx} 的形式注入sql语句中
*/

@Mapper
public interface UserDAO {
    int delete(@Param("id") long id);
}
```

在XML中添加Delete

```xml
<delete id="delete">
delete from user where id=#{id}
</delete>
```

在视图层添加

```java
@GetMapping("/user/del")
@ResponseBody
public boolean delete(@RequestParam("id") Long id) {
    return userDAO.delete(id) > 0;
}
```



---







## 万能Map方式增删改查

- 假设实体类或者数据库中的表，字段或者参数过多，应当考虑使用Map，Map方式不需要完整的将实体类实现 只要k值和sql语句对应即可

- Map传递参数，直接在SQL中取出key即可 【parameterType="map"】

- 对象传递参数，直接在SQL中取出对象属性即可 【parameterType="Object"】

- 只有一个基本类型参数情况下，可以直接在SQL中取到

  

在DAO接口中添加方法,参数直接传递Map

```java
User selectUserByNP2(Map<String,Object> map);
```

在XML中添加sql语句，需要传递参数类型，参数类型为map

```xml
<select id="selectUserByNP2" parameterType="map" resultType="com.kuang.pojo.User">
  select * from user where name = #{username} and pwd = #{pwd}
</select>
```

在视图层添加, Map的 key 为 sql中取的值即可，没有顺序要求

```java
Map<String, Object> map = new HashMap<String, Object>();
map.put("username","小明");
map.put("pwd","123456");
User user = mapper.selectUserByNP2(map);
```









## 模糊查询 **like**



**方法一**：在Java代码中添加sql通配符

```java
string wildcardname = “%李%”;
list<name> names = mapper.selectlike(wildcardname);
```

```xml
<select id=”selectlike”>
 select * from foo where bar like #{value}
</select>
```



---

**方法二：**在sql语句中拼接通配符，会引起sql注入

```java
string wildcardname = “李”;
list<name> names = mapper.selectlike(wildcardname);
```

```xml
<select id=”selectlike”>
     select * from foo where bar like "%"#{value}"%"
</select>
```









# MyBatis XML 动态SQL

- 什么是动态SQL：**动态SQL指的是根据不同的查询条件 , 生成不同的Sql语句.**
- 我们之前写的 SQL 语句都比较简单，如果有比较复杂的业务，我们需要写复杂的 SQL 语句，往往需要拼接，而拼接 SQL ，稍微不注意，由于引号，空格等缺失可能都会导致错误。
- 那么怎么去解决这个问题呢？这就要使用 mybatis 动态SQL，通过 if, choose, when, otherwise, trim, where, set, foreach等标签，可组合成非常灵活的SQL语句，从而在提高 SQL 语句的准确性的同时，也大大提高了开发人员的效率。

```sql
   - if
    - choose (when, otherwise)
    - trim (where, set)
    - foreach
```



## 条件语句 if-were-set-choose

**if+where语句**

- 如果只使用if标签，title为null时 查询语句为*select* from user where and author=#{author} 这是错误的 SQL 语句所以需要where
- where标签会知道如果它包含的标签中有返回值的话，它就插入一个‘where’ 此外，如果标签返回的内容是以AND 或OR 开头的，则它会剔除掉

```xml
<select id="queryBlogIf" parameterType="map" resultType="blog">
    select * from blog 
    <where>
        <if test="title != null">
            title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```



**set语句**

```xml
<!--注意set是用的逗号隔开-->
<update id="updateBlog" parameterType="map">
    update blog
      <set>
          <if test="title != null">
              title = #{title},
          </if>
          <if test="author != null">
              author = #{author}
          </if>
      </set>
    where id = #{id};
</update>
```



**choose语句**

有时候，我们不想用到所有的查询条件，只想选择其中的一个，查询条件有一个满足即可，使用 choose 标签可以解决此类问题，类似于 Java 的 switch 语句

```xml
<select id="queryBlogChoose" parameterType="map" resultType="blog">
    select * from blog
    <where>
        <choose>
            <when test="title != null">
                 title = #{title}
            </when>
            <when test="author != null">
                and author = #{author}
            </when>
            <otherwise>
                and views = #{views}
            </otherwise>
        </choose>
    </where>
</select>
```







## 循环语句-forEach



创建接口方法

```java
/*DAO 集合方式*/
int batchAdd(@Param("list") List<UserDO> userDOs);
```

编写sql语句

```xml
<!--
collection 指定集合的上下文参数名称，这里的list对应 @param("list")
item  指定遍历中的每一个数据的变量，一般用it命名，后面可以用it.对象变量参数获取具体值
index  集合索引值，从0开始
separator 遍历每条记录并添加分隔符

-->

<insert id="batchAdd" parameterType="java.util.List" useGeneratedKeys="true" keyProperty="id">
    INSERT INTO user (user_name, pwd, nick_name,avatar,gmt_created,gmt_modified)
    VALUES
    <foreach collection="list" item="it" index="index" separator =",">
        (#{it.userName}, #{it.pwd}, #{it.nickName}, #{it.avatar},now(),now())
    </foreach >
</insert>


<!--等同于-->
INSERT INTO user (user_name, pwd, nick_name,avatar,gmt_created,gmt_modified)
    VALUES
    (?, ?, ?,?,now(),now()),
    (?, ?, ?,?,now(),now())
```



批量查询

创建接口方法

```java
/*DAO 集合方式*/
    List<UserDO> findByIds(@Param("ids") List<Long> ids);
```

编写sql语句

```xml
<!--
collection 指定集合的上下文参数名称，这里的list对应 @param("list")
item  指定遍历中的每一个数据的变量，一般用it命名，后面可以用it.对象变量参数获取具体值
index  集合索引值，从0开始

separator 遍历每条记录并添加分隔符 这里是，
open 表示节点开始时自定义的分隔符 这里是（
close 表示节点结束时的分隔符 这里是）
-->
<select id="findByIds" resultMap="userResultMap">
    select * from user
    <where>
        id in
        <foreach item="item" index="index" collection="ids"
                    open="(" separator="," close=")">
            #{item}
        </foreach>
    </where>
</select>


/*等同于*/
select * from user where id in (?,?,?)
```









## >= <== > < &符号解析

在判断时，>=、<、<=、>、>=、& 这类表达式会导致MyBatis解析失败 需要使用<![CDATA[key]]>

```xml
<if test="time != null">
      and  gmt_created <![CDATA[ >= ]]> #{time}
    </if>
```







# MyBatis 分页插件-分页模型

在学习mybatis等持久层框架的时候，会经常对数据进行增删改查操作，使用最多的是对数据库进行查询操作，如果查询大量数据的时候，我们往往使用分页进行查询，也就是每次处理小部分数据，这样对数据库压力就在可控范围内。

**使用分页插件pagehelper**

```xml
<!--pagehelper依赖-->
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.13</version>
</dependency>
```



在企业开发中，都会额外封装一个通用的分页模型Paging用于处理返回值

```java
/* 分页模型 */
public class Paging<R> implements Serializable {

    private static final long serialVersionUID = 522660448543880825L;
    /* 页数 */
    private int pageNum;

    /* 每页数量 */
    private int pageSize = 15;
    /* 总页数*/
    private int totalPage;

    /* 总记录数*/
    private long totalCount;

    /* 集合数据 */
    private List<R> data;

    public Paging() {

    }
        public Paging(int pageNum, int pageSize, int totalPage, long totalCount, List<R> data) {
        this.pageNum = pageNum;
        this.pageSize = pageSize;
        this.totalPage = totalPage;
        this.totalCount = totalCount;
        this.data = data;
    }

    // 省略 getter、setter
}
```



在控制类中实现调用

```java
  @GetMapping("/users")
    @ResponseBody
          public Paging<UserDO> getAll() {
        // 设置当前页数为1，以及每页3条记录
        Page<UserDO> page = PageHelper.startPage(1, 3).doSelectPage(() -> userDAO.findAll());

        return new Paging<>(page.getPageNum(), page.getPageSize(), page.getPages(), page.getTotal(), page
                .getResult());
    }

/*
lambda语法，在doSelectPage lambda方法中执行MyBatis查询方法，就会自动执行分页逻辑，并返回分页对象Page

startPage 第一个参数是指定页数，第二个参数是每页记录数
返回类型Page对象是MyBatis封装的分页模型。可以使用：
getResult（） 获取分页数据
getPages（） 获取总页数
getTotal（） 获取总记录数
get PageNum（） 获取当前页面数
*/
```









# 连接池-数据库连接的性能优化

- Java数据库的操作会面对一个问题，就是性能优化，一般数据源连接池就是最优方案。
- Java连接数据库非常耗时，如果每次查询都重新连接数据库，那样性能低下，换成连接池后，数据库操作就无需每次都去连接数据库，只是复用连接，从而完成性能提升。
- 基于性能考虑，SpringBoot默认集成的连接池是HikaeiCP 无需额外处理，但推荐使用阿里的Druid



**使用步骤**

配置依赖

```xml
<!--Druid依赖-->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.23</version>
</dependency>
```

配置项中开启监控

```properties
spring.datasource.druid.stat-view-servlet.enabled=true    //#是否启用StatViewServlet（监控页面）默认值为false
spring.datasource.druid.stat-view-servlet.url-pattern=/druid/*   
spring.datasource.druid.stat-view-servlet.login-username=druid
spring.datasource.druid.stat-view-servlet.login-password=druid
spring.datasource.druid.stat-view-servlet.allow=
spring.datasource.druid.stat-view-servlet.deny=

#login-username 和 login-password 可以自己定义
```





# 密码不显-通用返回模型泛型-json返回过滤null值

**json返回密码不显示**

```java
/*在实体类上添加jackson注解 API在返回json结果时就不会有这个字段值*/
@JsonSerialize(using = NullSerializer.class)
    private String pwd;
```



---



**泛型**

```java
/* 类名后书写<D>是声明泛型 此时声明的属性D（data）是不确定类型的，在使用其进行实例化对象时，
就可以确定data属性的类型了*/

Result<D> result = new Result<>();
```

通用返回模型

```java
/**
 * JSON 返回模型
 */
public class Result<D> implements Serializable {

    // 表示执行成功或失败
    @JsonProperty("isSuccess")  //自定义JSON输出时的字段名称
    private boolean success = false;

    // 返回消息短码，一般用于出错时，简短描述错误
    private String code;
    // 返回消息具体信息，一般用于出错时，比较详细的描述错误
    private String message;

    // 返回的具体数据
    private D data;

    // 省略 getter、setter

}
```



---



**过滤json空值**：

将值为null字段的json过滤掉，使其不输出到网页

只需要在配置项中添加：

```properties
spring.jackson.deserialization.fail-on-unknown-properties=false
spring.jackson.default-property-inclusion=non_null
```





# 判断非空-密码加密-禁止评论HTML

**判断非空**：

企业中结合commons-lang3库来处理字符串

​        配置commons-lang3依赖

```xml
<!--commons-lang3依赖-->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.10</version>
</dependency>
```

​        使用

```java
StringUtils.isEmpty(str)   //为空返回true
```



---



**密码加密**

​        配置md5依赖

```xml
/*md5算法进行加密 使用commons-codec库进行加密处理*/
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.14</version>
</dependency>
```

​       使用

```java
// 密码加自定义盐值，确保密码安全
String saltPwd = pwd + "_ykd2050";
// 生成md5值，并转为大写字母
String md5Pwd = DigestUtils.md5Hex(saltPwd).toUpperCase();
```



---



**禁止评论内容为html语言**

​        配置commons-text依赖

```xml
<!--依赖-HTML转义commons-text-->
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-text</artifactId>
    <version>1.8</version>
</dependency>
```

​        使用

```java
//转义
String body = StringEscapeUtils.escapeHtml4(content);
```





# DO和Model互转

将转化代码抽象成公共方法放在DO对象里，命名为toModel

 			原代码：每个都要执行一次

```java
// 将 UserDO 对象转化为 User 对象
User user = new User();
user.setId(userDO.getId());
user.setUserName(userDO.getUserName());
user.setNickName(userDO.getNickName());
user.setAvatar(userDO.getAvatar());
user.setGmtCreated(userDO.getGmtCreated());
user.setGmtModified(userDO.getGmtModified());
```

​			现代码：只需要调用，简介

```java
   /**
     * DO 转换为 Model
     *
     * @return
     */
    public User toModel() {
        User user = new User();
        user.setId(getId());
        user.setUserName(getUserName());
        user.setNickName(getNickName());
        user.setAvatar(getAvatar());
        user.setGmtCreated(getGmtCreated());
        user.setGmtModified(getGmtModified());
        return user;
    }

/*调用：*/
User user=userService.toModel();
```





# 本章节表创建的代码

**关于创建第一章，第二章sql表语句**

```sql
CREATE TABLE `user`(
  `id` bigint UNSIGNED AUTO_INCREMENT NOT NULL,
  `title` VARCHAR(20) NOT NULL,
  `pwd` VARCHAR(32) NOT NULL,
	`nick_name` VARCHAR(20)  NULL,
	`avatar` VARCHAR(200) NULL,
  `gmt_created` datetime NOT NULL ,
  `gmt_modified` datetime NOT NULL,

  PRIMARY KEY ( id )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `comment`(
  `id` bigint UNSIGNED AUTO_INCREMENT NOT NULL,
  `ref_id` VARCHAR(32) NOT NULL,
  `user_id` bigint NOT NULL,
	`content` VARCHAR(1000)  NOT NULL,
	`parent_id` bigint NULL,
  `gmt_created` datetime NOT NULL ,
  `gmt_modified` datetime NOT NULL,

  PRIMARY KEY ( id )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO user(user_name,pwd,nick_name,gmt_created,gmt_modified) VALUES('admin','123','管理员',now(),now());
```



# ##############SSM################

后续补充......

```sql
drop table if exists `user`;
drop table if exists `comment`;

CREATE TABLE `user`(
  `id` bigint UNSIGNED AUTO_INCREMENT NOT NULL,
  `user_name` VARCHAR(20) NOT NULL,
  `pwd` VARCHAR(32) NOT NULL,
	`nick_name` VARCHAR(20)  NULL,
	`avatar` VARCHAR(200) NULL,
  `gmt_created` datetime NOT NULL ,
  `gmt_modified` datetime NOT NULL,

  PRIMARY KEY ( id )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `comment`(
  `id` bigint UNSIGNED AUTO_INCREMENT NOT NULL,
  `ref_id` VARCHAR(32) NOT NULL,
  `user_id` bigint NOT NULL,
	`content` VARCHAR(1000)  NOT NULL,
	`parent_id` bigint NULL,
  `gmt_created` datetime NOT NULL ,
  `gmt_modified` datetime NOT NULL,

  PRIMARY KEY ( id )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO user(user_name,pwd,nick_name,gmt_created,gmt_modified) VALUES('admin','123','管理员',now(),now());


INSERT INTO comment(id,ref_id,user_id,content,parent_id,gmt_created,gmt_modified) VALUES(1,'文章ID','111','测试评论',111,now(),now());
```





```properties
spring.datasource.url=jdbc:mysql://rm-cn-nwy3erlst000khdo.rwlb.rds.aliyuncs.com:3306/wbldb?serverTimezone=GMT%2B8
spring.datasource.username=root
spring.datasource.password=Wbl123456
```

```sql
#验证是否登录
sudo docker ps

#进入服务
sudo docker exec -it mysql bash

#登录
mysql -uroot -p000000
```







# ############SpringBoot##############

# Spring Boot介绍

- 去除XML配置 全部采用注解
- 内嵌tomcat
- 快速开发
- 加了@SpringBootApplication的注解的类是启动类，是整个系统的入口

---

Spring Boot比较传统SSM开发，简化整合步骤，提高开发效率。

简化Maven项目的pom.xml依赖导入，直接一键导入 springboot、spring、springmvc、tomcat、json等包

---

- 作用：降低Java Web工程的创建、运行和部署的难度
- Spring Boot的核心还是Spring（所以无需单独管理Maven依赖），只是多了一些工程化方案：

1.  比如说Java Web容器的嵌入集成（有了Spring Boot就不需要再额外部署Tomcat ，Spring Boot默认集成了Tomcat）
2.  SpringBoot自定义了工程打包格式，通过这个直接把一个java Web工程转化为普通的java工程，启动一个mian就可以把Spring工程启动起来
3.  SpringBoot默认集成了你能想到的第三方框架和服务，开发者再也不用关心负载的Maven依赖，开箱即用
4.  SpringBoot还提供了标准的属性配置文件，支持应用的参数动态配置，让代码运行更加灵活
5.  SpringBoot强调开箱即用

---



# Spring Boot开发

> **Spring Boot的包引入 pom.xml**

```xml
<!--SpringBoot父工程 告诉Maven在构建过程中使用指定的SpringBoot Starter Parent作为父项目-->
		<!--创建spring boot项目必须写 注意：不在dependencies标签中 -->
		<parent>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-parent</artifactId>
			<version>3.1.2</version>
			<relativePath/> 
		</parent>

		<!--导入web项目场景启动器：会自动导入和web开发相关的所有依赖[jar/库]-->
		<!--将springboot、spring、springmvc、tomcat、日志、json等都引入 可以点进去看-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
```

> ​	**java程序**

```java
@Controller
public class UserController {

    @GetMapping("login")
    @ResponseBody
    public String login(){
        return "ok";
    }
}
```

> **Spring Boot启动类**

```java
@SpringBootApplication
public class SpringbootApplication {
	public static void main(String[] args) { 
		SpringApplication.run(SpringbootApplication.class, args);
	}
}
```

- 加了@SpringBootApplication的注解的类是启动类，而Spring Boot框架会默认**扫描启动类所在包及其包下子包**进行解析，如果有与启动类所在包平级的其他包，并不会扫描，也不会实例化
- 解决平级包不自动扫描实例化办法：为启动类注解@SpringBootApplication加一个参数，告知系统需要扫描的所有包
- 参数名是scanBasePackages 参数值是字符串数组，用于指定多个包，需要把所有待扫描的包前缀都写入

```java
@SpringBootApplication(scanBasePackages={"fm.douban.app", "fm.douban.service"})
public class SpringbootApplication {
  public static void main(String[] args) {
    SpringApplication.run(SpringbootApplication.class, args);
  }
}
```

> **非Spring Boot启动类**

- 若不是Spring Boot启动类，可以使用独立注解@ComponentScan，作用相同，用于指定多个待扫描包

```java
@ComponentScan({"fm.service", "fm.app"})
public class SpringConfiguration {
  ... ...
}
```







# 依赖管理和自动配置

## 约定优于配置

约定优于配置(ConventionoverConfiguration/COC)，又称按约定编程，是一种软件设计 规范, 本质上是对系统、类库或框架中一些东西假定一个大众化合理的默认值(缺省值)

例如在模型中存在一个名为User的类，那么对应到数据库会存在一个名为user的表， 只有在偏离这个约定时才需要做相关的配置 (例如你想将表名命名为t_user等非user时才 需要写关于这个名字的配置)

简单来说就是假如你所期待的配置与约定的配置一致，那么就可以不做任何配置，约 定不符合期待时, 才需要对约定进行替换配置

约定优于配置理念：约定其实就是一种规范，遵循了规范，那么就存在通用性，存在通用性，那么事情就会变 得相对简单，程序员之间的沟通成本会降低，工作效率会提升，合作也会变得更加简单



## 依赖管理

> 1. spring-boot-starter-parent 还有父项目，声明了开发中常用的依赖的版本号
> 2. 并且进行了自动版本仲裁，即如果程序员没有指定某个依赖的jar版本，则以父项目的版本为准

**自动版本仲裁原理：**

```xml
<!--spring boot 父工程 spring-boot-starter-parent-->
		<parent>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-parent</artifactId>
			<version>3.1.2</version>
			<relativePath/> 
		</parent>

<!--spring-boot-starter-parent 也有父工程，其父工程是spring-boot-dependencies-->
  		<parent>
    		<groupId>org.springframework.boot</groupId>
   			<artifactId>spring-boot-dependencies</artifactId>
   			<version>2.5.3</version>
  		</parent>
<!--在spring-boot-dependencies 中声明了大量的依赖版本号-->
		<properties>
    		<activemq.version>5.16.2</activemq.version>
  			 <antlr2.version>2.7.7</antlr2.version>
    		<appengine-sdk.version>1.9.90</appengine-sdk.version>
			<!--还有很多....-->
 		</properties>
```

**修改自动版本仲裁/默认版本号：**

```xml
		<!--导入web项目场景启动器：会自动导入和web开发相关的所有依赖[jar/库]-->
		<!--将springboot、spring、springmvc、tomcat、日志、json等都引入 可以点进去看-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<!--写法一：我们自己指定mysql驱动版本-->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.17</version>
		</dependency>


	<!--写法二：在dependency标签外指定mysql.version-->
	<properties>
		<mysql.version>5.1.49</mysql.version>
	</properties>
```



## starter场景启动器

开发中我们引入了相关的场景的starter，这个场景中所有的相关依赖都引入进来了，比如我们做web开发引入了，该starter将导入web开发相关的所有包。

1. 在开发中我们经常会用到 spring-boot-starter-xxx ，比如 spring-boot-starter-web，该场 景是用作 web 开发，也就是说 xxx 是某种开发场景
2. 我们只要引入starter，这个场景的所有常规需要的依赖我们都自动引入

---

 **SpringBoot支持的所有场景：**

https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters

![image-20230815170251887](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230815170251887.png)

---

**SpringBoot 也支持第三方 starter**：

1. 第三方starter不要从spring-boot开始，因为这是官方spring-boot保留的命名方式的。 第三方启动程序通常以项目名称开头。
2. 例如，名为thirdpartyproject的第三方启动程序项 目通常被命名为thirdpartyproject-spring-boot-starter
3. 也就是说：xxx-spring-boot-starter是第三方为我们提供的简化开发的场景启动器

---





## 自动配置

> Spring  Boot自动配置了什么？

1.自动配置了Tomcat

```xml
	<!--spring-boot-starter-web 父项目下的配置-->
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.5.3</version>
      <scope>compile</scope>
    </dependency>
```

2.自动配置了SpringMVC

```xml
	<!--spring-boot-starter-web 父项目下的配置-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.3.9</version>
      <scope>compile</scope>
    </dependency>
```

3.自动配置了Web常用功能：如字符过滤器 

```xml
.......
```





## 修改默认配置

> **1.修改默认包扫描路径 ： -该操作在Spring Boot开发中描述过了**



>  **2.resources\application.properties 配置大全**

SpringBoot 项目最重要也是最核心的配置文件就是 application.properties，所有的框架配置都可以在这个配置文件中说明

地址:https://blog.csdn.net/pbrlovejava/article/details/82659702

搜索技巧：ctrl+F 输入关键字  如--若端口相关则输入server.port

> **3.resources\application.properties 修改配置**

 各 种 配 置 都 有 默 认 , 可 以 在 resources\application.properties 修 改 ,  若没有application.properties 文件 我们可以手动创建

```properties
#默认 server.port=8080 
server.port=10000 
#比如:默认 spring.servlet.multipart.max-file-size=1MB
#该属性可以指定springboot上传文件大小的限制
#默认配置最终都是映到某个类上,比如这里配置会映射到 MultipartProperties
#把光标放在该属性， ctrl+b 就可以定位该配置映射到的类 
spring.servlet.multipart.max-file-size=10MB
```

> **4.resources\application.properties 常用配置**

```properties
#端口号
server.port=10000

#应用的上下文路径(项目路径) 类似 @RequestMapping 
server.servlet.context-path=/allModel

#指定 POJO 扫描包来让 mybatis 自动扫描到自定义的 POJO
mybatis.type-aliases-package=com.cxs.allmodel.model

#指定mapper.xml的路径
# (application 上配置了@MapperScan(扫面 mapper 类的路径)和 pom.xml 中放行了 mapper.xml 后，
#配置 mapper-locations 没有意义。如果 mapper 类和 mapper.xml 不在同一个路径下时，mapper-locations 就有用了)
mybatis.mapper-locations=classpath:com/cxs/allmodel/mapper

#session 失效时间(单位 s)
spring.session.timeout=18000



#数据库连接配置
#mysql 数据库 url
mysql.one.jdbc-url=jdbc:mysql://127.0.0.1:3306/test?serverTimezone=Asia/Shanghai&useSSL=false
#mysql 数据库用户名
mysql.one.username=
#数据库密码
mysql.one.password=
#线程池允许的最大连接数
mysql.one.maximum-pool-size=15



#日志打印:日志级别 trace<debug<info<warn<error<fatal 默认级别为 info，即默认打印 info 及其以上级别的日志
#logging.level 设置日志级别，后面跟生效的区域，比如 root 表示整个项目，也可以设置为某个包下，也可以具体到某个类名（日志级别的值不区分大小写）
logging.level.com.cxs.allmodel.=debug
logging.level.com.cxs.allmodel.mapper=debug
logging.level.org.springframework.web=info
logging.level.org.springframework.transaction=info
logging.level.org.apache.ibatis=info
logging.level.org.mybatis=info
logging.level.com.github.pagehelper=info
logging.level.root=info

#日志输出路径
logging.file=/tmp/api/allmodel.log




#配置 pagehelper 分页插件
pagehelper.helperDialect=mysql
pagehelper.reasonable=true
pagehelper.supportMethodsArguments=true
pagehelper.params=count=countSql




#jackson 时间格式化
spring.jackson.serialization.fail-on-empty-beans=false
#指定日期格式，比如 yyyy-MM-ddHH:mm:ss，或者具体的格式化类的全限定名
spring.jackson.date-format=yyyy-MM-ddHH:mm:ss
#指定日期格式化时区，比如 America/Los_Angeles 或者 GMT+10
spring.jackson.time-zone=GMT+8
#设置统一字符集
spring.http.encoding.charset=utf8




#redis 连接配置
#redis 所在主机 ip 地址
spring.redis.host=
#redis 服务器密码
spring.redis.password=
#redis 服务器端口号
spring.redis.port=
#redis 数据库的索引编号(0 到 15)
spring.redis.database=14
## 连接池的最大活动连接数量，使用负值无限制
#spring.redis.pool.max-active=8
#
## 连接池的最大空闲连接数量，使用负值表示无限数量的空闲连接
#spring.redis.pool.max-idle=8
#
## 连接池最大阻塞等待时间，使用负值表示没有限制
#spring.redis.pool.max-wait=-1ms
#
## 最小空闲连接数量，使用正值才有效果
#spring.redis.pool.min-idle=0
#
## 是否启用 SSL 连接.
##spring.redis.ssl=false
#
## 连接超时，毫秒为单位
#spring.redis.timeout=18000ms
#
## 集群模式下，集群最大转发的数量
#spring.redis.cluster.max-redirects=
#
## 集群模式下，逗号分隔的键值对（主机：端口）形式的服务器列表
#spring.redis.cluster.nodes=
#
## 哨兵模式下，Redis 主服务器地址
#spring.redis.sentinel.master=
#
## 哨兵模式下，逗号分隔的键值对（主机：端口）形式的服务器列表
#spring.redis.sentinel.nodes=127.0.0.1:5050,127.0.0.1:5060
```

> **5. resources\application.properties 自定义配置**

还可以在 properties 文件中自定义配置，通过@Value("${}")获取对应属性值

```properties
# application.properties 文件
my.website=https://www.baidu.com
```

```java
//某个Bean
@Value("${my.website}")
private String bdUrl;
```





## 在哪里配置读取配置文件

> **Spring Boot在 ConfigFileApplicationListener 监听器中配置读取配置文件的各种设置**

```java
@Deprecated
public class ConfigFileApplicationListener implements EnvironmentPostProcessor, SmartApplicationListener, Ordered {
    
    //SpringBoot默认搜索配置文件的路径【classpath: 就是src/main/resources】
    private static final String DEFAULT_SEARCH_LOCATIONS = "classpath:/,classpath:/config/,file:./,file:./config/*/,file:./config/";
    
    //配置文件的默认名称
    private static final String DEFAULT_NAMES = "application";
    
  .......
}
```



## 自动配置按需加载原则

**1.自动配置遵守按需加载原则：也就是说，引入了哪个场景 starter 就会加载该场景关联的 jar 包，没有引入的 starter 则不会加载其关联 jar。**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230816145507662.png" alt="image-20230816145507662" style="zoom: 80%;" />

**2.SpringBoot 所 有 的 自 动 配 置 功 能 都 在 spring-boot-autoconfigure 包 里 面。**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230816145613151.png" alt="image-20230816145613151" style="zoom:80%;" />

**3.在 SpringBoot 的 自 动 配 置 包 , 一 般 是 XxxAutoConfiguration.java, 对 应 XxxxProperties.java, 如图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230816145654948.png" alt="image-20230816145654948" style="zoom:67%;" />

---





# Spring Boot容器功能

1. > **@Component、@Controller、 @Service、@Repository 这些在 Spring 中的传统注解仍然有效，通过这些注解可以给容器注入组件**

2. > **Spring Boot提供的注解**

```java
@Configuration      //声明当前类为配置类，相当于xml形式的Spring配置（类上），其中内部组合了@Component注解，表明这个类                       是一个bean（类上）

@Bean                //注解在方法上，声明当前方法的返回值为一个bean，替代xml中的方式（方法上）示把此方法返回的对象实例注                        册成为bean

@ComponentScan       //用于对Component进行扫描，相当于xml中的（类上）

@WishlyConfiguration //为@Configuration与@ComponentScan的组合注解，可以替代这两个注解




```





## 配置类注解@Configuration

**@Configuration 标识一个类为配置类，等价于配置文件，程序员可以通过@Bean 注解注入Bean对象到容器**

> 传统方式如何通过配置文件注入组件

```xml
    <bean class="com.wang.spring.bean.Monster" id="monster01">
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>
```

> **使用SpringBoot的@Configuration配置类添加/注入组件**
>
> 1.@Bean:给 容 器 中 添 加 组 件
>
> 2.monster01(): 默 认 方 法 名 作 为 组 件 的 id
>
> 3.Monster: 返 回 类 型 就 是 组 件 类 型 , 返 回 的 值 就 是 new Monster( "牛魔王","芭蕉扇")  Monster类本身并不需要注册到容器
>
> 4.@Bean("monster_nmw"):重 新 指 定 组 件 的id= “monster_nmw”
>
> 5.配置类里面使用 @Bean 标注在方法上给容器注册组件，默认单例的
>
> 6.@Configuration 配置类本身也会注入到容器中

```java
@Configuration 
public class BeanConfig{
 
    //@Bean("monster_nmw") 
    @Bean 
    public Monster monster01(){
        return new Monster("牛魔王","芭蕉扇"); 
    }
}
```

> **SpringBoot2 新增特性： proxyBeanMethods 指定 Full 模式 和 Lite 模式**
>
> 1.proxyBeanMethods ： 代 理 bean的 方 法 
>
> ​	(1)Full(proxyBeanMethods=true)【 保证每个 @Bean方法被调用多少次返回的组件都是单实例的 ,是代理方式 】 
>
> ​	(2) Lite(proxyBeanMethods = false) 【 每个 @Bean 方法被调用多少次返回的组件都是新创建的 ,是非代理方式 】
>
> 2.特 别 说 明 : proxyBeanMethods是在调用 @Bean方法才生效，因此需要先获取BeanConfig配置类组件，再调用方法而不是直接通过SpringBoot主程序得到的容器来获取bean
>
> 3.如 何 选 择 : 组件依赖必须使用 Full 模式默认； 如果不需要组件依赖使用 Lite模
>
> 4.Lite模也称为轻量级模式 ，因为不检测依赖关系，运行速度快

```java
//配置类
@Configuration(proxyBeanMethods = true)
public class BeanConfig {

    @Bean
    public Monster monster01(){
        return new Monster("牛魔王","芭蕉扇");
    }
}

//测试
@SpringBootApplication
public class SpringbootApplication {
	public static void main(String[] args) {
		ConfigurableApplicationContext run = SpringApplication.run(SpringbootApplication.class, args);
        
        //先获取配置类组件
		BeanConfig bean = run.getBean(BeanConfig.class);
        //通过配置类组件获取bean
		Monster monster = bean.monster01();
		System.out.println(monster);
	}
}
```



## 组件注入注解@Import

通过某一个类的类型，进行组件注入 【可以指定class的数组，可以注入指定类型的Bean】

通过@Import 方式注入的组件，默认组件名字就是对应的类型全类名

```java
@Configuration(proxyBeanMethods = true)
@Import(value = {Monster.class})
public class BeanConfig {

}

```

> **注意：**
>
> 使用`@Import`注解导入的组件是无法直接设置值的，因为`@Import`注解主要是用于导入其他配置类或者组件类，并将它们注册到Spring容器中。
>
> **如果你希望给导入的组件设置值，可以考虑以下几种方法：**
>
> 1. 使用属性注入：
>    - 在导入的组件类中使用`@Value`注解，将需要设置的值通过属性注入的方式进行注入。
>    - 确保导入的组件类上使用了`@Component`或其他合适的注解，以便让Spring能够扫描并管理该组件。
> 2. 继承或实现关系：
>    - 如果导入的组件类具有继承或实现关系，可以通过创建子类或实现类来设置相应的值。
>    - 在子类或实现类中重写相关方法，可以通过方法参数或其他方式传递需要设置的值。
> 3. 使用BeanPostProcessor：
>    - 实现`BeanPostProcessor`接口，并在`postProcessAfterInitialization`方法中对导入的组件进行处理。
>    - 在处理的过程中，可以通过一些逻辑来设置需要的值，并返回修改后的组件对象。





## 条件装配注解@Conditional

条件装配：满足 Conditional 指定的条件，则进行组件注入

Conditional 是一个根注解，下面有很多扩展注解

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230817111905188.png" alt="image-20230817111905188" style="zoom: 80%;" />

> 实例1.要求只有在容器中有 name=monster_nmw 组件时，才注入 dog01

```java
@Configuration
public class BeanConfig {

    @Bean
    public Monster monster01(){
        return new Monster("牛魔王","芭蕉扇");
    }

    //显然不成功，因为容器中没有name = "monster_nmw"的bean
    @Bean
    @ConditionalOnBean(name = "monster_nmw")
    public Dog dog01(){
        return new Dog();
    }
}
```

测试

```java
@SpringBootApplication
public class SpringbootApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext run = SpringApplication.run(SpringbootApplication.class, args);
		Dog bean = run.getBean(Dog.class);

		System.out.println(bean);
    }
}
```

> 实例2.要求只有在容器中没有 name=monster_nmw 组件时，才注入 dog01

```java
@Configuration
public class BeanConfig {

    @Bean(value ="monster_nmw")
    public Monster monster01(){
        return new Monster("牛魔王","芭蕉扇");
    }

    //显然不成功，因为上面已经指定了@Bean(value ="monster_nmw") 所以容器中有name ="monster_nmw"的bean
    @Bean
    @ConditionalOnMissingBean(name ="monster_nmw" )
    public Dog dog01(){
        return new Dog();
    }
}
```

> 实例3.某一类中所有bean注入都要进行条件约束

```java
@Configuration
@ConditionalOnBean(name ="monster_nmw" )
public class BeanConfig {

}
```





## 配置文件引入@ImportResource

作用：原生配置文件引入，也就是可以直接导入Spring传统的bean.xml,可以认为是SpringBoot对Spring容器文件的兼容

场景：将bean.xml文件导入到某个类，获取bean.xml中配置的组件

@ImportResource 可以导数组  @ImportResource(value = {"classpath:bean.xml","classpath:bean2.xml"})

> 实例1：将 beans.xml 导入到 BeanConfig.java 配置类， 并测试是否可以获得 beans.xml 注入/配置的组件

xml配置

```xml
    <bean class="com.wang.springboot.bean.Monster" id="monster01">
        <property name="name" value="悟空"/>
        <property name="skill" value="金箍棒"/>
    </bean>
```

java代码

```java
@Configuration
@ImportResource(value = "classpath:bean.xml")
public class BeanConfig {
    
}
```

测试

```java
@SpringBootApplication
public class SpringbootApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext run = SpringApplication.run(SpringbootApplication.class, args);
		Monster bean = run.getBean(Monster.class);

		System.out.println(bean);
    }
}
```

---



## 配置绑定注解 【重】

@ConfigurationProperties是一个注解，用于标识Java类，表示该类的属性可以从配置文件中读取。它是Spring框架中的一个核心注解之一，用于简化配置文件的读取和管理。

在使用@ConfigurationProperties注解时，需要指定一个prefix参数，表示配置文件中属性的前缀。Spring会根据该前缀，自动将配置文件中以该前缀开头的属性值，绑定到被注解标识的类的对象上

---

**使用java读取到SpringBoot核心配置文件 application.properties  的内容，并把它封装到JavaBean中。**

> 案例：将application.properties 指定的K-V 和JavaBean绑定

**application.properties 配置**

```properties
#设置Monster的属性 K-V
#1.注意中文要转unicode码
#2.前面的 monster01 是前缀，用于区别不同的绑定对象，这样可以在绑定多个monster bean属性时进行区分
monster01.name=\u5b59\u609f\u7a7a
monster01.skill=\u91d1\u7b8d\u68d2
```

**java 类**

```java
@Component
@ConfigurationProperties(prefix = "monster01")   //prefix的值是配置文件中设置的k的前缀
public class Monster {
    private String name;
    private String skill;
    
    //省略一系列get set 构造
}
```

**测试**

```java
@SpringBootApplication
public class SpringbootApplication {

	public static void main(String[] args) {
		ConfigurableApplicationContext run = SpringApplication.run(SpringbootApplication.class, args);
		Monster bean = run.getBean(Monster.class);
		System.out.println(bean);
	
	}
}
```

**也可以通过依赖注入，在网页上显示**

```java
@Controller
public class UserController {

    @Resource
    private Monster monster;

    @GetMapping("getMonster")
    @ResponseBody
    public Monster getMonster(){
        System.out.println("getMonster 被访问");
        return monster;
    }
}
```

注意：使用@ConfigurationProperties(prefix = "monster01") 需要添加依赖

```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-configuration-processor</artifactId>
			<optional>true</optional>
		</dependency>
```

**注意：**

Spring Boot在 ConfigFileApplicationListener 监听器中配置读取配置人家的各种设置中，默认配置文件名就是application

所以若改为其他名称，必须修改默认配置文件名,

例如：在`src/main/resources`目录下创建你想要的配置文件，`myconfig.properties`或`myconfig.yml`。

```properties
#打开application.properties文件，并添加以下配置
spring.config.name=myconfig
```

```yml
#或者在application.yml文件中添加以下配置：
spring:
  config:
    name: myconfig
```







#  Lombok

> **Lombok作用：**
>
> - 简化JavaBean开发，可以使用Lombok的注解使代码更简洁。
> - Java项目中，很多没有技术含量又必须存在的代码：get/set；异常处理；I/O流的关闭操作等等，这些代码既没有技术含量，又影响代码美观，Lombok应运而生。

**Lombok常用注解**

![image-20230818161559894](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230818161559894.png)

---



# Spring Intailizr

> **Spring Intailizr作用：**
>
> - 程序员通过Maven Archetype来生成Maven项目，项目原型相对简陋，需要手动配置，比较灵活。
> - 通过Spring官方提供的Spring Initializr来构建Maven项目，能完美支持Idea和Eclipse，让程序员来选择需要的开发场景(starter),还能自动生成启动类和单元测试代码。

**实例：使用Spring Intailizr 创建SpringBoot项目，并支持web，支持Mybatis**

> 方式一：IDEA

1.新建项目

2.选择Spring Initializr 【如果无本选项，需要安装Spring Initializr 插件】

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230821095015909.png" alt="image-20230821095015909" style="zoom:50%;" />

3.项目设置

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230821095627645.png" alt="image-20230821095627645" style="zoom: 33%;" />

4.选择需要开发的场景

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230821095842391.png" alt="image-20230821095842391" style="zoom:33%;" />

5.点击创建 【至此结束】

---

> 方式二：

1.通过网站创建集成：https://start.spring.io/

2.项目设置【通过ADD Dependencies 添加依赖】

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230821100843801.png" alt="image-20230821100843801" style="zoom: 50%;" />

3.注意事项：

1.如果Spring Initailier的Pom.xml报红

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230821101130422.png" alt="image-20230821101130422" style="zoom:50%;" />

解决方法：指定版本和当前springboot一致，刷新maven即可解决

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230821101245824.png" alt="image-20230821101245824" style="zoom:50%;" />

---







# yaml

1. YAML 以数据作为中心，而不是以标记语言为重点
2. YAML 仍然是一种标记语言，但和传统标记语言不同，是以数据为中心的标记语言。
3. YAML 非常适合用来做以数据为中心的配置文件

注意：读取和 properties 是一样的

---

**基本语法**

1. 形式为Key: Value ； 注意冒号后面有空格
2. 区分大小写
3. 使用缩进表层级关系
4. 缩进不允许使用tab，只允许空格
5. 缩进的空格数不重要，只要相同层级元素左对齐即可
6. 字符串无需加引号
7. 注释使用#

```yaml
monster: 
  id: 100
  name: 牛魔王
```

---

**数据类型**：

1.字面量【字面量：单个的、不可再分的值】。 比如 date、boolean、string、number、null

```yml
monster: 
  id: 100
```

2.对象【对象：键值对的集合】，比如map、hash、set、object

```yml
#行内写法：
k: {k1: v1,k2: v2}

#或
k: 
 k1: v1
 k2: v2
 
 #实例
monster: 
  id: 100
  name: 牛魔王
```

3.数组【数组：一组按次序排列的值】，比如array、list、queue

```yml
#行内写法：
k: [v1,v2]

#或
k: 
 - v1
 - v2
 
#实例
hobby: 
 - 打篮球
 - 踢足球
```

---



# web开发-静态资源访问

1.静态资源放在类路径下：/static、/public、/resources、/META-INF/resources可以直接被访问- 对应文件WebProperties.java

2.常见静态资源：JS、css、图片、字体文件等

3.访问方式：默认-项目根路径/+静态资源名 比如：http：//localhost：8080/hi.html ;  设置-WebMvcProperties.java

注意：【WebProperties.java】【WebMvcProperties.java】 都是Springboot启动时自动注入的bean

```java
//WebProperties.java
@ConfigurationProperties("spring.web")
public class WebProperties {
 	public static class Resources {
        	private static final String[] CLASSPATH_RESOURCE_LOCATIONS = new String[]{
                "classpath:/META-INF/resources/", 
                "classpath:/resources/", 
                "classpath:/static/",
                "classpath:/public/"};
        //.....
	 }
}

//WebMvcProperties.java
@ConfigurationProperties(
    prefix = "spring.mvc")
public class WebMvcProperties {
	public WebMvcProperties() {
    	this.staticPathPattern = "/**";
        //.....
	}
}
```

---

**注意事项：**

静态资源访问原理：静态映射是/**，也就是对所有请求拦截，请求进来，先看Controller能不能处理，不能处理的请求交给静态资源处理器，如果静态资源找不到则404

**改变静态资源访问前缀**【注意只是改变访问前缀】：比如希望http：//localhost：8080/wang/* 去请求静态资源

```properties
#properties
#修改静态资源的访问路径
spring.mvc.static-path-pattern=/wang/**    
#指定静态资源的位置
spring.resources.static-locations=classpath:/wang/


#yml
spring:
  mvc:
  #修改静态资源的访问路径
    static-path-pattern: /wang/**     
  web:
    resources:
    #指定静态资源的位置，数组，可以指定多个
      static-locations: [classpath:/wang/]  
```



# Rest风格请求处理

Rest风格支持（使用HTTP请求方式动词来表示对资源的操作）

GET-  获取;DELETE- 删除 ;PUT-  修改;POST- 保存 ;

```java
@RestController  //本类所有请求都返回json形式
public class MonsterController {

    //等价写法 @RequestMapping(value = "/monster",method = RequestMethod.GET)
    @GetMapping("/monster")
    public String getMonster(){
        return "get获取";
    }

    //等价写法 @RequestMapping(value = "/monster",method = RequestMethod.DELETE)
    @DeleteMapping("/monster")
    public String deleteMonster(){
        return "delete删除";
    }

    //等价写法 @RequestMapping(value = "/monster",method = RequestMethod.PUT)
    @PutMapping("/monster")
    public String putMonster(){
        return "put修改";
    }

    //等价写法 @RequestMapping(value = "/monster",method = RequestMethod.POST)
    @PostMapping("/monster")
    public String postMonster(){
        return "post增加";
    }
    
}
```

---

**Rest风格注意事项**：

> 1.客户端是PostMan 可以直接发送PUT、DELETE等方式的请求，可以不设置Filter。
>
> 2.如果需要Spirngboot支持页面表单的Rest功能，则需要注意如下细节：
>
> ​	 1).HiddenHttpMethodFilter: 浏览器form表单只支持GET和POST请求 而DELTET等methood并不支持
>
> ​	 2).Spring添加了一个过滤器，可以将form不支持的请求转换未
>
>  	2).Rest风格请求核心Filter; 表单请求会被 HiddenHttpMethodFilter 拦截，获取到表单_method的值，再判断是PUT/DELETE
>
> ​	 3).如果需要Spirngboot支持页面表单的Rest功能，需要在application.properties启用filter功能，否则无效

【rest.html  -form提交】

```html
<body>
<h1>测试rest风格url，来完成请求</h1>
<form action="/monster" method="post">
    u:<input type="text" name="name">
    
    <!--通过隐藏域 _method 参数指定值  type="hidden" name="_method" 固定写法-->
    <input type="hidden" name="_method" value="put">
    
    <input type="submit" value="提交">
</form>
</body>
```

【application.properties启用filter功能】

```properties
#启用HiddenHttpMethodFilter 支持Filter
spring.mvc.hiddenmethod.filter.enabled=true
```

【也可以在application.yml中启用filter功能】

```yml
spring:
  mvc:
    hiddenmethod:
      filter:
        enabled: true   #启用HiddenHttpMethodFilter 支持Filter
```

---



# 接收参数相关注解

SpringBoot接收客户端提交数据/参数会使用到相关注解。

```java
@PathVariable
@RequestHeader
@ModelAttribute
@RequestParam
@CookieValue
@RequestBody
```



## @PathVariable

```java
    @GetMapping("/getPathVariable/{name}/{skill}")
    public String getPathVariable(@PathVariable("name") String name,
                                  @PathVariable("skill") String skill) {
        System.out.println(name);
        System.out.println(skill);
        return "get获取";
    }
```

网页输入：http://localhost:8080/getPathVariable/nihao/hehe

控制台打印nihao    hehe

---



## @RequestHeader

指定获取Http请求头信息

```java
    @GetMapping("/getRequestHeader")
    public String getRequestHeader(@RequestHeader("HOST") String host,
                                   @RequestHeader("accept") String accept,
                                   @RequestHeader("User-Agent") String Agent) {
        System.out.println(host);
        System.out.println(accept);
        System.out.println(Agent);
        return "get获取";
    }
```

网页输入：http://localhost:8080/getRequestHeader

控制台打印: localhost:8080 

​					text/html,application/xhtml+xml.......
​							Mozilla/5.0 (Windows NT 10.0; Win64; x64) .....

---





## @RequestParam

获取请求参数

```java
    @GetMapping("/request")
    public String getRequest(@RequestParam("name") String name,
                             @RequestParam("skill") String skill) {
        System.out.println(name);
        System.out.println(skill);
        return "get获取";
    }
```

网页输入：http://localhost:8080/request?name=悟空&skill=金箍棒

控制台打印: 悟空   金箍棒

---





## @CookieValue

获取cookie值

```java
    @GetMapping("/getCookie")
     //读出k为JSESSIONID的v值并保存到jSessionId;
	//required 默认为true 当为false时，接收不到cookie不会报错，返回null
    public String getCookie(@CookieValue(value = "JSESSIONID",required = false) String jSessionId) {
        System.out.println(jSessionId);
        return "get获取";
    }
```

网页输入：http://localhost:8080/getCookie

因为没有session，所以cookie获取不到，又required = false 所以返回null

控制台打印: null 

---



## @RequestBody

获取POST请求体

```java
    @PostMapping("/postMapping")
    public String postMapping(@RequestBody String name) {
        System.out.println(name);
        return "get获取";
    }
```

可以html中测试

```xml
<body>
<h1>测试rest风格url，来完成请求</h1>
<form action="/postMapping" method="post">
    u:<input type="text" name="name">
    <input type="submit" value="提交">
</form>
</body>
```

控制台打印 name=wang

也可以Postman中测试

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230823110920304.png" alt="image-20230823110920304" style="zoom:67%;" />

控制台打印: wang

---



## @ModelAttribute

获取Request域属性 

```java
    @GetMapping("/login")
    public String login(HttpServletRequest request) {
        request.setAttribute("user", "wang");
        System.out.println("login ok!");
        return "forward:/ok";  //请求转发
    }

    @GetMapping("/ok")
    @ResponseBody
    public String ok(@RequestAttribute(value = "user",required = false) String userName){
        System.out.println(userName);
        return "ok!";
    }
```

网页输入：http://localhost:8080/login

控制台打印: login ok!   wang

---





## 复杂参数

1. SpringBoot在响应客户端请求时，也支持复杂参数

2. Map、Model、Errors/BindingResoult、RedirectAttributes、ServletResponse、SessionStatus、UriComponentsBuilder、

   ServletComponentsBuilder、HttpSession

3. Map、Model数据会呗放在request域

4. RedirectAttributes 重定向携带参数

---

```java
    //注册请求
    @GetMapping("/register")
    public String register(Map<String, Object> map,
                           Model model,
                           HttpServletResponse response){

        //将注册数据封装到map或model
        map.put("user","wang");
        model.addAttribute("pwd","123456");

        //创建cookie
        Cookie cookie = new Cookie("JSESSIONID", "hello");
        response.addCookie(cookie);
        return "forward:/registerOk";
    }

    //请求响应
    @GetMapping("/registerOk")
    @ResponseBody
    public String registerOk(HttpServletRequest request){
        Object user = request.getAttribute("user");
        System.out.println(user.toString());
        Object pwd = request.getAttribute("pwd");
        System.out.println(pwd.toString());
        Cookie[] cookies = request.getCookies();
        for (Cookie cookie : cookies) {
            System.out.println(cookie.getName()+"="+cookie.getValue());
        }
        return "ok";
    }
```

网页输入：http://localhost:8080/register

控制台打印：wang     123456    JSESSIONID=hello

---





## 自定义对象参数

1. 在开发中，SpringBoot在响应客户端/浏览器请求时，也支持自定义对象参数
2. 完成自动类型转换与格式化
3. 支持级联封装

---

**实例：将form表单提交的数据封装为monster对象 【自动封装，类型转换】**

form表单 rest.html

```html
<body>
<h1>测试rest风格url，来完成请求</h1>
<form action="/saveMonster" method="post">
    姓名:<input type="text" name="name">
    能力:<input type="text" name="skill">  
    <!--注意，如果monster中有其他对象属性，例如Car car，可以将name=car.name-->
    <input type="submit" value="提交">
</form>
</body>
```

java代码

```java
    @PostMapping("/saveMonster")
    @ResponseBody
    public String saveMonster(Monster monster){
        System.out.println(monster);
        return null;
    }
```

网页输入：http://localhost:8080/rest.html    参数输入 haha   enen

控制台打印：Monster(name=haha, skill=enen)





# 自定义转换器

SpringBoot在响应客户端请求时，将提交的数据封装成对象，使用了内置转换器

SpringBoot支持自定义转换器

SpringBoot提供124个转换器，GenericConverter-ConvertiblePair

---

**实例：给monstr类增加一个属性Car car， 将form表单提交的数据通过 自定义转换器 封装为monster对象**

Monster类、Car类

```java
//Monster
@Data
@Component
public class Monster {
    private String name;
    private String skill;
    private Car car;
}

//Car
@Data
public class Car {
    private String name;
    private Double price;
}
```

HTML网页 rest.html

```html
<body style="text-align: center">
<h1>添加 Monster</h1>
    
<form action="/saveMonster" method="post">
    姓名:<input type="text" name="name" value="悟空"> <br>
    能力:<input type="text" name="skill" value="金箍棒"> <br>
    
    <!--使用自定义转换器关联car， car中属性name和price 使用字符串以逗号隔开并整体提交-->
    坐骑:<input type="text" name="car" value="筋斗云,999.9"> <br>
    
    <input type="submit" value="提交">
</form>
    
</body>
```

Controller控制类

```java
    @PostMapping("/saveMonster")
    @ResponseBody
    public String saveMonster(Monster monster){

        System.out.println(monster);
        return null;
    }
```

配置类 MyWebConfig

```java
@Configuration
public class MyWebConfig {

    //注入Bean WebMvcConfig
    @Bean
    public WebMvcConfigurer webMvcConfigurer() {

        return new WebMvcConfigurer() {
            @Override
            public void addFormatters(FormatterRegistry registry) {
           /**
            * addFormatters() 方法是 WebMvcConfigurer 接口的一个抽象方法。它可以用来注册自定义的格式化程序或转换器
            * FormatterRegistry是一个用于注册格式化程序和转换器的接口。它提供了一些方法来添加和删除格式化程序和转换器。
            * 1.在addFormatters方法中，添加自定义转换器
            * 2.这个自定义转换器的功能是 String转换为Car
            * 3.这个自定义转换器 会注入到 converters 容器中
            * 4.converters底层结构是ConcurrentHashMap
            */
                //创建自定义转换器
                Converter<String, Car> stringCarConverter = new Converter<String, Car>() {
                    @Override
                    public Car convert(String s) {   //s中就是传入的 value="筋斗云,999.9" 字符串数据
                        //这里开始写自定义业务逻辑代码
                        if (!StringUtils.isEmpty(s)) {  //判空
                            String[] split = s.split(",");//字符串分割
                            //写入car
                            Car car = new Car();
                            car.setName(split[0]);
                            car.setPrice(Double.parseDouble(split[1]));//类型转换
                            return car;
                        }
                        return null;
                    }
                };

                //将自定义转换器添加到FormatterRegistry  注意转换器可以创建多个，也可以添加多个
                registry.addConverter(stringCarConverter);
            }
        };
    }
}
```

网页输入：http://localhost:8080/rest.html

控制台打印： Monster(name=悟空, skill=金箍棒, car=Car(name=筋斗云, price=999.9))

---





# 内容协商

根据客户端接收能力的不同，SpringBoot返回不同媒体类型的数据。

比如：客户端Http请求 Accept: application/xml 则返回xml数据；客户端Http请求 Accept: application/json 则返回json数据

---

**实例：客户端Http请求 Accept: application/xml  返回xml数据**

1.因为SpringBoot默认没有处理xml请求的依赖，只有处理JSON的依赖，所以先导入处理xml请求的依赖

```xml
		<!--客户端Http请求 处理xml数据的依赖-->
		<dependency>
			<groupId>com.fasterxml.jackson.dataformat</groupId>
			<artifactId>jackson-dataformat-xml</artifactId>
		</dependency>
```

2.利用Postman工具去请求 并设置Accept: application/xml  【网页直接打开也可以，添加xml依赖后，网页直接返回xml类型】

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230823165428904.png" alt="image-20230823165428904" style="zoom: 65%;" />

> **注意：**
>
> text/html, application/xhtml+xml, application/xml;q=0.9
>
> image/avif, image/webp, image/apng, \*/*;q=0.8
>
> application/signed-exchange; v=b3; q=0.7
>
> 即：application/xml 的权重为0.9；而application/json (\*/*) 权重0.8； 故**当有xml依赖的时候，返回的就是xml格式**

---

**如果需要后端处理机既可以处理xml，又可以处理json【即自定义指定其返回什么类型】**

1. Postman可以通过修改Accept的值，来返回不同类型的数据格式。
2. 对于浏览器，我们无法修改Accept，若想返回不同类型的数据格式，解决方案是开启支持基于请求参数的内容协商功能

```properties
#开启基于请求参数的内容协商功能
spring.mvc.contentnegotiation.favor-parameter=true

#指定一个内容协商的参数名 不指定，则默认为format
# spring.mvc.contentnegotiation.parameter-name=wang
```

 在网页url上添加 ?format=json 可以转换为json格式，?format=xml 可以转换为xml格式。

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230824103439776.png" alt="image-20230824103439776" style="zoom: 80%;" />

---



# 日志Logger

在Spring这种比较复杂的系统中，普通输出sout打印的内容会输出到什么地方，是不确定的。所以在企业项目中，都是使用日志系统来记录信息

---

**日志系统的两大优势:**

1. 日志系统可以轻松的控制日志是否输出。例如淘宝这样超大型的网站，在开发阶段需要打印出调试信息，但是发布到正式环境就不能打印了，因为每天几十几百亿的访问量，大量调试信息到导致磁盘撑爆。这时候就需要控制日志的输出，而不是修改所有的代码。
2. 日志系统可以灵活的配置日志的细节，例如输出格式，通常在日志输出时，需要自动附带输出日志发生的时间、打印日志的类名等信息，这样能很方便的观察日志分析问题。

---

**使用日志系统的两大步骤：**

1. 配置 --修改 application.properties 增加日志级别配置：

```java
logging.level.root=info //表示所有日志（root）都为info级别 写法需紧凑，不留空格
    
/*
日志级别：
优先级： 级别：       含义：                           使用类型            作用
最高    ERROR      错误信息日志                          错误       不输出更低优先级的日志
高      WARN       暂时不出错但高风险的警告信息日志        警告       只输出定义的级别及更高
中      INFO       一般的提示语、普通数据等不重要信息日志   一般       级别的日志
低      DEBUG      进行开发阶段需要关注的调试信息日志       调试
*/
/*在开发阶段配置为DEBUG 在项目发布时调整为INFO，即可以做到不改代码而控制日志*/
```

​	2.编码 --配置完成后，编码很简单，只需要实例化日志对象即可打印

```java
@RestController
public class SongListControl {
    private static final Logger LOG = LoggerFactory.getLogger(SongListControl.class);
    @PostConstruct
    public void init(){
        LOG.info("SongListControl 启动啦");
    }
}

/*先定义一个类变量LOG，然后调用LOG的方法，在方法参数中输入日志内容
注意：LOG的方法名和日志级别一一对应  不输出更低级别日志，只输出本身和更高级日志
*/
```

**日志打印列表**

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MyClass {
    private static final Logger log = LoggerFactory.getLogger(MyClass.class);

    public static void main(String[] args) {
        List<String> list = Arrays.asList("Item 1", "Item 2", "Item 3");
        log.info("List: {}", list);
    }
}
/*在以上示例中，使用了占位符 {}，并将列表对象 list 作为参数传递给 log.info 方法。日志库会自动将列表转换为字符串，并将其打印到日志中。*/
```









# Thymeleaf

1. Thymeleaf是模板引擎，可完全替代JSP。
2. Thymeleaf是一个java类库，是一个xml/xhtml/html5的模板引擎，可以作为mvc的web应用的view层。

---

**优点：**

1. 实现了JSTL、OGNL表达式效果；
2. Thymeleaf模板页面无需服务器渲染，也可以被浏览器运行，页面简洁；
3. SpringBoot支持FreeMarker、Thymeleaf、veocity。

**缺点：**

1. 并不是一个高性能的引擎，适用于单体应用
2. 如果要做一个高并发应用，选择前后端分离更好，也就是vue+ElementPlus+Axios+SpringBoot。

---

**Thymeleaf机制：**

Thymeleaf是服务器渲染技术，页面数据是在服务端进行渲染的。

比如：manage.html中有一段Thymeleaf代码，不管是请求转发，还是重定向，在用户请求该页面时，由Thymeleaf模板引擎在服务器端完成处理，并将结果返回。

因此，使用Thymeleaf，并不是前后端分离。

---

**Thymeleaf注意事项：**

1. 若要使用Thymeleaf语法，首先需要声明名称空间： xmlns:th="http://www.thymeleaf.org"
2. 设置文本内容用 th：text ；设置input值用 th:value；循环输出用 th：each；条件判断用 th：if ；插入代码块用 th：insert ；         定义代码块用 th：fragment ；声明变量用 th：object；
3. th：each用法需要注意，如果你要循环一个div中的p标签，则th：each必须放在p标签上，如果放在div上，则循环的是整个div。
4. 变量表达式中提供了很多内置方法，该内置方法是用#开头，不要与消息表达式#{}弄混。

---

**Thymeleaf依赖**

```xml
<!--Thymeleaf依赖  引入后项目会自动完成配置，程序员按规则开发就可以了-->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

---

**Thymeleaf模板相关属性【默认的位置和后缀】**

```java
@ConfigurationProperties(
    prefix = "spring.thymeleaf"
)
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    //...
}
```

---







## 数据传递-运算符

> **数据传递Model**
>
> - Spring MVC把页面数据层封装的非常完善，只需要在方法参数里引入一个Model对象，就可以通过Model对象传递数据到页面
> - 导入：import org.springframework.ui.Model;
>

```java
//实例
@Controller
public class SongListControl {
  @Autowired
  private SongListService songListService;
  @RequestMapping("/songlist")
  public String index(@RequestParam("id")String id,Model model){
    SongList songList = songListService.get(id);
    //传递歌单对象到模板当中
    //第一个 songList 是模板中使用的变量名
    // 第二个 songList 是当前的对象实例
    model.addAttribute("songList",songList);
    return "songList";
  }
}
```

> **模板文件**:
>
> Spring MVC对于模板文件有**固定的存放位置**，放置在工程的**src/main/resources/templates**中,所以上面的 return "songList"; 其实会去查找 src/main/resources/templates/songList.html文件，系统会自动去匹配后缀的，所以不需要写成return "songList.html";
>

```html
<!--Thymeleaf模板文件是以html为文件格式
xmlns:th="http://www.thymeleaf.org"作用是让软件识别Thymeleaf语法 -->
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="/css/songList.css" />
    <title>豆瓣歌单</title>
  </head>
  <body>
    <h1 th:text="${songList.name}"></h1>
  </body>
</html>
```

---

> **Thymeleaf运算符**

**数学运算：**

\+  ， -  ，*  ，/  ，%

---

**布尔运算：**

and ，or

一元运算：！ ，not

---

**比较运算：**

比较：> , < , >= ,<=  ( gt , lt , ge , le )

等式： == ， ！=  （eq ，ne）

---

**条件运算：**

if-then: ( if ) ? ( then )

if-then-else: ( if )? ( then ) : (else)

defualt: ( value ) ? : ( defaultvalue )

---





## 表达式-数据转化-字符串处理-url插入

**表达式：**

| 表达式名   | 语法   | 用途                                |
| ---------- | ------ | ----------------------------------- |
| 变量取值   | ${...} | 获取请求域、session域、对象等值     |
| 选择变量   | *{...} | 获取上下文对象值                    |
| 消息       | #{...} | 获取国际化等值                      |
| 链接       | @{...} | 生成链接                            |
| 片段表达式 | ~{...} | jsp：include 作用，引入公共页面片段 |

---

**字面量:**

文本值：‘wang’ .....;   数字： 1 ...    ; 布尔值：true false；

空值：null；

变量：name .....; 变量不能有空格

---

**文本操作：**

字符串拼接： +

变量替换：|age=${age}|

```java
//设置模板上下文
@RequestMapping("/demo")
  public String index(Model model){
    String totalTime = "45:00";
    model.addAttribute("totalTime",totalTime);
    return "demo";
  }

```

```html
<!--第一种拼接：-->
<span th:text="'00:00/'+${totalTime}"></span>  //00:00/45:00

<!--第二种拼接：-->
<span th:text="|00:00/${totalTime}|"></span>   //00:00/45:00
```

---

**数据转化一：日期时间**

Thymeleaf默认集成大量的工具类可以进行数据转化，一般使用dates

工具类使用语法是  #{工具类}

- 处理LocalDate和LocalDateTime类需要的依赖

```xml
<!-- spring thymeleaf 支持 这个库会自动添加一个工具类 temporals-->
<dependency>
  <groupId>org.thymeleaf.extras</groupId>
  <artifactId>thymeleaf-extras-java8time</artifactId>
  <version>3.0.4.RELEASE</version>
</dependency>
```

- dates / temporals 日期到字符串的转化
  - dates支持Date类
  - temporals支持LocalDate和LocalDateTime类

```java
//模板上下文
  @RequestMapping("/demo")
  public String index(Model model){
    Date dateVar = new Date();
    model.addAttribute("dateVar",dateVar);
    return "demo";
  }
```

```html
<p th:text="${#dates.format(dateVar, 'yyyy-MM-dd HH:mm:ss')}"></p>
    
<p th:text="${#temporals.format(dateVar, 'yyyy年MM月dd日 ')}"></p>
```

---

**strings 字符串处理**

```java
${#strings.toUpperCase(name)} //字符串全大

${#strings.toLowerCase(name)}  //字符串全小

${#strings.arrayJoin(array,',')},//将字符数组合并为字符串，并逗号隔开例如： ["a","b"] =》 a,b

${#strings.arraySplit(str,',')}, //将字符串分割为数组，并逗号隔开  例如a,b =》["a","b"]

${#strings.trim(str)} //去字符串空格（左右）

${#strings.length(str)} //获得字符串长度

${#strings.equals(str1,str2)}  //比较是否全等

${#strings.equalsIgnoreCase(str1,str2)} //忽略大小写比较相等
```

**插入url th:src**

```html
<img th:src="@{${url}}">
```

---





## 模板变量-循环-行数显示

> 由于Thymeleaf完全兼容HTML，所以为了不破坏HTML结构，Thymeleaf采用自定义HTML属性生成动态内容

![image-20230824123813881](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230824123813881.png)

---

> **模板变量 th：text**    【th:text 语法作用就是动态的替换掉html标签内容】

**控制类：**第一步：设置变量到模板上下文 model.addAttribute("msg",str);

```java
@Controller
public class DemoControl {
  @RequestMapping("/demo")
  public String index(Model model){
    String str = "你好";
    model.addAttribute("msg",str);
    return "demo";
  }
}
```

**模板**   第二步：在模板中调用

```html
<span th:text="${msg}"></span> //打印出你好

<!--如果是对象变量则通过 . 来获取对象成员变量（不是getset方法）-->
<span th:text="${sl.id}"></span>
```

---



**循环语句 th：each**

```html
<ul th:each="song : ${songs}">
  <li th:text="${song.name}">歌曲名称</li>
</ul>
```

**行数显示（列表索引值）th：each另一种写法**

```html
<ul th:each="song,it: ${songs}">
  <li>
    <span th:text="${it.count}"></span>
    <span th:text="${song.name}"></span>
  </li>
</ul>


<!--
it是作为可选参数出行
it.index   从0开始显示行数


it.count   从1开始显示行数

it.size    被迭代对象大小（列表长度

it.current 当前迭代变量，等同于song

it.even/odd  布尔值，当前循环是否是偶数/奇数（从0开始）

it.first  布尔值，当前循环是否第一个

it.last    布尔值，当前循环是否最后一个

-->
```





## 内联表达-条件语句-字符串逻辑判断

**内联表达**

==注意：只有 th:text 可以用[[]]表示==

```html
<!--原始表达：-->
<span th:text="${msg}"></span>

<!--内联表达  -->
<span> [[${msg}]]</span>

```



---

**条件语句 th：if th:unless**

默认如下表达为ture：
1.值非空
2.值非零数字
3.值是字符串，但不是false、off、no
4.值不是布尔值、数字、character或字符串

```html
<!-- th:if 表达式的值是ture情况下就会执行渲染 -->
<span th:if="${user.sex == 'male'}">男</span> //若ture，则显示男

<!-- th:unless 表达式的值是false 情况下才进行渲染 -->
<span th:unless="${user.sex == 'male'}">女</span> //若false，则显示女  【on lai s】
```



---

**逻辑判断 #strings**

```java
${#strings.isEmpty(name)}  //检查字符串是否为空（null），在检查之前会先执行trim()操作,trim是去左右空格

${#strings.arrayIsEmpty(name)}//检查数组是否为空（null）...

${#strings.listIsEmpty(name)} //检查集合是否为空（null）...


${#strings.contains(name,'abc')} //检查字符串变量是否包含片段
    
${#strings.containsIgnoreCase(name,'abc')} //忽略大小写，判断是否包含

${#strings.startsWith(name,'abc')}    //判断字符串是否以abc开头

${#strings.endsWith(name,'abc')} //判断字符串是否以abc结束

```





## 表单-数据效验注解-布局Layout

> th:object="${user}" 用于替换对象 使用了就不需要每次编写xxx.name 直接name
>

**form表单提交格式**

```html
<!--结合数据效验使用，遇到错误会渲染--> 

<form action="/user/save" th:object="${user}" method="POST">
        <div th:classappend="${#fields.hasErrors('name')} ? 'error' : ''">   <!--输入框变色-->
            <label>用户名称:</label>
            <input type="text" th:field="*{name}">  <!--存留输入信息-->
            <p th:if="${#fields.hasErrors('name')}" th:errors="*{name}"></p>   <!--报错-->
        </div>
        <div>
            <button type="submit">保存</button>
        </div>
    </form>
```

控制类

```java
@Controller
public class BookControl {
  //缓存所有书籍数据
  private static List<Book> books = new ArrayList<>();

  @GetMapping("/book/add.html")
  public String addBookHtml(Model model){
    return "addBook";
  }
  @PostMapping("/book/save")
  public String saveBook(Book book){
    books.add(book);
    return "saveBookSuccess";
  }
```

---

**数据效验**

 配置Validation注解依赖

```xml
<!--Validation注解依赖-->
<dependency>
  <groupId>jakarta.validation</groupId>
  <artifactId>jakarta.validation-api</artifactId>
  <version>2.0.1</version>
</dependency>
<!--控制渲染-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

Validation注解

```java
@NotNull  //不允许为null对象

@AssertTrue  //是否为ture

@Size   //约定字符串长度

@Min  //字符串最小长度

@Max   //字符串最大长度

@Email  //是否是邮箱格式

@NotEmpty  //不允许为空和null，可判断字符串、集合

@NotBlank  //不允许为null和空格
```

**数据效验实例**

​            pojo类中： 效验注解需写在pojo类中

```java
    @NotEmpty(message = "名称不能为 null")
    private String name;

    @Min(value = 18, message = "你的年龄必须大于等于18岁")
    @Max(value = 150, message = "你的年龄必须小于等于150岁")
    private int age;

    @NotEmpty(message = "邮箱必须输入")
    @Email(message = "邮箱不正确")
    private String email;
```

​        控制类中：

```java
/*控制类中对效验注解进行分析
BindingResult errors 接收注解message的值（如果错误就产生message）
若无错则errors.hasErrors()==0
*/
    @PostMapping("/user/save")
    public String saveUser(@Valid User user, BindingResult errors) {
        if (errors.hasErrors()) {
            // 如果校验不通过，返回用户编辑页面
            return "user/addUser";   //页面产生报错
        }
        // 校验通过，返回成功页面
        return "user/addUserSuccess";
    }
```



---

**布局Layout**

layout解决模板复用问题，推荐使用 `th:include` + `th:replace` 方案完成布局开发

```html
<!--::content指的是选择器，这个选择器指的是加载当前页面th:fragment的值
当页面渲染的时候，布局会合并content这个fragment内容一起渲染 -->
th:include="::content"
```

**实例**：

​			layout.html模板- th：include

```html
!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>布局</title>
    <style>
        .header {background-color: #f5f5f5;padding: 20px;}
        .header a {padding: 0 20px;}
        .container {padding: 20px;margin:20px auto;}
        .footer {height: 40px;background-color: #f5f5f5;border-top: 1px solid #ddd;padding: 20px;}
    </style>
</head>
<body>
<header class="header">
    <div>
        <a href="/book/list.html">图书管理</a>
        <a href="/user/list.html">用户管理</a>
    </div>
</header>
<div class="container" th:include="::content">页面正文内容</div>
<footer class="footer">
    <div>
        <p style="float: left">&copy; youkeda.com 2017</p>
        <p style="float: right">
            Powered by 优课达
        </p>
    </div>
</footer>
</body>
```

​			th:fragment fragment（片段）

```html
/*
  th:replace="layout" 指定布局的名称，一旦声明，页面会被替换成layout的内容
  th:fragment="content" 当页面渲染时，可以通过选择器指定使用这个片段，上面th:include="::content"指定的就是这个值
*/ 
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org"
      th:replace="layout">
<div th:fragment="content">
    <h2>用户列表</h2>
    <div>
        <a href="/user/add.html">添加用户</a>
    </div>
</div>

</html>
```

---



## Springboot+Thymeleaf登录注册





# Spring Session

![image.png](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1679017538907-361dc178-672b-4246-90b9-a48ad422546c.png)

- Cookie是客户端会话技术，Session是服务器端会话技术
- 从客户端连接到服务器开始，一直到客户端关闭的整个过程，就是一次会话范围
- 会话只属于一个用户的，不能多用户共享，一次会话中可以包含多次请求
- **Cookie是服务器存放在浏览器的一小份数据**，浏览器每次访问该服务器的时候都会将这小份数据携带到服务器
- 一般使用Cookie来记住用户登录的用户名，下一次登录时，用户名自动填充到输入框中；也可以用来保存电影的播放进度。

---



## cookie-读写

服务端既要返回cookie给客户端，也要读取客户端提交的cookie

Cookie属性值作用：https://ham.youkeda.com/articles/detail/5f37597b5e205f30b2c2b32f

> **从Cookie中取出数据**

**法一：通过HttpServletRequest**

1、读方法添加一个参数HttpServletRequest 系统会自动传入方法参数需要的HttpServletRequest对象
        2、通过request.getCookies() 取得cookie数组，再循环遍历

```java
@RequestMapping("/songlist")  //解析url请求的路径，默认支持所有http method
public Map index(HttpServletRequest request) {
  Map returnData = new HashMap();
  Cookie[] cookies = request.getCookies();  //获取cookie对象数组（cookie以键值对存储）
  returnData.put("cookies", cookies);   //存入所有cookie
  return returnData;
}
```

---

**法二：注解方式**

前提：需要知道cookie的名字（即key）

优势：通过注解方式读取，不需要再遍历数组

```java
/* 为该方法添加  @CookieValue("xxxx") String xxxx  参数即可 需要填入正确的cookie名字，否则该注解报错
 cookie名字和写入的cookie名字成对
*/
@RequestMapping("/songlist")
public Map index(@CookieValue("JSESSIONID") String jSessionId) { //读出k为JSESSIONID的v值并保存到jSessionId
  Map returnData = new HashMap();
  returnData.put("JSESSIONID", jSessionId);
  return returnData;
}
```

---

> **写入cookie数据**

1、为写方法添加一个 HttpServletResponse 参数，系统会自动传入方法参数所需的 HttpServletResponse对象
​		2、创建cookie对象，并进行赋值
​		3、调用 response.addCookie() 方法添加cookie即可

```java
@RequestMapping("/songlist")
public Map index(HttpServletResponse response) {
  Map returnData = new HashMap();

 //初始化cookie对象 第一个参数是名称，第二个参数是对应的值
  Cookie cookie = new Cookie("sessionId","CookieTestInfo");
  // 设置的是 cookie 的域名，就是会在哪个域名下生成 cookie 值
  cookie.setDomain("youkeda.com");
  // 是 cookie 的路径，一般就是写到 / ，不会写其他路径的
  cookie.setPath("/");
  // 设置cookie 的最大存活时间，-1 代表随浏览器的有效期，也就是浏览器关闭掉，这个 cookie 就失效了。
  cookie.setMaxAge(-1);
  // 设置是否只能服务器修改，浏览器端不能修改，安全有保障
  cookie.setHttpOnly(false);

//写入cookie
  response.addCookie(cookie);

  returnData.put("message", "add cookie successful");
  return returnData;
}
```





## SessionAPI-读写

- 解决将用户id、状态等重要信息放入cookie 的安全隐患。Session绘画机制将重要信息放在服务端，避免安全隐患。
- 使用会话机制时，cookie会作为sessionid的载体与客户端连接
- 名字为JSESSIONID的cookie是专门用来记录session的，是标准通用的名字

---

> **登录信息类**

1、登录信息实例对象因为要在网络上传输，必须实现 序列化接口 Serializable   若不实现则报错
​		2、根据需要设计属性，需要get set

```java
public class UserLoginInfo implements Serializable {
  private String userId;
  private String userName;
}
```

> **写session操作**

1、为方法添加一个参数 HttpServletRequest
​		2、使用 request.getSession() 返回一个对象 从中取得HttpSession对象
​		3、使用 session.setAttribute() 写入session登录信息

```java
@RequestMapping("/loginmock")
public Map loginMock(HttpServletRequest request, HttpServletResponse response) {
  Map returnData = new HashMap();

  // 假设对比用户名和密码成功 实际程序需要通过
    
  // 仅演示的登录信息对象
  UserLoginInfo userLoginInfo = new UserLoginInfo();
  userLoginInfo.setUserId("12334445576788");
  userLoginInfo.setUserName("ZhangSan");
    
  // 取得 HttpSession 对象
  HttpSession session = request.getSession();
    
  // 写入登录信息
  session.setAttribute("userLoginInfo", userLoginInfo);
  returnData.put("message", "login successful");

  return returnData;
}
```

> **读session操作**

1、为方法添加一个参数 HttpServletRequest 
​		2、使用 request.getSession() 返回一个对象 从中取得HttpSession对象 在attribute属性中使用键值对存储多个数据
​		3、使用 session.getAttribute("userLoginInfo") 读取登录信息 参数和写操作的key一一对应

==注意：==session.getAttribute（）返回的是Object 需要强制类型转换为登录信息实例对象，并用其接收

```java
@RequestMapping("/songlist")
public Map index(HttpServletRequest request, HttpServletResponse response) {
  Map returnData = new HashMap();

  // 取得 HttpSession 对象
  HttpSession session = request.getSession();
  // 读取登录信息 强转为登录信息类   获取的参数与写入的参数名对应
  UserLoginInfo userLoginInfo = (UserLoginInfo)session.getAttribute("userLoginInfo");
  if (userLoginInfo == null) {
    // 未登录
    returnData.put("loginInfo", "not login");
  } else {
    // 已登录
    returnData.put("loginInfo", "already login");
  }
  return returnData;
}
```





## session-配置类

**官方写法**：https://docs.spring.io/spring-session/docs/2.3.0.RELEASE/reference/html5/guides/java-custom-cookie.html

**Spring Session 的配置类,其作用是配置和定制化 Spring Session 的行为，配置类中的这些方法，可以定制化会话的 Cookie 属性和会话数据的存储方式，以满足特定的需求或安全性要求。**

> **配置session依赖**

```xml
<!-- spring session 支持 -->
<dependency>
    <groupId>org.springframework.session</groupId>
    <artifactId>spring-session-core</artifactId>
</dependency>
```

> **配置类**

1、在类上添加 @Configuration注解 表示这是配置类，系统会自动扫描处理
​		2、在类上添加 @EnableSpringHttpSession注解 开启session
​		3、在方法上添加 @Bean注解 表示把此方法返回的对象实例注册为Bean
​		4、DefaultCookieSerializer类 将Cookie对象与字符串的转换，以便在网络中传输

==注意：==
		CookieSerializer  读写Cookie中的Sessionid信息
		MapSessionRepository  Session信息在服务器上的存储仓库

```java
@Configuration
@EnableSpringHttpSession
public class SpringHttpSessionConfig {
  @Bean
  public CookieSerializer cookieSerializer() 
    
    DefaultCookieSerializer serializer = new DefaultCookieSerializer();
    //获取cookie
    serializer.setCookieName("JSESSIONID");

    // 用正则表达式配置匹配的域名，可以兼容 localhost、127.0.0.1 等各种场景
    serializer.setDomainNamePattern("^.+?\\.(\\w+\\.[a-z]+)$");

   //路径
    serializer.setCookiePath("/");
   //设置是否只能服务器修改，浏览器端不能修改，安全有保障
    serializer.setUseHttpOnlyCookie(false);
    // 最大生命周期的单位是秒
    serializer.setCookieMaxAge(24 * 60 * 60);
    return serializer;
  }

  // 当前存在内存中
  @Bean
  public MapSessionRepository sessionRepository() {
    return new MapSessionRepository(new ConcurrentHashMap<>());
  }
}
```









# 拦截器

- SpringBoot项目中，拦截器是开发常用手段，要来做登录验证、性能检查、日志记录等。
- 在实际项目中，有大量页面功能是需要判断用户是否登录，如果让每一个页面都判断是否登录，太繁琐，所以需要一种统一处理相同逻辑的机制，Spring提供HandlerInterceptor拦截器满足需求

---

**基本步骤：**

1. 编写一个拦截器，需要实现HandlerInterceptor接口；
2. 拦截器注册到配置类中(实现 WebMvcConfigurer 的 addInterceptors( ) 方法);
3. 指定拦截规则；

---

> **创建拦截器-实现HandlerInterceptor接口**
>
> 1、拦截器必须实现 HandlerInterceptor 接口。可以在三个点进行拦截
>
> - ​    Controller 执行前  最常用，例如是否登录的验证要在preHandle()方法中处理
> - ​    Controller 执行时  例如记录日志、统计方法执行时间 要在postHandle()方法中处理
> - ​    Controller 执行后 不常用 例如统计整个请求但的执行时间时使用 在afterCompletion()方法中处理
>
> ==注意：==preHandle( )  方法参数中有 HttpServletRequest 和 HttpServletResponse ，可以像controller 中一样使用session

```java
@Component
public class InterceptorDemo implements HandlerInterceptor {

  // Controller方法执行之前
  @Override
  public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

    // 只有返回true才会继续向下执行，返回false取消当前请求
    return true;
  }
    
  //Controller方法执行之后
  @Override
  public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
      ModelAndView modelAndView) throws Exception {

  }

  // 整个请求完成后（包括Thymeleaf渲染完毕）
  @Override
  public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

  }
}
```

> **管理拦截器-实现 WebMvcConfigurer 接口  --将拦截器注册到配置类中**
>
> 1、创建一个类实现WebMvcConfigurer，并实现addInterceptors()方法。这个步骤用于管理拦截器
>
> 2、实现类要加上@Configuration注解，让框架可以自动扫描
>
> 3、管理拦截器最重要的是为拦截器设置拦截范围，常用addPathPatterns("/**") 表示拦截所有url
>
> 4、也可以设置excludePathPatterns()方法排除某些url，例如登录页本身就不需要登录，需要排

```java
@Configuration
public class WebAppConfigurerDemo implements WebMvcConfigurer {
    
    @Autowired   //拦截器类实例化注入
    private InterceptorDemo interceptorDemo;
    
  @Override
  public void addInterceptors(InterceptorRegistry registry) {
    // 多个拦截器组成一个拦截器链
    // 仅演示，设置所有 url 都拦截，排除登录网页以及静态资源  excludePathPatterns排除
    registry.addInterceptor(interceptorDemo).addPathPatterns("/**")
        .excludePathPatterns("登录网页");  //注意一定要加/ 使其变为绝对路径
  }
}
```

> **实例：在拦截器中判断登录状态**

```java
/*若未登录，跳转登录页面  需要在执行前判断*/
 @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           LOGGER.info(" ---------执行前---------");
        // 取得 HttpSession 对象
        HttpSession session = request.getSession();
        // 读取登录信息 强转为登录信息类   获取的参数与写入的参数名对应
        UserLoginInfo userLoginInfo = (UserLoginInfo)session.getAttribute("userLoginInfo");
        if (userLoginInfo == null) {
            // 未登录
            LOGGER.info("---未登录--跳转--");
            String loginPageUrl = "/app/login";  //和管理拦截器中排除网页一致（否则多次定向）
            response.sendRedirect(loginPageUrl);
            return false;
        }else {
            LOGGER.info("---已登录--跳转--");
            return true;
        }
    }
```

> **注意，拦截器也可以像自定义转换器一样配置**

```java
@Configuration
public class WebAppConfigurerDemo2 {

    //注入Bean WebMvcConfig
    @Bean
    public WebMvcConfigurer webMvcConfigurer() {
        
        return new WebMvcConfigurer() {
            @Override
            public void addInterceptors(InterceptorRegistry registry) {

                registry.addInterceptor(new InterceptorDemo())
                        .addPathPatterns("/**")
                        .excludePathPatterns("/app/login");
            }
        };
    }
}
```

---

> **扩展：URL 和URI的区别**

sURL：资源定位符，可以提供找到该资源的路径

URI: 资源标识符，唯一标识一个资源

```java
String requestURI=request.getRequestURI();
String requestURL=request.getRequestURL().toString();
```

当网页请求：http://localhost:8080/rest.html

输出：requestURI=/rest.html   ;  

​			requestURL=http://localhost:8080/rest.html  ;

---





# SpringBoot文件上传

> **实例：模拟用户注册**
>
> 要求：
>
> 1. 用户头像上传，一次只允许上传一张，提交到指定文件夹中；
> 2. 用户宠物图片上传，一次允许上传多张，提交到指定文件夹中；

**Thymeleaf设置注册页面 -UserRegister.html**

```xml
<body style="text-align: center" >
<div style="background-color: aqua;  margin-left:200px;margin-right:200px">
    <h1>User Register</h1>

    <!--enctype="multipart/form-data" 文件提交-->
    <form action="/register" method="post" enctype="multipart/form-data">
        
        用户名:<input type="text" name="userName" > <br><br>
        密 码:<input type="text" name="userPwd" > <br><br>

        <!--提交文件 type="file"   如果想一次性上传多个文件 ，添加multiple-->
        头 像:<input type="file" name="header" > <br><br>
        宠 物:<input type="file" name="photos" multiple> <br><br>

        <input type="submit" value="注册">
        <br>
    </form>
</div>
</body>
```

**java代码-注册控制**

```java
@Controller
@Slf4j
public class UserController {
    
    @Resource
    private UserServiceImpl userService;

    //用户注册页
    @GetMapping("/userRegister")
    public String userRegister(){
        return "/userRegister.html";
    }

    //处理用户注册请求 ,传输文件是 MultipartFile 类型
    @PostMapping("/register")
    @ResponseBody
    public String register(@RequestParam("userName")String userName,
                           @RequestParam("userPwd")String userPwd,
                           @RequestParam("header") MultipartFile header,
                           @RequestParam("photos")MultipartFile[] photos) throws IOException {
        //先判断用户存在不存在
        List<User> userList = userService.getUserList();
        for (User user : userList) {
            if(user.getUserName().equals(userName)){
                return "用户已存在，请登录";
            }
        }

        log.info("上传的文件 userName={} userPwd={} header={}  photos={}",userName,userPwd,header,photos);

        //处理头像 头像只有一张
        if(!header.isEmpty()){
            //获取文件名（上传的文件原名）
            String headerFileName = header.getOriginalFilename();
            //构建header文件 (文件保存路径+文件原名)
            header.transferTo(new File("D:\\img\\"+headerFileName));
        }

        //处理宠物，宠物很多要循环
        if(photos.length>0){
            for (MultipartFile photo : photos) {
                if(!photo.isEmpty()) {
                    //获取文件名（上传的文件原名）
                    String photosFileName = photo.getOriginalFilename();
                    //构建photo文件 (文件保存路径+文件原名)
                    photo.transferTo(new File("D:\\img\\"+photosFileName));
                }
            }
        }

        //将user保存
        User user=new User(userName,userPwd,header,photos);
        boolean b = userService.setUserTOUserList(user);
        if (!b){
            return "用户保存失败";
        }
        return "用户注册成功";
    }
}

```

**也可以上传到程序中[部分核心代码]**

```java
 //上传到程序 C:\Users\admin\Desktop\porject\springboot\springboot\target\classes\static\images
        //1.得到类路径（运行时的）   path 拿到 C:\Users\...\target\classes
        String path = ResourceUtils.getURL("classpath:").getPath();
        //2.动态构建文件（没有则创建）
        File file = new File(path + "static/images/");
        if(!file.exists()){ //不存在则创建
            file.mkdirs();
        }

        //处理头像 头像只有一张
        if(!header.isEmpty()){
            //获取文件名（上传的文件原名）
            String headerFileName = header.getOriginalFilename();
            //构建header文件 (文件保存路径+文件原名) 指定绝对路径  注意要加“/”
            header.transferTo(new File(file.getAbsolutePath()+"/"+headerFileName));
            log.info("保存文件的绝对路径={}",file.getAbsolutePath()+"/"+headerFileName);
        }


        //处理宠物，宠物很多要循环
        if(photos.length>0){
            for (MultipartFile photo : photos) {
                if(!photo.isEmpty()) {
                    //获取文件名（上传的文件原名）
                    String photosFileName = photo.getOriginalFilename();
                    //构建photo文件 (文件保存路径+文件原名) 指定绝对路径
                    photo.transferTo(new File(file.getAbsolutePath()+"/"+photosFileName));
                }
            }
        }
```

> **文件上传注意：**
>
> 1.在上传的时候有一个属性类 MultipartProperties ，这个类对文件进行了限制
>
> ```java
> public class MultipartProperties {
>     private boolean enabled = true;
>     private String location;
>     //单个文件最大1M
>     private DataSize maxFileSize = DataSize.ofMegabytes(1L);
>     //多个文件最多10M
>     private DataSize maxRequestSize = DataSize.ofMegabytes(10L);
>     private DataSize fileSizeThreshold = DataSize.ofBytes(0L);
>     private boolean resolveLazily = false;
> }
> ```
>
> 可以在配置文件中修改application.properties
>
> ```properties
> #单个文件最大
> spring.servlet.multipart.max-file-size=10MB
> #多个文件加起来不超过
> spring.servlet.multipart.max-request-size=50MB
> ```

---





# ############SpringCloud##############

















# ############LinuxFirewall##############

# Linux 防火墙设置

```sh
sudo systemctl start firewalld #开启防火墙

sudo firewall-cmd --set-default-zone=trusted #允许所有流量通过防火墙
sudo firewall-cmd --set-default-zone=block #禁止所有流量通过防火墙

sudo firewall-cmd --add-port=8080/tcp --permanent #允许指定端口的流量通过防火墙
sudo firewall-cmd --remove-port=8080/tcp --permanent #禁止指定端口的流量通过防火墙

sudo firewall-cmd --reload #重新加载 firewalld 服务的配置文件，以便更新防火墙规则
```





# ############Redis##################

Redis官网：https://redis.io/

Redis中文：http://redis.cn/

---

> **为什么需要Redis**

1.企业需求：高并发、高可用、高性能、海量用户

2.对关系型数据库(如Mysql)进行一个补充。

​                      Mysql性能瓶颈：磁盘Io性能低下；

​                      Mysql扩展瓶颈：数据关系复杂，扩展性差，不利于大规模集群；

3.Redis优势： 内存存储-降低磁盘Io次数；

​                          不存储关系，仅存储数据-数据间关系，越简单越好；

---

> **简介**

**Redis 是一个用C语言开发的一个开源的高性能键值对(key-value) 数据库。**  【需要gcc环境】

---

> **Redis特征：**

1. 数据间没有必然的关联关系
2. 高性能。官方提供测试数据，50个并发执行十万请求，读速度11w次每秒，写宿速度8.1w此每秒
3. 多种数据结构支持 【字符串类型string 、列表类型list、散列类型hash、集合类型set、有序集合类型sorted_set】
4. 持久化，可以进行数据灾难恢复

---

> **应用场景**

- 为热点数据加速查询，如热点商品、热点新闻、热点资讯、推广类等高访问量信息等。
- 任务队列，如秒杀、抢购、购票排队等。
- 即时信息查询，如排行榜、各类网站访问统计。
- 时效性信息控制，如验证码控制、投票控制等。
- 分布式数据共享，如分布式集群架构中的session分离。
- 消息队列
- 分布式锁

---

> **NoSQL数据库**

非关系型数据库，作为关系型数据库的补充。

作用是应对在海量用户和海量数据的情况下，带来的数据处理问题。

**NoSQL优点：**

- 可扩容，可伸缩
- 大数据量下高性能
- 灵活的数据模型
- 高可用

**常见NoSQL数据库：**Redis、memcache 、Hbase、MongoDB

---

 



# Redis安装使用

**下载地址：**https://download.redis.io/releases/redis-6.2.13.tar.gz?_gl=1

---

**环境：**Linux-Centos7 开发环境

---

> **安装：**

1.使用yum安装gcc ：

```shel
 yum install -y gcc
```

2.将下载的tar包发送到linux中。

3.到上传的包包下进行解压  :

```shell
tar -zxvf redis-6.2.13.tar.gz
```

4.进入解压后的包中执行make命令 ：

```shell
cd redis-6.2.13 
make
```

5.如果执行make 报错，原因是没有配置好c语言环境(即安装gcc)，解决方法： 执行make distclean 再执行make 即可。

6.执行make install  安装，安装默认目录是/usr/local/bin

```java
make install 
```

---

> **安装目录解析：**【/usr/local/bin】

- redis-benchmark  -性能测试工具，可以在自己机器运行，看看自己机器性能如何
- redis-check-aof   -修复有问题的AOF文件，即Redis持久化机制中的一种
- redis-check-rdb  -用于检查和修复有问题的RDB（Redis Database）文件，即Redis持久化机制中的另一种。
- redis-check-dump -用于检查和修复有问题的dump.rdb文件，与redis-check-rdb功能相同。
- redis-sentinel  -Redis集群使用，用于实现Redis高可用性和故障转移的解决方案，监视Redis主从节点状态并发出相应的命令。
- redis-cli    -客户端，操作入口，Redis命令行界面，用于与Redis服务器进行交互，执行各种Redis命令和操作。
- redis-server -Redis服务器启动命令，Redis服务器进程，负责接收客户端请求、处理数据以及执行各种Redis操作。

---

> **配置启动Redis**

1.拷贝一份redis.conf 到其他目录。比如/etc 目录  

```sh
cd /opt/redis-6.2.13  #进入解压目录
cp redis.conf /etc/redis.conf #复制到/etc 目录下
```

3.修改/etc/redis.conf 后台启动设置 daemonize no改为yes，并 :wq 保存退出

3.配置redis环境变量  

```sh
vi /etc/profile #进入环境变量配置文件

#末行写入
export REDIS_HOME=/opt/redis-6.2.13
export PATH=$PATH:$REDIS_HOME/bin

#退出后source刷新一下
source /etc/profile
```

4.启动Redis

```sh
redis-server /etc/redis.conf 
```

5.查看redis是否后台启动成功

```sh
ps -aux | grep redis
```

---

> **Redis使用**

**客户端访问**

```sh
redis-cli   #客户端访问
redis-cli -p 6379  #指定端口方式访问

quit #退出
```

**Redis关闭**

```sh
redis-cli shutdown  #单实例关闭
redis-cli -p 6379 shutdown #多实例关闭，指定端口关闭
```

---





# Redis指令

指令文档：http://redis.cn/commands.html

---

> **基础操作**

```sh
set key value  #设置k-v数据
get key        #根据k查询v，不存在返回空(nil)
```

演示

```sh
[root@localhost ~]# redis-server /etc/redis.conf
[root@localhost ~]# redis-cli -p 6379
127.0.0.1:6379> set str hello,world
OK
127.0.0.1:6379> get str
"hello,world"
127.0.0.1:6379>
```

---

> **对Key键的操作**

```sh
keys *         #查看当前库中所有key
exists key     #判断某个k是否存在
type key       #查看你的k是什么类型
del key        #删除指定的k
unlink key     #根据v选择非阻塞删除(仅将k从keyspace元数据中删除)，真正的删除在后续的异步操作中
expire key 10  #十秒钟，为给定的k设置过期时间
ttl key        #查看还有多少秒过期  -1永不过期  -2表示已经过期
```

---

> **对DB(数据库)的操作**

```sh
select     #命令切换数据库 redis安装后默认有编号 0-15 的16个库。默认操作的是0号库
dbsize     #查看当前数据库k的存量
flushdb    #清空当前库
flushall   #清空全部库
```

---





# Redis五大数据类型/结构

**常用命令：**https://blog.csdn.net/qq_73574147/article/details/130649582

> **Redis数据存储格式**

Redis自身是一个Map，采用k:v的形式存储 ，k是字符串，v是数据 ，v支持多种类型/结构

---

> **String**

```sh
set <key><vlaue> #添加键值对
get <key> #查询对应键值

append <key><value> #将给定的value追加到原值的末尾

strlen <key> #获取值的长度

setnx <key><value> #只有在k不存在时，设置k值

incr <key>  #将k中存储的数字值(字符串)增1，只能对数字值操作，如果为空，新增值1
decr <key> #将k中存储的数字值(字符串)减1，只能对数字值操作，如果为空，新增值-1

incrby/decrby <key><步长> #将k中存储的数字值增/减，自定义步长

mset <key1><value1><key2><value2>...  #同时设置多个k-v
mget <key1><key2><key3>...  #同时获取多个k的v值

msetnx <key1><value1><key2><value2>... #同时设置多个k-v,且仅有全部给定的k都不存在才执行成功

getrange <key><起始位置><结束位置> #获取值的范围，类似截取字符串subString
setrange <key><起始位置><value> #用<value>覆盖<key>所存储的字符串值，从<起始位置>开始，索引从0开始

setex <key><过期时间><value>  #设置键的同时，设置过期时间，单位秒
getset <key><value> #以旧换新，设置了新值同时获得旧值
```

---

> **List**

- List是一个双向链表
- List适用于具有操作先后顺序的数据控制；例如按照时间顺序，将最近通知显示在前面

```sh
lpush/rpush <key><value1><value2>...  #从左/右 插入一个或多个值 (lpush顺序为 ... value2 value1; rpush则相反)
lpop/rpop <key>  #从左/右 吐出一个值 (输出并删除)

rpoplpush <key1><key2>... #从<key1>列表右边吐出一个值（取出并删除），插入到<key2>列表左边

lrange <key><start><stop> #按照索引下标获取元素（自左向右）lrange mylist 0 -1 （0左第一个， -1右第一个，表获取所有）
lindex <key><index> #按照索引下标获取元素（自左向右）

llen <key> #获取列表长度

linsert <key> before <value> <newValue> #在<value> 前面插入 <newValue>值

lrem <key><n><value> #从左边删除n个<value>

lset <key><index><value> #将列表key下标为index的值替换为value
```

---

> **Set**

set和list类似，但set是可以自动排重，即值不允许重复

```sh
sadd <key><value1><value2>... #将一个或多个member元素加入集合<key>中，已经存在的member将被忽略

smembers <key>  #取出该集合所有值

sismember <key><value>  #判断集合<key>中是否含有该<value>值，有1无0

scard <key> #返回该集合的元素个数

srem <key><value1><value2>.... #删除集合中某个元素

spop <key>  #随机从该集合吐出一个值（会删除）

srandmember <key><n> #随机从该集合中取出n个值，不会从集合中删除

smove <source><destination><value> #将<source>集合中的数据<value>移动到<destination>集合

sinter <key1><key2> #返回两个集合的交集元素
sunion <key1><key2> #返回两个集合的并集元素
sdiff <key1><key2> #返回两个集合的差集元素

```

---

> **Hash**

hash是键值对集合，适用于存储对象

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230912122906987.png" alt="image-20230912122906987" style="zoom:50%;" />

```sh
hset <key><field><value>  #给<key>集合中的<field>键赋<value>值 成功返回1，如果field 以存在，则覆盖并返回0
hget <key><field>  #从<key>集合中取出<field>的值  若key或field不存在，返回nil

hmset <key1><field1><value1> <field2><value2> #批量设置hash的值
hget <key1><field1><field2>  #批量取出hash的field值

hexists <key1><filed> #查看key中 filed是否存在 有1无0

hkeys <key> #列出hash集合中所有field
hvals <key> #列出hash集合中所有value

hincrby <key><field><increment> #为哈希表key中的域field的值加上增量increment 1 -1 （若field存储的为字符串，报错;若key 不存在 则创建key再执行hincrby： 若field不存在，则创建field并初始值为0）

hsetnx <key><field><value> #将hash表key中域field值设置为value，当且仅当filed不存在
```

---

> **有序集合Zset**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230912135945415.png" alt="image-20230912135945415" style="zoom:80%;" />

```sh
zadd <key><score1><value1> <score2><value>... #将一个或多个value元素及其score值加入到有序集合key中

zrange <key><start><stop> [WITHSCORES] #返回有序集合key中下标<start>到<stop>的元素，默认从小到大。添加 [WITHSCORES] 会使value的score一起返回； 
zrevrange <key><start><stop> [WITHSCORES] #同上，从大到小返回

zscore <key><member> #返回有序集合key中成员member的score值

zrangebyscore <key><min><max> [WITHSCORES][limit offest count] #返回有序集合key中，所有score值介于[min,max]之间的成员，有序集合按score值递增次序排列；[limit offest count] 限制返回结果的偏移量和数量
zrevrangebyscore <key><max><min> [WITHSCORES][limit offest count] #同上，有序集合按score值递减次序排列

zincrby <key><increment><value> #为元素的score加上增量increment

zrem <key><value>   #删除该集合下，指定值的元素

zcount <key><max><min>  #统计该集合中，score区间内的元素个数

zrank <key><value>  #返回该值在集合中的排名
```

---





# Redis配置文档

/opt/redis-6.2.13/redis.conf

配置文档：https://www.cnblogs.com/nhdlb/p/14048083.html#_label0

---



## Units单位

![image-20230913133922549](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913133922549.png)

- 配置大小单位，开头定义了一些基本度量单位，只支持bytes，不支持bit
- 不区分大小写

---



## INCLUDES引入公共配置

![image-20230913134230055](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913134230055.png)

- 多实例的情况下，可以把公用的配置文件提取出来，然后include

---



## NETWORK 网络

> **bind 设置访问**

![image-20230913134620877](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913134620877.png)

1. 默认情况 bind=127.0.0.1 -::1  只能接收本机的访问请求
2. 如果服务器，需要远程访问，需要将其注释掉
3. 启动redis，查看当前允许连接的情况

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913135026726.png" alt="image-20230913135026726" style="zoom:67%;" />

---

---

> **protected-mode 设置是否接收远程连接**

![image-20230913135300159](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913135300159.png)

- 默认是保护模式 yes
- 如果需要支持远程访问，需要将yes 改为no

---

---

> **port 设置服务器端口号**

![image-20230913135518325](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913135518325.png)

- redis服务器默认端口 6579

---

---

> **timeout 设置超时**

![image-20230913135801947](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913135801947.png)

-  一个空闲的客户端维持多少秒后关闭，0表示关闭该功能，即永不超时

---

---

> **tcp-keepalive 检测用户端是否存活**

![image-20230913140026836](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913140026836.png)

- tcp-keepalive 是对访问客户端的一种心跳检测 每搁n秒，检测一次；当客户端和服务器连接，检测，用于测试客户端是否存活
- 如果设置为0 则不会进行 tcp-keepalive 检测，一般设为60

 **心跳检测机制意义：**

1. TCP协议中有长连接和短连接，短连接环境下，数据交互完毕后，主动释放连接。
2. 长连接环境下，进行一次数据交互，很长一段时间内无数据交互，客户端可能意外断开，这些TCP未来得及正常释放，那么连接的另一方不知道对端情况，会一直维持连接，长时间的积累会导致非常多的半打开连接，造成资源的浪费，且有可能导致在一个无效的数据链路层发送业务数据，结果发送失败。所以服务器要做到快速感知失败，减少无效链接操作

---

---





## GENERAL 通用

> **daemonize -是否以守护线程启动**

![image-20230913152537499](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913152537499.png)

- 是否为后台进程
- 设置为yes后，表守护进程，后台启动

---

---

> **pidfile**

![image-20230913153546560](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913153546560.png)

存放pid文件的位置，每个实例会产生不同的pid文件，记录redis进程号

---

---

> **loglevel -日志级别**

![image-20230913154631803](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913154631803.png)

- redis日志分为4个级别，默认的设置为notice，开发测试阶段可以用debug，生产模式一般使用notice

---

---

> **logfile -指定日志文件位置**

![image-20230913154820648](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913154820648.png)

- logfile 指定日志文件的位置
- kogfile " " 就是说，默认为控制台打印，并不生成日志文件

---

---

> **database 设定库数量**

![image-20230913155616780](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913155616780.png)

- 设定库的数量，默认16，默认库编号为0
- 可以使用select \<dbid> 命令连接指定库

---

---



## SECURITY 安全

> **设置密码**

![image-20230913160021979](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913160021979.png)

- 永久设置，需要在配置文件进行设置
- 取消注释，自定义一个密码(foobared) 
- 当设置密码后，对redis进行操作需要输入密码，进行验证，否则不能使用

![image-20230913161910371](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913161910371.png)

---

---





## LIMITS 限制

> **maxclients 限制连接数**

![image-20230913164115459](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913164115459.png)

- 设置redis同时可以与多少个客户端进行连接
- 默认情况下为10000个客户端
- 如果达到了限制，redis会拒绝新连接，并向请求的连接发出“max number of clients reached”

---

---

> **maxmemory 限制内存**

![image-20230913165957020](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230913165957020.png)

- 在默认情况下，对32位 实例会限制在3GB，因为32位的机器最大只支持4GB内存，而系统本身就需要一定的内存资源来支持运行，所以32位机器限制最大3GB的可用内存是非常合理的，这样可以避免redis因为内存不足而崩溃
- 在默认情况下，对应64位实例是没有限制的
- 当用户开启了 maxmemory 选项，那么redis将限制选项的值不能小于1MB

**建议：**

1. redis的 maxmemory 设置取决于使用情况，有些网站只需要32MB，有些可能需要12GB
2. maxmemory 只能根据具体的生产环境来调试，不需要预设一个值，从小到大测试，基本标准是不干扰正常程序的运行
3. redis的最大使用内存跟搭配方式有关，如果只是用redis做纯缓存，64-128M对一般小型网站就足够了
4. 如果使用redis做数据库的话，设置到物理内存的1/2到3/4左右都可以

---

---

> **maxmemory-policy 内存策略**

![image-20230914123655182](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914123655182.png)

**maxmemory-policy 内存策略，当内存满了后，执行的策略：**

- volatile-lru 使用LRU算法移除key，只对设置了过期时间的键；
- allkeys-lru 在所有集合key中，使用LRU算法移除key
- volatile-random 在过期集合中移除随机的key，只对设置了过期时间的键；
- allkeys-random 在所有集合key中，移除随机的key；
- volatile-ttl 移除那些TTL值最小的key，即那些最近要过期的key；
- noeviction 不进行移除，针对写操作，只是返回错误；

---

---

> **maxmemory-samples 样本大小配置**

![image-20230914124336801](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914124336801.png)

**当内存由于数据过多才会进行内存策略，对数据进行移除：**

- 设置样本数量，LRU算法和最小TTL算法都并非是精确的算法，而是估算值，所以可以设置样本大小，redis默认会检查这么多key并选择其中LRU的那个
- 一般设置3-7的数字，数值越小样本越不准确，但性能消耗越小

---

---







# 发布与订阅

**Redis	发布订阅（pub/sub）是一种消息通信模式：发送者(pub)发送消息，订阅者(sub)接收消息**

Redsi 客户端可以订阅任意数量的频道

---

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914130141204.png" alt="image-20230914130141204" style="zoom: 67%;" />

---

> **任务队列**

1. 任务队列，顾名思义，就是传递消息的队列；
2. 与任务队列进行交互的实体有两类，一类是生产者（producer），另一类是消费者（consumer）。生产者将需要处理的任务放入任务队列中，而消费者则不断从任务队列中读入任意任务信息，并执行；

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914131056846.png" alt="image-20230914131056846" style="zoom:67%;" />

**从Pub/Sub机制看来，它更像一个广播系统；多个订阅者可以订阅多个频道，多个发布者可以向多个频道发布消息：**

- 发布者(Publisher)：电台，可以向不同FM频道发送消息；
- 频道(Channel): 不同的FM频道；
- 订阅者(Subscriber): 收音机，可以收到多个频道，并以队列方式显示；

---

## 发布订阅模式分类

> **一个发布者，多个订阅者**

主要应用于：通知、公告；

可以作为消息队列或消息管道；

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914132846730.png" alt="image-20230914132846730" style="zoom:67%;" />

---

> **多个发布者，一个订阅者**

各应用程序作为Pub发布者向Channel频道中发送消息，Sub订阅者端收到消息后执行相应的业务逻辑，比如写数据库，显示...

主要应用：排行榜、投票、计数

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914133406278.png" alt="image-20230914133406278" style="zoom:67%;" />

---

> **多个发布者，多个订阅者**

可以向不同的Channel频道中发送消息，由不同的Sub订阅者接收

主要应用:群聊、聊天

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914133623776.png" alt="image-20230914133623776" style="zoom:67%;" />

---

## 命令实现发布和订阅

> **常用指令**

```sh
PUBLISH channel message   #将信息 message 发送到指定的频道channel

SUBSCRIBE channel [channel ...] #订阅频道，可以同时订阅多个

UNSUBSCRIBE [channel ...]  #取消订阅的频道，如果不指定频道，则取消全部频道

PSUBSCRIBE pattern [pattern ...] #订阅一个或多个符合给定模式的频道，每个频道以 * 作为匹配符，比如 it* 匹配频道（it.news it.blog ...）

PUNSUBSCRIBE [pattern [pattern ...]] #退订指定的规则，如果没有参数，则退订所有规则
```

---

> 实现一个发布者，多个订阅者

先订阅

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914142153776.png" alt="image-20230914142153776" style="zoom:67%;" />

再发布

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914142549895.png" alt="image-20230914142549895" style="zoom:67%;" />

---





# Redis持久化-RDB

**RDB（Redis Database）：在指定的时间间隔内将Redis内存中的数据以快照的形式保存到磁盘上。**

**RDB持久化方式通过生成一个二进制文件（通常称为RDB文件），将Redis数据库的快照数据保存在磁盘上。**

**当需要从RDB文件进行恢复时，Redis会读取RDB文件，将其中的数据加载到内存中。**

---

> **RDB持久化流程**

![image-20230915182415426](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230915182415426.png)

1).redis客户端执行bgsave命令或者自动触发bgsave命令；

2).主进程判断当前是否已经存在正在执行的子进程，如果存在，那么主进程直接返回；

3).如果不存在正在执行的子进程，那么就fork一个新的子进程进行持久化数据，fork过程是阻塞的，fork操作完成后主程序即可执行  		其他操作；(Fork作用是复制一个与当前进程一样的进程，新进程的所有数据和原进程一致，且作为原进程的子进程；Linux中fork引		入了“写时复制技术”，即一般情况下父子进程共用同一物理内存，只有进程空间的内容要发生变化时，才会将父进程内容复制一份给		子进程)

4).子进程先将数据写入到临时的rdb文件中，待快照数据写入完成后再原子替换旧的rdb文件；

5).同时发送信号给主进程，通知主进程rdb持久化完成，主进程更新相关的统计信息；

---

> 1. 整个过程中，主进程是不进行任何IO操作的，这就确保了极高的性能；
>
> 2. 如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那么RDB方式要比AOF方式更高效；
> 3. RDB的缺点是最后一次持久化后的数据可能丢失；(正常关闭不会丢失，如果是redis异常终止/宕机，就可能丢失)

---

> **RDB优势：**

1. **适合大规模的数据恢复；** 

   （RDB可以生成一个完整的Redis数据库快照，以二进制形式保存到磁盘上。在恢复过程中只需加载这个快照文件即可）

2. **对数据完整性和一致性要求不高的情况下，更适合使用；**

    (RDB是通过在定期时间间隔或满足一定的条件时生成数据库快照，这意味着在生成快照之前的数据更新可能会丢失）

3. **节省磁盘空间；**

   （RDB文件是以二进制格式存储的，相对于AOF持久化方式，它可以更有效地利用磁盘空间。RDB文件通常较小）

4. **恢复速度快；**

   （由于RDB是一个完整的数据库快照，恢复的过程非常快。只需将RDB文件加载回Redis内存中，并重新加载应用程序即可。）

> **RDB劣势：**

1. 虽然redis在fork时使用看写拷贝技术，但是如果数据庞大时还是比较消耗性能；数据丢失以及恢复时间可能较长；
2. 在备份周期在一定间隔时间做一次备份，所以如果redis意外终止，就会丢失最后一次快照的所有修改；

---

## RDB配置&命令

> **dump.rdb文件**

**在redis.conf中，配置文件名称默认为dump.rdb**

![image-20230916104947783](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916104947783.png)

redis在持久化时，默认将数据持久化到文件中，文件的名字由dbfilename指定，默认dump.rdb;

**该文件默认在Redis启动时命令行所在目录：**

![image-20230916105823158](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916105823158.png)

---

**注意：**

1.redis在关闭时会进行持久化，将数据保存在dump.rdb中;

2.当重启redis时，redis会读取rump.rdb中的数据，使数据恢复；

3.若设置dump.rdb 文件位置为 ./ ,则表示dump.rdb只在启动目录下(动态)，当换目录启动则找不到原目录启动的dump.rdb；

4.故如果在A目录下启动redis并持久化，那么在B目录下重启，redis是获取不到数据的(B目录没有dump.rdb文件或为空文件)；

5.为避免，可以给dump.rdb一个固定的目录位置，比如：  dir /root/

---

---

> **默认快照配置**

![image-20230916115946925](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916115946925.png)

1. 注意时间段：每60秒进行变化统计，60秒结束后，下一个60秒为新的统计时间段;
2. 如果我们没有开启save的注释，那么在退出redis时也会进行备份，更新dump.redb;

---

> **关闭写操作-stop-writes-on-bgsave-error**

- 当Redis执行后台保存（bgsave）操作时遇到错误时，该选项的作用是停止写入操作，以防止数据丢失或损坏
- 当redis无法写入磁盘(比如：磁盘满了)，直接关闭redis写操作，推荐yes

![image-20230916131817626](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916131817626.png)

---

> **是否压缩-rdbcompression**

- 对于存储到磁盘中的快照，可以设置是否进行压缩存储，如果是，redis会采用LZF算法进行压缩；
- 如果不想销毁CPU来进行压缩，可以设置关闭；默认yes打开

![image-20230916132115506](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916132115506.png)

---

> **持久化过程中进行校验 -rdbchecksum**

- 在存储快照后，可以让redis使用CRC64算法进行数据效验，保证文件是完整的；
- 会增加大约10%的性能消耗，推荐开启yes

![image-20230916132526588](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916132526588.png)

---

>  **停止 RDB**

**禁用RDB备份：**

![image-20230916131459103](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916131459103.png)

- 给save传入空字符串，将不会自动执行RDB快照，从而禁用了默认的自动持久化机制。
- 禁用RDB持久化可能会导致数据在Redis重启时丢失。因此，如果选择禁用RDB持久化，请确保有其他机制来确保数据的持久性，如使用AOF（Append-Only File）持久化或外部备份。

---

> **动态停止RDB：**  

```sh
# 禁用 RDB
redis-cli config set save ""

#打开RDB 将save指令设置为默认值，表在900秒内，如果发生至少1个键的变化，且距离上次save指令执行已经过去300秒，执行RDB快照。
redis-cli config set save "900 1 300 10 60 10000"
```

---

> **保存命令 -save VS bgsave**

- save:    save时只管保存，其他不管，全部阻塞。手动保存，不建议；
- bgsave：redis会在后台异步进行快照操作，快照同时还可以响应客户端请求；
- 可以通过 lastsave 命令获取最后一次成功执行快照的时间(时间戳)

---

> **清空命令 -flushall**

- 执行flushall命令，也会产生一个dump.red文件，数据为空；
- flushall命令用于清空整个redis服务器的数据(删除所有数据库的所有key)；

---

## RDB备份&恢复

1. redis可以充当缓存，对项目进行优化，因此重要/敏感的数据建议在Mysql要保存一份；
2. 从设计层面上，redis的内存数据，都是可以重新获取(可能来自程序，也可能来自mysql)
3. redis启动时，初始化数据是从dump.rdb中获取的；

---

**1.查询dump.rdb的位置**

```sh
127.0.0.1:6379> CONFIG GET dir
1) "dir"
2) "/root"
127.0.0.1:6379>
```

**2.将dump.rdb进行备份，如果有必要，可以写shell脚本来定时备份(linux 105)**

```sh
[root@localhost ~]# cp /root/dump.rdb dump.rdb.bak
```

---



# Redis持久化-AOF

**AOF（Append-Only File）** append追加；only仅； Append-Only是一种保护数据不被修改或覆盖的机制；

- 以日志的形式来记录每个写操作(增量保存)，将Redis执行过的所有写指令记录下来( set/del操作会记录，读操作get不记录)；
- 只许追加文件但不可以改写文件；
- redis启动之初会读取该文件重新构建数据；
- redis重启的话就根据日志文件的内容将写指令从前到后执行一次，以完成数据的恢复工作；

---

> **AOF持久化流程**

![image-20230916143207477](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916143207477.png)

1).客户端的请求写命令会被append追加到AOF缓冲区内；

2).AOF缓冲区根据AOF持久化策略[alawys,everysec,no]将操作sync同步到磁盘的AOF文件中；

3).AOF文件大小超过重写策略或手动重写时，会对AOF文件rewrite重写，压缩AOF文件容量；

4).redis服务重启时，会重新load加载AOF文件中的写操作达到数据恢复的目的；

---

> **AOF优势**

1. 备份机制更稳健，丢失数据概率更低；
2. 可读的日志文本，通过操作AOF文件，可以处理误操作；

> **AOF劣势**

1. 比RDB占用更多的磁盘空间；
2. 恢复备份速度慢；
3. 每次读写都要同步，有一定的性能压力；

---

## AOF开启&恢复&修复

> **开启AOF**

1.在redis.conf中配置文件名称，默认为appendonly.aof

2.AOF文件的保存路径，和RDB路径一致

3.AOF和RDB同时开启，系统默认取AOF数据

![image-20230916144515809](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230916144515809.png)

---

> **AOF恢复**

AOF的备份机制和性能虽然和RDB不同，但是备份和恢复的操作和RDB一样，都是拷贝备份文件，需要恢复时再拷贝到redis工作目录下，启动系统即自动加载；

---

> **AOF异常恢复(修复)**

**建议：**备份AOF文件。当你并未备份，而AOF文件又损坏，则需要修复；

当AOF文件损坏，redis是启动不起来的，虽然执行redis-server命令不会报错，但ps -aux查询时，是查不到redis启动项的；

如果遇到AOF文件损坏，通过 /usr/local/bin/redis-check-aof --fix appendonly.aof 进行恢复(不保证能完全修复，可能会数据丢失)

![image-20230917121917373](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917121917373.png)

---



## AOF同步频率&重写机制

> **同步频率设置 -appendfsync**
>
> always 始终同步，每次redis的写入都会立刻记入日志，性能差但数据完整性好；【谨慎】
>
> everysec 每秒同步，每秒记入日志一次，如果宕机，本秒的数据可能丢失； 【默认】
>
> no 不主动进行同步，把同步时机交给操作系统；【不推荐】

![image-20230917122751822](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917122751822.png)

---

> **压缩-rewrite重写**

1. AOF文件越来越大，需要定期对AOF文件进行重写，达到压缩；
2. 旧的AOF文件含有无效命令会被忽略，保留最新的数据命令；【当有：set a a1;set a a2；  只会保留最后一条 set a a2 】
3. 多条写命令会被合并为一个；【当有 set a a1；set b b2; 会重写为 set a a1 b b2；】
4. AOF重写降低了文件占用；更小的AOF文件可以更快的被redis加载；

---

**1.手动触发rewrite重写 -bgrewriteaof**

```sh
127.0.0.1:6379> BGREWRITEAOF
Background append only file rewriting started
127.0.0.1:6379>
```

**2.配置自动触发**

![image-20230917124647247](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917124647247.png)

- auto-aof-rewrite-min-size ：设置文件最小重写大小，默认64mb，只有当AOF文件大于等于该值才触发重写；
- auto-aof-rewrite-percentage ：当前AOF文件大小和最后一次重写后的大小之间比率等于或大于指定的增长百分比，100代表当前AOF文件是上次重写时两倍的时候才重写；

系统载入时或上此重写完毕时，redis会记录此时aof的大小，设置为base_size;

如果redis的AOF文件大小 >= base_size+base_size*100%(默认) 且当前大小 >=64mb(默认) 的情况下，redis会对AOF进行重写

---





# AOF和RDB的取舍

官方推荐同时开启，不冲突；

如果两个都开启，启动时默认走的是AOF恢复；

如果只做缓存：如果只希望你的数据在服务器上运行的时候存在，可以不使用任何持久化方式；(比如：QQ的用户在线/离校状态)

---





# Redis事务

> **什么是redis事务**

事务（Transaction），是指将一个业务逻辑作为一个整体一起执行。事务其实就是打包一组操作（或者命令）作为一个整体，在事务处理时将顺序执行这些操作，并返回结果，如果其中任何一个环节出错，所有的操作将被取消。

Redis 的事务可以保证只有在执行完事务中的所有命令后，才会继续处理此客户端的其他命令。也就是说，只有一个用户可以操作事务中的数据

1. Redis事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序执行；
2. 事务在执行过程中，不会被其他客户端发送来的命令请求打断；
3. redis的事务主要作用就是串联多个命令防止别的命令插队；

---

> **redis事务三特性**

- **单独的隔离操作**：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断
- **没有隔离级别的概念**：队列中的命令没有提交之前都不会实际被执行，因为事务提交前任何指令都不会被实际执行
- **不保证原子性**：事务中如果有一条命令执行失败，其后的命令仍然会被执行，不进行回滚

---

> **redis事务指令示意图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917133752058.png" alt="image-20230917133752058" style="zoom:67%;" />

1).从输入Multi命令开始，输入的命令都会依次进入命令队列，但不会执行；(类似Mysql的开启事务)

2).输入Exec后，redis会将之前的命令队列中的命令依次执行(类似mysql的commit提交事务)

3).组队的过程中可以通过discard来放弃组队(类似mysql的rollback回滚事务)

**4).redis事务和mysql事务本质是完全不同的**

---

> **redis 事务四大指令: MULTI、EXEC、DISCARD、WATCH**

- WATCH 用于客户端并发情况下，为事务提供一个锁（CAS，Check And Set） 可以用 watch 命令来监控一个或多个变量如果在执行事务之前，某个监控项被修改了，那么整个事务就会终止执行
- MULTI 开启一个事务；
- EXEC 执行一个事务；
- DISCARD 取消一个事务；

---

## Redis事务案例&注意事项

> **实例**

需求：使用redis事务依次向redis中添加三组数据

![image-20230917134949563](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917134949563.png)

---

> **注意事项**

1.在组队过程中，可以通过discard来放弃组队

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917135348560.png" alt="image-20230917135348560" style="zoom:80%;" />

2.如果在组队阶段报错(比如语法错误)，会导致exec失败，那么事务的所有指令都不会被执行

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917135415189.png" alt="image-20230917135415189" style="zoom:80%;" />

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917135913801.png" alt="image-20230917135913801" style="zoom:80%;" />

---

## Redis事务冲突&解决

> **问题：三个人同时抢票问题**

![image-20230917142951331](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917142951331.png)

如果不进行控制，会造成超卖现象 【解决方法有两种：悲观锁或乐观锁】

---

> **解决 -悲观锁**

![image-20230917143154573](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230917143154573.png)

> **解决-乐观锁**

![image-20230923130327210](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230923130327210.png)



# --------以上是redis数据库操作--------



# java操作redis -Jedis

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230914143654920.png" alt="image-20230914143654920" style="zoom:50%;" />

---

**Jedis中文文档：**https://www.mklab.cn/onlineapi/jedis/

**jedis重要的类：**redis.clients.jedis包下的jedis类

---

## Jedis项目搭建

> **添加Jedis依赖**

```xml
        <!--Jedis 依赖-->
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>3.2.0</version>
        </dependency>
```

---

> **Jedis连接到Redis**
>
> 1.首先要开启远程连接； bind 、protected-mode
>
> 2.修改防火墙策略，允许端口通过；
>
> 3.Redis如果配置了密码，需要进行身份验证；

```java
public class HelloJedis {

    @Test
    //建一个方法 用于 连接Redis
    public void con(){

        //通过构造函数 指定ip 和端口 Jedis(String host, int port) 得到连接
        Jedis jedis = new Jedis("192.168.100.10", 6379);

        //如果redis配置了密码，则需要进行身份验证  jedis.auth( String password)
        //jedis.auth("foobared");

        //进行各种操作
        String ping = jedis.ping(); //会返回 PONG
        System.out.println(ping);

        //关闭当前连接，并不是关闭redis
        jedis.close();
    }
}
```

---

> **Jedis操作key**

```java
public class HelloJedis {

    @Test
    //建一个方法 用于 连接Redis
    public void con(){

        //通过构造函数 指定ip 和端口 Jedis(String host, int port) 得到连接
        Jedis jedis = new Jedis("192.168.100.10", 6379);

        //如果redis配置了密码，则需要进行身份验证  jedis.auth( String password)
        //jedis.auth("foobared");

        //进行各种操作
        //设置key
        jedis.set("k1","v1");
        jedis.set("k2","v2");
        jedis.set("k3","v3");
        jedis.set("k4","v4");

        //获取所有k
        Set<String> keys = jedis.keys("*");
        for (String key : keys) {
            System.out.print(key +"  ");
        }

        //判断key是否存在
        System.out.println(jedis.exists("k1"));

        //查看某个key的ttl(过期时间)，未设置返回-1
        System.out.println(jedis.ttl("k1"));

        //获取key值
        System.out.println(jedis.get("k1"));

        //关闭当前连接，并不是关闭redis
        jedis.close();
    }
}
```

---



## Jedis操作五大数据类型

> **Jedis 操作 String**

```java
        //批量设置k-v
        jedis.mset("k1","jack","k2","tom");
        //批量获取k-v
        List<String> mget = jedis.mget("k1", "k2");
        System.out.println(mget);

```

---

> **Jedis 操作 List**

```java
        //创建list 存入数据
        jedis.lpush("k_list", "v1", "v2", "v3");
        //读取list
        List<String> kList = jedis.lrange("k_list", 0, -1);
        System.out.println(kList);
```

---

> **Jedis 操作 Set**

```java
        //创建set
        jedis.sadd("k_set","v1","v2");
        //插入
        jedis.sadd("k_set","v3");
        
        //获取v
        Set<String> kSet = jedis.smembers("k_set");
        for (String s : kSet) {
            System.out.print(s+" ");
        }
```

---

> **Jedis 操作 hash**

```java
        //创建hash
        jedis.hset("k_hash","f1","v1");

        //获取
        String hget = jedis.hget("k_hash", "f1");
        System.out.println(hget);
```

```java
        //构建map
        Map<String,String> maps=new HashMap<>();
        maps.put("f2","v2");
        maps.put("f3","v3");

        //构建hash 将map一次性插入
        jedis.hset("k_hash",maps);

        //一次性获取
        List<String> hmgetmap = jedis.hmget("k_hash","f2", "f3");
        System.out.println(hmgetmap);
```

---

> **Jedis 操作 Zset**

```java
        //创建Zset
        jedis.zadd("k_Zset", 1,"v1");
        jedis.zadd("k_Zset", 2,"v2");
        jedis.zadd("k_Zset", 3,"v3");

        //取出 从小到大
        Set<String> kZset = jedis.zrange("k_Zset", 0, -1);
        for (String s : kZset) {
            System.out.println(s);
        }
        //取出，从大到小
        Set<String> kZset1 = jedis.zrevrange("k_Zset", 0, -1);
        for (String s : kZset1) {
            System.out.println(s);
        }
```

---





# SpringBoot整合Redis环境

在SpringBoot中整合Redis；

可以通过RedisTemplate 完成对redis的操作，包括设置数据/获取数据

---



> **修改pom.xml,引入依赖**

```xml
<!--除却spring boot需要的依赖外，还需引入：-->

        <!--redis-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>

        <!--集成redis所需要的commons-pool-->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-pool2</artifactId>
        </dependency>
```

> **配置Redis  在 application.properties 中** 

```properties
#Redis 服务器地址
spring.redis.host=192.168.100.10
#Redis 服务器连接端口
spring.redis.port=6379
#Redis 如果有密码，需要配置 没有密码则无需配置
# spring.redis.password=
#Redis 数据库索引 默认0
spring.redis.database=0
#Redis 连接超时时间 (毫秒)
spring.redis.timeout=1800000
#Redis 连接池最大数量 (负值表没有限制)
spring.redis.lettuce.pool.max-active=20
#Redis 最大阻塞等待时间
spring.redis.lettuce.pool.max-wait=-1
#Redis 连接池最大空闲连接
spring.redis.lettuce.pool.max-idle=5
#Redis 连接池最小空闲连接
spring.redis.lettuce.pool.min-idle=0
```

> **Redis配置类**
>
> 1. 是对要使用的RedisTemplate bean对象的配置，可以理解成是一个常规配置
> 2. 如果不配置，springboot会使用默认配置，这个默认配置，会出现一些问题，比如：RedisTemplate 的key序列化等

```java
package com.wang.redis.config;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.JsonTypeInfo;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.jsontype.impl.LaissezFaireSubTypeValidator;
import org.springframework.cache.CacheManager;
import org.springframework.cache.annotation.CachingConfigurerSupport;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.RedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

import java.time.Duration;

/**
 * @author: wang
 * @version: 1.0
 */

@EnableCaching  //启用缓存
@Configuration
public class RedisConfig extends CachingConfigurerSupport {

    /**
     * 创建一个配置好的RedisTemplate对象，用于对Redis进行操作，
     * 设置了键和值的序列化方式。这样可以方便地将Java对象存储到Redis中，并在需要时进行反序列化和读取。
     */
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        //创建一个RedisTemplate<String,Object>的实例并赋值给template变量，该实例用于操作Redis存储。
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        System.out.println("template===>" + template);

        //创建一个StringRedisSerializer实例作为键的序列化器。
        RedisSerializer<String> redisSerializer = new StringRedisSerializer();

        //建一个Jackson2JsonRedisSerializer实例作为值的序列化器。它使用ObjectMapper对象进行值的序列化和反序列化操作。
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer =
                new Jackson2JsonRedisSerializer(Object.class);

        //创建一个ObjectMapper对象，并进行一些配置，如设置Sring的可见性、启用默认类型信息等
        ObjectMapper objectMapper = new ObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        //使用LaissezFaireSubTypeValidator.instance来激活默认类型验证，防止序列化后的JSON信息丢失类型信息
        //ObjectMapper.DefaultTyping.NON_FINAL 表只为非基本类型的类启用类型信息。非基本类型的对象才会有类型信息。
        //JsonTypeInfo.As.WRAPPER_ARRAY 表示将类型信息包装在数组中，以确保类型信息的正确性和兼容性。
        objectMapper.activateDefaultTyping(
                LaissezFaireSubTypeValidator.instance,
                ObjectMapper.DefaultTyping.NON_FINAL,
                JsonTypeInfo.As.WRAPPER_ARRAY);

        //将上一步创建的ObjectMapper对象设置到jackson2JsonRedisSerializer中
        jackson2JsonRedisSerializer.setObjectMapper(objectMapper);
        //将RedisConnectionFactory对象设置到template中，以便后续操作与Redis进行连接
        template.setConnectionFactory(factory);
        //key序列化方式
        template.setKeySerializer(redisSerializer);
        //value序列化方式
        template.setValueSerializer(jackson2JsonRedisSerializer);
        //value hashmap序列化
        template.setHashValueSerializer(jackson2JsonRedisSerializer);

        return template;
    }


    /**
     * 配置了一个基于Redis的缓存管理器
     * 用于管理Redis缓存，包括缓存的序列化、过期时间等设置。
     * 它提供了一种方便的方式来操作Redis缓存，并与Spring框架集成。
     */
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {

        //使用StringRedisSerializer对缓存的键进行序列化，即将键转换为字符串
        RedisSerializer<String> redisSerializer = new StringRedisSerializer();
        //使用Jackson2JsonRedisSerializer对缓存的值进行序列化，即将值转换为JSON格式的字符串
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);

        //解决查询缓存转换异常的问题 ,配置一个ObjectMapper对象，用于处理和转换缓存中的对象
        ObjectMapper objectMapper = new ObjectMapper();
        //设置ObjectMapper的可见性，即将所有属性都设置为可见
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        //使用LaissezFaireSubTypeValidator.instance来激活默认类型验证，防止序列化后的JSON信息丢失类型信息
        //ObjectMapper.DefaultTyping.NON_FINAL 表只为非基本类型的类启用类型信息。非基本类型的对象才会有类型信息。
        //JsonTypeInfo.As.WRAPPER_ARRAY 表示将类型信息包装在数组中，以确保类型信息的正确性和兼容性。
        objectMapper.activateDefaultTyping(
                LaissezFaireSubTypeValidator.instance,
                ObjectMapper.DefaultTyping.NON_FINAL,
                JsonTypeInfo.As.WRAPPER_ARRAY);

        //将上一步创建的ObjectMapper对象设置到jackson2JsonRedisSerializer中
        jackson2JsonRedisSerializer.setObjectMapper(objectMapper);

        //配置序列化(解决乱码问题)，配置缓存的默认设置，包括缓存的过期时间为600秒、键使用键序列化器进行序列化、值使用值序列化器进行序列化，并禁止缓存空值。
        RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                .entryTtl(Duration.ofSeconds(600))
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(redisSerializer))
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(redisSerializer))
                .disableCachingNullValues();

        //使用Redis连接工厂和缓存配置创建一个RedisCacheManager实例。
        RedisCacheManager cacheManager = RedisCacheManager.builder(factory)
                .cacheDefaults(config)
                .build();

        return cacheManager;
    }

}
```

---

> **测试**

```java
@RestController
@RequestMapping("/redis")
public class RedisController {

    //装配 RedisTemplate
    @Resource
    private RedisTemplate redisTemplate;

    //操作String
    @GetMapping("/testString")
    public String testString() {

        //设置值到redis （ redisTemplate 已经直接连接redis）
        redisTemplate.opsForValue().set("book", "java");

        //读出
        String k1 = (String) redisTemplate.opsForValue().get("book");
        
        return k1;
    }

    //操作list
    @GetMapping("/testList")
    public String testList() {
        
        //设置值到redis
        redisTemplate.opsForList().leftPushAll("books", "java", "python", "math");
        
        //读出
        List books = redisTemplate.opsForList().range("books", 0, -1);
        
        return books.toString();
    }

    //操作Set
    @GetMapping("/testSet")
    public String testSet() {
        
        //设置值到redis
        redisTemplate.opsForSet().add("bookSet", "english");
        
        //读出
        Set<String> book = redisTemplate.opsForSet().members("bookSet");
        String books = "";
        for (String o : book) {
            books = books + " " + o;
        }
        
        return books;
    }

    //操作Hash
    @GetMapping("/testHash")
    public String testHash() {

        //设置值到redis
        redisTemplate.opsForHash().put("bookHash", "name", "java");
        
        //读出
        String o1 = (String) redisTemplate.opsForHash().get("bookHash", "name");
        
        return o1;
    }

    //操作Zset
    @GetMapping("/testZset")
    public String testZset() {
        //设置值到redis
        redisTemplate.opsForZSet().add("bookZset", "java", 1);

        //读出
        Set<String> bookZset = redisTemplate.opsForZSet().range("bookZset", 0, -1);
        String books = "";
        for (String o : bookZset) {
            books = books + " " + o;
        }
        
        return books;
    }
}
```

---

> **注意事项**
>
> 1.如果不提供RedisConfig配置类，springboot会使用默认配置；
>
> 2.springboot默认配置,会存在问题，比如redisTemplate模糊查找key数据为空；  Set keys = redisTemplate.keys("*");
>
> 3.报错：Unrecognized token 'xxx' :was expecting('true','false' or 'null'); 这个报错是jason转换异常，因为redisTemplate在存储时会将数据序列化，读取时也会反序列化，而在redis客户端set时并不会序列化，因此set中的值读取时会报转换异常；

---



# SpringBoot操作五大数据类型

> **String**
>
> 要读写缓存 *Value* ，就要调用 `redisTemplate.opsForValue()` ，然后再调用 `get()` 方法根据参数 *Key* 取得缓存值。

```java
//设置值到redis （ redisTemplate 已经直接连接redis）
redisTemplate.opsForValue().set(userName, userDO);

//读出key为userName 的value值
UserDO userDO = (UserDO)redisTemplate.opsForValue().get(userName);

//修改缓存（实质是重新赋值-覆盖）
redisTemplate.opsForValue().set(userName, userDO1);

//删除缓存 （按k删除）
redisTemplate.delete(userName);

//设置过期时间
redisTemplate.opsForValue().set(userName, userDO, 5, TimeUnit.MINUTES);
```

---

> **List**
>
> - `leftPush()` 和 `rightPush()` 方法第一个参数都是 Key，第二个参数是数据对象。返回值Long
> - 注意：整个列表是 Value，列表中的数据元素不能称为 Value
> - Java 系统会先把对象进行序列化，然后存入 Redis 。Redis 会把相同 Key 的数据组织到一个数据结构 List 中
> - redisTemplate.expire()是通用方法，可以为任何类型设置过期时间

```java
//添加数据（从头部，尾部使用 rightPush ）Category类需要实现 Serializable接口，标识为可序列化对象。
Category category = new Category();
redisTemplate.opsForList().leftPush("categoryList", category);


//查询列表长度
Long size = redisTemplate.opsForList().size("categoryList");

//根据索引查询
Category category = (Category)redisTemplate.opsForList().index("categoryList", index);

//范围查询 （k,开始，结束） 【0, 0表示只查询第一条数据】【0，-1表示查询整个列表的所有数据】
List<Category> categoryDatas = redisTemplate.opsForList().range("categoryList", 0, 1);


//修改  （k，索引，新的对象）
Category category = new Category();
redisTemplate.opsForList().set("categoryList", 0, category);


//删除 （头删 ，尾删使用rightPop）
Category cat = (Category)redisTemplate.opsForList().leftPop("categoryList");

//设置过期时间 （列表无法和String一样，插入时直接设置过期，需要先插入，后按照k设置过期时间）
redisTemplate.opsForList().leftPush("category", category);
redisTemplate.expire("category", 60, TimeUnit.MINUTES);
```

---

> **Set

---

> **ZSet**

```java
//升序查询   0和-1代表查询该键的所有值默认是按升序排序
Set tv = redisTemplate.opsForZSet().rangeWithScores("TV", 0, -1)
    
//降序查询 reverseRangeWithScores是根据score降序排序
Set tv = redisTemplate.opsForZSet().reverseRangeWithScores("TV", 0, -1);
```

```java
//Zset遍历返回Set集合
Set<TypedTuple<PersonalRecord>> datas = redisTemplate.opsForZSet().rangeWithScores("integralRank", 0, -1);

// 遍历
datas.forEach(data -> {
    // 存入的对象
    PersonalRecord pr = data.getValue();
    // 对应的分数
    Double score = data.getScore();
    System.out.println(pr.getId() + " - " + score);
});
```

- 查询返回 Set 集合中的元素类型是 `TypedTuple` ，用于整合查询结果对象（通过 `add()` 方法放入 ZSet 中的对象）及其对应的分数，封装在一起，便于读取。
- TypedTuple 是 ZSetOperations 接口中定义的内部接口
- 于是，通过 `getValue()` 可以取得放入 `ZSet` 的元素对象，通过 `getScore()` 可以取得元素的分数。

---

> **Hash**

```java
//添加 （k，field ，value）【k对应映射表  field对应属性名 value对应属性值】
redisTemplate.opsForHash().put("integralRankUser", userDO.getUserName(), userDO);

//修改 （覆盖）
UserDO userDO = (UserDO)redisTemplate.opsForHash().get("integralRankUser", userName);

//删除 （根据 k和field）
redisTemplate.opsForHash().delete("integralRankUser", userName);

//删除多个 （根据 k和field）
redisTemplate.opsForHash().delete("integralRankUser", userName, "zhangsan", "lisi");
```

---

> **Set**

```java
//添加
redisTemplate.opsForSet().add("ranks", personalRecord1, personalRecord2);

//删除
redisTemplate.opsForSet().remove("ranks", personalRecord);

//修改 【无修改操作，需要先删除旧数据，后添加新数据】

//基本查询 （通过K查询集合中的所有数据。返回值的泛型，就是新增数据的类型，往Set缓存里放了什么数据，拿出来就是什么数据。）
Set<PersonalRecord> datas = redisTemplate.opsForSet().members("ranks");
```

> **Set多集合操作**

- 使用 Set 一般来说并不是用于数据对象的缓存，因为无序，实际上操作很不方便，不能像列表一样精确查询。
- 使用 Set 多用于集合间的操作。所以，推荐 Set 存储简单的数据，比如 Java 的字符串或数字，而不要在 Set 中存入复杂的 Java 自定义对象。
- 比如只存入个人战绩的 id 值而不是整个对象。

```java
//求并集 union() [给定两个集合A，B，把他们所有的元素合并在一起组成的集合，叫做集合A与集合B的并集]
List<String> keys = new ArrayList<>();
keys.add("ranks1");
keys.add("ranks2");
keys.add("ranks3");
Set<Long> unionDatas = redisTemplate.opsForSet().union(keys);

//求交集 intersect() [集合论中，设A，B是两个集合，由所有属于集合A且属于集合B的元素所组成的集合，叫做集合A与集合B的交集]
List<String> keys = new ArrayList<>();
keys.add("ranks1");
keys.add("ranks2");
keys.add("ranks3");
Set<Long> interDatas = redisTemplate.opsForSet().intersect(keys);

//求差集 difference() [设A，B是两个集合，以属于A而不属于B的元素为元素的集合成为A与B的差集] 
List<String> otherkeys = new ArrayList<>();
otherkeys.add("ranks2");
otherkeys.add("ranks3");
Set<Long> diffDatas = redisTemplate.opsForSet().difference("ranks1", otherkeys);
```

---







# Redis缓存Session

通过Redis作为Session数据的缓存，以解决分布式系统的共享问题；

---

> **引入依赖**

先删除旧的依赖

```xml
<dependency>
  <groupId>org.springframework.session</groupId>
  <artifactId>spring-session-core</artifactId>
</dependency>
```

然后添加相关的依赖：

```xml
<!-- spring session 支持 -->
<dependency>
  <groupId>org.springframework.session</groupId>
  <artifactId>spring-session-data-redis</artifactId>
</dependency>
<!--redisson-spring-boot-starter-->
<dependency>
  <groupId>org.redisson</groupId>
  <artifactId>redisson-spring-boot-starter</artifactId>
  <version>3.13.0</version>
</dependency>
```

---

> **Session配置类**
>
> 1.在spring中，配置类使用的是 @EnableSpringHttpSession；若要使用redis存储session，则需要使用@EnableRedisHttpSession
>
> 2.在spring中，系统未提供默认数据仓库，所以需要sessionRepository() new一个仓库对象出来；而使用redis则不需要，因为redis		   就是一个仓库，系统已经封装好了
>
> 3.cookieSerializer 作用是定制Cookie中的Session信息内容格式
>
> 4.使用注解：只需要一个注解，系统自动完成Session数据同步存储到redis，不需要手写代码，但需要去yml中配置；
>
> 5.maxInactiveIntervalInSeconds = 300 设置过期时间，单位秒，不设置默认1800

```java
@Configuration
@EnableRedisHttpSession(maxInactiveIntervalInSeconds = 300)
public class SpringHttpSessionConfig {
    @Bean
    public CookieSerializer cookieSerializer() {
        ... ...
        ... ...
    }
}
```





# 缓存穿透

**场景：**当通过大量错误的用户和密码请求登录时，由于都是错误的，所以redis不会存入缓存数据，程序实际上还是会每次查询数据库，导致数据库压力仍然过大，读写变慢，系统看起来使用了redis，但实际上这种被错误数据攻击的情况下，redis失去了缓存的意义，称之为**缓存穿透**；

**解决方法：**第一次从数据库查询不到数据时，仍然把这个空结果进行缓存，然后设置过期时间，一般不超过五分钟；

```java
// 只 new 实例但不设置任何属性，相当于一个空对象
userDO = new UserDO();
redisTemplate.opsForValue().set(userName, userDO, 5, TimeUnit.MINUTES);
```

当用户第二次访问时，，无论是否正确，redis都已经缓存了数据，避免再次查询数据库，而缓存的错误数据，由于没有属性值，则验证失败，不会执行登录

---

常用时间单位：

- TimeUnit.MILLISECONDS  毫秒
- TimeUnit.SECONDS 秒
- TimeUnit.MINUTES  分钟
- TimeUnit.HOURS  小时
- TimeUnit.DAYS  天

---

设置list的过期时间

```java
//列表结构操作的方式：
redisTemplate.opsForList().leftPush()
    
//这时可使用如下，设置过期时间 （第一参是k  第二参是时间数  第三参是时间单位） 
//redisTemplate.expire()是通用方法，可以为任何类型设置过期时间
redisTemplate.expire("category", 60, TimeUnit.MINUTES);
```

---

> **实例：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230927121717365.png" alt="image-20230927121717365" style="zoom:80%;" />

```java
        //从redis获取数据
		UserDO userDO = (UserDO)redisTemplate.opsForValue().get(userName);

        if (userDO == null) {
            userDO = userDAO.findByUserName(userName);
        }

        if (userDO.getUserName()==null){
            result.setCode("602");
            result.setMessage("用户名不存在");

            //创建无属性用户实例
            redisTemplate.opsForValue().set(userName,new UserDO());

            return result;
        }
```

---



# java中操作redis事务基础框架

```java
try {
    redisTemplate.execute(new SessionCallback<List<Object>>() {
        @Override
        public List<Object> execute(RedisOperations operations) throws DataAccessException {

        }
    });
} catch (Exception e) {
    LOG.error("redisTemplate.execute() error. ", e);
}
```

1. `redisTemplate.execute();` 是执行事务的方法，**推荐** 写在 *try...catch* 异常抓取语句中，这样执行过程中有任何问题，都打印出日志，方便排查问题。
2. 这个写法基本上就是固定了的。具体的事务就写在方法参数 `SessionCallback` 接口的 `execute()` 方法体内部。
3. `new SessionCallback(){}` 这个写法就是匿名类，每个项目在 execute() 方法中实现具体的业务逻辑
4. 方法参数 `RedisOperations` 提供了前面讲过的四大指令操作

---



## 监听对象

在开启事务前，先选择一个要监听的对象，即 Redis 中的某个 Key：

```java
redisTemplate.execute(new SessionCallback<List<Object>>() {
    @Override
    public List<Object> execute(RedisOperations operations) throws DataAccessException {
        //监听商品的ID
        operations.watch(id);
    }
});
```

1. `operations.watch()` 方法传入待监视的 Redis 数据 Key。

**注意：**这个 Key 必须在 Redis 中存在，否则会抛异常。

---



## Redis 事务三阶段

Redis 中的事务从开始到结束要经历 3 个阶段

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/guocheng.svg)

> **1. 开启事务**

```java
redisTemplate.execute(new SessionCallback<List<Object>>() {
    @Override
    public List<Object> execute(RedisOperations operations) throws DataAccessException {
        //监听商品的ID
        operations.watch(id);

        //开启事务
        operations.multi();
    }
});
```

`operations.multi()` 开启事务时不需要参数。

---

> **2. 命令入列**

所谓命令入列，就是指读写 Redis 数据的业务逻辑。在开启事务后，就可以写具体业务逻辑的代码了。

```java
redisTemplate.execute(new SessionCallback<List<Object>>() {
    @Override
    public List<Object> execute(RedisOperations operations) throws DataAccessException {
        //监听商品的ID
        operations.watch(id);

        //开启事务
        operations.multi();

        // 插入一条订单数据。
        // 缓存库的存减 1
        operations.opsForValue().set(idKey, (stock - 1));
        // 数据库的库存减 1
        productDAO.reduceStock(id, 1);
    }
});
```

在 `execute()` 方法中，Redis 的操作不再使用 `redisTemplate.opsForValue()`，而是使用 `operations.opsForValue()` ，这样系统才知道是同一个事务中的操作。

---

> **3. 执行事务**

在完成业务逻辑后，就可以执行事务了：

```java
redisTemplate.execute(new SessionCallback<List<Object>>() {
    @Override
    public List<Object> execute(RedisOperations operations) throws DataAccessException {
        //监听商品的ID
        operations.watch(id);

        //开启事务
        operations.multi();

        // 插入一条订单数据。
        // 缓存库的存减 1
        // 数据库的库存减 1

        // 执行事务
        List exec = operations.exec();
    }
});
```

1. `operations.exec()` 用于执行事务，返回值是 List 列表，存放了每个事务执行结果的标记。事务开启后执行的每个操作，如果成功则放入 true 值作为标记，操作失败则不放入结果标记。有几个操作就有几个结果标记
2. 因为事务是要么每个操作都成功，要么都失败，所以一般来说可以简单处理，不用判断 operations.exec() 方法返回值列表中的每个元素是否都为 true，只要判断返回值列表长度大于 0 则表示执行成功。

---

> **4. 取消事务**

在 `execute(RedisOperations operations)` 方法抛异常时，会自动取消事务，本案例不必写取消事务的代码。

如果有的项目需求，需要手动取消事务的话，代码也非常简单，只需要用：

```java
operations.discard();
```

即可取消事务。

当然，取消事务和执行事务是互斥的，要注意 `exec()` 和 `discard()` 代码的顺序逻辑。

---



## SpringBoot操作Redis事务实例

```java
        try {
            //事务监听
            redisTemplate.execute(new SessionCallback<List<Object>>() {
                @Override
                public List<Object> execute(RedisOperations operations) throws DataAccessException {

                    //获取库存
                    Integer stock = (Integer) operations.opsForValue().get(getKey(id));

                    // 判断该商品的库存是否大于1
                    if (stock == null || stock < 1) {
                        result.setMessage("商品已购完。");
                        return null;
                    }
                    //监听商品的ID
                    operations.watch(getKey(id));

                    //开启事务
                    operations.multi();

                    // 插入一条订单数据。
                    // 由于在我们这里不是重要学习逻辑，可以不写，仅作为逻辑标注

                    // 缓存库的存减 1
                    operations.opsForValue().set(getKey(id), (stock - 1));
                    // 数据库的库存减 1
                    productDAO.reduceStock(id, 1);

                    // 执行事务
                    List exec = operations.exec();

                    if (exec.size() > 0) {
                        result.data(true);
                        result.setSuccess(true);
                    } else {
                        result.setMessage("抢购失败");
                    }
                    return exec;
                }
            });
        } catch (Exception e) {
            System.out.println("redisTemplate.execute() error. "+e);
        }
       
```





# 分布式锁

> **引入：**

**问题：**在商品抢购中采用reids事务，以保证redis中库存数据不会错乱超卖，但会产生两个问题：

1.当库存为3时，十个线程抢购模拟10人抢购，只有一人抢购成功，库存值减为2；

2.数据库中的库存值和redis中不一致，数据库中值可能为负数；

---

**原因：**

- 问题一：事务不是独占的，10个线程由于速度快，都在同一时间开启事务进行抢购，而事务中的操作都互不干扰。Redis中的库存为3，而各个线程最终只有一个可以成功的修改库存值为2。于是，其他线程在最终执行后修改时，不是基于最新值修改（即数据状态已经改变了），那么修改不成功。
- 问题二：redis的事务，只能影响redis的操作，execute(RedisOperations operations) 方法抛出异常时，只能使所有redis操作取消，但影响不到数据库，他们是不同的软件。

---

**解决方法：**

事务不能很好解决抢购的问题，那么可以使用分布式锁来解决。

----



> **什么是分布式**

![servier.svg](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/servier.svg)

分布式结构就是一个完整的系统，按照业务功能，拆分成的一个个单独的子系统，在分布式结构中，每个子系统被称为“服务”。

---

> **什么是分布式锁**

在java中，synchronized关键字等都是本地锁，只能解决一台服务器并发问题。随着业务的增大，单机结构不满足那么大的访问量，需要变成集群或者分布式结构，因此我们无法保证某个数据的改变是同一台服务器操作的。我没看需要一个能锁住所有服务器的锁，这就是分布式锁。

----



## 集成 Reddissin

要使用redis分布式锁，就需要用到 Reddissin 客户端，它提供的功能要远远超出一个 Redis客户端的范畴，在可以使用基本的Redis功能的同时，也能使用它提供的高级服务：

- 远程调用
- 分布式锁
- 分布式对象、容器

---

> **SpringBoot集成Reddissin**

```xml
<!--redisson-->
<dependencies>
    <dependency>
        <groupId>org.redisson</groupId>
        <artifactId>redisson-spring-boot-starter</artifactId>
        <version>3.13.0</version>
    </dependency>
</dependencies>
```





## Redis分布式锁实现

> **1.先注入 ReddissinClient实例**

```java
//import org.redisson.api.RedissonClient;
@Autowired
private RedissonClient redissonClient;
```

---

> **2.取得锁**

```java
RLock rLock = redissonClient.getLock("CUSTOM_NAME"); //CUSTOM_NAME 只是代码举例哦
```

用 `redissonClient.getLock()` 得到一个 Redis 锁对象，方法参数是 *字符串* 类型的自定义锁名称，不一定要用数据 Key ，一般推荐用容易理解的、业务相关的名称。

为了减少冲突、明确含义、易于理解和维护，不要以简单的数字 id 值作为 Redis 中的数据 Key，推荐的格式是：

```txt
productId-1-stock
```

这样就知道 Redis 缓存中这个 Key 的作用和含义。同样，锁的名称也不要太简单，推荐的格式是：

```txt
productId-1-lock
```

这样也比较明确、容易理解。

当然，这种命名格式并不是强制规定，只是经验之谈，大家可以按照自己的喜好指定格式。

---

> **3.上锁**

```java
rLock.lock();
```

并发情况下，每个线程都会竞争锁：

- 竞争成功（获取锁）的线程会继续运行
- 竞争失败的线程会被禁用，并且重新获取锁之前，该线程将一直处于休眠状态。

简单说，抢不到锁的线程会持续等待，所以使用锁要特别小心。

---

> **4.解锁**

```java
rLock.unlock();
```

有上锁就必须解锁，否则会导致线程持续等待而产生死锁，系统也就卡死了。

所以，推荐把业务操作放在 *try...catch...finally* 中：

```java
try {
  rLock.lock();
  // 抢购业务逻辑
} catch (Exception e) {
    LOG.error("some error. ", e);
} finally {
    rLock.unlock();
}
```

---



# 分布式ID

ID是数据的唯一标识，常见的做法是用数据库的自增主键机制，自动生成ID。



> **引入**

**问题**：随着业务增长，数据量会越来越大，一张表、一个库可能无法容纳数据，需要对数据进行分表，分表后每个表的数据会按自己的节奏进行自增，这样会造成id冲突，这时需要一个单独的机制来负责生成唯一id。

---

**应用**：例如网购的订单号，会根据但当天时间即订单生成的序号来生成一个唯一id

---

redis有个特点是所有命令操作都是单线程，没有多线程的概念。基于这个特点，redis提供了原子自增命令，能保证生成id是唯一有序的。

---

---



> **Redis生成分布式ID**

**1.引入关键类：**

```java
import org.redisson.api.RAtomicLong;
import org.redisson.api.RedissonClient;
```

**2.过程代码**

```java
//格式化格式为年月日
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyyMMdd");
//获取当前时间
String now = LocalDate.now().format(dateTimeFormatter);

//通过redis的自增获取序号 
RAtomicLong atomicLong = redissonClient.getAtomicLong(now); //先获取一个自增实例对象
atomicLong.expire(1, TimeUnit.DAYS); //设置过期
long number = atomicLong.incrementAndGet(); //再取得实际自增值（第一次调用，返回值是 1。每调用一次则加 1）

//拼装订单号
String orderId = now + "" + number;
```

- Redis 是一个 Key-Value 存储结构，那么通过 Redis 获取一个自增 ID，也需要一个 Key。
- 实例代码中，格式化当前日期的作用也是如此，用 *yyyyMMdd* 格式的日期作为 Key，获取自增 ID 值。当然，这是因为本案例的业务特点，订单号跟日期有关决定的，其它场景下可以根据需要自定义 Key。

---

 

# ############JUnit&&Swagger###############



# 单元测试JUnit  -创建

> **添加依赖**
>
> - *spring-boot-starter-test* 是 SpringBoot 集成了单元测试的库，里面包含了很多单元测试的组件。在 `https://start.spring.io/` 中创建项目的时候，会自动添加好这个依赖库的，所以一般不用手动添加。
> - 但是要用到一些 *junit* 单元测试框架的特殊功能，所以要额外再加一个依赖。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

**scope 标签的作用：**此标签规定了本依赖库在整个项目中起作用的阶段。*scope* 常见的值包括：

- compile 这是默认值，如果依赖库没有注明 scope ,则等同于`<scope>compile</scope>`,表示本依赖库在项目编译时就开始使用。全程有效
- test 表示本依赖库仅仅参与项目测试相关的工作，包括测试代码的编译，执行。项目功能代码编译时不起作用。那么，如果项目不运行单元测试程序，就没有作用了。即 **spring-boot-starter-test** 和 **junit** 仅仅用于项目的单元测试。
- runtime  被依赖项目无需参与项目的编译，不过后期的测试和运行时需要其参与。

---

> **创建单元测试类**

测试类一定要写在项目的：src/test/java/ 目录下。相对应的，功能代码必须写在 `src/main/java`目录下。这是Maven规范

测试类的包路径要跟主类一致，测试类名一般以Tests或Test结尾。

---

> **单元测试类基本写法**

```java
@SpringBootTest
class KanbanApplicationTests {

      @Test
      public void contextLoads() {

      }
}
```

**单元测试类重要的是两个注解（Annotation）：**

- `@SpringBootTest` 从注解名可以看出来，其作用就是标注此类是一个基于 *SpringBoot* 的单元测试类。
- `@Test` 标注此方法是要执行的测试方法。当然，方法可以写多个，想让系统执行测试方法就加上注解，不想执行就去掉注解。

具体的测试代码就在加了 `@Test` 注解的 `contextLoads()` 方法内实现。

同样，单元测试类也可以写多个，看项目的需要了。例如，每个服务实现都单独写一个单元测试，比较清晰明了。

---



# 单元测试JUnit -断言

JUnit 中使用 ***Assert*** （断言）类来检查单元测试中的数据是不是正确。断言对于单元测试来说，是非常重要的。 所谓正确，是指是否符合预期。

---

例如：注册用户后，为了确认用户是否真正注册成功，可以做一次查询，如果能查询到，那肯定注册成功了。那么有两处需要检查是否符合预期：

1. 注册后，返回的 User 实例对象 id **大于 0** 。大于 0 表示注册成功。
2. 调用 *findByIds()* 方法，返回的列表**不是空的**。

如果满足条件（符合预期），就认为注册肯定成功，并且 *findByIds()* 方法也是 OK 的。

---

> **断言的写法**

首先 *import* 断言类：

```java
import org.junit.Assert;
```

然后在测试方法中，调用 *Assert* 类的相关方法进行判断：

```java
Result<User> userResult = userService.register("LiSi", "123");
User user = userResult.getData();
Assert.assertNotNull("注册后返回 User 对象不能为 null 。", user);
Assert.assertTrue("注册后返回 User 对象的 id 值必须大于 0 。", user.getId() > 0);
```

这里用到了两个断言方法：

- `Assert.assertNotNull()` 方法的作用，顾名思义，就是判断对象 **不为** `null`。第一个参数是字符串，内容是自定义的错误提示信息，如果判断失败，系统自动输出这个错误提示；第二个参数是待判断的对象。

  ➣ 如果 user 实例对象不为 null 则表示符合期望。

- `Assert.assertTrue()` 方法的作用是判断 *条件表达式* 是否为 *true* 。第二个参数就是待判断的*条件表达式*；同样，第一个参数是字符串，内容是自定义的错误提示信息。

  ➣ 如果 `user.getId() > 0` 则表示符合期望。

这两个断言方法是最常用的。

---

> **其它断言方法**

***Assert* 的所有断言方法，第一个参数都是自定义的错误提示信息。**

- `Assert.assertNull()` ：判断对象为 null，相当于 `assertNotNull()` 取反。例如删除数据后，期望查不到数据了，那么可以用此方法。

- `Assert.assertFalse()` ：判断第二个参数 *条件表达式* 是否为 *false* ，相当于 `Assert.assertTrue()` 取反。

- `Assert.assertEquals()` ：判断第二、三参数的两个对象是否相等。该断言不能用于数组的比较

  ```java
  String a = new String("张三");
  String b = new String("张三");
  Assert.assertEquals("姓名必须相等", a, b); //通过。实例对象内容相等。
  ```

- `assertArrayEquals()` ：判断两个数组是否相等

  ```java
  int[] a = {1, 2, 3};
  int[] b = {4, 5, 6};
  Assert.assertArrayEquals("两个数组必须相等", a, b); //不通过。数组不相等。
  ```

---

> **不常用的断言方法**

- `assertSame()` ：判断两个对象的引用是否相同，即是否为同一个对象实例。
- `assertNotSame()` ：判断两个对象的引用是否不同，即不为同一个对象实例。

```java
String a = new String("张三");
String b = new String("张三");
Assert.assertSame("姓名必须是同一个实例对象", a, b); //不通过，内容一致但不是同一个对象
```





# Swagger

Swagger是一个文档在线自动生成器。不仅可以生成文档，更是一个规范且完整的框架，由于生成、描述、调用、和可视化RESTful风格的web服务。

简单说,Swagger的核心功能是生成API文档，以及在线测试API

---

以前项目中使用的写test control方式是最粗糙的测试方式。

为了保证项目质量，在完成DAO、service后写单元测试保证基础功能没问题。完成control、API后用Swagger的接口文档跟前端开发工程师确认交互，用在线测试功能验证功能的可用性，可以更全面保证整体质量。

---

> **一 集成Swagger**

**引入库**

```xml
<dependency>
    <groupId>com.battcn</groupId>
    <artifactId>swagger-spring-boot-starter</artifactId>
    <version>2.1.5-RELEASE</version>
</dependency>
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.0</version>
</dependency>
```

- *swagger-spring-boot-starte* 就是 *SpringBoot* 集成 *Swagger* 的库
- *jaxb-api* 是运行 *Swagger* 额外需要依赖的库，主要用于对象和XML之间的序列化和反序列化，在集成 *Swagger* 是不会直接用到。

---

> **二 启用 Swagger**

在 *application.properties* 中添加：

```properties
spring.swagger.enabled=true
```

表示项目是否启用 *Swagger* 。在项目开发和测试阶段开启；在项目发布上线时改为 false 表示关闭，即可避免安全问题。

---

> **三 为 API 加上注解**

Swagger 是通过注解的方式来生成对应的 API，在每个 API 方法上我们需要加上各种注解来描述。

```java

    @ApiOperation(value = "任务数据保存", notes = "提交任务数据", httpMethod = "POST")
    @ApiResponses({ @ApiResponse(code = 200, message = "保存任务数据成功", response = Result.class) })
    @PostMapping(path = "/api/task/save")
    @ResponseBody
    public Result<Task> save(@ApiParam(name="任务对象",value="任务对象以json格式传入",required=true) @RequestBody TaskGroupAction taskAdd) {
      ... ...
    }
```

**API 方法是主要用到三种注解：**

1. `@ApiOperation` 用于描述此 API 方法的作用。
   - `value` 值用于描述此 API 方法的名称
   - `notes` 值用于描述此 API 方法的说明
   - `httpMethod` 注明是 *GET* 还是 *POST* ，免得前端调用错误导致请求失败
2. `@ApiResponses` 用于述此 API 方法执行完毕后的响应状态。可以描述多种响应状态，最常见的是描述 200 状态。
   - 一个 `@ApiResponse` 用于描述一种响应状态
   - `code` 值就是“http状态码”，最常见的是 200
   - `message` 值用于解释意思返回内容
   - `response` 值用于描述返回对象的类型
3. `@ApiParam` 用于描述每个方法参数
   - `name` 值用于解释参数名称
   - `value` 值用于说明此参数的作用
   - `required` 表示是否必填参数

 **项目启动后，输入 http://localhost:8080/swagger-ui.html 即可访问 Swagger 文档页面**

---

> **四 为模型加上注解**

`@ApiParam` 可以描述参数的作用，而参数类 的每个属性是什么意思，有什么作用，也可以用相关的注解来描述。

```java
public class TaskGroupAction {

    @ApiModelProperty(value = "任务组 id",example="1")
    private long taskGroupId;

    @ApiModelProperty(value = "任务实例")
    private Task task;
}
```

1. `@ApiModel` 写在模型类上，解释其作用。
   - `value` 可以写上完整的类名
   - `description` 描述类的作用
2. `@ApiModelProperty` 写在模型类的属性上，解释属性的作用。
   - `value` 描述此属性的作用
   - `example` 如果有需要，可以设置一个用于测试的默认值

**关联的其他类也可以同样加注释。**

```java
public class Task {

    @ApiModelProperty(value = "任务标题", required=true, example="开发任务")
    private String title;
}
```

@ApiModelProperty 还可以用 `required` 参数标识是否是必填项

---





# Docker

> 一 ：**申请镜像仓库并登录**

每个人都可以构建自己的应用程序镜像，但是要想比较方便的分发到其它计算机的运行部署，就需要一个在线的仓库。

由于 Docker 的官方仓库属于外网，速度非常慢，所以推荐使用阿里云的镜像仓库服务。



<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20231015140148736.png" alt="image-20231015140148736" style="zoom:50%;" />

**账号：**  aliyun9069865285

密码：123qwe()

命名空间：  wbl_docker



登录实例： 【用户名：aliyun9069865285      公网地址：registry.cn-hangzhou.aliyuncs.com】

```sh
sudo docker login --username=aliyun9069865285 registry.cn-hangzhou.aliyuncs.com
```

---

> **二：配置**

**1.项目打包**

一定要进入项目目录，执行 ls 命令后能看到 pom.xml的地方执行：

```shell
mvn package
```

**2.撰写 *Dockerfile***

在项目目录下新建 *Dockerfile* 文件，文件名必须是 Dockerfile（大小写一致且没有后缀）

```shell
# 添加 Java 11 镜像来源
FROM openjdk:11.0.4

# springboot 端口
EXPOSE 8080

# 作者
MAINTAINER xxxxx <xxxxx@youkeda.com>

# 添加 Spring Boot 包
ADD target/kanban-0.0.1-SNAPSHOT.jar app.jar

# 执行启动命令
ENTRYPOINT ["java","-Duser.timezone=GMT+8","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

文件内容每一行都是一条指令，各行指令解释如下：

- 自己的项目镜像必须从另一个基础镜像扩充内容后得来，所以第一行的 `FROM` 指令就表示本镜像以 jdk11 作为基础镜像。意味着 JDK11 已经内置了。 【`FROM` 指令必须放在第一行】
- `EXPOSE 8080` 是暴露 SpringBoot 的默认端口。
- `MAINTAINER` 指令这一行是说明本镜像的作者，注意作者名称和邮箱的格式，空格不能省略。作者名称不要写中文，容易出现乱码。
- `ADD` 指令表示把项目中的文件添加到镜像中，并且重命名为 *app.jar*  【上一步 `mvn package` 执行完后，会在项目的 target 目录下产生项目程序包 xxx.jar】
- `ENTRYPOINT` 指令用于启动镜像开启容器后，系统自动执行的命令。后面方括号的内容，有点像个字符串数组，系统会自动把这些字符串组合成命令执行 【启动镜像开启容器后，系统自动执行 `java -Duser.timezone=GMT+8 -Djava.security.egd=file:/dev/./urandom" -jar /app.jar`】

---

> **三： 构建镜像**

写完 *Dockerfile* 文件后就可以构建了。

**1.镜像版本**

- 因为每个项目都不可能是一次完成的，所以项目代码每次有任何修改，在测试（单元测试+Swagger在线测试）完毕后，都需要构建新的镜像。
- 于是有了镜像版本的概念，每次构建新的镜像，都有一个特定的版本号。推荐用以下命令产生版本号： 

```shell
TZ=CST-8 date '+%Y%m%d-%H%M'

#得到的结果类似于：20210915-1314 【以当前时间的“年月日-时分”格式作为版本号】
```

- 然后再在自己电脑上，在一个文本文件里按照下列格式写好构建命令：

```shell
sudo docker build --no-cache -t 容器镜像仓库的公网地址/命名空间/项目名称:版本号 .

#案例
# sudo docker build --no-cache -t registry.cn-zhangjiakou.aliyuncs.com/xxxxx/kanban:20210915-1401 .

```

拷贝写好的命令粘贴到终端执行，可能比较慢，尤其是第一次构建，需要自动下载 *openjdk:11.0.4* 基础镜像，就比较慢。



**2.推送镜像到仓库**

```shell
sudo docker push 容器镜像仓库的公网地址/命名空间/项目名称:版本号

#案例
#sudo docker push registry.cn-zhangjiakou.aliyuncs.com/xxxxx/kanban:20210915-1401
```



**3.登录阿里云镜像仓库网页查看**

---

> **四 ：运行**

登录阿里云控制台 -> 容器镜像服务 -> 个人实例 -> 镜像仓库 -> 点击仓库名称，再基本信息页面，可以看到路径：

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20231015151106554.png" alt="image-20231015151106554" style="zoom:80%;" />

执行下面命令运行：

```shell
sudo docker run --name kanban -it --restart=always \
    -d -p 8080:8080 \
    registry.cn-xxxxxxxx.aliyuncs.com/xxxxxxxx/kanban:[镜像版本号]
    
#实例
#sudo docker run --name kanban -it --restart=always \
#   -d -p 8080:8080 \
#   registry.cn-hangzhou.aliyuncs.com/wbl_docker/kanban:20231015-1427
```





