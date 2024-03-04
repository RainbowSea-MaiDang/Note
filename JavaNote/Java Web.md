 	 	

# ############html#################

**网页组成**

![image-20230829145425091](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829145425091.png)





# HTML

- HTML（HyperTextMark-upLanguage）即超文本标签语言(可以展示的内容类型很多)
- HTML 文本是由 HTML 标签组成的文本，可以包括文字、图形、动画、声音、表格、链接等
- HTML 的结构包括头部（Head）、主体（Body）两大部分，头部描述浏览器所需的信息，主体则包含所要说明的具体内容。

> **html 结构**

![image-20230829145220300](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829145220300.png)

> **html 的标签/元素**

在线文档 :https://www.w3school.com.cn 

---

1. HTML 标签用两个尖括号”<>”括起来
2. HTML标签一般是双标签，如<b>和</b> 前一个标签是起始标签, 后一个标签为结束标签
3. 两个标签之间的文本是html元素的内容
4. 某些标签称为"单标签",因为它只需单独使用就能完整地表达意思,如\<br/>\<hr/>
5. HTML元素指的是从开始标签到结束标签的所有代码。

---

## html标签

### 字体标签\<font>

> **应 用 实 例1 ： 在 网 页 上 显 示 北 京 ， 并 修 改 字 体 为 微 软 雅 黑 ，颜 色 为 蓝 色 。**
>
>  font 标 签 是 字 体 标 签 , 它 可 以 用 来 修 改 文 本 的 字 体 , 颜 色 , 大 小 ( 尺 寸 )
>
>  (1)color 属 性 修 改 颜 色
>
>  (2)face 属 性 修 改 字 体 
>
> (3)size 属 性 修 改 文 本 大 小 

```html
<font size="40px" face="微软雅黑" color="red">北京</font> 
```



###  字符实体（显示特殊符号）

 在网页上显示一些特殊的符号，称为字符实体(也叫符号实体)。

> **应用实例 将 \<hr/>标签以文本方式显示在页面---- \<hr/>标签的作用是画一 条 线**
>
> 常 用 的 特 殊 字 符 : 
>
>  < :   \&lt;    
>
> \>:    \&gt; 
>
> 空 格: \&nbsp;

```html
<body> 
<hr/>   
<!--lt;hr/&gt;  网页显示为<hr/>-->
&lt;hr/&gt; 
</body> 
```

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829155413738.png" alt="image-20230829155413738" style="zoom:80%;" />

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829155440946.png" alt="image-20230829155440946" style="zoom:80%;" />

---



### 超链接标签\<a>

> ​       **HTML\<a> 元素**（或称锚元素）可以通过它的 href属性 创建通向任何其他 URL 的超链接。
>
> - href 属 性设置连接的地址
> - target 属性设置哪个目标进行跳转 
> - _self :表示当前页面 ( 默 认 值 )
> - _blank :表示打开新页面来进行跳转
> - text-decoration: none;  去除下划线
> - download 属性指示浏览器下载 URL 而不是导航到它因此,将提示用户将其保存为本地文件,如果属性有一个值，那么此值将在下载保存过程中作为预填充的文件名（如果用户需要，仍然可以更改文件名）

```html
<!--链接到外部地址-->
<a href="https://example.com">Website</a>

<!--链接到本页某个位置-->
<a href="#属性">Description of Same-Page Links</a>
  
  <!--创建可点击图片-->
<a href="https://developer.mozilla.org/en-US/">
  <img src="mdn_logo.png"
       alt="MDN logo" />
</a>

<!--创建emali链接-->
<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>
```



### 无序/有序列表\<ul>/\<ol>

> **语法：**
>
> - ul : 表 示 无 序 列 表
>
> - li : 列表项
>
> - type 属 性 ： 指 定 列 表 项 前 的 符 号
>
>   ---
>
> - ol : 表 示 有 序 列 表
>
> - li : 列表项
>
> - type 属 性 ：指定列表项排序方式 ，默认为 "1"   【1 阿拉伯；2 小写字母；3 大写字母；4 小写罗马数字；5 大写罗马数字】
>
> - start 属性：排序起始值

```html
    <ul type="属性值">
      <li>列表内容</li>
    </ul>

    <ol type="属性值" start="启始值">
        <li>列表内容</li>
    </ol>
```



### 图像标签\<img> 

img 标签可以在 html 页面上显示图片

> - src:属 性 可 以 设 置 图 片 的 路 径 
> - width: 属 性 设 置 图 片 的 宽 度 
> - height: 属 性 设 置 图 片 的 高 度 
> - border: 属 性 设 置 图 片 边 框 大 小
> - alt:属 性 设 置 当 指 定 路 径 找 不 到 图 片 时 , 用 来 代 替 显 示 的 文 本 内 容 

```html
<img class="fit-picture"
     src="/media/cc0-images/grapefruit-slice-332-332.jpg"
     alt="Grapefruit slice atop a pile of other slices">
```



### 音频标签\<audio> 

​       **HTML <**audio**> 元素**元素用于在文档中嵌入音频内容。\<audio> 元素可以包含一个或多个音频资源，这些音频资源可以使用 src 属性或者\[]元素来进行描述：浏览器将会选择最合适的一个来使用。也可以使用 [MediaStream](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaStream) 将这个元素用于流式媒体。

> autoplay  布尔值属性；声明该属性，音频会尽快自动播放，不会等待整个音频文件下载完成
>
> controls  声明该属性，浏览器将提供一个包含声音，播放进度，播放暂停的控制面板，让用户可以控制音频的播放

```html
<audio 
       controls
        src="/media/cc0-audio/t-rex-roar.mp3">
            <a href="/media/cc0-audio/t-rex-roar.mp3">
                Download audio
            </a>
    </audio>
```



### 表格标签\<table>

> - table ：   标 签 是 表 格 标 签
> - border ： 设 置 表 格 标 签
> - width ： 设 置 表 格 宽 度
> - height ： 设 置 表 格 高 度
> - align ： 设 置 表 格 相 对 于 页 面 的 对 齐 方 式 
> - cellspacing ： 设置单元格间距
> - tr ： 是 行 标 签 
> - th ： 是 表 头 标 签 
> - td ： 是 单 元 格 标 签 
> - align ： 设 置 单 元 格 文 本 对 齐 方 式
> - b ： 是 加 粗 标 签 

```html
<table width="500" border="6" align="center"> 
    <h1 align="center">表格标签的使用</h1> 
    <tr> 
        <th>名字</th> 
        <th>住址</th> 
        <th>邮件</th> 
    </tr> 
    <tr>
        <td>第1行第1列</td> 
        <td>第1行第2列</td> 
        <td>第1行第3列</td> 
    </tr> 
</table> 
```



### 表格标签-跨行跨列表格

![image-20230829162240797](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829162240797.png)

> - 合 并 列: colspan=" 列 数 "
> - 合 并 行: rowspan=" 行 数 " 
> - bordercolor:指 定 表 格 边 框 的 演 示

```html
<table border="1" height="250" bordercolor="#E87EFA" cellspacing="0" width="500">
    <tr>
        <!--合 并 了 3 列 -->
        <td align="center" colspan="3">第1行第1列</td>
    </tr>

    <tr>
        <!--合 并 行 ， 跨 行row行 -->
        <td rowspan="2">第2行第1列</td>
        <td>第2行第2列</td>
        <td>第2行第3列</td>
    </tr>

    <tr>
        <td>第3行第2列</td>
        <td>第3行第3列</td>
    </tr>

    <tr>
        <!--合 并 行 ， 跨 行 row 行 -->
        <td rowspan="2">第4行第1列</td>
        <td>第4行第2列</td>
        <td>第4行第3列</td>
    </tr>

    <tr>
        <td>第5行第2列<img src="imgs/2.png" width="100">
        </td>
        <td>第5行第3列</td>
    </tr>
</table>
```





### 分类标签\<label>

\<label>标签是用来给某个元素或者文本进行分类或者标记的一种方式。

```html
```



### 定义段落\<p>

-  \<p> 标签定义段落
- p 元素会自动在其前后创建一些空白。

```html
<p>这是段落中的文本。</p>
```



### span 标签

- span 标签是内联元素，不像块级元素（如：div 标签、p 标签等）有换行的效果
-  如果不对span应用样式，span标签没有任何的显示效果
- 往 往 是 为 了 单 独 的 去 控 制 某 个 关 键 的 内 容

```html
您的购物车有<sapn style="color: red;font-size: 40px">10</sapn>个商品 
```



### 加粗\<strong>

```html
<p><strong>这是段落中的文本。</strong></p>
```



### 分隔区块\<div> 

\<div> 标签可以把文档分割为独立的、不同的部分

\<div> 是一个块级元素。它的内容自动地开始一个新行

```html
<div>
  <p>这是段落中的文本。</p>
</div>
<div>
  <p>这是段落中的文本。</p>
</div> 
```



### 导航区块\<nav>



```html
<nav>
  <p>这是段落中的文本。</p>
</nav>
```

### 网页主体区块\<main>

```html
<main>
<p>这是段落中的文本。</p>  
</main>
```



## 表单标签



### 表单\<form>

 **HTML \<form> 元素**表示文档中的一个区域，此区域包含交互控件，用于向 Web 服务器提交信息

> - action  处理表单提交的URL(即数据被发送到的位置)。这个值可被 \<button>、\<input type="submit"> 或 \<input type="image"> 元素上的 formaction 属性覆盖。
>
> - method  提交方式   1.post:表单数据会包含在表单体内被发送给服务器 
>
>   ​                                  2.get:表单数据会附加在 action 属性的 URL 中，并以 '?' 作为分隔符 
>
>   ​                                  3.dialog:如果表单在 \<dialog> 元素中，提交时关闭对话框。此值可以被 \<button>、\<input type="submit"> 或 \<input type="image"> 元素中的 formmethod 属性覆盖.

```html
<!-- action=""则表单信息将提交到当前页面 -->
<form action="" method="post">
        <input type="text" />
    <button type="submit">提交</button>
</form>
```

> **表单提交注意事项**
>
> action 属性设置提交的服务器地址/资源
>
> method 属性设置提交的方式 GET(默认值)或 POST
>
> 表单提交的时候，数据没有发送给服务器的三种情况:
>
> (1)表单某个元素项(比如text,password)没有 name 属性值
>
> (2)单选、复选（下拉列表中的 option 标签）都需要添加 value 属性，以便发送给服务器
>
> (3)表单项不在提交的 form 标签中

---





### 单行输入框\<input/>

> - type          事件的类型 【 type=text 是文件输入框；   --
>
>   ​                                          type=password 是密码输入框； --输入内容不可见,以黑点显示
>
>    										 type=radio 是单选框； --name属性可以对其进行分组，checked="checked" 表示默认选中
>
>   ​										  type=checkbox 是复选框；--checked="checked" 表示默认选中
>
>   ​                                         type=reset 是重置按钮 --value属 性修改按钮上的文本
>   ​                                         type=submit是 提交按钮 --value属 性修改按钮上的文本
>   ​                                         itype=button是按钮--value属性修改按钮上的文本
>
>   ​                                          type=file是文件上传域
>
>   ​                                          type=hidden 是隐藏域 --当要发送某些信息 ，而这些信息 ，不需要用户参与，就可以使用隐藏域 】  
>
> - placeholder   占位文本提示用户,点击输入框并输入内容后消失
>
> - name       输入框的名字,防止提交数据时和其他输入框混乱
>
> - value       预输入

```html
<input type="text" placeholder="昵称" name="nick" value="小明" disabled />

<!-- type="password" 使输入内容不可见,以黑点显示 -->
<input type="password" name="password" placeholder="密码" />
```



### 单行输入框-文件上传域

当\<input/> 标签的 type="file" 时，表文件上传

```html
<input type="file" name="file" />
```



### 单行输入框-单选/复选框

> 当\<input/> 标签:  type=radio 是单选框； 
>
> name属性可以对其进行分组 ,
>
> checked="checked" 表示默认选中

```html
<!-- type属性表示表单元素的类型，name属性表示表单元素的名称，value属性表示表单元素的值 -->

<!--同一问题要单选框同名-->
<input type="radio" name="gender" value="male" />
<input type="radio" name="gender" value="female" />

<!--点击文字也可以选择-->
<label> <input type="radio" name="gender" value="male" />男 </label>
<label> <input type="radio" name="gender" value="female" />女 </label>
<!--或-->
<input id="male" type="radio" name="gender" value="male" />
<label for="male">男</label>
<input id="female" type="radio" name="gender" value="female" />
<label for="female">女</label>
```

>  当\<input/> 标签: type=checkbox 是复选框；
>
> checked="checked" 表示默认选中

```html
<label> <input type="checkbox" name="interest" value="coding" />编程 </label>
<label> <input type="checkbox" name="interest" value="other" />其他 </label>
```



### 单行输入框-重置/提交按钮

>  当\<input/> 标签: type=reset 是重置按钮 --value属 性修改按钮上的文本

```html
 <input type="reset" value="重置"/> 
```

> 当\<input/> 标签: type=submit是 提交按钮 --value属 性修改按钮上的文本

```html
<input type="submit" value="提交"/>
```









### 多行输入框\<textarea>

> - rows    行数(行高)
> - cols    文本域可视宽度
> - name属性表示表单元素的名称，placeholder属性表示表单元素的占位文本

```html
<textarea  name="sign" rows="5" cols="30" placeholder="请输入个性签名"> </textarea>
```



### 按钮\<button>

在软件开发和用户界面设计中，“button”（按钮）是一种常用的交互元素，它可以触发特定的动作或执行特定的操作。

> - type="button"   表示该按钮是一个普通按钮，点击按钮时不会触发表单提交或其他默认行为。这种类型的按钮常用于执行与表单无关的自定义操作，例如展示弹窗、切换视图等
> - type="submit" 表示该按钮是一个提交按钮，点击按钮时会触发表单的提交操作。通常用于将表单数据提交到服务器进行处理，比如登录、注册等需要提交数据的场景。
> - type="reset" 表示该按钮是一个重置按钮，点击按钮时会将表单中的所有字段重置为默认值。这种按钮通常用于清空用户填写的表单数据，让用户可以重新填写。
>
> ---
>
> 1. id：指定按钮的唯一标识符，用于JavaScript等操作。
> 2. value：指定按钮的值，将作为表单提交时携带的数据，默认为空。
> 3. disabled：禁用按钮，使其不可点击。
> 4. autofocus：自动聚焦按钮，页面加载后会自动定位到这个按钮。
> 5. form：指定按钮所属的表单，可与form元素关联。
> 6. formaction：指定提交表单时要发送的URL。
> 7. formnovalidate：指示是否取消表单的验证。
> 8. formtarget：指定将响应发送到的目标窗口或帧。
> 9. onclick：定义按钮被点击时执行的JavaScript代码。

```java
<button type="submit">注册</button>
```





###  选项菜单\<select> 

每个选项用\<opyion>表示，一组选项用\<select>包裹

```html
<!--单选-->
<select name="career">
  <option value="default">请选择职业</option>
  <option value="staff">公司职员</option>
  <option value="freelancer">自由职业者</option>
  <option value="student">学生</option>
  <option value="other">其他</option>
</select>


<!--多选添加multiple-->
<select name="career" multiple>
  <option value="default">请选择职业</option>
  <option value="staff">公司职员</option>
  <option value="freelancer">自由职业者</option>
  <option value="student">学生</option>
  <option value="other">其他</option>
</select>

<!--注意：如果选择公司职员则提交信息是career:staff-->
```



### **设置只读输入框**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1670827104489-a19b08b3-bd58-466d-af1b-9675c2aa01f3.png" alt="image.png" style="zoom:67%;" />

```html
<input type="text" placeholder="昵称" name="nick" value="小明" disabled />

<input type="text" placeholder="昵称" name="nick" value="小明" readonly />
```





# CSS

 CSS 指的是层叠样式表 (CascadingStyleSheets)

官方文档:https://www.w3school.com.cn/css/index.asp

---

**为什么需要 CSS**

1.  在没有 CSS 之前，我们想要修改 HTML 元素的样式需要为每个 HTML 元素单独定义样式属性，费心费力。所以 CSS 就出现了
2. 使用CSS将HTML页面的 内容与样式分离提高web开发的工作效率(针对前端开发)
3. CSS可以让 html 元素(内容)+ 样式(CSS)分离，更好的控制页面

---



## 文档美化

标签添加声明 style=" "各属性用封号隔开

> **常见属性**

```tex
font-size      字体大小
font-weight    字体加粗
color          字体颜色
text-align     对齐方式center居中 left左 right右
line-height    行高（设置和div同高，可以获得文字上下居中效果）
letter-spacing 字间距
text-shadow    文字阴影
```

![image.png](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1676801397655-6eaacc73-481f-4376-9047-5b88d3714bf4.png)

---



## CSS 引用-内部/外部样式

**内部样式**

> 1.在\<head>标签内声明\<style>标签
>
> 2.将相同标签的样式写在同一个大括号内，大阔号外加上标签名

```html
<style>
p {
  font-size: 16px;
  color: #ffffff;
}
</style>
<!--意味着以后每一个p标签都是这个样式-->
```

---

**外部样式**

> 1.创建.css文件
>
> 2.建立html和css文件的联系，即在\<head>中用\<link>标签引入css文件
>
> 3.css文件格式即为内部样式第二条
>
> ---
>
> - rel属性  规定当前文档与被链接文档的关系
> - stylesheet 是被所有浏览器支持的文档外部样式表
> - type  属性规定了被链接文档的MIME类型，值一般为text/css 该类型为样式表
> -  href  属性描述链接的地址

```html
<link rel="stylesheet" type="text/css" href="index.css" />
```



## 相对/绝对路径

**绝对路径**

> 绝对路径指的是文件在硬盘上真正存在的路径

```html
<img src="E:\images\beauty.jpg" />

<link rel="stylesheet" href="E:\style\css\index.css">
```

---

**相对路径**

> 相对路径就是相对于文件自身位置，去寻找要引入的资源位置，文件自身位置即"`./`"

```html
<link rel="stylesheet" href="./index.css">
<!-- 或者./去掉也可以，效果是一样的 -->
<link rel="stylesheet" href="index.css">

<!--"../"是回到上一级目录，即到当前文件的上级目录中，如果有多层，就用多个../-->
<link rel="stylesheet" href="../index.css">
<link rel="stylesheet" href="../../index.css">
<link rel="stylesheet" href="../css/index.css">
```



## 选择器

选择器具有重叠性，名字相同的会进行添加以及覆盖（后面的会覆盖前面的，和引用顺序无关，只和定义顺序有关）



### 标签选择器

```html
h3 {
  font-size: 25px;
  color: #330867;
}
h3 {
  font-weight: 700;
  color: red;
}
 <!--font-weight属性在之前的h3标签里没有写，那么这里就会添加新的效果
   color这个属性前面已经定义了，这里再写，就会覆盖前面的字体颜色-->
```



### 类选择器

> 一个标签可以增加多个类，类名之间用空格隔开，同属性覆盖只和定义顺序有关

```html
<!--定义（内外皆可）-->
.article {
  color: red;
  font-size: 14px;
}

<!--使用-->
<p class="article">
  class是定义类的关键字，article是类名，类名可以任意，但是要符合规范
</p>


<!--一个标签可以增加多个类，类名之间用空格隔开，同属性覆盖只和定义顺序有关-->
<p class="common color font-size">
  common设置通用样式，color设置特殊颜色，font-size设置特殊字体大小
</p>
```



### id选择器

> id选择器只会在文档中出现一次，不允许重复使用

```html
<!--定义-->
#p-item {
  font-size: 24px;
  font-weight: 400;
}

<!--使用-->
<p id="p-item">这是一段文字</p>
<a href="#" id="link">点击进入详情</a>
```



## 高级选择器

### 后代选择器

后代选择器是对所有后代生效

```html
<!--选择所有p标签内部的所有span标签-->
p span{}

<!--选择所有p标签内部的所有类名为spanItem的标签 -->
p .spanItem{}

<!--选择id名为password的标签内部所有类名为box的元素内部的所有p标签-->
#password .box p{}
<!--html-->
<ul class="first-ul">
    <li>苍苍竹林寺，杳杳钟声晚。</li>
    <li>荷笠带斜阳，青山独归远。</li>
</ul>

<!--css-->
ul li {
    /* 去除li标签前面的小圆点 */
    list-style: none;
    font-size: 22px;
}
.first-ul li {
    color: rgb(212, 166, 28);
}
```



### 交集选择器

```html
<!--在所有a标签中，类名为special的标签-->
a.special{}
```



```html
<!--html-->
<ul>
    <li><a href="" class="special">电子产品</a></li>
    <li><a href="">家居服饰</a></li>
    <li><a href="">电竞手办</a></li>
    <li><a href="" class="special">家装服务</a></li>
    <li><a href="">房屋出租</a></li>
</ul>


<!--css-->
<!--ul标签内部的 所有li标签内部的 a标签中的 类名为special的标签s-->
ul li a.special {
    color: orangered;
}
```



### 子选择器

后代选择器是对所有后代生效，子选择器只对子生效

```html
<!--子选择器只对p标签内部的子标签有效（即下一级标签）-->
p>span {
    color: orangered;
}
<!--html-->
<p>
    <span>Span1   <span>Span2 </span>   </span>
</p>


<!--css-->
<!--只会更改p标签的下一级span标签，即只更改sapn1-->
p>span {
    color: orangered;
}
```



### 并集选择器

给不同的标签，或不同的类名标签添加相同的样式

```html
<!--在标签名或类名后用逗号隔开-->
<!--给类名为box、phone，标签名为p、h3添加相同的属性-->
.box,p,h3,.phone{}
```



## 选择器优先级

**单个选择器优先级：**行内样式 >ID 选择器 >class 选择器 > 元素选择器

---

**多个选择器优先级** 根据选择器的权重叠加性，优先级越高，权重越大。权重高的覆盖权重低的（层叠性只有权重相同才有效）

---

设：ID选择器权重100，  类选择器权重10， 标签选择器权重1。

当有如下两个选择器：

```css
ul li p{
    color:blue;
}

p{
    color:red;
}
```

```html
<ul>
    <ul>
        <p>haha</p>
    </ul>
</ul>
```

很显然，上面的选择器权重更高，所以p为blue

---

当有如下两个选择器：

```css
ul li {
    color:blue;
}

p{
    color:red;
}
```

<ul>
    <ul>
        <p>haha</p>
    </ul>
</ul>

虽然上面选择器更高，但没有选中p标签，故权重再高也没用，故p为red。

---



## CSS盒模型

网页布局就是一个个大小不一的小块构成，要画一个矩形，就需要<div>标签

<div>标签就是一个干净透彻的矩形

```tex
background-color  背景颜色

padding           内边距（-上下左右）

box-sizing        计算元素总宽、高 默认值content-box（宽=内容的宽，高=内容的高）
                                         border-box（宽=border+padding+内容的宽，高同理）

border            边框（-上下左右）（粗细width 颜色color 线型style【实线solid 虚线dashed】                
border-bottom: none; 无边框
border-radius: 12px; 圆角边框

            x偏移|y偏移|阴影模糊半径|阴影扩散半径| 阴影颜色 0.2是透明度
box-shadow: 2px   2px   2px           1px       rgba(0, 0, 0, 0.2);     边框阴影
 

margin            外边距（-上下左右）

display           行内元素与块元素互转（块元素默认属性值是block，行内元素默认属性是inline）

display:linline-block;   块元素同行显示  

word-spacing: -50px;     意为单词间的距离 在父元素中添加，可去除两个同行块元素之间的空格

background-image  为一个元素设置一个或者多个背景图像
```

---

**元素水平居中**

如果内部是行内元素，我们可以在父容器上使用 ：

```css
text-align：center
```

如果内部是块元素，我们可以在子容器上使用：【如果此元素不是块元素，需要设置 display：block 使其变为块元素】

```css
margin:0 auto
```

---

**元素垂直居中**

使用margin完成垂直居中

```css
margin-top=(model高度-img高度)/2
```

可以flex实现元素垂直居中。







## 背景/图片

> 设置div的背景以及长宽

```html
.box {
  width: 200px;
  height: 100px;
  background-color: purple;
}
```

> 设置背景图片

```html
<--插入背景图-->
background-image：url(https://logo.png);

<--禁止图片重复-->
background-repeat: no-repeat;

<--图片居中-->
background-position: center;

<--图片放大到最大宽高，使得完全适应内容区域-->
background-size:contain;
```

---

> **设置背景图片重复-background-repeat值：**

| 值        | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| repeat    | 这是默认值。如果背景图片比容器小，将在垂直和水平方向进行重复 |
| repeat-x  | 背景图片只在水平方向重复                                     |
| repeat-y  | 背景图片只在垂直方向重复                                     |
| no-repeat | 背景图片只显示一次，不重复                                   |

> **设置背景图片布局-background-position值：**

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1676808788121-81497358-a6d4-4230-adb6-6b7f8b92137c.png)

> **设置背景图片大小-background-size值：**

| 值      | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| cover   | 把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。背景图像的某些部分也许无法显示在背景定位区域中。 |
| contain | 把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。 |
| xpx ypx | 手动设置宽度和高度                                           |
| x%  y%  | 手动设置宽度和高度相对于容器的百分比                         |





## 内边距padding

> 内边距即div中文字和边框的距离，没有设置默认为0

```css
.box {
    padding:20px;          /*上下左右所有内边距*/  

    padding-top: 20px;     /*上内边距*/
    padding-bottom: 20px;   /*下内边距*/
    padding-left: 20px;     /*左内边距*/
    padding-right: 20px;   /*右内边距*/

<!--简写按照 上、右、下、左 顺序 无值的默认和对值相同-->
    padding:20px 20px 20px 20px;    /*上下左右一样内边距*/
    padding: 20px 30px;               /*上下一样，左右一样内边距*/   

}
```





## 边框border

```css
.box {
  border: 2px solid blue;   /*值的顺序可以忽略*/
}

.box {
  /* 添加顶部border */
  border-top: 1px solid black;
  /*添加右侧border*/
  border-right: 3px solid orange;
  /*添加底部border*/
  border-bottom: 5px dashed pink;
  /*添加左侧border*/
  border-left: 10px dashed purple;
}
```

---

> **利用层叠性设置边框**

情景：要设置一个矩形，矩形的左右上边框样式相同，下边框样式不一样

解决：使用属性层叠性 【1.统一设置矩形的所有边框样式；2.重新设置一个下边框的样式来层叠掉统一设置的边框的样式】

```css
.box {
  /*设置矩形的宽*/
  width: 300px;
  /*设置矩形的高*/
  height: 300px;
  /*设置矩形的背景颜色*/
  background-color: white;
    
  /*设置矩形的边框*/
  /*统一设置矩形的所有边框样式*/
  border: 2px solid black;
  /*重新设置一个下边框的样式来层叠掉统一设置的边框的样式*/
  border-bottom: 5px solid orange;
}
```

---

> **无边框-圆角边框-边框阴影**

```css
/*--无边框设置*/
.box {
  border-bottom: none;
}

/*圆角边框设置，值是弧度*/
.box {
  border-radius: 12px;
}

/*圆角边框分开设置，值是弧度*/
.box {
  border-top-left-radius: 5px;  左上
  border-top-right-radius: 10px;右上
  border-bottom-left-radius: 20px;左下
  border-bottom-right-radius: 15px;右下
}

/*边框阴影设置*/
.box {
  /* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影扩散半径 | 阴影颜色 0.2是透明度*/
  box-shadow: 2px 2px 2px 1px rgba(0, 0, 0, 0.2);
}
```

**边框阴影的实现原理可以看作是在矩形下面有一个重叠，同样大小的矩形，如果它在x，y轴上移动，就会有阴影效果。**

- x偏移量：在x轴上移动，向右为正；
- y偏移量：在y轴上移动，向下为正；
- 阴影模糊半径：就是边线清晰度；
- 阴影颜色：就是矩形下面矩形的背景色；

---





## 外边距margin

**所谓外边距，就是矩形与矩形的距离**

```css
.box{
    /*总写*/
    margin: 20px;

    /*分开写*/
    margin-top: 20px;
    margin-right: 20px;
    margin-bottom: 20px;
    margin-left: 20px;
}
```

---

> **盒子左右居中**

margin还有一个左右就是使盒子可以在父盒子中左右居中，但是有一个前提，必须有宽度

```html
<div class="father">
    <div class="son"></div>
</div>
```

```css
.father{
    width: 400px;
    height: 200px;
    border: 1px solid #ccc;
}
.son{
    width: 200px;
    height: 100px;
    margin: 0 auto;
    border: 1px solid #ccc;
}
```





## 行内元素与块元素互转display

**标签是行内元素还是块元素，其根本是标签自带的默认display属性**

- 块元素display默认属性值是block
- 行内元素display默认属性是inline

**如果给标签的display值为none，那么这个标签就会消失不显示**

---

> **行内转块**

```html
<span class="demo"> 这是一个span标签 </span>
```

```css
.demo {
  /*将span标签转换成块元素*/
  display: block;
  width: 300px;
  height: 100px;
  background-color: #fff2cc;
}
```

> **块转行内**

```html
<div class="demo">这是一个span标签</div>
```

```css
.demo {
  /*将div标签转换成行内元素*/
  display: inline;
  /* 转换成行内元素以后，宽、高的设置就会失效，即使我们仍然设置了它们 */
  width: 300px;
  height: 100px;
  /* 背景颜色也不会是300*100范围，而是文字有多少面积，背景颜色就又多少面积 */
  background-color: #fff2cc;
}
```

> **linline性质**

1.行内元素不能设置宽高

2.行内元素可以设置padding

3.行内元素可以设置左右margin，但不能设置上下margin

---





## CSS定位 position

**position属性用于定位DOM元素，修改DOM元素的布局**

DOM：文档对象模型。 DOM是Javascript看到其包含页面数据的方式。它是一个对象，包括HTML / XHTML / XML的格式，以及浏览器状态。 DOM元素类似于页面上的DIV，HTML，BODY元素。可以使用CSS向所有这些类添加类，或使用JS与它们进行交互



### Position-static 默认定位

浏览器会自动给所有DOM元素添加上：

```css
position: static
```



### Position-relative 相对定位

**在当前位置进行偏移，同时不影响整体布局（原位置保留）,和margin不同，margin会影响其他地方发生变化**

> - relative 先遵循默认的文档流布局，也就是static布局，然后就在不改变页面布局的前提下根据上下左右调整位置。
> - 元素的上下左右调整都是相对于当前元素static布局的位置进行调整。 【即偏移自身位置】

```css
<!--距离原来的左侧和顶部偏移50px-->
.first {
  position: relative;
  left: 50px;
  top: 50px;
}
```



### Position-absolute 绝对定位

**脱离文档流，变成第二个图层，不再保存原位置，其后的所有DOM元素会自动占据它的原位置，偏移**

**absolute 绝对定位不为元素预留空间，通过指定元素相对于最近的非static定位祖先元素的偏移，来确定元素位置**

---

相对于最近的非static定位祖先元素的偏移： 【最近 ，非static定位 ，祖先元素】：

设有一张图片元素：

```html
<img class="frist" src="xxx"/>
```

```css
.first {
  position: absolute;
  left: 50px;
  top: 50px;
}
```

我们发现它是absolute 布局，因此寻找到它的父节点：

```html
<div class="img_box">
```

我们发现此元素并未配置Position属性，默认为static ，不符合非static要求，所以继续寻找父节点 :【若非static，则直接偏移】

```html
<body>
```

body已经没用父节点了，所以按照body的位置进行偏移

---





### Position-fixed 固定定位

**将一个元素固定在屏幕上，会脱离文档流**

**固定定位和绝对定位类似，但元素的包含块为屏幕视口。固定元素不为元素预留空间，而是通过指定元素相对于屏幕视口的位置来指定元素位置，元素的位置在屏幕滚动时不会改变**

```css
/*距离屏幕左30上30处固定*/
h1 {
  position: fixed;
  left: 30px;
  top: 30px;
  z-index: 1;
  color: yellowgreen;
}
```



---

> **图层优先级z-index**

**HTML页面是由多个图层构成，通过z-index决定谁覆盖谁**

1. 默认非static的元素z-index都为0
2. z-index越大，优先级越高，越在最上面
3. 同样的z-index，在HTML中元素越靠后，越在最上面

```html
<h1>MOUNTAIN</h1>
<div class="img-box"></div>
```

以上实例：由于h1 和div都是非static，所以z-index都是0,而h1在文档流前面，因此会 被后者遮挡

---





### Position-sticky 粘性定位

**结合了相对定位和固定定位，不脱离文档流，在页面滑动到指定距离后固定在屏幕上**

```css
/*在页面向上滑动50px时，h1固定在屏幕上*/
h1 {
  position: sticky;
  color: yellowgreen;
  top: 50px;
  z-index: 1;
}
```



### float 浮动-左右排版

**float场景：**

1. 如果想要一组元素同时靠左靠右对齐，可以使用float
2. 如果想要文字围绕图片，可以使用float

```css
.logo {
  float: left;
}

.avatar {
  float: right;
}
```



## 渐变背景色

> **background的新值--linear-gradient**
>
> 第一个参数是渐变方向
>
> 第二个参数是开始颜色
>
> 第三个参数是结束颜色

```css
background: linear-gradient(to right,#cccccc,#cccccc);
```

---

> **渐变方向-使用语义化英语实现，具有如下值：**

- to right / to left      【向右/向左渐变】
- to top / to bottom    【向上/向下渐变】
- to right bottom / to right top   【向右下/向右上渐变】
-  to left bottom / to left top  【 向左下/向左上渐变】

---

> **渐变位置--渐变不是一定从开始到结束，可以设置各种中间状态**

实例：在30%~70%位置进行渐变---可以在每个色值后面根一个百分比，xp，来约定变色起止位置

```css
background: linear-gradient(to bottom,
rgba(0,0,0,0.05) 0%,rgba(0,0,0,0.15) 50%,rgba(0,0,0,0.05) 50%,rgba(0,0,0,0.15) 100%);
```

![image-20230829202241798](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230829202241798.png)

---

> **背景渐变-自上而下**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1676808067862-5320ba69-605c-4bf6-9237-1d8aa5a7013a.png" alt="image.png" style="zoom:150%;" />

----





# ############JavaScript#################

**官方文档：**https://www.w3school.com.cn/js/index.asp

![image-20240131155327593](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240131155327593.png)

---

**js特点：**

- js是一种解释型脚本语言，c语言先编译后执行，而js是在程序运行过程中，逐步进行解释；
- js是一种基于对象的脚本语言，可以创建和使用对象；
- js是弱类型，对变量的数据类型不做严格要求，变量的数据类型在运行过程中可以变化；
- js可以不带封号，带也可以，建议写上

---

**js弱类型数据类型：**

- 数值类型：number
- 字符串类型：string
- 对象类型：object
- 布尔类型：boolean
- 函数类型：function

---

**js特殊值：**

- undefined  变量未赋初始值时，默认undefined
- null  空值
- nan     （not a number）   非数值

---

**外部引用：**js文件和css一样，写在html以外

```html
<!--注意：写在body的最下面-->
<script type="text/javascript">src="index.js"</script>

<script type="text/javascript" src="hello.js"></script>
```

---

**内部使用：** js代码可以写在scrip标签中   --type="text/javascript" 标识这个脚本（scrip）类型是javascript

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var name="wang"
        alert(name)  //弹窗输出
    </script>
</head>
```



# 常用代码集合

```toml
console.log(i);                    输出
alert(i)                           弹窗输出
typeof i                           返回数据的类型 （NAN非数值型，number数字，string字符串）
parseInt(number);                  将小数字符串、整数字符串、小数转化为整数
parseFloat(number)                 将小数字符串转换为小数
变量名.unshift('要添加的值')         数组头插
变量名.push('要添加的值')            数组尾插
变量名.shift('要删除的值')           数组头删
变量名.pop('要删除的值')             数组尾删
splice（起始位置，步长，要替换的值）  数组修改
indexOf（要找的值，开始寻找的位置）   数组值下标查找
```



# 字符串

**模板字符串核心是反引号（\` `）和占位符${变量名} ，反引号作用是将字符串和变量包裹，占位符是在字符串中插入变量**

> 占位符-${变量名}

```javascript
let firstName = "胡";
let lastName = "雪岩";
let say = `大家好，我姓${firstName}，名${lastName}`;
console.log(say);
```

> 多行字符串拼接，自带回车

```javascript
let str = `春眠不觉晓
处处闻啼鸟
夜来风雨声
花落知多少`;
console.log(str);
```

> 字符串使用表达式

```javascript
let number1 = 20;
let number2 = 10;
console.log(`两个数的和是：${number1 + number2} 。`);
```

> 字符串三元表达式

```javascript
let str = `这里是${true ? "江苏" : "浙江"}-${true ? "南京" : "常州"}`;
console.log(str); /* 这里是江苏-南京*/
```





# 变量隐式转换与强制类型转换

> 数字字符串加数字，数字隐式转换为字符串，则+为拼接

```javascript
console.log(20 + "20"); // 2020
```

> 数字字符串与数字做非加法运算，字符串隐式转换为数字

```javascript
console.log("20" - 10); // 10
console.log(10 * "10"); // 100
console.log(10 / "2"); // 5
```

> 数字字符串与数字字符串做非加法运算，字符串隐式转化为数字

```javascript
console.log("20" - "10"); // 10
console.log("20" / "10"); // 2
console.log("20" * "10"); // 200
```

> 强制类型转换，注意：小转整要舍弃小数

```javascript
let number = "20.9";
let converNumber = parseInt(number);   //  将number转换为整数类型,舍弃小数 20

let number = "20.9";
let converNumber = parseFloat(number); //将小数字符串转换小数  20.9
```





# 数组操作-增删改查

> 头插法 --变量名.unshift('要添加的值')

```javascript
let arr=[];

let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.unshift('河海大学');
```

> 尾插法 --变量名.push('要添加的值')

```javascript
let arr=[];
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.push('河海大学');
```

> 指定位置增加 splice

```js
let arr=[];
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.splice(2, 0, '江西理工大学'); //在下标为2的元素开始，往后选择第0个元素替换，类似在下标为2位置增加一个
console.log(schools);
```

> 头删法--变量名.shift('要删除的值')

```js
let arr=[];
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.shift();
```

> 尾删法--变量名.pop('要删除的值')

```js
let arr=[];
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.pop();
```

> 指定位置删除 splice

```js
let deleteSchools = schools.splice(1);// 删除从下标为1的位置到结束位置的值，并返回被删元素
console.log(deleteSchools); 

let deleteSchools = schools.splice(0, 2);//删除从下标为0开始往后两个元素，并返回被删元素
console.log(deleteSchools);
```

> 指定位置修改 splice
>
> splice（）方法可以增删改
>
> splice（起始位置，步长，要替换的值）;

```js
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
schools.splice(2, 2, '江西理工大学');
console.log(schools); //选择下标为2开始，往后俩个元素替换为江西理工大学，结果：["清华大学", "北京大学", "江西理工大学"]
```

> 查询 indexOf（要找的值，开始寻找的位置），找不到返回-1

```js
/*indexOf（要找的值，开始寻找的位置），找不到返回-1*/
let schools = ['清华大学', '北京大学', '浙江大学', '同济大学'];
let result = schools.indexOf('大连理工');
console.log(result); // -1

let result2 = schools.indexOf('浙江大学', 3);
console.log(result2); // -1
```





# 二维数组创建-插入-删除

```javascript
/* 定义一个一维数组*/
let arr1 = [];
// 给一维数组里面添加数据
arr1[0] = '宇智波佐助';
let arr = [];
arr[0] = arr1; /*将一维数组添加到另一个数组中，形成二维数组*/



/*push方法插入*/
let arr = [];
arr.push([]);  /*将一个空数组添加到 arr */
arr[0].push('宇智波佐助'); /*将字符串 '宇智波佐助' 添加到 arr 中的第一个数组中，
                         /*数组 arr 现在包含一个子数组，该子数组包含了字符串 '宇智波佐助'*/

/*pop方法删除*/
arr[0].pop();
```



# 循环-for..in 与for..or

> for...in循环会访问数组每一项，i对应数组下标

```js
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];
for (let i in peppaFamily) {
  console.log(peppaFamily[i]);
}

```

> for...or循环会访问数组每一项，item对应数组每一项值

```javascript
let peppaFamily = ["佩奇", "乔治", "猪妈妈", "猪爸爸"];
for (let item of peppaFamily) {
  console.log(item);
}
```



# 函数-定义-调用-计数器

函数是由事件驱动的，或者当它被调用，执行的可重复使用的代码块

> **函数定义**

**语法**

```js
//第一种
function 函数名(形参列表){
    函数体
    return 表达式
}


//第二种
var 函数名=function(形参列表){
    函数体
    return 表达式
}

//调用
函数名（实参列表）
```

**实例**

```js
//作用：弹窗
function hi(){
    alert("hello")
}
```

> **函数调用**

**方法一：主动调用**

```js
function hi(){
    alert("hello")
}
//调用
hi()
```

**方法二：事件调用**  onclick事件触发调用

```html
<body>
<!-- onclick="hi()" 表示给按钮绑定onclick 事件 -->
<button type="button" value="点击" onclick="hi()" >点击</button>
</body>
<script type="text/javascript" src="hello.js"></script>
```

---

> **js函数注意事项**

1. **JS 中函数的重载会覆盖掉上一次的定义  【可以理解为 js没有重载】**

```js
function hi(){
    alert("hello")
}

function hi(name){
    alert("hello "+name)
}

//调用会显示 hello undefined  因为这个hi()调用的是有参的函数，而又未传值，故为undefined
hi();  
```

2. **函数的 arguments 隐形参数（作用域在 function 函数内）**  

​		(1).隐形参数: 在 function 函数中不需要定义，可以直接用来获取所有参数的变量。

​		(2).隐形参数特别像 java 的可变参数一样。 publicvoidfun(int...args)

​		(3).js 中的隐形参数跟 java 的可变参数一样。操作类似数组

```js
function f1(){
console.log(arguments)  //输出：[Arguments] { '0': 1, '1': 2, '2': 3 }
}

//成功调用  function f1() == function f1(arguments)    arguments是数组，可以接收所有形参
f1(1,2,3)
```

**3.如果我们的函数有形参，在传入时，按照顺序赋值，并且所有数据都会被arguments 接收**

**4.如果形参数大于实参，则未匹配到值的形参会赋值为undefined**

---





​	











---

> **随机数生成**

```javascript
// num1 的范围是 [0.1, 1)
const num1 = Math.random() * 0.9 + 0.1;

// num2 的范围是 [100, 1000)
const num2 = Math.floor(num1 * 1000);
console.log(num2);
```

## 计数器1-延迟执行-setTimeout：

setTimeout函数用来指定某个函数或某段代码，在多少毫秒后执行，它返回一个整数，表示定时器编号，以后也可以用来取消这个定时器

---

> **基础语法 let timerId=setTimeout(函数名或代码，延迟时间/ms);   timeId是定时器编号**
>
> 第一个参数是代码，注意代码需用引号包裹，否则会立即执行代码
>
> 第二个参数是 1000，即 1000ms 后执行 console.log(2)

```javascript
console.log(1);
setTimeout('console.log(2)', 1000);


/**
 * 第一个参数是匿名函数
 * 第二个参数是 2000，即 2s 后执行 console.log(3)
 */
setTimeout(function () {
  console.log(3);
}, 2000);


// 第一个参数是函数名，注意函数名后不要加小括号“()”，否则会立即执行 print4
setTimeout(print4, 3000);
console.log(5);
function print4() {
  console.log(4);
}
// 首先定义计时总秒数，单位 s
let i = 60;

// 定义变量用来储存定时器的编号
let timerId;

// 写一个函数，这个函数即每次要执行的代码，能够完成上述的 1、2、3
function count() {
  console.log(i);
  i--;
  if (i > 0) {
    timerId = setTimeout(count, 1000);
  } else {
    // 清除计时器
    clearTimeout(timerId);
  }
}

// 首次调用该函数，开始第一次计时
count();
```



## 计数器2-无限调用-setInterval：

setInterval指定某个任务每隔一段时间就执行一次，也就是无限次的执行

---

**基础语法  let timer = setInterval(函数名或代码，延迟时间/ms);**

```javascript
let i = 60;
print();         //函数前置一次可以使得要打印的第一个数不延时
let timer = setInterval(print, 1000);

function print() {
  console.log(i);
  i--;
  if (i < 1) {
    clearInterval(timer);   //使得计时器有限次
  }
}
```





# 对象

> **常用方法**

```tex
delete person.name                  删除对象属性
person.gender = 'male';             添加对象属性以及值
Object.keys(person);                查看person对象属性，并返回由属性构成的数组
person.hasOwnProperty('name');      判断自身属性是否存在 

JSON.stringify(obj);                javaScript对象==>json格式

window.localStorage.setItem（）      数据存入网页 两参（'k','v'）
window.localStorage.getItem();       读取数据 一参（'k'）
window.localStorage.clear();         清除网页缓存

arr.join();                        以指定参数连接字符串，并返回
arr.reverse();                     将原数组倒序并返回新数组，不改变原数组
arr.sort(func);                     自定义排序，根据传入的参数函数func将数组成员排序
arr.map(func);                     根据传入的参数函数func对数组进行遍历并返回操作后的数组三参（数组成员，下标，整个数组）
arr.forEach(func);                 根据传入的参数函数func对数组进行遍历 三参（数组成员，下标，整个数组）

new Date();                        无参则获取当前时间 有参则生成特定时间对象
Date.parse();                      解析日期 返回该时间距离时间零点（1970-1-1 00：00：00的毫秒数）
dt.toJSON();                      时间对象转字符串

/*get获取时间  变get为set即为设置时间 */
dt.getTime();                     返回实例距离1970年1月1日00:00:00的毫秒数
dt.getDate();                      返回实例对象对应每个月的几号（从1开始）
dt.getDay();                        返回星期几，星期日为0，星期一为1，以此类推
dt.getFullYear();                     返回四位的年份
dt.getMonth();                    返回月份（0表示1月，11表示12月）
dt.getHours();                       返回小时（0-23）
dt.getMilliseconds();               返回毫秒（0-999）
dt.getMinutes();                    返回分钟（0-59）
dt.getSeconds();                     返回秒（0-59）
```



## 对象的创建-操作-增删改查-遍历

> **创建对象法一 -{}形式**

```js
let person = {
  //设置属性 逗号隔开
  name: 'henry',
  age: 18,
    
  //设置函数  函数名:function(){}
 run: function() {
    console.log('running');
  } 
}
```

---

> **创建对象法二 -通过 new object**

```js
//person是一个空对象
var person=new Object();
//增加属性
person.name="wang";
person.age=20;
//增加方法
person.say=function (){
    console.log( person.name+person.age);
}
//调用
person.say()
```

> **创建对象法三-使用构造函数创建对象**
>
> 1. 第一步：创建构造函数
> 2. 第二步：通过 new 创建对象实例

```js
// 第一步：创建构造函数
function People(name, age) {
  this.name = name;
  this.age = age;
}
// 第二步：通过 new 创建对象实例
let person = new People('henry', 18);
console.log(person);
```

---

> **查看对象的所有属性 即k**

```js
let keys=Object.keys(person);
Object.keys()  //查看对象属性，并返回由属性构成的数组
```

> **属性的删除和修改**

```js
/*删除某个属性*/
let person = {
  name: 'henry',
  age: 18
}
delete person.name;
console.log(person);  //{ age: 18 }
```

```js
/*添加某个属性*/
let person = {
  name: 'henry',
  age: 18
}
person.gender = 'male';  //{ name: 'henry', age: 18, gender: 'male' }
```

---

> **遍历属性**

**法一：直接for循环**

```js
let person = {
  name: 'henry',
  age: 18,
}

for (let key in person) {
  console.log('键名：' + key + '；键值：' + person[key]);
}
```

**法二：借助Object.keys遍历数组**

```js
let person = {
  name: 'henry',
  age: 18,
}
let keys = Object.keys(person);
for (let i = 0; i < keys.length; i++) {
  console.log('键名：' + keys[i] + '；键值：' + person[keys[i]]);
}
```



## 面向对象编程-创建-继承

> 类和对象创建

```javascript
//创建学生类
class Student{
    constructor(name){
        this.name=name;
    }
    hello(){
        alert('hello')
    }
}

//创建对象
var student1=new Student('xiaominng');
```

> 继承

```javascript
//创建学生类
class Student{
    constructor(name){
        this.name=name;
    }
    hello(){
        alert('hello');
    }
}

class Xiaoming extends Student{
      constructor(name,grade){
          super(name);
        this.grade=grade;
    }
    myGrade(){
        alert('myGrade');
    }
    
}

//创建对象
var student1=new Xiaoming('xiaominng',3);
```





## 实例---输出所有键值对

> **例题-输出所有键值对**

```javascript
let person = {
    name: 'henry',
    age: 18,
    family: {
      papa: 'jack',
      mama: 'mary',
      sister: 'jane'
    }
  };
  
  // 使用 for...in
  function byForIn(obj) {
    // 循环 obj（person）对象
    for (const key in person) {
      if (key === 'family') {
        const family = obj.family;
        // 循环打印 person.family 
        for (const familyKey in person.family) {
          console.log('键名:' + familyKey + '；键值:' + person.family[familyKey]);
        }
      } else {
        console.log(key + ':' + obj[key]);
      }
    }
  }
  console.log('使用 for...in:');
  byForIn(person);  


/*注意： person.family[familyKey]  和 person.family.familyKey不一样
点只能取方法中有的属性，不能去取遍历的值
*/
```



## 继承--判断属性是否存在--json与js转换

> **创建对象的三种方法**

```javascript
// 字面量
let o1 = {
  name: 'alice',
};

// 构造函数  除字面量和自定义构造方法创建对象外，还可以用js提供的构造函数object（）或者继承来创建对象
let o2 = new Object();
let o3 = new Object();

// 继承  
funtion O4() {
}; 
O4.prototype = o1; 
let o4 = new O4();
```

> **判断属性是否存在** 
>
> in运算符可以判断对象是否拥有某个属性（包括继承到的）

```javascript
let person = {
  name: 'henry',
  age: 18,
};
'name' in person;        //true;
'gender' in person;      //false;
'toString' in person;    //true;  tostring是obj对象，person继承自obj，所以也有
```

> 判断自身属性是否存在 hasOwnproperty （只看自身，不包括继承）

```js
let person = {
  name: 'henry',
  age: 18,
};

person.hasOwnProperty('name');     //true;
person.hasOwnProperty('gender');   //false;
person.hasOwnProperty('toString');  //false; person自身不存在tostring
```

> **json字符串与javaScript对象的转换**
>
> JSON.parse()：    json格式==>javaScript对象

```javascript
// 一个 JSON 字符串
const jsonStr =
  '{"sites":[{"name":"Runoob", "url":"www.runoob.com"},{"name":"Google", "url":"www.google.com"},{"name":"Taobao", "url":"www.taobao.com"}]}';

// 转成 JavaScript 对象
const obj = JSON.parse(jsonStr);
```

> JSON.stringify()：javaScript对象==>json格式
>

```js
const jsonStr2 = JSON.stringify(obj)；
```





# 内置对象

## Math对象-静态属性与静态方法

> **静态属性与静态方法**

```tex
/*math静态变量*/
Math.E // 常数e。
Math.LN2 // 2 的自然对数。
Math.LN10 // 10 的自然对数。
Math.LOG2E // 以 2 为底的e的对数。
Math.LOG10E // 以 10 为底的e的对数。
Math.PI // 常数π。
Math.SQRT1_2 // 0.5 的平方根。
Math.SQRT2 // 2 的平方根。


/*math静态方法 注：除random都需要传递合适参数*/
Math.abs() // 绝对值
Math.ceil() // 向上取整
Math.floor() // 向下取整
Math.round() // 四舍五入取整
Math.max() // 最大值
Math.min() // 最小值
Math.pow() // 指数运算
Math.sqrt() // 平方根
Math.log() // 自然对数
Math.exp() // e的指数
Math.random() // 随机数
```





## Storage接口-数据的存、取、清除

**查看存储情况：检查-->application-->local Storage;**

---

- storage接口用于脚本在浏览器中保存数据，两个对象部署了这个接口 window.sessionStorage 与 window.localStorage;

-  sessionStorage保存数据用于浏览器的一次会话（session）,但会话结束（通常是窗口关闭），数据被清空

-  localStorage保存的数据长期存在，下一次访问该网站，网页可以直接读取以前保存的数据

---

>  **主要看LocalStorage用法-数据的存、取、清除**
>

```javascript
/*数据的存入 setltem   window.localStorage.setItem（）方法接收两个参数，
分别是k和v，两个参数都是字符串，不是字符串的参数会被转化成字符串后再存入浏览器*/
window.localStorage.setItem('myLocalStorage', 'storage Value');


/*如果要存入的数据不是字符串，最好先转化为字符串，存入一个对象：*/
const obj = {
  name: 'henry',
  age: 18
}
const value = JSON.stringify(obj);
window.localStorage.setItem('myLocalStorage', value);



/*数据读取 getltem*/
window.localStorage.getItem('myLocalStorage');  //接收一个参数，即k



/*清除缓存 clear*/
window.localStorage.clear();
```





## String对象-看java基础的字符串函数笔记

由于java基础的字符串函数笔记已经记录的非常详细，这里就不写了

> **内置string对象**

```javascript
/*js原生提供三个包装对象-string ， number ， boolean*/

/*包装对象：原生对象可以把原始类型的值变成（包装成）对象*/
let v2 = new String('abc');
```





## Array对象-连接数组-排序-map/forEach遍历

> **连接数组 join()**
>
> - join方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回，不提供则默认逗号
> - join不会改变原数组

```javascript
let arr = [1, 2, 3, 4]; 
arr.join(" "); // '1 2 3 4'
arr.join(" | "); // "1 | 2 | 3 | 4"
arr.join(); // "1,2,3,4"

```

> **排序-倒序排列reverse()**
>
> - reverse方法用于颠倒排列元素，返回改变后的数组
> - reverse会改变原数组

```js
let arr = ["a", "b", "c"];
arr.reverse(); // ["c", "b", "a"]
arr; // ["c", "b", "a"]
```

> **排序 sort()**
>
> - sort方法队数组成员进行排序，默认是按照字典顺序排序。如果想自定义，可传入参数

```js
let arr = [
  { name: "jenny", age: 18 },
  { name: "tom", age: 10 },
  { name: "mary", age: 40 },
];

arr.sort(function (a, b) { //sort有一个函数作为参数，而函数的两参数分别是进行比较的成员，
  return a.age - b.age;    //当这个函数返回值大于0时，表示第一个成员应该排在第二个成员之后
});
console.log(arr);
```

> **有返回值遍历  map**
>
> - 接收一个函数，将数组的所有成员依次传入这个参数函数，最后把执行结果组成新数组返回

```js
let arr = [
  { name: "jenny", age: 18 },
  { name: "tom", age: 10 },
  { name: "mary", age: 40 },
];

// elem: 数组成员
// index: 成员下标
// a: 整个数组
const handledArr = arr.map(function (elem, index, a) {
  elem.age += 1;
  console.log(elem, index, a);
  return elem.name;
});

console.log(arr);
console.log(handledArr);
```

> **无返回值遍历  forEach**

```js
const handledArr = arr.forEach(function (elem, index, a) {
  elem.age += 1;
  console.log(elem, index, a);
  return elem.name;
});

console.log(handledArr);
```





## Data对象-获取--比较--解析--转换

> **Data对象-获取**

```javascript
/*获取当前时间  new Date()*/
let now = new Date();
console.log(now);

/*获取时间 get*/
let dt = new Date();
let year = dt.getFullYear();
console.log(year);

/*设置时间 set*/
let dt = new Date();
dt.setFullYear(2030);
console.log(dt);


/*生成特定时间对象*/
// 传入表示“年月日时分秒”的数字
let dt1 = new Date(2020, 0, 6, 0, 0, 0);
console.log(dt1);

// 传入日期字符串
let dt2 = new Date("2020-1-6");
console.log(dt2);

// 传入距离国际标准时间的毫秒数
let dt3 = new Date(1578240000000);
console.log(dt3);
```

> **Data对象-比较与运算**

```js
/*日期间运算与比较*/
let dt1 = new Date(2020, 2, 1);
let dt2 = new Date(2020, 3, 1);
// 求差值
let diff = dt2 - dt1;

// 一天的毫秒数
let ms = 24 * 60 * 60 * 1000;
console.log(diff / ms); // 31
console.log(dt1 > dt2); // false
console.log(dt1 < dt2); // true
```

> **Data对象-解析**

```js
/*解析日期字符串  Date.parse()  返回该时间距离时间零点的毫秒数*/
let dt = Date.parse("2020-1-6");
console.log(dt); // 1578240000000
```

> **Data对象-转换**

```js
/*时间对象转时间字符串  .toJSON()*/
let dt = new Date();
let dtStr = dt.toJSON();
console.log(dtStr); // 2020-01-03T09:44:18.220Z
```

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677140809053-6f5d636a-57af-47dd-8f7a-de8d0e6b58d0.png)



## Data例题-时间比较与格式化

> **例题：已知一组活动，按照时间排序，并格式化时间**

```javascript
let infoList = [
    {
      id: '20020101',
      startTime: '2020-01-01 13:00:00',
      description: '现在加入，即刻领取属于自己的英雄'
    },
    {
      id: '20032101',
      startTime: '2020-03-21 14:00:00',
      description: '寓教于乐一家亲，深入浅出一片心'
    },
    {
      id: '20011001',
      startTime: '2020-01-10 08:00:00',
      description: '让孩子在游戏中爱上学习'
    },
    {
      id: '19111101',
      startTime: '2019-11-11 09:30:00',
      description: '发行的不是游戏，是快乐'
    }
  ];

  // 排序
  infoList.sort((a, b) => {
    let atime=new Date(a.startTime);
    let btime=new Date(b.startTime);
  return atime - btime;
  });
  
  // 格式化时间
  infoList.forEach(info => {
    info.formattedDate = formatDate(info.startTime);

  });
  
  // 打印结果
  console.log(infoList);
  
  // 格式化时间的函数
  function formatDate(dtStr) {

    // 把时间字符串转为 Date 实例
let time=new Date(dtStr); 
    // 获取：年、月、日、时、分
    const year = time.getFullYear();
    const month =time.getMonth();
    const day = time.getDay();
    const hour = time.getHours();
    const min = time.getMinutes();
    return year + '年' + month + '月' + day + '日 ' + hour + '点' + min + '分';
  }
```







# BOM

## window窗口框架-属性与方法

https://developer.mozilla.org/zh-CN/docs/Web/API/Window

[//developer.mozilla.org/zh-CN/docs/Web/API/Window](https://developer.mozilla.org/zh-CN/docs/Web/API/Window)

---

> **window属性**

```js
Window.frameElement  //返回嵌入窗口的元素，如果未嵌入窗口，则返回 null。  【fo ren e le meng te】

Window.frames       //返回当前窗口中所有子窗体的数组。

Window.fullScreen    // 此属性表示窗口是否以全屏显示。
Window.history         //返回一个对 history 对象的引用。

Window.innerHeight //获得浏览器窗口的内容区域的高度，包含水平滚动条 (如果有的话)。

Window.innerWidth //获得浏览器窗口的内容区域的宽度，包含垂直滚动条 (如果有的话)。
Window.outerHeight //返回浏览器窗口的外部高度。

Window.outerWidth //返回浏览器窗口的外部宽度。

Window.location    //获取、设置 window 对象的 location，或者当前的 URL.

Window.locationbar //返回 locationbar 对象，其可视性可以在窗口中切换。

Window.localStorage //返回用来存储只能在创建它的源下访问的数据的本地存储对象的引用

Window.menubar ///返回菜单条对象，它的可视性可以在窗口中切换
```

> **window方法**

```javascript
Window.open()//打开一个新窗口。

Window.postMessage() //为一个窗口向另一个窗口发送数据字符串提供了一种安全方法，该窗口不必与第一个窗口处于相同的域中。

Window.print() //打开打印对话框以打印当前文档。

Window.prompt()   //返回用户在提示对话框中输入的文本。
```

---





## location-页面刷新与跳转

location代表当前页面的URL信息



**保存当前网页位置的信息**

**官方文档：**https://developer.mozilla.org/zh-CN/docs/Web/API/Location

---

> **刷新**
>
> location.reload()刷新页面 ，需要放到延迟函数里，不然会无限刷新

```javascript
/*下代码作用是每隔三秒刷新一次，原理是每次刷新都会重新加载js文件
*/
setTimeout(function () {
  window.location.reload();
}, 3000);
```

> **跳转--**跳转到新的网页
>
> 可以通过修改location，直接将网页赋值给location

```js
window.location = 'https://www.youkeda.com';

//也可以直接设置
location.assign( 'https://www.youkeda.com');
```



![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677224981880-09e828ad-c80f-456a-8715-47ba8cf13118.png)

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677225004253-5489578a-c987-4676-ac13-b17e6763f597.png)



## history-返回上一页与下一页

**存储窗口的历史记录-允许操作浏览器的曾经在标签页或框架里的访问的会话历史记录**

**官方文档：**https://developer.mozilla.org/zh-CN/docs/Web/API/History

---

> **history方法**

```tex
back()；
此异步方法转到浏览器会话历史的上一页，与用户单击浏览器的 Back 按钮的行为相同。等价于 history.go(-1)。
调用此方法回到会话历史的第一页之前没有效果并且不会引发异常。

forward()；
此异步方法转到浏览器会话历史的下一页，与用户单击浏览器的 Forward 按钮的行为相同。等价于 history.go(1)。
调用此方法超越浏览器历史记录中最新的页面没有效果并且不会引发异常。
```



## navigator-浏览器基本信息

**表示用户代理的状态和标识，也就是浏览器的基本信息 ，其中一个属性userAgent代表当前浏览器的用户代理**

> **输出浏览器信息**

```javascript
console.log(navigator.userAgent);
```



## screen-返回窗口属性

**返回当前渲染窗口中和屏幕有关的属性**

```javascript
// 打印电脑屏幕的宽度
console.log(window.screen.width);

// 打印电脑屏幕的高度
console.log(window.screen.height);
```





# 全局变量冲突

由于我们所有的全局变量都会绑定到Window上。如果不同的js文件，使用了相同的全局变量，会造成冲突。

如何减少？

```javascript
//唯一全局变量
var my={};

//定义全局变量
my.name='';
my.add=function(a,b){
    return a+b;
}
```

把自己的代码全部放入自己定义的唯一空间名字中，降低全局命名冲突







# DOM文档对象模型

DOM文档对象模型就是把文档中的标签、属性、文本转换成对象来管理

**DOM可以将web页面与脚本或编程语言连接起来**

![image-20230831150045617](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230831150045617.png)

---

> **常用代码**

```javascript
/* 注意：divDom都是自定义名*/
document.querySelector('div');  查询满足条件的第一个节点并返回节点 【kuai le se lai ke te】
document.querySelectorAll('input'); 查询满足条件的所有结节点，并返回数组，可通过下标访问

divDom.attributes; 获取节点所有属性，得到字典，可通过.key得value  【a chuo biu ci】
divDom.nodeType     
divDom.nodeName    获取标签名称
divDom.nodeValue   获取文本内容

divDom.outerHTML    获取整个DOM的html代码
divDom.innerHTML    获取DOM内部的html代码
divDom.innerText    获取DOM内部纯文本

divDom.firstChild    获取第一个子节点
divDom.lastChild     获取最后一个子节点
divDom.childNodes    获取所有子节点
divDom.parentNode    获取父节点

divDom.classList     获取所有class的名称

document.createElement('div'); 节点创建   【creat ai le meng te】
div.appendChild(txt);  将节点加入节点 默认最后（txt加入div）  【e peng cha er】
document.body.insertBefore(div,div1);将新节点div插入目标节点div1之前

img.setAttribute('k','v');   设置css属性

div.classList.add("foo", "bar", "baz");    添加class
div.classList.remove("foo", "bar", "baz");  移除class
```



## 获取根元素DOCUMENT

根元素会存储在全局变量window中，可以通过.document访问

![image-20230831150935590](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230831150935590.png)

```js
window.document;
```



## 选择器-查询满足条件的节点

> **查询满足条件的第一个节点 .querySelector**

```javascript
/*基础筛选条件，如果页面有多个class为subtitle的节点，则筛选结果就不大准确*/
'.subtitle';


/*加强版本，加上父亲筛选， 筛选 main标签下面 -> class为core的节点下面 -> 
class为subtitle的节点 ，结果是HTMLDivElement类型*/
document.querySelector('main .core .subtitle');


/*当我们得到subtitle元素后，还可以利用这个元素继续筛选，最终得到HTMLAnchorElement节点*/
let subtitle = document.querySelector('main .core .subtitle');
console.log(subtitle.querySelector('a'));
```

> **查询满足条件的所有节点 .querySelectorAll**

```javascript
/*改为querySelectorAll ,返回的是数组，可以通过下标访问  NodeList对象*/
document.querySelectorAll('input');
```





## DOM种类与属性信息获取

> **DOM种类**

```javascript
<!-- HTMLDocument 根文档 -->
<html>
  ……
</html>

<!-- HTMLDivElement DIV类型 -->
<div class="subtitle">
  ……
</div>

<!-- HTMLAnchorElement 超链接类型 -->
<a class="free-bright">免费靓号</a>

<!-- HTMLInputElement Input类型 -->
<input class="password" type="pasworkd" placeholder="请输入密码" />
```

**属性：**

1.元素节点  所有的标签都属于元素节点

2.特性节点  所有的标签属性属于特性节点

3.文本节点  所有的纯文本都属于文本节点

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677325631193-ff5e1ca8-214e-414c-83e1-a95bafb377ca.png)

```javascript
// 获取DIV节点的id属性
let attDom = divDom.attributes.id;
console.log(attDom.nodeType, attDom.nodeName, attDom.nodeValue);
```





## DOM内容-代码及文本获取

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677325784292-177f7451-0ff0-4078-95ec-10e198590074.png" alt="img" style="zoom:67%;" />

> 实例

```javascript
/*获取id为test的div内容*/
let divDom = document.querySelector('div#test');
console.log(divDom.outerHTML, divDom.innerHTML, divDom.innerText);
```

> 注意

```js
/*innerHTML值是DOM的内部代码，设置为空可以清空一个节点的所有后代内容 同时也可以添加纯文本*/
dom.innerHTML = ' ';
dom.innerHTML = txt;
```



## DOM亲属-通过父子节点获取信息

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677302788445-7ccab5fc-f791-4119-ab1d-4d51d0bb75c4.png" alt="img" style="zoom: 67%;" />

> 实例

```javascript
let divDom = document.querySelector('div#test');
console.log(divDom.nodeType, divDom.nodeName, divDom.nodeValue);

// 获取DIV节点的第一个儿子节点，代表 '优课达' 这个字符串
let txtDom = divDom.firstChild;

//获取DIV节点的最后一个儿子节点，代表 <p>学的比别人好一点</p>
console.log(divDom.lastChild);

//获取DIV节点的所有子节点
console.log(divDom.childNodes);

//获取DIV节点的父节点
console.log(divDom.parentNode);
```











## DOM-css样式访问与数据额外存储

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677303008381-bce8fde7-6706-4e41-aae1-301437ba83ec.png)

> 实例

```javascript
const h1Dom = document.querySelector('h1');

//获取所有的class名称，并返回数组
console.log(h1Dom.classList);

//获取css样式
console.log(h1Dom.style);

//获取css样式中color的值
console.log(h1Dom.style.color);
```

---

> **数据属性：**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677303049430-ab760d52-6195-4541-b51d-ff1f936c387d.png" alt="img" style="zoom:67%;" />

```javascript
/*存储额外*/
<body>
  <article data-parts="3" data-words="1314" data-category="python">
    ...
  </article>   //article标签一般是用来存放文章
  <script src="./index.js"></script>
</body>


/*获取*/
const article = document.querySelector('article');
console.log(article.dataset);
```



## DOM操作-节点创建与插入及删除

> **节点创建 document.createElement**

```javascript
//创建div document.createElement
const div = document.createElement('div');

//设置标签(可选)
div.setAttribute('id','hehe');

//添加纯文本  document.createTextNode
const txt = document.createTextNode('优课达-学的比别人好一点');

//把文本放入div
div.appendChild(txt);

//把div放入body   appendChild是在某节点插入子节点，且是在所有子节点之后添加
document.body.appendChild(div);

//把div放入body并在div1之前    insertBefore(新节点,目标节点) //将新节点插入到目标节点之前
document.body.insertBefore(div,div1);
```

> **节点删除**
>
> 需要先获取父节点，再通过父节点删除自身

```html
<html>
	<div>
    	<p>hehe</p>
    </div>  
</html>



<script>
//1.获取父节点
var divDom = document.querySelector('div');

//2.获取自身
var pDom = document.querySelector('p');

//删除
divDom.removeChild(pDom);
</script>
```







## DOM操作-样式设置与增删

> **样式设置 .setAttribute**

```javascript
/*设置图片的css属性  style是k ，后面是v  注意是反引号*/
img.setAttribute('style', 'width: 100%; height: 100%;');

/*也可以通过. 单独替换某一个 注意是反引号 反引号内容不需要封号*/
dom.style.color = `xxxx`;
```

```js
//创建标签节点
var myScript= document.createElement('script');
//设置样式
myScript.setAttribute('type','text/javascript');
```

> **添加与删除class .classList**

```javascript
const div = document.createElement('div');
div.className = 'foo';

// 初始状态：<div class="foo"></div>
console.log(div.outerHTML);

// 使用 classList API 移除、添加类值
div.classList.remove("foo");
div.classList.add("anotherclass");

// <div class="anotherclass"></div>
console.log(div.outerHTML);

// 如果 visible 类值已存在，则移除它，否则添加它
div.classList.toggle("visible");

// add/remove visible, depending on test conditional, i less than 10
div.classList.toggle("visible", i < 10 );

console.log(div.classList.contains("foo"));

// 添加或移除多个类值
div.classList.add("foo", "bar", "baz");
div.classList.remove("foo", "bar", "baz");

// 使用展开语法添加或移除多个类值
const cls = ["foo", "bar"];
div.classList.add(...cls);
div.classList.remove(...cls);

// 将类值 "foo" 替换成 "bar"
div.classList.replace("foo", "bar");
```





## DOM解析xml

不管是 html 文件还是 xml 文件它们都是标记型文档，都可以使用 w3c 组织制定的 dom 技术来解析

document 对象表示的是整个文档（可以是 html 文档，也可以是 xml 文档）

---

 **DOM4J** 

- Dom4j 是一个简单、灵活的开放源代码的库(用于解析/处理 XML 文件)。Dom4j 是由早期开发 JDOM 的人分离出来而后独立开发。
- 与 JDOM 不同的是，dom4j 使用接口和抽象基类，虽然 Dom4j 的 API 相对要复杂一些， 但它提供了比 JDOM 更好的灵活性。
- Dom4j 是一个非常优秀的 JavaXMLAPI，具有性能优异、功能强大和极易使用的特点。 现在很多软件采用的 Dom4j
- 使用 Dom4j 开发，需下载 dom4j 相应的 jar 文件

---

> 读取XML文件,获得document对象

```java
//创建一个解析器
SAXReader reader=new SAXReader();

//XMLDocument
Document document = reader.read(new File("src/input.xml"));
```

> 解析XML形式的文本,得到document对象

```java
String text="<members></members>";
Document document=DocumentHelper.parseText(text);
```

> 主动创建document对象

```java
//创建根节点
Document document=DocumentHelper.createDocument();
Elementroot=document.addElement("members");
```

---

---

> 实例-演示Dom4j 对xml文件的增 删改查/遍历

**xml配置**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--
    1 xml :表示该文件的类型 xml
    2 version="1.0"版本
    3 encoding="UTF-8" 文件编码
    4. students: root元素/根元素, 程序员自己来定
    5. <student></student> 表示students一个子元素, 可以有多个
    6. id就是属性 name, age, gender 是student元素的子元素
-->
<students>
    <student id="100">
        <name>jack</name>
        <age>10</age>
        <gender>男</gender>
    </student>
    <student id="200">
        <name>mary</name>
        <age>18</age>
        <gender>女</gender>
    </student>
</students>

```

**java代码**

```java
public class Dom4j_ {

    /**
     * 演示如何加载xml文件
     */
    @Test
    public void loadXML() throws DocumentException {
        //得到一个解析器
        SAXReader reader = new SAXReader();
        //老师的代码技巧->debug 看看document对象的属性
        //分析了document对象的底层结构
        Document document = reader.read(new File("src/students.xml"));
        System.out.println(document);

    }

    /**
     * 遍历所有的student信息
     */
    @Test
    public void listStus() throws DocumentException {
        //得到一个解析器
        SAXReader reader = new SAXReader();
        //老师的代码技巧->debug 看看document对象的属性
        //分析了document对象的底层结构
        Document document = reader.read(new File("src/students.xml"));

        //1. 得到rootElement, 你是OOP
        Element rootElement = document.getRootElement();
        //2. 得到rootElement的student Elements
        List<Element> students = rootElement.elements("student");
        //System.out.println(student.size());//2
        for (Element student : students) {//element就是Student元素/节点
            //获取Student元素 的name Element
            Element name = student.element("name");
            Element age = student.element("age");
            Element resume = student.element("resume");
            Element gender = student.element("gender");

            System.out.println("学生信息= " + name.getText() + " " + age.getText() +
                    " " + resume.getText() + " " + gender.getText());
        }

    }

    /**
     * 指定读取第一个学生的信息 就是 dom4j+xpath
     */
    @Test
    public void readOne() throws DocumentException {

        //得到一个解析器
        SAXReader reader = new SAXReader();
        //老师的代码技巧->debug 看看document对象的属性
        //分析了document对象的底层结构
        Document document = reader.read(new File("src/students.xml"));

        //1. 得到rootElement, 你是OOP
        Element rootElement = document.getRootElement();

        //2. 获取第一个学生
        Element student = (Element) rootElement.elements("student").get(1);
        //3. 输出该信息
        System.out.println("该学生的信息= " + student.element("name").getText() + " " +
                student.element("age").getText() + " " + student.element("resume").getText() +
                student.element("gender").getText());

        //4. 获取student元素的属性
        System.out.println("id= " + student.attributeValue("id"));
    }

    /**
     * 加元素(要求: 添加一个学生到xml中) [不要求，使用少，了解]
     * @throws Exception
     */
    @Test
    public void add() throws Exception {

        //1.得到解析器
        SAXReader saxReader = new SAXReader();
        //2.指定解析哪个xml文件
        Document document = saxReader.read(new File("src/students.xml"));


        //首先我们来创建一个学生节点对象
        Element newStu = DocumentHelper.createElement("student");
        Element newStu_name = DocumentHelper.createElement("name");
        //如何给元素添加属性
        newStu.addAttribute("id", "04");
        newStu_name.setText("宋江");
        //创建age元素
        Element newStu_age = DocumentHelper.createElement("age");
        newStu_age.setText("23");
        //创建resume元素
        Element newStu_intro = DocumentHelper.createElement("resume");
        newStu_intro.setText("梁山老大");

        //把三个子元素（节点）加到 newStu下
        newStu.add(newStu_name);
        newStu.add(newStu_age);
        newStu.add(newStu_intro);
        //再把newStu节点加到根元素
        document.getRootElement().add(newStu);
        //直接输出会出现中文乱码:
        OutputFormat output = OutputFormat.createPrettyPrint();
        output.setEncoding("utf-8");//输出的编码utf-8

        //把我们的xml文件更新
        // lets write to a file
        //new FileOutputStream(new File("src/myClass.xml"))
        //使用到io编程 FileOutputStream 就是文件字节输出流
        XMLWriter writer = new XMLWriter(
                new FileOutputStream(new File("src/students.xml")), output);
        writer.write(document);
        writer.close();

    }

    /**
     * //删除元素(要求：删除第一个学生) 使用少，了解
     * @throws Exception
     */
    @Test
    public void del() throws Exception {
        //1.得到解析器
        SAXReader saxReader = new SAXReader();
        //2.指定解析哪个xml文件
        Document document = saxReader.read(new File("src/students.xml"));
        //找到该元素第一个学生
        Element stu = (Element) document.getRootElement().elements("student").get(2);
        //删除元素
        stu.getParent().remove(stu);
//        //删除元素的某个属性
//        stu.remove(stu.attribute("id"));
        //更新xml
        //直接输出会出现中文乱码:
        OutputFormat output = OutputFormat.createPrettyPrint();
        output.setEncoding("utf-8");//输出的编码utf-8
        //把我们的xml文件更新
        XMLWriter writer = new XMLWriter(
                new FileOutputStream(new File("src/students.xml")), output);
        writer.write(document);
        writer.close();
        System.out.println("删除成功~");
    }


    /**
     * //更新元素(要求把所有学生的年龄+3) 使用少，了解
     * @throws Exception
     */
    @Test
    public void update() throws Exception {

        //1.得到解析器
        SAXReader saxReader = new SAXReader();
        //2.指定解析哪个xml文件
        Document document = saxReader.read(new File("src/students.xml"));
        //得到所有学生的年龄
        List<Element> students = document.getRootElement().elements("student");
        //遍历, 所有的学生元素的age+3
        for (Element student : students) {
            //取出年龄
            Element age = student.element("age");
            age.setText((Integer.parseInt(age.getText()) + 3) + "");
        }

        //更新
        //直接输出会出现中文乱码:
        OutputFormat output = OutputFormat.createPrettyPrint();
        output.setEncoding("utf-8");//输出的编码utf-8

        //把我们的xml文件更新
        XMLWriter writer = new XMLWriter(
                new FileOutputStream(new File("src/students.xml")), output);
        writer.write(document);
        writer.close();
        System.out.println("更新成功~");
    }
}

```











# DOM事件

**事件是电脑输入设备与页面进行交互的响应**

**事件通常与函数配合使用，这样就可以通过发生的事件来驱动函数执行**

**官方文档：**https://www.w3school.com.cn/js/js_events.asp

---

> **事件**

```javascript
dom.addEventListener("input", function () {});  监听，input可换如下：
/*鼠标*/
click 点击事件
dblclick  双击事件
mousedown 在元素上按下任意鼠标
mouseenter 指针移到有事件监听的元素内
mouseleave 指针移除元素范围外（不冒泡）
mousemove 指针在元素内移动时持续触发
mouseover 指针移到有事件监听的元素或它的子元素内
mouseout 指针移出元素，或者移到它的子元素上
mouseup 在元素上释放任意鼠标按键


/*键盘*/
keydown 键盘按下事件
keyuo  键盘释放事件


/*视图*/
scroll 文档滚动
resize 窗口缩放事件


/*资源*/
load 资源加载成功事件
```

---

**事件分类：**

  1.事件的注册（绑定）

​		事件注册(绑定)：当事件响应(触发)后要浏览器执行哪些操作代码，叫事件注册或事件绑定

2. 静态注册事件

​		通过 html 标签的事件属性直接赋于事件响应后的代码，这种方式叫静态注册

3. 动态注册事件（dom）

​		通过 js 代码得到**标签的 dom 对象**，然后再通过 dom 对象.事件名 =function(){} 这种形式叫动态注册

---



## 加载完成事件onload

**onload：某个页面或图像被完成加载后完成事件**

> 实例body页面完成加载后触发-方法一 静态注册：

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        var say=function(){
            alert("body页面完成加载后触发-静态注册")
        }
    </script>
</head>
<!--静态注册-->
<body onload="say()">
</body>
```

> 实例body页面完成加载后触发-方法二 动态注册：
>
> 1. 在 js中 ，将页面窗口映射成  window dom对象
> 2.  window.onload 表示页面被加载完毕,后 面 的function (){}表示加载完毕后 ，要执行的函数/代码

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        
        window.onload=function(){
            alert("body页面完成加载后触发 -动态注册")
        }
        
    </script>
</head>
<body>
```





## 点击事件onclick

> 静态注册

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">
        
       var say=function (){
           alert("静态say")
       }
    </script>
</head>
<body>
  <!--静态注册-->  
<button onclick="say()">按钮</button>

</body>
```

> 动态绑定

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        //动态绑定需要 先设置页面加载完毕，然后才能在这其中才能写自己代码，否则不会生效
        window.onload = function () {
            
            //先拿到id=”“的button的dom对象
            var buttonOnClick = document.getElementById("but01");
            //再通过dom对象动态绑定点击事件
            buttonOnClick.onclick = function () {
                alert("say")
            }
            
        }

    </script>
</head>
<body>
<button id="but01">按钮</button>
```





## 失去焦点事件onblur

**鼠标移动出某范围，称为元素失去焦点**

> 静态注册 -实例鼠标移开输入框，则输入框中数据全大写

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        var myOnblur = function () {
            //先得到输入框的value--->得到对应的dom对象
            var content = document.getElementById("input01");
            //将其中的value数据全大写后再赋值到本身 。  toUpperCase()是字符串转换全大写的方法
            content.value = content.value.toUpperCase();
        }

    </script>
</head>
<body>

请输入:<input type="text" id="input01" onblur="myOnblur()"/><br>
</body>
```

> 动态绑定 -实例鼠标移开输入框，则输入框中数据全大写

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        //动态绑定需要先加载页面
        window.onload = function () {
            //先得到输入框对应的dom对象
            var elementById = document.getElementById("input01");

            //通过dom调用事件
            elementById.onblur = function () {
                //将其中的value数据全大写后再赋值到本身 。  toUpperCase()是字符串转换全大写的方法
                elementById.value = elementById.value.toUpperCase();
            }
        }

    </script>
</head>
<body>

请输入:<input type="text" id="input01"/><br>
</body>
```



## 内容发生改变事件onchange

onchange:域的内容被改变触发

> 静态注册

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        var myOnchange=function (){
          alert("输入框内容改变了")
        }

    </script>
</head>
<body>

请输入:<input type="text" id="input01" value="www" onchange="myOnchange()"/><br>

</body>
```

> 动态注册

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">


        //动态绑定需要先加载页面
        window.onload = function () {
            //先得到输入框对应的dom对象
            var elementById = document.getElementById("input01");

            //通过dom调用事件
            elementById.onchange = function () {
                alert("改变了")
            }
        }

    </script>
</head>
<body>

请输入:<input type="text" id="input01" value="www"/><br>

</body>
```





## 表单提交事件onsubmit

**onsubmit:注册按钮被点击，提交表单（判断表单内容是否符合规范） **

---

> 静态注册 -实例-用户名和密码不得为空
>
> 静态注册时注意：onsubmit=” “； html中需要接受返回值  return不可少

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        var myOnsubmit = function () {

            //先通过id拿到数据的dom对象（这里即用户名和密码）
            var userName = document.getElementById("userName");
            var passWord = document.getElementById("passWord");

            //取出value进行判空
            if (userName.value == "" || passWord.value == "") {
                alert("用户名或密码不得为null")
                return false;
            }
            alert("提交成功")
            return true;
        }

    </script>
</head>
<body>
    <!--注意：onsubmit需要接受返回值 return不可少 -->
<form action="#" method="post" onsubmit="return myOnsubmit()">
    用户名:<input type="text" id="userName"/><br>
    密 码: <input type="password" id="passWord"><br>
    <input type="submit" value="注册"/>
</form>
</body>
```

> 动态注册
>
> 注意：因为动态绑定是直接绑定onsubmit事件的，所以html中无需接受返回值

```html
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript">

        //动态绑定需要先加载页面
        window.onload = function () {

            //先通过id拿到表单的dom对象（这里即用户名和密码）
            var form01 = document.getElementById("form01");

            //给form01动态绑定表单提交事件
            form01.onsubmit = function () {
                //通过form表单的dom 取得表单中 输入框值(这种方法需要给输入框指定name)
                // （也可以和静态注册一样通过输入框id获取值）
                if (form01.userName.value == "" || form01.passWord.value == "") {
                    alert("用户名或密码不得为null")
                    return false;
                }
                alert("提交成功")
                return true;
            }
        }

    </script>
</head>
<body>
<form action="#" method="post" id="form01">
    用户名:<input type="text" id="userName" name="userName"/><br>
    密 码: <input type="password" id="passWord" name="passWord"><br>
    <input type="submit" value="注册"/>
</form>
</body>
```















## 事件监听-鼠标-键盘-视图-资源

> **监听input输入**

```javascript
dom.addEventListener("input", function () {}); 【e de wen ling si le】
```

> **监听鼠标**

```js
// 监听鼠标放置，移动事件 指针移到有事件监听的元素或它的子元素内
dom.addEventListener("mouseover", function () {});  【mo sei over】

//指针移出元素，或者移到它的子元素上
dom.addEventListener("mouseout", function () {});  【mo sei out】
```

> **键盘事件**

```js
//键盘按下事件
dom.addEventListener("keydown", function () {});   

//键盘释放事件
dom.addEventListener("keyuo", function () {});
```













## 事件冒泡-捕获-委托

**冒泡：从当前元素开始，沿着祖先节点向上依次触发各种事件**

> **阻止冒泡 .stopPropagation()**

```javascript
// ......省略
likeBtn.addEventListener('click', function(e) {
  // 点击事件
  e.stopPropagation()   【stop pao po kei shen】

// ......省略
```

---

> **捕获：从根节点向下依次移动到当前节点**
>
> - addEventListener('click', function(e)是在冒泡阶段监听，若想在捕获阶段监听，需要第三参数true

```javascript
dom.addEventListener('click', function() {}, true);
```

---

**委托：委托是冒泡事件的应用，如果想在大量子元素中单击任何一个都可以运行的代码，我们可以将事件监听器设置在其父节点上，并让子节点上发生的事件冒泡到父节点上，而不是每个子节点单独设置**

> **实例**

```javascript
//原始写法，每个子节点设置
const box = document.querySelector('.box');
const imgArr = box.children;
for (let i = 0; i < imgArr.length; i++) {
  imgArr[i].addEventListener('click', function() {
    document.body.style.backgroundImage = `url(${imgArr[i].src})`;
  });
}


//委托，只需要监听box
const box = document.querySelector('.box');
box.addEventListener('click', function(e) {
  //获取图片  target表示真实响应事件的DOM节点
  // 注意box区域比img大，如果点击在空白间隔区域，那么返回的节点将不会是IMG，需要特殊处理一下
  if (e.target.nodeName === 'IMG') {//判断点击是否是图片标签
    
    document.body.style.backgroundImage = `url(${e.target.src})`;
  }
});
```





## 鼠标移动事件案例

> 移动事件案例二

```javascript
//清空ul
let htmlDom=document.querySelectorAll('ul');
for(let i in htmlDom){
htmlDom[i].innerHTML=' ';
}

//获取第一个ul
const firstMenuBox = document.querySelector('.first');
//获取第二个ul
const secondMenuBox = document.querySelector('.second');


//循环遍历data是为了获取data中的值
for (let i = 0; i < data.length; i++) {

  //创建节点
  const li = document.createElement('li');
  const div=document.createElement('div');
  const img=document.createElement('img');
  const span=document.createElement('span');
  const txt=document.createTextNode(data[i].title);
  
  //将节点由内到外加入其父节点
  span.appendChild(txt);
  div.appendChild(img);
  div.appendChild(span);
  li.appendChild(div);

  //设置节点的样式以及值
  div.classList.add("left");
  img.classList.add("icon");
  img.src=data[i].icon;

//如果值为'新建' 则需要再加一个三角图片
  if(data[i].title==='新建'){  
    const img2=document.createElement('img');
    img2.classList.add("more");
    img2.src=`https://style.youkeda.com/img/pizza/context-menu/more.png`;
    li.appendChild(img2);     
    }
  //将组装好的html放入ul中
 firstMenuBox.appendChild(li);


//下面开始组装第二部分ul，是新建选项下的二级菜单，所以需要先判断
if(data[i].title=='新建'){

  //循环获取data中的children中的值
for(let n=0;n<data[i].children.length;n++){
  //创建节点
 const li2 = document.createElement('li');
 const div2=document.createElement('div');
 const img3=document.createElement('img');
 const span2=document.createElement('span');
const txt2=document.createTextNode(data[i].children[n].title);

//设置节点样式和值
 div2.classList.add("left");
img3.classList.add="icon";
img3.src=data[i].children[n].icon;

//将节点由内到外加入其父节点
   span2.appendChild(txt2);
   div2.appendChild(img3);
   div2.appendChild(txt2);
   li2.appendChild(div2);

//将组装的html放入ul
   secondMenuBox.appendChild(li2);
   }
  }
}

//获取一级菜单的第一个li节点，即'新建'菜单
const firstMenuBoxli = document.querySelector('li');
//先令二级菜单不可见
secondMenuBox.setAttribute('style', 'display: none');

//创建鼠标放置事件，若在其上，则修改display属性使其可见
firstMenuBoxli.addEventListener("mouseover",function(){
  secondMenuBox.setAttribute('style', 'display: block');
});
//创建鼠标移除事件，若移走，则修改display属性使其不可见
firstMenuBoxli.addEventListener("mouseout",function(){
    secondMenuBox.setAttribute('style', 'display: none');
  });
```





## 表单元素-焦点--表单内容值

> **焦点**
>
> - 获取focus 
> - 失去blur

```javascript
const nick = document.querySelector('input.nick');
nick.addEventListener('focus', function() {
  console.log('获取焦点');
});

nick.addEventListener('blur', function() {
  console.log('失去焦点');
});


/*
两种监听内容变化input和change
*/
const nick = document.querySelector('input.nick');
/*每次输入input都会触发*/
nick.addEventListener('input', function() {
  console.log('-----input');
  console.log(nick.value);
});


/*只有输入框失去焦点时才会触发  当为选项框时，每次选择都会触发*/
nick.addEventListener('change', function() {
  console.log('-----change');
  console.log(nick.value);
});
```

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677401390935-c0f8e597-3708-4b9e-a405-d86488208e94.png)



## 滚动事件

> **无尽滚动 scroll**

```javascript
/*滚动事件 scroll  【si kuai er】*/
window.addEventListener('scroll', function () {   
  console.log(window.scrollY);//滚动距离
});

/*案例
内容高度：document.body.clientHeight
浏览器高度：window.screen.height
滚动距离：window.scrollY
滚动距离底部距离： 内容高度 - 浏览器高度 - 滚动距离
*/
window.addEventListener('scroll', function () {
  // 可以通过clientHeight获取内容高度
  const height = document.body.clientHeight;

  // 通过screen.height获取浏览器的高度
  const screenHeight = window.screen.height;

  // 当距离底部的距离小于500时，触发页面新增内容
  if (height - window.scrollY - screenHeight < 500) {
    console.log('加载新文章内容');
    // 在底部添加10张图片
    const div = document.createElement('div');
    let str = '';
    for (let i = 0; i < 10; i++) {
      str += `
       <img
        class="first"
        alt=""
        src="https://document.youkeda.com/P3-1-HTML-CSS/1.8/1.jpg?x-oss-process=image/resize,h_300"
      />
      `;
    }
    div.innerHTML = str;
    document.body.appendChild(div);
  }
});
```



# 网络请求

> get请求
>

```javascript
fetch(  //fetch会返回一个包含响应结果的response对象
  'https://www.fastmock.site/mock/b73a1b9229212a9a3749e046b1e70285/f4/f4-11-1-1'
)  //使用回调函数，将response对象作为参数
  .then(function (response) {
    //转化为json文件并返回
    return response.json();
  }) //使用第二次回调 将第一次回调返回的json文件作为参数
  .then(function (myJson) {
    console.log(myJson);
  });
```



## POST-请求--提交

> post请求 method: 'POST'

```javascript
fetch(
  'https://www.fastmock.site/mock/b73a1b9229212a9a3749e046b1e70285/f4/f4-11-4-1',
  {
    method: 'POST'
  })
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  });


/*请求后获取json中的数据*/
fetch(
  'https://www.fastmock.site/mock/b73a1b9229212a9a3749e046b1e70285/f4/f4-11-5-10')
  .then(function(response) {
    return response.json();
  }).then(function(data){
    console.log(data[0].title);
  }
```

---

> **post提交**
>
> 注意：
> 				1.数据要先json化
> 				2.通过body完成post请求的传参   body: data,
> 				3.在headers中声明传入的数据的类型

```javascript
// 把JSON数据序列化成字符串
const data = JSON.stringify({
  username: 'admin',
  password: '123456'
});

fetch(
  'https://www.fastmock.site/mock/b73a1b9229212a9a3749e046b1e70285/f4/f4-11-4-1',
  {
    method: 'POST',  //post方法请求
    body: data,      //通过body传参
    headers: {      //声明参数类型
      'content-type': 'application/json'
    }
  }
)
  .then(function(response) {
    return response.json();
  })
  .then(function(myJson) {
    console.log(myJson);
  });
```



## 开发者工具

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677499454697-e38d5758-5fc9-4184-a79b-08e162a5b231.png)

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677499477422-2a1ac05e-650b-4d69-8d4c-8cedca94494a.png)

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/1677499523661-db1ead00-81bb-4482-9f49-c578acef018b.png)



# 查看js错误信息

> chrome浏览器  更多工具--》开发者---》控制台





# #############jQuery#####################

jQuery的意义：简化javaScritp

文档工具：https://jquery.cuishifeng.cn/

# jQuery安装

> **方式一：**

通过官网下载到本地导入项目（拖入项目文件夹,再引入即可） http://www.ab173.com/gongju/jquery/

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <!--本地引入-->
    <script src="/lib/jquery-3.4.1.js"></script>
</head>
<body>

</body>
</html>
```

> **方式二：**

直接引用： https://www.bootcdn.cn/?ref=www.8kmm.com

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <!--CDN 引入-->
    <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.4.1/core.js"></script>
</head>
<body>

</body>
</html>
```



# jQuery 选择器

> **jQuery公式： $(selector).action( )**    selector--选择器   action--事件

---

> jQuery与javaScritp的对比

```html
<script>
    //原生js，选择器少，麻烦不好记
    //1.标签
    document.getElementsByTagName();
    //2.id
    document.getElementById();
    //3.类
    document.getElementsByClassName();

    //使用jQuery  --唯一公式： $(selector).action( )
    //1.标签
    $('p').click();
    //2.id
    $('#id').click();
    //3.类
    $('.class').click();
    
    //多层选择 例如 ul下的li  其中：ul的id为 text-ul li的name为li1  
    $('#text-ul li[name=li1]').click();
    $('#text-ul li[id=li1]').click();
    $('#text-ul li[class=li1]').click();
</script>
```





# jQuery事件的响应

文档工具：https://jquery.cuishifeng.cn/ 全面

> **jQuery公式： $(selector).action( )**    selector--选择器   action--事件
>
> 当网页元素加载完毕后，响应事件

```js
    //原始写法：
    //1.$(document) 选择当前文档 2. .ready表加载完成  function (){} 事件
    $(document).ready(function () {
        //事件体
        $('#div')
    });


   //精简写法：
    $(function () {
        //事件体...(可嵌套多个事件)
        $('')
    });
```

---

> 实例：鼠标事件：获取鼠标移动坐标

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery</title>
    <!--本地引入-->
    <script src="jquery-3.4.1.js"></script>
</head>
<body>

<!--鼠标移动区域div-->
<div style="width: 800px;height: 700px;background-color: aqua"></div>
<!--鼠标坐标-->
<span>鼠标坐标：</span> <span id="mouse"></span>

</body>
<script>
    $(function () { //网页加载完毕，响应事件
        //事件体
        $('div').mousemove(function (e) { //鼠标移动事件 e为鼠标移动的数据

            $('#mouse').text('x:'+e.pageX+'  y:'+e.pageY); //修改文本
        });
    });
</script>
</html>
```



# jQuery操作DOM

> **jQuery公式： $(selector).action( )**  

---

> 常用节点文本操作：

```js
$('').text("text");  //设置（修改）文本  当.text()无参时，为取值
$('').html("text");  //设置（修改）html  html()无参时 为取值
```

> 常用css操作 

```js
$("p").css("color");  //取得第一个段落的color样式属性的值
$("p").css({ "color": "#ff0011", "background": "blue" }); //将所有段落的字体颜色设为红色并且背景为蓝色。
$("p").css("color","red"); //将所有段落字体设为红色
```

> 常用  元素的显示和隐藏  本质是使用了display=none

```js
$('').show();  //显示
$('').hide();  //隐藏
```

> 常用 获取属性

```js
$(window).width();
$(document).width();
```















# ##############http#################

# HTTP Request Header 请求头

![image-20230903161949680](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230903161949680.png)

![image-20230903162010820](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230903162010820.png)



# HTTP Responses Header 响应头

![image-20230903162037063](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230903162037063.png)

![image-20230903162054053](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230903162054053.png)





# GET/POST请求

> GET请求有哪些

1. form 标签 method=get
2. a 标签
3. link 标签引入 css
4. Script 标签引入js文件
5. img 标签引入图片
6. iframe 引入html页面
7. 在浏览器输入地址回车

---

> POST请求有哪些

1. form 标签 method=post

---





# MIME类型

MIME 是http协议中数据类型，MIME类型的格式是“大类型/小类型”，并于某一种文件的拓展名相对应。

在响应包Content-Type中有指定

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230904094641778.png" alt="image-20230904094641778" style="zoom:67%;" />

---









# ##############Servlet#################





# web基本概念

## Web应用程序

Web应用程序：可以提供浏览器访问的程序；

- 我们能访问的任何一个页面或资源，都存在与某一台计算机上

- URL：统一资源定位符

- 这个统一的Web资源会被放在同一个文件夹下，web应用程序-->Tomcat：服务器

- 一个Web应用由多部分组成：

  - html，css，js
  - jsp，servlet
  - java程序
  - jar包
  - 配置文件properties

  web应用程序编写完毕后，若想供给外界访问，需要一个服务器统一管理

---



## 静态Web

- *.htm   *.html都是网页后缀，如果服务器上一直存在这些东西，我们就可以直接读取.

![image-20230521125823281](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230521125823281.png)

- 静态web缺陷：
  - web页面无法动态更新，所有用户看到的都是同一页面
    - 轮播图：点击特效-伪动态
    - JavaScript
  - 无法与数据库交互（数据无法持久化）



## 动态Web

页面会动态展示：web页面展示的效果因人而异

![image-20230521132044792](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230521132044792.png)



**缺陷：**

- 加入服务器的动态web资源出现了错误，我们需要重新编写后台程序，重新发布  
  - 停机维护

**优势：**

- web页面可以动态更新
- 可以与数据库交互

---





# Tomcat

> **Tomcat目录结构**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230901131709451.png" alt="image-20230901131709451" style="zoom:80%;" />

- server.xml 用于配置tomcat的基本设置(启动端口，关闭端口, 主机名)
- wex.xml 用于指定tomcat运行时配置(比如servlet等..)
- webapps 目录是存放 web应用，就是网站

---



## 	 **Tomcat 服务中部署 WEB 应用**

一个WEB应用由多个WEB资源或其它文件组成，包括html文件、css文件、js文件、动 态web页面、java程序、支持jar包、配置文件等。开发人员在开发web应用时，按照规 定目录结构存放这些文件。否则，在把 web应用交给web服务器管理时，不仅可能会使 web应用无法访问，还会导致web服务器启动报错。

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230901131937254.png" alt="image-20230901131937254" style="zoom:67%;" />

---

**部署方式1：将 web 工程的目录拷贝到 Tomcat 的 webapps 目录下 **：

**【 Tomcat 的 webapps 目录 相当于  http://ip[域名]   当没有Web工程/应用名时，默认访问的是 ROOT 工程**

**在浏览器地址栏中输入的访问地址如下： http://ip[域名]:port/工程名/ ，没有资源名， 默认访问 index.jsp 页面】**

1. newsWeb工程(目前都是静态资源 html, 图片)
2. 将该news目录/文件夹 拷贝到 Tomcat 的webapps目录下 
3. 浏览器输入： http://ip[域名]:port/news/子目录../文件名

---



## 浏览器请求资源流程

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230901160000857.png" alt="image-20230901160000857" style="zoom:80%;" />













# Servlet 开发

地址:https://tomcat.apache.org/tomcat-8.0-doc/servletapi/index.html

---

> **什么是 Servlet**

Servlet在开发动态WEB工程中，得到广泛的应用，掌握好Servlet非常重要了,Servlet(基 石)是SpringMVC的基础

---

> **Servlet(java 服务器小程序)特点:**

- 他是由服务器端调用和执行的(一句话：是Tomcat解析和执行) 
- 他是用java语言编写的, 本质就是Java类
- 他是按照Servlet规范开发的(除了tomcat->Servlet 还有weblogic->Servlet) 
- 功能强大，可以完成几乎所有的网站功能(在以前，使用Servlet开发网站)

---

> **为什么需要Servlet？**

提出需求: 请用你现有的htmlcssjavascript，开发网站，比如可以让用户留言/购物/支付, 你能搞定吗?

显然不能，所以需要 引入我们动态网页(能和用户交互)技术 ===>Servlet 

---

> **Servlet 在 JavaWeb 项目位置**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230901164454036.png" alt="image-20230901164454036" style="zoom:80%;" />



---





## 构建Maven项目

**Maven安装**：https://www.bilibili.com/video/BV16Q4y127BZ/

> **第一步-idea创建maven**

idea---->新建项目----->修改

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230525211703490.png" alt="image-20230525211703490" style="zoom:80%;" />

> **第二步-删除src项目。这个空的工程就是Maven的主工程**

> **第三步-解决工程中没有iml文件的方法： 打开项目终端，输入：`mvn idea:module`下载  如果有则无需此操作**

> **第四步-pom添加基本依赖**

```xml
     <!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api jsp依赖-->
     <dependency>
         <groupId>javax.servlet.jsp</groupId>
         <artifactId>javax.servlet.jsp-api</artifactId>
         <version>2.3.3</version>
         <scope>provided</scope>
     </dependency>
     <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api  servlet依赖-->
     <dependency>
         <groupId>javax.servlet</groupId>
         <artifactId>javax.servlet-api</artifactId>
         <version>4.0.1</version>
         <scope>provided</scope>
     </dependency>
```

> **第五步-idea构建子项目**

右击主项目-->新建-->新模块

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230525212312114.png" alt="image-20230525212312114" style="zoom:80%;" />

此时，父子项目的pom中，会多出如下代码：

```xml
<!--父pom中-->
    <modules>
        <module>servlet-01</module>
    </modules>

<!--子pom中-->
    <parent>
        <groupId>com.wang</groupId>
        <artifactId>javaweb-01-servlet</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>
```



## Maven环境优化

> 第一步-修改子项目中web.xml为最新（因为自动配置的已经很古老了）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
</web-app>
```

> **第二步-将maven环境构建完整（在子项目main包中创建java包和资源包resources）**



## 配置Tomcat

> 第一步-运行按钮左-->编辑配置-->选择Tomcat --->本地  -->点击+号

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230902103108134.png" alt="image-20230902103108134" style="zoom: 67%;" />

> 第二步-点击 部署--->点击+号

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230902103515516.png" alt="image-20230902103515516" style="zoom: 67%;" />

注意：如果是页面修改，保存即可生效，无需重启

---



## Servlet编写-实现Servlet接口

> 第一步-编写一个普通类，实现Servlet接口

```java
public class ServletTest implements Servlet {

    /**
     * 作用：初始化Servlet
     * 当Tomcat创建 ServletTest 实例时，会调用init方法
     * 该方法只会调用一次
     * @param servletConfig
     * @throws ServletException
     */
    public void init(ServletConfig servletConfig) throws ServletException {
    }

    /**
     * 作用：返回 ServletConfig 也就是返回 Servlet 的配置
     * @return
     */
    public ServletConfig getServletConfig() {
        return null;
    }

    /**
     * service方法 处理浏览器的请求（包括get和post）
     * 当浏览器每次请求Servlet时，就会调用一次service方法
     * 当Tomcat调用该方法时，会把http请求的数据封装成 ServletRequest 对象
     * 1.通过参数 ServletRequest  --得到用户提交的数据
     * 2.通过参数 ServletResponse  --用于返回数据给浏览器 （通过 tomcat-->浏览器）
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        //ServletRequest 没有得到提交方式的方法-getMethod;看看 ServletRequest 子接口有没有相关方法
        //把 servletReqeust 转成 HttpServletRequest 引用
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
        String method = httpServletRequest.getMethod();
        if("GET".equals(method)) {
            doGet(); // 用 doGet() 处 理 GET 请 求
        } else if("POST".equals(method)) {
            doPost(); // 用 doPost() 处 理 POST 请 求
        }
    }

    /**
     * 处理post请求
     */
    private void doPost() {
    }

    /**
     * 处理get请求
     */
    private void doGet() {
    }    
        

    /**
     * 返回 Servlet信息   使用少
     * @return
     */
    public String getServletInfo() {
        return null;
    }

    /**
     *销毁 Servlet实例 只会调用一次
     */
    public void destroy() {
    }
}

```

此时配置好了servlet，但还没有使浏览器获取servlet 

> 第二步：在web.xml中配置servlet 的实例 ServletTest，即给ServletTest提供对外访问的接口

```xml
    <!--注册servlet-->
    <servlet>
        <servlet-name>servlet_001</servlet-name>
        <servlet-class>com.wang.servlet.ServletTest</servlet-class>
    </servlet>

    <!--servlet请求路径-->
    <servlet-mapping>
        <servlet-name>servlet_001</servlet-name>
        <url-pattern>/servlet_001</url-pattern>
    </servlet-mapping>
```

浏览器输入：http://localhost:8080/wang/servlet_001

---



## Servlet编写-继承HttpServlet类

> 第一步-编写一个普通类，继承HttpServlet类

```java
public class helloServlet extends HttpServlet {   
    @Override   //get请求 get和post都是实现请求的不同形式，所以可以相互调用，业务逻辑也一样
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doGet(req, resp);
    }

    @Override  //post请求
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```

> 第二步-编写Servlet的映射  -web.xml中
>
> （为什么需要映射：我们写的是JAVA程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注   			册我们写的Servlet，还需给他一个浏览器能够访问的路径。）

```xml
<!--注册servlet-->
<servlet>
 <servlet-name>helloservlet</servlet-name>
 <servlet-class>com.sunyiwenlong.servlet.HelloServlet</servlet-class>
</servlet>

<!--servlet请求路径-->
<servlet-mapping>
 <servlet-name>helloservlet</servlet-name>
 <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

---



## Servlet配置初始参数

> 在web.xml中配置servlet 的实例 ServletTest

```xml
    <!--注册servlet-->
    <servlet>
        <servlet-name>servlet_001</servlet-name>
        <servlet-class>com.wang.servlet.ServletTest</servlet-class>
        
        <!--为该servlet配置初始参数-->
        <init-param>
            <!--参数名-->
            <param-name>user</param-name>
            <!--参数值-->
            <param-value>root</param-value>
        </init-param>
    </servlet>

    <!--servlet请求路径-->
    <servlet-mapping>
        <servlet-name>servlet_001</servlet-name>
        <url-pattern>/servlet_001</url-pattern>
    </servlet-mapping>
```

> 注解方式:@WebInitParam
>
> @WebInitParam 注解需要配合 @WebServlet 和 @WebFilter 使用，用于为 Servlet 或过滤器初始化参数。

```java
@WebServlet(urlPattern={"/sample"},name="sampleServlet",
initParams = {@WebInitParam(name="username",value="uservalue"),
             @WebInitParam(name="pwd",value="pwdvalue")})
public class sampleServlet extends HttpServlet{
	//....
}
```







## 浏览器调用Servlet流程

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230902130639432.png" alt="image-20230902130639432" style="zoom:80%;" />



## Servlet生命周期

> 主要有三个方法：
>
> 1. init()初始化阶段
> 2. service()处理浏览器请求阶段
> 3. .destroy()终止阶段

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230902130852333.png" alt="image-20230902130852333" style="zoom:67%;" />



> **init()初始化阶段：**

- Servlet容器(比如:Tomcat)加载Servlet，加载完成后，Servlet容器会创建一个Servlet实例 并调用init()方法，init()方法只会调用一次,
- Servlet容器(Tomcat)启动时自动装载某些servlet，实现这个需要在web.xml文件中添加 \<load-on-startup>1\</load-on-startup>1表示装载的顺序
- Servlet重新装载时(比如tomcat 进行redeploy【redeploy会销毁所有的Servlet实例】)， 浏览器再向Servlet发送请求的第1次



> **处理浏览器请求阶段(service方法):**

-  每收到一个http请求，服务器就会产生一个新的线程去处理[线程]
-  创建一个用于封装 HTTP 请求消息的 ServletRequest 对象和一个代表 HTTP 响应消息的 ServletResponse对象
- 然后调用Servlet的service()方法并将请求和响应对象作为参数传递进去



> **终止阶段 destory方法(体现Servlet完整的生命周期):**

- 当web应用被终止， 或者Servlet容器终止运行， 或者Servlet类重新装载时， 会调用destroy() 方法
- 比如重启tomcat,或者 redeployweb应用

---







# Servlet注解开发

> @WebServlet注解部分属性：

```java
public @interface WebServlet {
    String name() default "";

    String[] value() default {};

    //对应web.xml中的 url-pattern
    String[] urlPatterns() default {};
    
    //。。。。
}
```

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230903160130177.png" alt="image-20230903160130177" style="zoom:67%;" />

---



> **具体步骤**
>
> 1. 编写类OkServlet去继承HttpServlet 
> 2.  注解方式配置OkServlet, 一个Servlet支持配置多个urlPattern 

---

> 编写类OkServlet去继承HttpServlet

```java
//精准匹配
@WebServlet(urlPatterns = {"/ok1"})
public class OkServlet extends HttpServlet {
    //doGet ,doPost.....
}


//目录匹配
@WebServlet(urlPatterns = {"/ok/*"})
public class OkServlet extends HttpServlet {
    //doGet ,doPost.....
}


//扩展名匹配
@WebServlet(urlPatterns = {".html"})
public class OkServlet extends HttpServlet {
    //doGet ,doPost.....
}


//任意匹配
@WebServlet(urlPatterns = {"/"})   @WebServlet(urlPatterns = {"/*"})
public class OkServlet extends HttpServlet {
    //doGet ,doPost.....
}

```

> **注意：注解开发注意事项**

- web.xml的顶层标签中，有一个属性 metadata-complete ，该属性用于指定当前web.xml是否是完全的，若为true，则该容器只依赖于xml，忽略所有注解，若不配置，或配置为false，则表示支持注解

  ```xml
  <web-app   metadata-complete="false">
  ```

- 当 Servlet 配置了 "/", 会覆盖 tomcat 的 DefaultServlet, 当其他的 utl-pattern 都匹配不上时 ，都 会 走 这 个 Servlet, 这 样 可 以 拦 截 到 其 它 静 态 资 源 

- 当Servelt配置了 "/*", 表示可以匹配任意访问路径

- 优先级遵守: 精确路径 > 目录路径 > 扩展名路径 >/*>/

---







# ServletConfig 

**介绍：**

- ServletConfig 类是为 Servlet 程序的配置信息的类
- Servlet 程序和 ServletConfig 对象都是由 Tomcat 负责创建
- Servlet 程序默认是第 1 次访问的时候创建，ServletConfig 在 Servlet 程序创建时，就创 建一个对应的 ServletConfig 对 象

---

**功能：** 

1.  获取 Servlet 程序的 servlet-name 的值
2. 获取初始化参数 init-param
3. 获取 ServletContext 对象

---

**实例：** 编写 DBServlet.java 完成如下功能-

   1.在web.xml配置连接mysql的用户名和密码；

2. 在DBServlet 执行 doGet()/doPost() 时，可以获取到web.xml配置的用户名和密码

```java
//注解方式配置servlet
@WebServlet(urlPatterns = "/db", initParams = {@WebInitParam(name = "username", value = "root"),
        @WebInitParam(name = "pwd", value = "123456")})
public class DBServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //在 DBServlet 执行doGet/doPost时，可以获取到Servlet配置的用户名和密码
        //OOP程序员--》现有的方法或对象搞定 先查本类方法，没有就去查父类
        // HttpServlet没有，其父类 GenericServlet 有一个 getServletConfig 方法 获取servlet配置
        ServletConfig servletConfig = getServletConfig();
        //获取配置中的值
        String username = servletConfig.getInitParameter("username");
        String pwd = servletConfig.getInitParameter("pwd");
        //打印输出
        System.out.println(username + " " + pwd);
    }
}
```

---

> **ServletConfig 注意事项** 
>
> -  重写init方法时,
>
> ```java
> public class DBServlet extends HttpServlet {
> 
>     @Override
>     public void init(ServletConfig config) throws ServletException {
>         super.init(config);
>     }
> }
> ```
>
> 1.当 DBServlet 实例化时,会同时创建一个 ServletConfig 对象
>
> 2.这时如果 DBServlet  init( ) 方法 中你调用了 super.init(config)  
>
> 3.super.init(config)  会调用父类 GenericServlet 中 init方法
>
> ```java
> // super.init(config)传给 GenericServlet 
> public void init(ServletConfig config) throws ServletException {
>     this.config = config;
>     this.init();
> }
> ```
>
> 这时就会把Tomcat创建的Config对象赋给 GenericServlet 的属性 this.config
>
> 4.而  ServletConfig servletConfig = getServletConfig(); 返回的 servletConfig 对象就是 GenericServlet 的 this.config 属性
>
> ```java
> //GenericServlet 
> public ServletConfig getServletConfig() {
>     return this.config;
> }
> ```
>
> ---
>
> **故总结:**
>
> **如果重写init方法时, 不写 super.init(config);** 
>
> **那么 ServletConfig servletConfig = getServletConfig();  返回的 servletConfig 对象就是null的**
>
> 

---









# ServletContext对象

**介绍**

- ServletContext 是一个接口，它表示 Servlet 上下文对象
- 一个 web 工程，只有一个 ServletContext 对象实例
- ServletContext对象 是在 web 工程启动的时候创建，在 web 工程停止的时销毁
- .ServletContext 对象可以通过 ServletConfig.getServletContext 方法获得对 ServletContext 对象的引用，也可以通过this.getServletContext()来获得其对象的引用。
- 由于一个WEB应用中的所有Servlet共享同一个ServletContext对象，因此Servlet对象 之间可以通过ServletContext对象来实现多个Servlet间通讯。 ServletContext对象通常也被 称之为域对象

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用。

---

使用场景: 如果我们希望统计某个 web 应用的所有 Servlet 被访问的次数，怎么 办?   

---

**作用:**

1.  获取 web.xml 中配置的上下文参数 context-param[信息和整个 web 应用相关，而不是 属于某个 Servlet]
2. 获取当前的工程路径，格式:/工程路径 =》 比如 /servlet
3.  获 取 工 程 部 署 后 在 服 务 器 硬 盘 上 的 绝 对 路 径 
4.  像 Map 一样存取数据, 多个Servlet共享数据

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230904104542883.png" alt="image-20230904104542883" style="zoom:67%;" />

---





## 共享数据

- 共享数据：在这个Servlet中保存的数据，可以在另一个Servlet中拿到

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230903161006291.png"/>

> 一个servllet放入数据

```java
public class HelloServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     // this.getInitParameter(); 获取初始化参数（web.xml文件中的初始化参数）
     // this.getServletConfig(); 获取servlet的配置（web.xml文件中的配置）
     // this.getServletContext(); 获取servlet上下文
     ServletContext context = this.getServletContext();
     String username = "张三";
     context.setAttribute("username",username);// 将一个数据保存在了ServletContext中
 }
}
```

> 其他servlet取数据

```java
public class GetServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     ServletContext context = this.getServletContext();
     String username = (String) context.getAttribute("username"); //获取k为username的数据
     String contextPath = servletContext.getContextPath(); //获取项目工程路径
     String realPath = servletContext.getRealPath("/");//获取项目发布后，正在工作的路径 "/"表示项目发布后的根路径
     resp.setContentType("text/html");
     resp.setCharacterEncoding("utf-8");
     resp.getWriter().println("名字"+username);
 }
}
```





## 获取初始化参数

> web.xml中

```xml
<!--配置一些web应用一些初始化参数-->
<context-param>
 <param-name>url</param-name>
 <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
</context-param>
```

> 取出

```java
public class ServletDemo03 extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     String url = this.getInitParameter("url");
     resp.getWriter().println(url);
 }
}
```









## 请求转发

> 转发和重定向

![image-20230530212527850](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230530212527850.png)

> 转发不会改变请求路径
>
> 重定向会改变



> web.xml

```xml
<servlet>
 <servlet-name>gp</servlet-name>
 <servlet-class>com.sunyiwenlong.servlet.ServletDemo03</servlet-class>
</servlet>
<servlet-mapping>
 <servlet-name>gp</servlet-name>
 <url-pattern>/gp</url-pattern>
</servlet-mapping>

<servlet>
 <servlet-name>sd4</servlet-name>
 <servlet-class>com.sunyiwenlong.servlet.ServletDemo04</servlet-class>
</servlet>
<servlet-mapping>
 <servlet-name>sd4</servlet-name>
 <url-pattern>/sd4</url-pattern>
</servlet-mapping>
```

> 配置servlet

```java
// 请求/sd4找到ServletDemo04，ServletDemo04进行请求转发到/gp，到/gp的页面
// (浏览器路径是sd4的路径，页面拿到的是/gp的数据)
public class ServletDemo04 extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     ServletContext context = this.getServletContext();
     // RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");// 转发的路径
     // requestDispatcher.forward(req,resp);// 调用forward请求转发
     
     context.getRequestDispatcher("/gp").forward(req,resp);   // "/gp"是web.xml中配置的路径
 }
}
```



## 读取资源文件

1. Properties

- 在java目录下新建properties
- 在resources目录下新建properties发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath。

> 思路：需要一个文件流

```Properties
username=root
password=123456
```

```java
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //流的形式读取资源文件  /WEB-INF/CLASSES/db.properties是web服务器的相对地址
        InputStream stream = this.getServletContext().getResourceAsStream("/WEB-INF/CLASSES/db.properties");
        //创建Properties类
        Properties properties = new Properties();
        properties.load(stream);
        //通过键获取值
        String username = properties.getProperty("username");
        String password = properties.getProperty("password");
        resp.getWriter().println(username+":"+password);
    }
}
```





## 实例:网站计数器

**需求:** 

1. 完成一个简单的网站访问次数计数器：
2. 使用 Chrome 访问 CountServlet_01, 每访问一次，就增加 1访问次数，在后台输出，并将结 果返回给浏览器显示
3. 使用火狐访问CountServlet_02，每访问一次，就增加1访问次数，在后台输出，并将结果返 回给浏览器显示

---

**代码实现: [注意CountServlet_01 和CountServlet_02代码完全相同 唯一不同是@WebServlet]**

```java
@WebServlet("/countServlet_01")
public class CountServlet_01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //获取 ServletContext
        ServletContext servletContext = getServletContext();
        System.out.println(servletContext);
        //从 ServletContext 中获取计数 visit_count
        Object visitCount = servletContext.getAttribute("visit_count");

        //判断
        if (visitCount == null) {//为null 说明没有 visitCount 即第一次访问
            //那么将其value变为1
            visitCount = 1;
            servletContext.setAttribute("visit_count", visitCount);
        } else { //不为空即 第二次即以后的访问 将 visit_count 的value加1
            //由于 visitCount是object 所以需要先将其转换为string，再提供Integer转换为包装类进行加一操作
            visitCount = Integer.parseInt(visitCount + "") + 1;
            //改变后的value放入
            servletContext.setAttribute("visit_count", visitCount);
        }

        //输出显示
        resp.setContentType("text/html;charset=utf-8"); //设置输出编码
        //创建一个PrintWriter对象，用于向响应的输出流写入文本,将生成的响应文本发送回客户端。
        PrintWriter writer = resp.getWriter();
        writer.print("<h1>网站被访问的次数是" + servletContext.getAttribute("visit_count") + "</h1>");
        writer.flush(); //刷新 写入的任何文本都将立即发送给输出流

        //关闭资源
        writer.close();
    }
}
```

访问:http://localhost:8080/servlet/countServlet_01 和http://localhost:8080/servlet/countServlet_02

---





# HttpServletRequest

- HttpServletRequest代表客户端的请求
- 用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到 HttpServletRequest
- 通过这个HttpServletRequest的方法，获得客户端的所有信息

---

> **常用方法**

```java
getRequestURI() //获取请求的资源路径
getRequestURL() //获取请求的统一资源定位符（绝对路径）
getRemoteHost() //获取客户端的 主机,getRemoteAddr()
getHeader()     //获取请求头
getParameter()  //获取请求的参数(前端传递的参数)
getParameterValues() //获取请求的参数（多个值的时候使用） , 比如 checkbox, 返回的 数组
getMethod()  //获取请求的方式 GET 或 POST
setAttribute(key,value);  //设置域数据
getAttribute(key);  //获取域数据
getRequestDispatcher()  //获取请求转发对象, 请求转发的核心对象
```

---



## 获取前端传递的参数

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/kuangstudyfbb80cd9-dac2-49f1-aea8-625e2b074aa9.jpg)

---

> **实例:** 在一个表单提交数据给 Servlet, 然后在 Servlet 通过 HttpServletRequest对象获取相关数据

**request表单**[路径:src/main/webapp/request.html]

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>注册</title>
</head>
<body>
<h1>注册用户</h1>
<form action="http://localhost:8080/servlet/loginServlet" method="get">
    u: <input type="text" name="username"/><br><br>
    p: <input type="password" name="pwd"/><br><br>
    选择你喜欢的模块:
    <input type="checkbox" name="hobby" value="music">音乐
    <input type="checkbox" name="hobby" value="movie">电影
    <input type="checkbox" name="hobby" value="game">游戏<br/>
    <br/>
    <input type="submit" value="注册用户"/>
</form>
</body>
</html>
```

**java代码**

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //输出请求的资源路径URI
        System.out.println("请求的资源路径URI= " + req.getRequestURI());
        //输出请求的URL
        System.out.println(" 请求的URL= " + req.getRequestURL());
        //输出请求的客户端ip 地址
        System.out.println("请求的客户端ip 地址=" + req.getRemoteAddr());
        //输出 http 请求头的信息
        System.out.println("http请求头HOST= " + req.getHeader("Host"));
        System.out.println("该请求的发起地址是= " + req.getHeader("Referer"));
        System.out.println("该请求的发起浏览器是= " + req.getHeader("User-Agent"));
        //输出http请求方式
        System.out.println("http请求方式= " + req.getMethod());


        //获取表单提交的数据[单个数据]
        String username = req.getParameter("username");
        String pwd = req.getParameter("pwd");
        System.out.println("username= " + username);
        System.out.println("pwd= " + pwd);

        //获取表单提交的数据[一组数据 多选框等等]
        String[] hobbies = req.getParameterValues("hobby");
        for (String hobby : hobbies) {
            System.out.println("hobby=" + hobby);
        }

    }
}

```





## 请求转发

- 实现请求转发：请求转发指一个 web 资源收到客户端请求后，通知服务器去调用另外 一个 web 资源进行处理
- HttpServletRequest对象(也叫Request对象)提供了一个getRequestDispatcher方法，该 方法返回一个RequestDispatcher对象，调用这个对象的forward方法可以实现请求转发
- request对象同时也是一个域对象，开发人员通过request对象在实现转发时，把数据 通过request对象带给其它web资源处理

```java
setAttribute
getAttribute 
removeAttribute 
getAttributeNames
```

---

**请求转发原理示意图**

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230904145519249.png" alt="image-20230904145519249" style="zoom:67%;" />

---

> **实例:**表单提交用户登录,如果是 root，提示为管理员，其它是普通用户.
>
> 表单提交到  loginServlet  然后通过 loginServlet处理后再通过 请求转发给  manageServlet读取并显示

**前端**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>登录</title>
</head>
<body>
<h1>用户登录</h1>
<form action="http://localhost:8080/servlet/logonServlet" method="post">
  u: <input type="text" name="username"/><br><br>
  p: <input type="password" name="pwd"/><br><br>
  <br/>
  <input type="submit" value="登录"/>
</form>
</body>
</html>
```

**后端-LogonServlet.java**

```java
@WebServlet("/logonServlet")
public class LogonServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //处理请求中文乱码（后期可以使用过滤器来解决）
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        //根据用户名 分配该用户是什么身份
        String username = req.getParameter("username");
        if("root".equals(username)){ //如果是root则分配为管理员
            req.setAttribute("role","管理员");
        }else {//否则则普通用户
            req.setAttribute("role","普通用户");
        }

        //获取分发器
        //1.getRequestDispatcher("/logonServlet"); 中 /logonServlet 表示要转放的servlet的url
        //2.“/” 会被解析成 http://localhost:8080/servlet/   【servlet是tomcat部署，由程序员手动指定的应用上下文】
        RequestDispatcher requestDispatcher = req.getRequestDispatcher("/manageServlet");

        // forward(req,resp) 表示把当前servlet的 req,resp 传递给下一个servlet使用 【必需】
        requestDispatcher.forward(req,resp);

    }
}

```

**后端-ManageServlet.java**

```java
@WebServlet("/manageServlet")
public class ManageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //取出用户名和身份
        String username = req.getParameter("username");
        String role = req.getAttribute("role").toString();

        //输出显示
        //处理请求中文乱码（后期可以使用过滤器来解决）
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        resp.setContentType("text/html;charset=utf-8"); //设置输出编码
        //创建一个PrintWriter对象，用于向响应的输出流写入文本,将生成的响应文本发送回客户端。
        PrintWriter writer = resp.getWriter();
        writer.print("<h1>用户名是" + username + "</h1>");
        writer.print("<h1>用户角色是" + role + "</h1>");
        writer.flush(); //刷新 写入的任何文本都将立即发送给输出流

        //关闭资源
        writer.close();
    }
}

```

---

> **请求转发注意事项:**
>
> 1. 浏览器地址不会变化(地址会保留在第 1 个 servlet 的 url)
> 2.  在同一次HTTP请求中，进行多次转发，仍然是一次HTTP请求  [请求转发只在服务器中,和浏览器无关,所以是一次请求]
> 3. 在同一次HTTP请求中，进行多次转发， 多个Servlet可以共享request域/对象的数据(因 为始终是同一个request对象)
> 4. 可以转发到 WEB-INF目录下
> 5. 不能访问当前WEB工程外的资源
> 6. 因为浏览器地址栏会停止在第一个servlet, 如果你刷新页面，会再次发出请求(并且会带数据), 所以在支付页面情况下，不要使用请求转发，否则会造成重复支付







# HttpServletResponse

- 每次 HTTP 请求，Tomcat 会创建一个 HttpServletResponse 对象传递给 Servlet 程序去使用。
- HttpServletRequest 表示请求过来的信息，HttpServletResponse 表示所有响应的信息， 如果需要设置返回给客户端的信息，通过HttpServletResponse 对象来进行设置即可

---

> 负责向浏览器发送数据的方法

```java
//字节流 getOutputStream(); 常用于下载（处理二进制数据）
public ServletOutputStream getOutputStream() throws IOException;
//字符流 getWriter(); 常用于回传字符串
public PrintWriter getWriter() throws IOException;
```

两个流同时只能使用一个。 使用了字节流，就不能再使用字符流，反之亦然， 否则就会报错

---





## 实例:下载文件

> 下载文件

```java
@WebServlet("/file")
public class FileServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     // 1.要获取下载文件的路径
     String realPath = "E:\\dev\\StudyProjects\\javaweb-servlet\\response\\src\\main\\resources\\大乔.jpg";
     // 2.下载的文件名是啥？  通过截取字符串substring 截取最后出现lastIndexOf的位置 +1即得到\后面的字符串
     String filename = realPath.substring(realPath.lastIndexOf("\\") + 1);
     // 3.设置让浏览器能够支持下载我们需要的东西 消息头（Content-disposition） URLEncoder.encode 转utf-8使得中文名的资源不报错
     resp.setHeader("Content-disposition","attachment;filename="+ URLEncoder.encode(filename,"utf-8"));
     // 4.获取下载文件的输入流
     FileInputStream in = new FileInputStream(realPath);
     // 5.创建缓冲区
     int len = 0;
     byte[] buffer = new byte[1024];// 每次读取的长度
     // 6.获取OutputStream对象
     ServletOutputStream out = resp.getOutputStream();
     // 7.将FileOutputStream流写入到bufer缓冲区
     // 8.使用OutputStream将缓冲区中的数据输出到客户端！
     while ((len = in.read(buffer))>0){// 每次读取的长度大于0的情况下，就写出去
         out.write(buffer,0,len);// 写出字节，从0写到len
     }
     // 9.关闭资源文件
     in.close();
     out.close();
 }
 @Override
 protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     this.doGet(req, resp);
 }
}
```





## 实例:验证码功能

```java
@WebServlet("/image")
public class ImageServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     // 让浏览器3秒刷新一次
     resp.setHeader("refresh", "3");
     // 在内存中创建一个图片
     BufferedImage image = new BufferedImage(80, 20, BufferedImage.TYPE_INT_RGB);// 宽、高、颜色
     // 得到图片
     Graphics2D g = (Graphics2D) image.getGraphics();// 得到一只2D的笔
     // 设置图片的背景颜色
     g.setColor(Color.white);
     g.fillRect(0, 0, 80, 20);// 填充颜色
     // 换个背景颜色
     g.setColor(Color.BLUE);
     // 设置字体样式：粗体，20
     g.setFont(new Font(null,Font.BOLD,20));
     // 画一个字符串（给图片写数据）
     g.drawString(makeNum(),0,20);
     // 告诉浏览器，这个请求用图片的方式打开
     resp.setContentType("image/jpeg");
     // 网站存在缓存，不让浏览器缓存
     resp.setDateHeader("expires",-1);
     resp.setHeader("Cache-Control","no-cache");
     resp.setHeader("Pragma","no-cache");
     // 把图片写给浏览器
     boolean write = ImageIO.write(image, "jpg",resp.getOutputStream());
 }
 // 生成随机数
 private String makeNum() {
     Random random = new Random();
     String num = random.nextInt(9999999) + "";// 随机数，最大七位，[0,9999999)
     StringBuffer sb = new StringBuffer();
     for (int i = 0; i < 7 - num.length(); i++) {// 不足七位，则添加0
         sb.append("0");
     }
     num = sb.toString()+num;// 不足七位，在随机数前面添加0
     return num;
 }
 @Override
 protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     this.doGet(req, resp);
 }
}
```





## 实现请求重定向

**请求重定向指：一个 web 资源收到客户端请求后，通知客户端去访问另外一个 web资源，这称之为请求重定向**

<img src="C:/Users/admin/AppData/Roaming/Typora/typora-user-images/image-20230904154944540.png" alt="image-20230904154944540" style="zoom:67%;" />

---



```java
public class RedirectServlet extends HttpServlet {
 @Override
 protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     /*resp.setHeader("Location","/response_war/image");
     resp.setStatus(HttpServletResponse.SC_NOT_MODIFIED);*/
     resp.sendRedirect("/response_war/image");// 重定向相当于上面两行代码
 }
 @Override
 protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
     this.doGet(req, resp);
 }
}
```

> **重定向注意事项**
>
> 1. 最佳应用场景：网站迁移，比如原域名是 www.wang.com 迁移到 www.wang.cn ，但 是百度抓取的还是原来网址.
> 2.  浏览器地址会发生变化，本质是两次http请求.
> 3. 不能共享Request域中的数据，本质是两次http请求，会生成两个HttpServletRequest 对象
> 4. 不能重定向到 /WEB-INF 下的资源
> 5. 可以重定向到Web 工程以外的资源， 比如 到 www.baidu.com
> 6. 重定向有两种方式, 推荐使用第1种.
>
> ```java
> //第一种
> resp.sendRedirect("/response_war/image");
> 
> //第二种
> resp.setStatus(302);  //设置状态码302 表示重定向
> resp.setHeader("Location","/response_war/image"); //设置响应头 说明新的地址在哪
> ```
>
> ​	7.动态获取到applicationcontext
>
> ```java
> String contextPath = getServletContext().getContextPath(); 
> response.sendRedirect(contextPath + "/downServletNew");
> ```
>
> 





---

## 重定向实例: 下载资源重定向

演示请求重定向的使用当访问 DownServlet 下载文件 ，重定向到 DownServletNew 下载文件

**前端html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>下载</title>
</head>
<body>
<h1>下载文件</h1>
<a href="http://localhost:8080/servlet/downServlet">点击下载</a>
</body>
</html>
```

**java代码-DownServlet.java**

```java
@WebServlet("/downServlet")
public class DownServlet extends HttpServlet {


    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //发出请求重定向
        //浏览器解析“/”时，会解析为 http://localhost:8080/
        resp.sendRedirect("/servlet/downServletNew");
    }
}

```

**java代码-downServletNew.java**

```java
@WebServlet("/downServletNew")
public class DownServletNew extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //输出显示
        //设置输出编码;  application/x-tar 表示下载弹窗
        resp.setContentType("application/x-tar;charset=utf-8"); 

    }
}

```

---









# 会话机制

- 无状态的会话：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话。
- 有状态的会话：一个用户打开一个浏览器，访问某些资源（网站），下次再来访问该资源（网站），我们会知道这个用户曾经来过，称之为有状态会话；

---

> 一个网站，怎么证明你来过？

1. 服务端给客户端一个信件，客户端下次访问服务端带上信件就可以了；cookie（客户端）
2. 服务器登记你来过了，下次你来的时候我来匹配你；seesion（服务端）

> cookie：

- 客户端技术，（响应、请求）

> session：

- 服务端技术，利用这个技术，可以保存用户的会话信息？我们可以把信息或者数据放在Session中。

---

**会话过程中要解决的一些问题**

1. 每个用户在使用浏览器与服务器进行会话的过程中，不可避免各自会产生一些数据，服 务器要想办法为每个用户保存这些数据
2. 例如：多个用户点击超链接通过一个servlet各自购买了一个商品，服务器应该想办法 把每一个用户购买的商品保存在各自的地方，以便于这些用户点结帐 servlet 时，结帐 servlet可以得到用户各自购买的商品为用户结帐。

---







## Cookie介绍

**Cookie(小甜饼)是客户端技术，服务器把每个用户的数据以cookie的形式写给用户各自的浏 览器。当用户使用浏览器再去访问服务器中的web资源时，就会带着各自的数据去。这样， web资源处理的就是用户各自的数据了。**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230904163051925.png" alt="image-20230904163051925" style="zoom:67%;" />

Cookie 是服务器在客户端保存用户的信息，比如登录名，浏览历史等, 就可以以 cookie 方式保存.

---

> **cookie：一般会保存在本地的用户目录下appdata**

- 一个Cookie只能保存一个信息；
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- Cookie大小有限制4kb
- 300个cookie浏览器上限

---

> **cookie常用方法**

```java
//如何创建一个cookie （服务端创建）
Cookie cookie=new Cookie(String name, String val);

//如何设置cookie的有效期，单位：秒
cookie.setMaxAge();

//如何将一个cookie添加到客户端
response.addCookie(cookie);

//如何读取cookie （客户端）
Cookie[] cookies=request.getCookies();

//如何获得cookie中的key
cookie.getName();

//如何获得cookie中的value
cookie.getValue();

```

---

> **JSESSIONID**

疑问：每个浏览器都会有cookie， tomcat怎么区分是哪个浏览器发出的请求？

答：通过JSESSIONID ，JSESSIONID将保存在客户端的cookie通过http请求发送给服务器

JSESSIONID 就像打电话时的手机号一样，用于区分给谁打电话

不同会话，JSESSIONID  不同 ，JSESSIONID 可以唯一标识一次会话  【每次关闭浏览器再打开访问为一次新会话】

----







## Cookie实例

> 实例一：保存用户上一次访问的时间

```java
// 保存用户上一次访问的时间
public class CookieDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 服务器告诉你，你来的时间，把这个时间封装成一个信息，你下次带来，我就知道你上次来的时间
        // 解决中文乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8"); //设置输出编码
        PrintWriter out = resp.getWriter();
        // Cookie，服务器端从客户端获取cookie
        Cookie[] cookies = req.getCookies();// 数组，说明cookie可以有多个
        // 判断cookie是否
        if (cookies != null) {
            out.write("你上一次登录的时间是：");
            for (int i = 0; i < cookies.length; i++) {
                // 获取cookie的名字
                if (cookies[i].getName().equals("lastLoginTime")) {
                    // 获取cookie的值
                    long l = Long.parseLong(cookies[i].getValue());
                    Date date = new Date(l);
                    out.write(date.toLocaleString());
                    
                    //修改cookie的值为当前登录时间
                    cookies[i].setValue(System.currentTimeMillis() + "");
                    resp.addCookie(cookies[i]); //通知客户端保存修改后的cookie
                }
            }
        } else {
            out.write("你是第一次登录！");
            
            //创建cookie放入
            Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis() + "");
            cookie.setMaxAge(24 * 60 * 60);// 设置cookie的有效期为一天，单位是：秒
            resp.addCookie(cookie);
    }
        
    
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
```

注意，也可以直接同名覆盖

```java
                    //修改cookie的值为当前登录时间
                   // cookies[i].setValue(System.currentTimeMillis() + "");
                  //  resp.addCookie(cookies[i]); //通知客户端保存修改后的cookie
                }
            }
        } else {
            out.write("你是第一次登录！");
    }
            //失败创建cookie放入，存在同名覆盖
            Cookie cookie = new Cookie("lastLoginTime", System.currentTimeMillis() + "");
            cookie.setMaxAge(24 * 60 * 60);// 设置cookie的有效期为一天，单位是：秒
            resp.addCookie(cookie);
```

---

> 实例二：完成自动填写登录账户应用案例 , 如果用户登录成功，则下次登录自动填写登录 账户
>
> ​               要求实现如果登录成功，则该用户，在3天内登录，可以自动填写其登录名
>
> 提示：登录页面需要使用servlet 返回，而不能使用html

**java代码-LogonServlet.java**

作用：接受用户输入，判断是否合法，并返回提示信息,实现自动填写其登录名功能

```java
@WebServlet("/logonServlet")
public class LogonServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //处理请求中文乱码（后期可以使用过滤器来解决）
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        //显示输出
        resp.setContentType("text/html;charset=utf-8"); //设置输出编码
        PrintWriter writer = resp.getWriter();


        //接受表单提交的数据
        String username = req.getParameter("username");
        String pwd = req.getParameter("pwd");

        //判断是否合法
        if (username.equals("root") && pwd.equals("123456")) {


            //实现登录成功后三天之内无需填写用户名（将登录成功的用户信息，以cookie形式保存到浏览器）
            //1.创建cookie
            Cookie logonUserCookie = new Cookie("logonUserCookie", username);
            //2.设置Cookie生命周期
            logonUserCookie.setMaxAge(60 * 60 * 24 * 3);
            //3.将Cookie添加到客户端
            resp.addCookie(logonUserCookie);
            //4.去用户页面 UserUiServlet.java 读取.....

            writer.print("<h1>登录成功</h1>");


        } else {
            writer.print("<h1>登录失败</h1>");
        }
        writer.flush();
        writer.close();

    }
}
```

**java代码-UserUiServlet.java**

作用：显示用户登录页面

```java
package com.wang.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * @author: wang
 * @version: 1.0
 */

@WebServlet("/userUiServlet")
public class UserUiServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //处理请求中文乱码（后期可以使用过滤器来解决）
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8"); //设置输出编码


        //读取从浏览器发送过来的Cookie
        String logonUserCookieName="";
        Cookie logonUserCookie = getCookieByName(req, "logonUserCookie");
        if(logonUserCookie !=null){ //如果有，表示非第一次登录
            //获取cookie的值
            logonUserCookieName = logonUserCookie.getValue();
        }

        //显示输出 servlet返回html页面  注意 form action=  和用户框中 value=\" "+logonUserCookieName+" \"
        PrintWriter writer = resp.getWriter();
        writer.print("<!DOCTYPE html>\n" +
                "<html lang=\"en\">\n" +
                "<head>\n" +
                "  <meta charset=\"UTF-8\">\n" +
                "  <title>登录</title>\n" +
                "</head>\n" +
                "<body>\n" +
                "<h1>用户登录</h1>\n" +
                "<form action=\"http://localhost:8080/servlet/logonServlet\" method=\"post\">\n" +
                "  u: <input type=\"text\" name=\"username\"/ " +
                "value=\" "+ logonUserCookieName +" \" ><br><br>\n" +
                "  p: <input type=\"password\" name=\"pwd\"/><br><br>\n" +
                "  <br/>\n" +
                "  <input type=\"submit\" value=\"登录\"/>\n" +
                "</form>\n" +
                "</body>\n" +
                "</html>");

        writer.flush();
        writer.close();
    }


    //读取cookie
    public Cookie getCookieByName(HttpServletRequest req, String name) {
        Cookie[] cookies = req.getCookies();

        if (!(cookies == null && cookies.length == 0)) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("logonUserCookie")) {
                    return cookie;
                }
            }
        }
        return null;
    }

}

```















## Cookie生命周期

**Cookie 的生命周期指的是如何管理 Cookie 什么时候被销毁（删除）**

> **setMaxAge( ) 设置cookie有效期**
>
> - 正数，表示在指定的秒数后过期
> - 负数，表示浏览器关闭，Cookie 就会被删除（默认值是-1）
> - 0，表示马上删除 Cookie





## 	Cookie有效路径

Cookie 有效路径 Path 的设置

Cookie 的 path 属性可以有效的过滤哪些 Cookie 可以发送给服务器。哪些不发。path属性是通过请求的地址来进行有效的过滤

---

>  规则如下:

```txt
//设置cookie的路径 不设置默认就是 /工程路径 
cookie1.setPath=/工程路径 
cookie2.setPath=/工程路径/aaa

请求地址:http://ip:端口/工程路径/资源 
cookie1 会发给服务器 
cookie2 不会发给服务器

请求地址:http://ip:端口/工程路径/aaa/资源 
cookie1 会发给服务器 
cookie2 会发给服务器
```



## Cookie注意事项

-  一个 Cookie 只能标识一种信息，它至少含有一个标识该信息的名称（NAME）和设置值 （VALUE）。
-  一个WEB站点可以给一个浏览器发送多个Cookie，一个浏览器也可以存储多个WEB站 点提供的Cookie。
- cookie 的总数量没有限制，但是每个域名的 COOKIE 数量和每个 COOKIE 的大小是有限 制的 (不同的浏览器限制不同, 知道即可),Cookie不适合存放数据量大的信息。
- 注意，删除cookie时，path必须一致，否则不会删除

---

> Javaservlet中cookie中文乱码解决

如果存放中文的cookie, 默认报错, 可以通过URL编码和解码来解决, 不建议存 放中文的cookie信息

```java
// 处理的中文乱码问题 -解决：URLDecoder
URLDecoder.decode(cookie.getValue(),"utf-8");
```

---









## Session介绍

**提问**

- 不同的用户登录网站后，不管该用户浏览该网站的哪个页面，都可显示登录人的名字， 还可以随时去查看自己的购物车中的商品, 是如何实现的?
- 一个用户在浏览网站不同页面时，服务器是如何知道是张三在浏览这个页面， 还是李四在浏览这个页面?

**解决-—session技术**

- Session 是服务器端技术，服务器在运行时为每一个用户的浏览器创建一个其独享的 session对象/集合
-  由于session为各个用户浏览器独享，所以用户在访问服务器的不同页面时，可以从各自 的session中读取/添加数据, 从而完成相应任务

---

>  **session 基本原理**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230906123651093.png" alt="image-20230906123651093" style="zoom:67%;" />



1. 当用户打开浏览器，访问某个网站, 操作session时，服务器就会在内存(在服务端)为该 浏览器分配一个session对象，该session对象被这个浏览器独占, 如图
2.  这个session对象也可看做是一个容器/集合,session对象默认存在时间为30min(这是在tomcat/conf/web.xml)，可修改,如下：

```xml
    <session-config>
        <session-timeout>30</session-timeout>
    </session-config>
```

---

 **Session 可以做什么**

1. 网上商城中的购物车
2. 保存登录用户的信息
3. 将数据放入到 Session 中，供用户在访问不同页面时，实现跨页面访问数据
4. 防止用户非法登录到某个页面
5. ....

---

**session 存储结构**

1. 你可以把session 看作是一容器类似HashMap，有两列(K-V)，每一行就是session的一 个属性。
2.  每个属性包含有两个部分，一个是该属性的名字(String)，另外一个是它的值(Object)

---

> **session 常用方法**

```java
//创建和获取 Session，API 一样 （第 1 次调用是创建 Session 会话， 之后调用是获取创建好的 Session 对象）
HttpSession hs=request.getSession();

//向 session 添加属性 （相同name 则覆盖）
hs.setAttribute(String name,Object val);

//从 session 得到某个属性
Object obj=hs.getAttribute(String name);

//从 session 删除调某个属性
hs.removeAttribute(String name);

//isNew(); 判断是不是刚创建出来的 Session
boolean aNew = hs.isNew();

//每个 Session 都有 1 个唯一标识 Id 值。通过 getId() 得到 Session 的会话 id 值
hs.getId();

```



## session 底层实现机制

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230906124741771.png" alt="image-20230906124741771" style="zoom:67%;" />

---

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230906124802440.png" alt="image-20230906124802440" style="zoom:67%;" />







## Session生命周期

1. public void setMaxInactiveInterval(intinterval)  设置 Session 的超时时间（以秒为单位， 超过指定的时长，Session 就会被销毁。
2. 值为正数的时候，设定 Session 的超时时长。
3. 负数表示永不超时
4. public int getMaxInactiveInterval( ) 获取 Session 的超时时间
5. public void invalidate()  让当前 Session 会话立即无效
6. 如果没有调用setMaxInactiveInterval( ) 来指定Session的生命时长，Tomcat会以Session 默认时长为准，Session默认的超时为 30 分钟， 可以在tomcat的web.xml 设置
7. Session的生命周期指的是 ：客户端/浏览器两次请求最大间隔时长，而不是累积时长。 即当客户端访问了自己的session， session的生命周期将从0开始重新计算。 (指的是同一个会话两次请求之间的间隔时间)
8.  底层:Tomcat用一个线程来轮询会话状态， 如果某个会话的空闲时间超过设定的最大值， 则将该会话销毁

---





## Session实例

**一个会话只能有一个Session**

> web.xml  设置会话自动过期

```xml
  <!--设置session默认的失效时间-->
  <session-config>
    <!--15分钟后session自动失效，以分钟为单位-->
    <session-timeout>15</session-timeout>
  </session-config>
```

**实例一：session使用   及手动注销session**

```java
public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // 解决中文乱码
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");
        // 得到session
        HttpSession session = req.getSession();
        // 给session中存东西
        session.setAttribute("name", "张三");
        // 获取session的id
        String sessionId = session.getId();
        // 判断session是不是新创建
        if (session.isNew()) {
            resp.getWriter().write("session创建成功，ID:" + sessionId);
        } else {
            resp.getWriter().write("session已经存在了，ID：" + sessionId);
        }
        // session创建的时候做了什么事情
        /*Cookie cookie = new Cookie("JSESSIONID", sessionId);
        resp.addCookie(cookie);*/
        //------------------
        // 从session中获取数据
        String name = (String) session.getAttribute("name");
        //------------------
        // 从session中删除指定name的数据
        session.removeAttribute("name");
        // 手动注销session
        session.invalidate();
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req, resp);
    }
}
```

---



> **实例二：防止非法进入管理页面**

**前端错误页面-error.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录失败</title>
</head>
<body>
<a href="./log_on.html">登录失败，点击返回登录</a>
</body>
</html>
```

**前端登录页面-log_on.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>登录</title>
</head>
<body>
<h1>用户登录</h1>
<form action="http://localhost:8080/servlet/loginCheckServlet" method="post">
  u: <input type="text" name="username" /><br><br>
  p: <input type="password" name="pwd"/><br><br>
  <br/>
  <input type="submit" value="登录"/>
</form>
</body>
</html>

```

**后端处理登录页面-LoginCheckServlet.java**

```java
@WebServlet("/loginCheckServlet")
public class LoginCheckServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //读取传入的数据
        String username = req.getParameter("username");
        String pwd = req.getParameter("pwd");

        //判断
        if(username.equals("root")&&pwd.equals("000000")){

            //将用户名保存到session
            HttpSession session = req.getSession();
            session.setAttribute("userNameSession",username);

            //请求转发
            RequestDispatcher requestDispatcher = req.getRequestDispatcher("/manageServlet");
            requestDispatcher.forward(req,resp);

        }else {
            //请求转发
            RequestDispatcher requestDispatcher = req.getRequestDispatcher("/error.html");
            requestDispatcher.forward(req,resp);
        }
    }
}

```

**后端管理员页面-ManageServlet.java**

```java
@WebServlet("/manageServlet")
public class ManageServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        // 解决中文乱码
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8"); //设置输出编码


        //判断是否获取到user Session 即是否登录
        HttpSession session = req.getSession();
        Object userNameSession = session.getAttribute("userNameSession");
        if(userNameSession==null ){
            //重定向，重新登录
            resp.sendRedirect(req.getContextPath()+"/log_on.html");
            return;
        }

        PrintWriter writer = resp.getWriter();
        writer.print("<h1>管理页面</h1><br>" +
                "<h4>你好，管理员:"+userNameSession.toString()+"  欢迎进入管理页面<h4>");

        writer.flush();
        writer.close();
    }

}
```







# JSP:后续补充

Java Server Pages  -java 服务页面  用于动态web技术

> 原理

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/kuangstudy91ca1997-e219-4e14-9457-6c0f4ce3ade4.jpg" alt="img" style="zoom:67%;" />

---







# #######监听器&过滤器###########



# 监听器

 **Listener 监听器介绍**

- Listener 监听器它是 JavaWeb 的三大组件之一。  JavaWeb 的三大组件分别是： Servlet 程 序、Listener 监听器、Filter 过滤器
- Listener 是 JavaEE 的规范，就是接口
- 监听器的作用是，监听某种变化(一般就是对象创建/销毁, 属性变化), 触发对应方法完成 相应的任务
- JavaWeb中的监听器（共八个）, 目前最常用的是 ServletContextListener


---





## ServletContextListener

**作用：监听ServletContext创建或销毁(当我们Web应用启动时，就会创建ServletContext)， 即生命周期监听。**

应用场景：(1)加载初始化的配置文件；比如 spring 的配置文件 

​                   (2)任务调 度（配合定时器 Timer/TimerTask)

---

**相关方法**

```java
void contextInitialized(ServletContextEvent sce) //创 建 Servletcontext 时 触 发 
void contextDestroyed(ServletContextEvent sce)  //销毁Servletcontext时
```

---

> **实例：**
>
> * 1.当一个类实现了 ServletContextListener ，该类就是一个监听 ServletContext 对象的创建和销毁的监听者
> * 2.该类可以监听的事件，由该类实现的监听接口决定
> * 3.当web应用启动时，就会产生一个ServletContextEvent事件，会调用监听器对应事件处理方法 contextInitialized 同时传递 事件对象
> * 4.程序员可以通过ServletContextEvent 事件对象，来获取需要的信息，再进行业务处理
> * 5.tomcat怎么知道的？ 因为我们需要在web.xml中配置

**web.xml中配置监听器【也可以直接使用注解@WebListener   该注解作用是使Servlet容器启动时自动注册这个监听器】**

```xml
<listener>
    <listener-class>com.wang.listener.MyServletContextListener</listener-class>
</listener>
```

**监听器-MyServletContextListener.java**

```java
@WebListener
public class MyServletContextListener implements ServletContextListener {

    // ServletContext 初始化时的处理逻辑 (在tomcat启动时触发)
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        System.out.println("MyServletContextListener 监听到："+sce.getServletContext()+"被创建");

        //可以对 ServletContext 进行一些操作，比如添加一些数据...
    }

    // ServletContext 销毁时的处理逻辑 (在tomcat关闭时触发)
    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        System.out.println("MyServletContextListener 监听到："+sce.getServletContext()+"被销毁");

        //可以对 ServletContext 进行一些操作，比如数据处理保存，日志管理....
    }
}
```







## ServletContextAttributeListener

 **作用：监听 ServletContext 属性变化** 很少使用

---

**相关方法**

```java
void attributeAdded(ServletContextAttributeEvent event) //添加属性时调用 
void attributeReplaced(ServletContextAttributeEvent event) //替换属性时调用
void attributeRemoved(ServletContextAttributeEvent event) //移除属性时调用
```

---

> **实例：**

**监听器-MyServletContextAttributeListener.java**

```java
@WebListener
public class MyServletContextAttributeListener implements ServletContextAttributeListener {

    //属性添加触发
    @Override
    public void attributeAdded(ServletContextAttributeEvent event) {

        System.out.println("MyServletContextAttributeListener 监听到属性添加 "+event.getName()+"="+event.getValue());
    }
    
    
    //属性删除触发
    @Override
    public void attributeRemoved(ServletContextAttributeEvent event) {

        System.out.println("MyServletContextAttributeListener 监听到属性删除 "+event.getName()+"="+event.getValue());
    }

    
    //属性替换触发
    @Override
    public void attributeReplaced(ServletContextAttributeEvent event) {
        System.out.println("MyServletContextAttributeListener 监听到属性替换 "+event.getName()+"="+event.getValue());

    }
}
```

**测试代码-任意文件中配置ServletContext都可以**

```java
        //可以对 ServletContext 进行一些操作，比如添加一些数据...
        ServletContext servletContext = sce.getServletContext();
        servletContext.setAttribute("name","wang");
        servletContext.setAttribute("name","bang");
```

---



##  HttpSessionListener 

**作用：监听 Session 创建或销毁，即生命周期监听**

---

**常用方法**

```java
void sessionCreated(HttpSessionEvent se) //创建 session 时 调 用 
void sessionDestroyed(HttpSessionEvent se) //销毁session时调
```

 **使用方法和前面一样, 可以用于监控用户上线，离线**

---

> **实例**

**监听器-MyHttpSessionListener.java**

```java
@WebListener
public class MyHttpSessionListener implements HttpSessionListener {

    //session创建触发
    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener 监听到 "+se.getSession().getId()+"创建");
    }

    //session销毁触发
    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener 监听到 "+se.getSession().getId()+"销毁");
    }
}

```

**测试-java**

```java
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException

        //获取session对象 （有返回，无创建）
        HttpSession session = req.getSession();
		//销毁session
        session.invalidate();

    }
```

---





## HttpSessionAttributeListener 

**作用：监听 Session 属性的变化**

---

**相关方法**

```java
void attributeAdded(ServletRequestAttributeEvent srae) //添加属性时 
void attributeReplaced(ServletRequestAttributeEvent srae) //替换属性时
void attributeRemoved(ServletRequestAttributeEvent srae) //移除属性时
```

**使用少 ， 使用方法和前面一样。**

---

> **实例**

**监听器-MyHttpSessionAttributeListener.java**

```java
@WebListener
public class MyHttpSessionAttributeListener implements HttpSessionAttributeListener {

    //添加Session 属性时
    @Override
    public void attributeAdded(HttpSessionBindingEvent event) {
        System.out.println("MyHttpSessionAttributeListener 监听到 session "+event.getName()+"的属性被添加"+event.getValue());

    }

    //修改添加Session属性时
    @Override
    public void attributeReplaced(HttpSessionBindingEvent event) {
        System.out.println("MyHttpSessionAttributeListener 监听到 session "+event.getName()+"的属性被修改"+event.getValue());

    }

    //移除session属性时
    @Override
    public void attributeRemoved(HttpSessionBindingEvent event) {
        System.out.println("MyHttpSessionAttributeListener 监听到 session "+event.getName()+"的属性被删除"+event.getValue());

    }
}
```

**测试**

```java
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //获取session对象 （有返回，无创建）
        HttpSession session = req.getSession();
        session.setAttribute("name","wang");
        session.setAttribute("name","ha");
        session.removeAttribute("name");
        session.invalidate();
    }
```

---





## ServletRequestListener 

**作用：监听Request创建或销毁，即Request生命周期监听**

---

**相关方法**

```java
void requestInitialized(ServletRequestEvent sre) //创建request时 
void requestDestroyed(ServletRequestEvent sre) //销毁request时
```

**可以用来监控, 某个IP访问我们网站的频率, 日志记录 ,访问资源的情况.**

---

> **实例**

**监听器-MyServletRequestListener.java**

```java
@WebListener
public class MyServletRequestListener implements ServletRequestListener {

    //创建request时
    @Override
    public void requestInitialized(ServletRequestEvent sre) {
        ServletRequest servletRequest = sre.getServletRequest();
        System.out.println("MyServletRequestListener 监听到 创建request："+servletRequest);
        System.out.println("该请求访问ip="+servletRequest.getRemoteAddr());
        System.out.println("该请求访问的资源="+((HttpServletRequest)servletRequest).getRequestURL());
    }

    //销毁request时
    @Override
    public void requestDestroyed(ServletRequestEvent sre) {
        ServletRequest servletRequest = sre.getServletRequest();
        System.out.println("MyServletRequestListener 监听到 销毁 request："+servletRequest);

    }
}
```

**测试**-随便访问一个servlet页面就可以了

---









## ServletRequestAttributeListener 

**作用：监听 Request 属性变化**

---

**相关方法**

```java
void attributeAdded(ServletRequestAttributeEvent srae) 添加属性时 
void attributeReplaced(ServletRequestAttributeEvent srae) 替换属性时
void attributeRemoved(ServletRequestAttributeEvent srae)移除属性时
```

**使用方法和前面类似**



## HttpSessionBindingListener 

**作用：用于监听某个对象是否被绑定到`HttpSession`中或从`HttpSession`中解绑的事件。**

---

**相关方法**

```java
valueBound(HttpSessionBindingEvent event) //当对象被绑定到HttpSession中时触发该事件
valueUnbound(HttpSessionBindingEvent event)//当对象从HttpSession中解绑时触发该事件
```

**在对象绑定和解绑时提供回调方法，以便在相关事件发生时执行相应的逻辑**

---





## HttpSessionActivationListener 

**作用：用于监听`HttpSession`对象的活化(即从磁盘反序列化)和钝化(即序列化到磁盘)事件。**

---

**相关方法**

```java
sessionWillPassivate(HttpSessionEvent se) //当HttpSession对象将要被钝化（即序列化到磁盘）时触发该事件。
sessionDidActivate(HttpSessionEvent se) //当HttpSession对象从钝化状态被激活（即从磁盘反序列化）时触发该事件
```

**可以利用`HttpSessionActivationListener`来准备对象以在钝化时保存必要的状态，并在激活时还原这些状态。**

---





# 过滤器

> **过滤器介绍**

- Filter 过滤器它是 JavaWeb 的三大组件之一(Servlet 程序、Listener 监听器、Filter 过 滤器)
- Filter 过滤器是 JavaEE 的规范，是接口
- Filter 过滤器它的作用是：拦截请求，过滤响应。

---

> **为什么需要过滤器**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230907161924733.png" alt="image-20230907161924733" style="zoom:67%;" />

---

> **应用场景**

- 权限检查
- 日记操作
- 事务管理

---



## Filter 过滤器基本原理

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230907162201542.png" alt="image-20230907162201542" style="zoom: 80%;" />

---



## Filter 过滤器基本配置

**1.需要实现Filter接口**

```java
@WebFilter("/manage/*")  // 访问/manage下资源则调用filter
public class ManageFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
      //到每次调用该filter时，doFilter被调用
        
        
        //如果这里，没有调用继续请求的方法，就停止

        //如果继续访问目标资源 --->等价于放行  （filterChain.doFilter 传走req和reps）
        //1.在调用过滤器前，request对象已经被创建并封装，所以可以直接通过request获取数据
        //2.servletRequest可以获取很多对象，比如url、session、访问的参数 。。。
        //3.可以做事务管理，数据获取，日志管理。。。
        filterChain.doFilter(servletRequest,servletResponse);
    }

    @Override
    public void destroy() {
        //Filter被销毁，destroy被调用
    }
}
```

**2.web.xml中配置过滤器【也可以直接使用注解@WebFilter("/manage/*")   该注解作用是使Servlet容器启动时自动注册这个过滤器】**

```xml
<filter>
    <filter-name>ManageFilter</filter-name>
    <filter-class>com.wang.filter.ManageFilter</filter-class>
</filter>
    <filter-mapping>
        <filter-name>ManageFilter</filter-name>
    <!--url-pattern 配置拦截路径，一旦有请求该路径，则调用过滤器 比如下面就是请求/manage文件下资源就会启动过滤器-->
        <url-pattern>/manage/*</url-pattern>
    </filter-mapping>
```

---







## Filter简单实例：登录访问

> 需求: 在 web 工程下，有后台管理目录 manage，要求该目录下所有资源（html、图片、 jsp 、Servlet 等）用户登录后才能访问
>

**后端登录验证-LoginCheckServlet.java**

```java
@WebServlet("/loginCheckServlet")
public class LoginCheckServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //读取传入的数据
        String username = req.getParameter("username");
        String pwd = req.getParameter("pwd");

        //判断
        if(username.equals("root")&&pwd.equals("000000")){

            //将用户名加入session
            HttpSession session = req.getSession();
            session.setAttribute("name",username);

            //请求转发 （请求转发是不经过过滤器的）
            RequestDispatcher requestDispatcher = req.getRequestDispatcher("/manage.html");
            requestDispatcher.forward(req,resp);

        }else {
            //请求转发
            RequestDispatcher requestDispatcher = req.getRequestDispatcher("/error.html");
            requestDispatcher.forward(req,resp);
       }
    }
}
```

**过滤器配置-ManageFilter.java**

```java
@WebFilter("/img/*")
public class ManageFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println("init");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //到每次调用该filter时，doFilter被调用
        System.out.println("doFilter");

        //获取session
        HttpSession session = ((HttpServletRequest) servletRequest).getSession();
        Object name = session.getAttribute("name");

        //判断
        if(name!=null){
            //放行
            filterChain.doFilter(servletRequest,servletResponse);
        }else {
            //回到登录页 请求转发
            RequestDispatcher requestDispatcher = servletRequest.getRequestDispatcher("/log_on.html");
            requestDispatcher.forward(servletRequest,servletResponse);
        }
    }
    @Override
    public void destroy() {

        //Filter被销毁，destroy被调用
        System.out.println("destroy");
    }
}
```

> **注意：**
>
> 1.url-pattern 配 置 拦 截 路 径  /manage/*
>
> 2.第 1个 / 被 服 务 器 解 析 为 ： http://ip:port/ 工 程 路 径 / 
>
> 3./manage/*  表 示 ： http://ip:port/ 工 程 路 径 /manage/* 所 有 资 源 请 求 都 经 过 该 过滤 器
>
> 4.请求转发是不经过过滤器的
>
> ---
>
> Filter 过滤器它只关心请求的地址是否匹配，不关心请求的资源是否存在

---





## Filter生命周期

![image-20230908161007491](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230908161007491.png)

---

> 1. filter 在web 项目启动时，由tomcat 来创建一个 filter实例，只会创建一次
> 2. 会调用filter默认的无参构造器，同时会调用init方法，只会调用一次
> 3. 在创建filter实例时，同时会创建一个FilterConfig对象，并通过init方法传入
> 4. 通过FilterConfig对象，程序员可以获取该filter相关配置
> 5. 当一个http请求和该filter的url-patter匹配时，就会调用doFilter方法
> 6. 在调用doFilter方法时，tomcat会同时创建ServletRequest和ServletResponse和FilterChain对象，并通过doFilter传入
> 7. 如果后面的请求目标资源(jsp,servlet,...) 会使用到request和response，那么会继续传递使用

---



 



## FilterConfig

**介绍**

- FilterConfig是Filter 过滤器的配置类
- Tomcat 每次创建 Filter 的时候，会创建一个 FilterConfig 对象，这里包含了 Filter 配 置文件的配置信息
- **FilterConfig 对象作用是获取 filter 过滤器的配置内容**

---

**FilterConfig 接口图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230908181235034.png" alt="image-20230908181235034" style="zoom:67%;" />

---

web.xml

```xml
    <filter>
        <filter-name>FilterConfig</filter-name>
        <filter-class>com.wang.filter.ManageFilter</filter-class>
        <init-param>
            <!--这里就是给filter配置的参数  -->
            <param-name>ip</param-name>
            <param-value>128.12</param-value>
        </init-param>
        <init-param>
            <param-name>port</param-name>
            <param-value>8888</param-value>
        </init-param>
    </filter>
    
    <filter-mapping>
        <filter-name>FilterConfig</filter-name>
        <url-pattern>/img/*</url-pattern>
    </filter-mapping>

```

如果使用注解方式：

```java
@WebFilter(filterName = "FilterConfig", urlPatterns = {"/img/*"}, initParams = {
        @WebInitParam(name = "ip", value = "128.12"),
        @WebInitParam(name = "port", value = "8888")
}, dispatcherTypes = {DispatcherType.REQUEST})
public class ManageFilter implements Filter{
    
}
//@WebFilter注解来标记该类是一个过滤器。其中，urlPatterns属性指定过滤器作用的URL模式，
//initParams属性用于传递初始化参数，
//dispatcherTypes属性用于指定过滤器的调度类型。
```

java使用

```java
public class ManageFilter implements Filter {
    
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println("init");
        //通过 filterConfig 获取相关参数
        String filterName = filterConfig.getFilterName(); //filter的名字
        System.out.println("filterName= " + filterName);
        String ip = filterConfig.getInitParameter("ip");
        System.out.println("ip= " + ip);

        //通信机制 ServletContext
        ServletContext servletContext = filterConfig.getServletContext(); 
        System.out.println("servletContext= " + servletContext);

        //获取所有初始化参数名字 枚举
        Enumeration<String> initParameterNames =filterConfig.getInitParameterNames();
        //遍历枚举
        while (initParameterNames.hasMoreElements()) {
            System.out.println(initParameterNames.nextElement());
        }
        
    }    
}
```

---





## FilterConfig简单实例

>  如果访问ip是127.0 网段开始的就返回登录页面,【即封杀某一网段，禁止其访问资源】

**web.xml配置**

```xml
    <filter>
        <filter-name>FilterConfig</filter-name>
        <filter-class>com.wang.filter.ManageFilter</filter-class>
        <init-param>
            <!--这里就是给filter配置的参数  -->
            <param-name>ip</param-name>
            <param-value>127.0</param-value>
        </init-param>
        <init-param>
            <param-name>port</param-name>
            <param-value>8888</param-value>
        </init-param>
    </filter>
    
    <filter-mapping>
        <filter-name>FilterConfig</filter-name>
        <url-pattern>/img/*</url-pattern>
    </filter-mapping>
```

**过滤器**

```java
public class ManageFilter implements Filter {

    private String ip; //从配置中取的禁用ip

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println("init");
        //通过 filterConfig 获取相关参数
        ip = filterConfig.getInitParameter("ip");
        System.out.println("封杀ip= " + ip);

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //到每次调用该filter时，doFilter被调用
        System.out.println("doFilter");

        //1.先获取到访问者ip
        String remoteAddr = servletRequest.getRemoteAddr();
        System.out.println("您的访问ip=" + remoteAddr);

        //2.判断  remoteAddr.contains(ip)是一个用于检查请求的远程IP地址是否包含指定的IP段的逻辑表达式。
        if (remoteAddr.contains(ip)) {
            System.out.println("ip网段=" + ip + "已被封杀");
            //回到登录页 请求转发
            RequestDispatcher requestDispatcher = servletRequest.getRequestDispatcher("/log_on.html");
            requestDispatcher.forward(servletRequest, servletResponse);
            return;
        }
        //放行
        System.out.println("ManageFilter 放行");
        filterChain.doFilter(servletRequest, servletResponse);


    }

    @Override
    public void destroy() {

        //Filter被销毁，destroy被调用
        System.out.println("destroy");
    }
}

```

> **注意：**
>
> 本机开发测试，ipv4为127.0.0.1  ；ipv6为0:0:0:0:0:0:0:1 ；

---



## 过滤器链 FilterChain

FilterChain: 在处理某些复杂业务时，一个过滤器不够，可以设计多个过滤器共同完成过滤任务，形成过滤器链。

![image-20230909095442136](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909095442136.png)

---



## 过滤器链FilterChain基本使用

> 演示过滤器链的使用

![image-20230909095935065](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909095935065.png)

---

**AFilter**

```java
public class AFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println(  "AFilter init");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //到每次调用该filter时，doFilter被调用
        System.out.println(" AFilter doFilter 前置代码");

        //放行
        System.out.println("AFilter filterChain.doFilter 放行");
        filterChain.doFilter(servletRequest, servletResponse);
        
        System.out.println(" AFilter doFilter 后置代码");
    }

    @Override
    public void destroy() {

        //Filter被销毁，destroy被调用
        System.out.println("destroy");
    }
}
```

**Bfilter**

```java
public class Bfilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println(" Bfilter init");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //到每次调用该filter时，doFilter被调用
        System.out.println(" Bfilter doFilter 前置代码");

        //放行
        System.out.println("Bfilter filterChain.doFilter 放行");
        filterChain.doFilter(servletRequest, servletResponse);

        System.out.println(" Bfilter doFilter 后置代码");
    }

    @Override
    public void destroy() {

        //Filter被销毁，destroy被调用
        System.out.println("destroy");
    }
}
```

**web.xml**

```xml
    <filter>
        <filter-name>AConfig</filter-name>
        <filter-class>com.wang.filter.AFilter</filter-class>
    </filter>
	<filter-mapping>
        <filter-name>AConfig</filter-name>
        <url-pattern>/admin/*</url-pattern>
    </filter-mapping>

    <filter>
        <filter-name>BConfig</filter-name>
        <filter-class>com.wang.filter.Bfilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>BConfig</filter-name>
        <url-pattern>/admin/*</url-pattern>
    </filter-mapping>
```

> **当访问admin目录下资源时，打印顺序为：**
>
> AFilter init
>
> Bfilter init
>
> AFilter doFilter 前置代码
>
> AFilter filterChain.doFilter 放行
>
> Bfilter doFilter 前置代码
>
> Bfilter filterChain.doFilter 放行
>
> Bfilter doFilter 后置代码
>
> AFilter doFilter 后置代码

---





## 过滤器链FilterChain注意事项

- 多个 filter 和目标资源在一次 http 请求，在同一个线程中
- 当一个请求 url 和 filter 的 url-pattern 匹配时, 才会被执行, 如果有多个匹配上，就会 顺序执行，形成一个 filter 调用链(底层可以使用一个数据结构搞定)
-  多个 filter 共同执行时,因为是一次 http 请求, 使用同一个 request 对象
- 多个 filter 执行顺序，和 web.xml 配置顺序保持一致
- chain.doFilter(req,resp)方法 将执行下一个过滤器的doFilter方法, 如果后面没有过滤器，则执行目标资源

---

**小结：**

执行过滤器链时, 顺序是(用前面的案例分析)Http请求 ->A过滤器 dofilter() ->A 过滤器前置代码 ->A 过滤器 chain.doFilter()->B 过滤器 dofilter()-> B 过滤器前置代 码 ->B过滤器 chain.doFilter()-> 目标文件 ->B过滤器后置代码 ->A过滤器后置代码 -> 返回给浏览器页面/数据

---





## Filter实例

**需求分析: 使用过滤器, 完成如下要求**

1. 点击发表评论页面topic.jsp, 可以在showTopic.jsp显示评论内容
2. 如果发表的评论内容,有关键字比如 "苹果""香蕉", 就返回topic.jsp, 并提示有禁用词
3. 要求发表评论到showTopic.jsp 时，经过过滤器的处理
4.  禁用词, 配置在过滤器, 在启动项目时动态的获取, 注意处理中文

---

**前端评论发布页面-topic.jsp**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head><title>发表评论</title></head>
<body>
<h1>发表对阿凡达电影评论</h1>
过滤词: 苹果, 香蕉 ~~${info}
<form method="post" action="<%=request.getContextPath()%>/comment/showTopic.jsp">
    用户: <input type="text" name="username"><br/>
    评论: <textarea rows="10" name="content" cols="20"></textarea><br/>
    <input type="submit" value="发表评论">
</form>
</body>
</html>
```

**前端评论显示页面-showTopic.jsp**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head><title>评论显示</title></head>
<body>
<h1>你发表的评论是</h1>
评论内容:<%=request.getParameter("content")%>
</body>
</html>
```

**过滤器配置-TopicFilter.java**

```java
public class TopicFilter implements Filter {
    //敏感词
    private String[] sensitive;

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        //当Tomcat创建 Filter创建，就会调用该方法，初始化
        System.out.println("TopicFilter init");

        //获取filter配置
        String ssv = filterConfig.getInitParameter("sensitive");
        sensitive = ssv.split("、");
        System.out.println("敏感词有="+ssv);

    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        //中文乱码
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");

        //获取评论内容
        String content = servletRequest.getParameter("content");

        //判断是否包含
        for (String s : sensitive) {
            if(content.contains(s)){
                System.out.println("TopicFilter filterChain.doFilter 已拦截");

                //写入提示信息并请求转发回评论页
                servletRequest.setAttribute("info","有敏感词");
                RequestDispatcher requestDispatcher = servletRequest.getRequestDispatcher("/comment/topic.jsp");
                requestDispatcher.forward(servletRequest,servletResponse);
                return;
            }
        }

        //不包含放行
        System.out.println("TopicFilter filterChain.doFilter 放行");
        filterChain.doFilter(servletRequest, servletResponse);
    }

    @Override
    public void destroy() {

        //Filter被销毁，destroy被调用
        System.out.println("destroy");
    }
}

```

**web.xml配置**

```xml
    <filter>
        <filter-name>topicFilter</filter-name>
        <filter-class>com.wang.filter.TopicFilter</filter-class>
        <init-param>
            <param-name>sensitive</param-name>
            <param-value>苹果、香蕉</param-value>
        </init-param>
    </filter>

    <filter-mapping>
        <filter-name>topicFilter</filter-name>
        <url-pattern>/comment/showTopic.jsp</url-pattern>
    </filter-mapping>
```

----





# ##############jQuery#################

# 后续补充





# ###########Json&Ajax###############

数据交换和异步请求 -JSON&Ajax

JSon 在线文档：https://www.w3school.com.cn/js/js_json_intro.asp

Ajax 在线文档：https://www.w3school.com.cn/js/js_ajax_intro.asp

---



# Json

> **介绍**

- JSON 指的是 JavaScript 对象表示法（JavaScriptObjectNotation）
- JSON 是轻量级的文本数据交换格式
- JSON 独立于语言 [即 java 、php、asp.net,go 等都可以使用 JSON]
- JSON 具有自我描述性，更易理解, 一句话，非常的好用..

---

> **Json定义格式**

```json
var 变量名 ={ 
    "k1":value,  //Number 类型 
    "k2" : "value",  // 字符串类型
	"k3":[],    // 数组类型 
    "k4":{},    //json 对象类型 
    "k5":[{},{}] //json 数组 
};
```

> **规则**

- 映射(元素/属性)用冒号 : 表示，"名称":值 , 注意名称是字符串，因此要用双引号引起来
- 并列的数据之间用逗号 , 分隔。"名称 1":值,"名称 2":值
- 映射的集合(对象)用大括号 {} 表示。{"名称 1":值,"名称 2":值}
- 并列数据的集合（数组）用方括号 [] 表示。 [{"名称 1":值,"名称 2":值},{"名称 1":值," 名称 2":值}]
- 元素值类型：string,number,object,array,true,false,null

---



## Json与字符串转换

> **相关方法**

```java
JSON.stringify(json)  //功能: 将一个 json 对象转换成为 json 字符串
JSON.parse(jsonString)  //功能: 将一个 json 字符串转换成为 json 对象
```

---

> **Json转字符串 简单应用**

```js
var jsonPerson={
    "name":"jack",
    "age":20
}

console.log(jsonPerson+"类型="+typeof jsonPerson);
var s = JSON.stringify(jsonPerson);
console.log(s+"类型="+typeof s);
```

**输出：**

[object Object]类型=object         

{"name":"jack","age":20}类型=string

---

> **字符串转Json 简单应用**

```js
//注意：要使string转为json ，该string的格式必须满足json格式
var str="{\"name\":\"jack\",\"age\":\"20\"}";

console.log(str+"类型="+typeof str);
var parse = JSON.parse(str);
console.log(parse+"类型="+typeof parse);
```

**输出：**

{"name":"jack","age":"20"}类型=string

[object Object]类型=object

---



## Json在java中的使用

> **说明：**

- java 中使用 json，需要引入到第 3 方的包 gson.jar
- Gson 是 Google 提供的用来在 Java 对象和 JSON 数据之间进行映射的 Java 类库
- 可以对 JSON 字符串 和 Java 对象相互转换

---

> **应用场景**

1. Javabean 对象和 json 字符串 的转换
2. List 对象和 json 字符串 的转换
3. map 对象和 json 字符串 的转换

---





## java对象与json互转

**maven导入Gson**

```xml
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.8.8</version>
    </dependency>
```

**java代码**

```java
public class javaJson {
    public static void main(String[] args) {
        //创建Gson 对象，作为一个工具类使用
        Gson gson=new Gson();

        Book book=new Book(100,"java");

        //把java对象转换为Json
        String s = gson.toJson(book);
        System.out.println(s);
        
        //把Json转换为java对象  （底层使用的反射）
        Book book1 = gson.fromJson(s, Book.class);
        System.out.println(book1);

    }
}
```





## List集合与Json互转

**首先：maven导入Gson**

> **java代码-list对象转换为json**

```java
public class javaJson {

    public static void main(String[] args) {
        //创建Gson 对象，作为一个工具类使用
        Gson gson=new Gson();

        List bookList=new ArrayList<>();
        bookList.add(new Book(101,"java"));
        bookList.add(new Book(102,"c++"));


        //list对象转换为json
        String str = gson.toJson(bookList);
        System.out.println(str);
    }
}
```

> **java代码-json转换为List对象**
>
> 1. 如果需要把json转换成复杂的List ,需要使用gson中提供的一个类 TypeToken
> 2. TypeToken 是一个自定义泛型，提供TypeToken 来指定我们要转换成的类型
> 3. 因为其他包也可能有我们徐娅转换的类，所以必须要完整路径反射，所以gson设计者就提供TypeToken 
> 4. TypeToken<List<Book>>(){}.getType() 是返回的类型的完整路径 java.util.List<com.wang.bean.Book>
> 5. TypeToken<List<Book>>(){} 实际上是一个匿名内部类无参构造

```java
        //json字符串转List对象
        //gson的设计者，需要得到类型的完整路径，然后进行底层反射
        //返回的类型的完整路径  java.util.List<com.wang.bean.Book>
        Type type=new TypeToken<List<Book>>(){}.getType();

        List<Book> listBook = gson.fromJson(str, type);
        System.out.println(listBook);
```

---





## Map对象与Json互转

**首先：maven导入Gson**

> **java代码**
>
> 如果需要把json转换成复杂的Map,需要使用gson中提供的一个类 TypeToken

```java
public class javaJson {

    public static void main(String[] args) {
        //创建Gson 对象，作为一个工具类使用
        Gson gson=new Gson();

        Map<String,Book> bookMap=new HashMap<>();
        bookMap.put("k1",new Book(103,"python"));
        bookMap.put("k2",new Book(104,"go"));
        
        //Map对象转换为json
        String strJson = gson.toJson(bookMap);
        System.out.println(strJson);

        //json字符串转Map对象
        Type type=new TypeToken<Map<String,Book>>(){}.getType();
        Map<String,Book> mapBook = gson.fromJson(strJson, type);
        System.out.println(mapBook);
        
    }
}
```

---



# Json更适用

基本格式：必须是对象{}或数组【】

---

值可以是数组对象，就意味着数据和对象可以任意嵌套、任意深度

如果需要处理LocalDateTime的json数据，不管是序列化还是反序列化，都需要在定义的字段上添加注解：

```java
@JsonDeserialize(using = LocalDateTimeDeserializer.class)
@JsonSerialize(using = LocalDateTimeSerializer.class)
@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")
```

---

> **maven添加jackson**

```xml
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.12.4</version>
    </dependency>
```

> **jackson介绍：**
>
> - `jackson-databind`模块提供了Jackson库的数据绑定功能，包括JSON序列化和反序列化。它允许您将Java对象序列化为JSON格式的字符串，以及将JSON格式的字符串反序列化为Java对象。
>
> - `ObjectMapper`类：这是Jackson库的核心类，在序列化和反序列化过程中起到关键作用。它提供了各种方法，用于将Java对象与JSON格式的字符串进行相互转换。
> - 注解：`jackson-databind`模块支持多种注解，用于自定义对象与JSON之间的映射关系，例如`@JsonProperty`、`@JsonFormat`等。
> - 配置选项：通过`ObjectMapper`类，您可以应用各种配置选项，例如设置日期格式、忽略空值字段等。

---





## 字符串集合转Json -序列化

```java
List<String> Str=new ArrayList<>();
Str.add("hello");
Str.add("world");
ObjectMapper mapper=new ObjectMapper();  //创建Jackson的核心对象ObjectMapper
try {
    //调用 writeValueAsString，将指定的对象转换成json
    String jsonstr = mapper.writeValueAsString(Str);  
    System.out.println(jsonstr);
}catch (Exception e){
    System.out.println(e);
}
```



## 单个对象转Json { }-序列化

```java
User user=new User();
user.setUserName("tom");
user.setPassword("tom123");
user.setGmtCreated(LocalDateTime.now());

//创建Jackson的核心对象ObjectMapper
ObjectMapper mapper=new ObjectMapper(); 

try {
    //调用 writeValueAsString，将指定的对象转换成json
    String jonsUser = mapper.writeValueAsString(user); 
    System.out.println(jonsUser);
    
}catch (Exception e){
    System.out.println(e);
}
```





## 集合对象转Json [ ] -序列化

```java
List<User> users = new ArrayList<>();

User user=new User();
user.setUserName("tom");
user.setPassword("tom123");
user.setGmtCreated(LocalDateTime.now());
users.add(user);

//创建Jackson的核心对象ObjectMapper
ObjectMapper mapper=new ObjectMapper();
try {
    //调用 writeValueAsString，将指定的对象转换成json
    String jonsUsers = mapper.writeValueAsString(users);
    System.out.println(jonsUsers);
    
}catch (Exception e){
    System.out.println(e);
}
```



## Json转化为对象集合-反序列化

```java
public static  List<SongList> songList=new ArrayList<SongList>();
songList= JSONArray.parseArray(content,SongList.class);
```



## Json转化为对象数组-反序列化

```java
SongList[] lists = JSON.parseObject(jsonString, SongList[].class);
```





## json文件转为User对象 -反序列化

> **Json形式单个对象转java对象：{ } -反序列化**

```java
ObjectMapper mapper=new ObjectMapper();

try {
    //将指定的文件夹中的内容读取出来以String的形式来显示 
    String content = FileUtils.readFileToString(new File("./data/users.json"), "utf-8");

    //转换
    User user = mapper.readValue(content, User.class);
    System.out.println(user.getUserName());
} catch (IOException e) {
    e.printStackTrace();
}
```

---



## json文件转为List集合-反序列化

> **Json形式多对象转换为java对象：[{ },{ }] -反序列化**

```java
ObjectMapper mapper=new ObjectMapper();
try {
    //将指定的文件夹中的内容读取出来以String的形式来显示
    String content = FileUtils.readFileToString(new File("./data/users.json"), "utf-8");
    //将Json字符串反序列化为List<User>集合
    List<User>users=mapper.readValue(content, new TypeReference<List<User>>() {
});
    for (User user : users) {
        System.out.println(user.getUserName());
    }
} catch (Exception e) {
    e.printStackTrace();
}
```



## JSON文件读取到集合

```java
static{
    if (usersFile.exists()) {//判空
        try {
            //将字符串写入到文件当中
            String conent = FileUtils.readFileToString(usersFile, "utf-8");
            List<User> users1 = mapper.readValue(conent, new TypeReference<List<User>>() {
        });
            users.addAll(users1); //将集合数据添加到集合
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```







# Ajax

> **介绍**

AJAX 即"AsynchronousJavascriptAndXML"(异步 JavaScript 和 XML)

Ajax 是一种浏览器异步发起请求(指定发哪些数据)，局部更新页面的技术

---

Ajax在线文档：https://www.w3school.com.cn/js/js_ajax_intro.asp

---

> **Ajax 经典应用场景**

- 搜索引擎根据用户输入关键字，自动提示检索关键字
- 动态加载数据，按需取得数据【树形菜单、联动菜单...】
- 改善用户体验。【输入内容前提示、带进度条文件上传...】
- 电子商务应用。 【购物车、邮件订阅...】
- 访问第三方服务。【访问搜索服务、rss阅读器】
- 页面局部刷新,https://piaofang.maoyan.com/dashboard

---





# Ajax 数据通信原理图

> **传统web应用**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909140103889.png" style="zoom:67%;" />

---

> **Ajax 原理示意图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909140142780.png" alt="image-20230909140142780" style="zoom:67%;" />

---

**Ajax相关方法**

```java
//创建 XMLHttpRequest 对象
variable = new XMLHttpRequest();

//向服务器发送请求
xhttp.open("GET", "ajax_info.txt", true); //参数:规定请求的类型、文件位置、同步false异步true 
xhttp.send(); //无参仅限GET 
xhttp.send(String); //有参仅限POST

//服务器响应属性 使用XMLHttpRequest对象的 responseText或responseXML属性
responseText //获取字符串形式的响应数据
responseXML  //获取 XML 数据形式的响应数据
    
```

![image-20230909171818157](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909171818157.png)

---





# Ajax实例-验证用户名是否存在

**演示 javascript 发送原生 ajax 请求的案例**

1. 在输入框输入用户名
2. 点击验证用户名, 使用 ajax方式， 服务端验证该用户名是否已经占用了, 如果该用户已经占用, 以json格式返回该用户信息
3. 假定用户名为 king, 就不可用, 其它用户名可以=》 后面我们接入DB[Mysql+JDBC]
4. 对页面进行局部刷新, 显示返回信息

---

**思路分析=> 程序框架图**

<img src="https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230909193750682.png" alt="image-20230909193750682" style="zoom:67%;" />

---

**登录页面-Log_on.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>登录</title>
  <script type="text/javascript">

    var checkUser=function () {

      //获取 Id 为 userName 的dom对象  【用户名输入框】
      var elementById = document.getElementById("userName");
      //获取 userName 值 【输入的用户名】
      var userName = elementById.value;

      //1.创建 XMLHttpRequest 对象 [ajax引擎对象]
      var xmlHttpRequest = new  XMLHttpRequest();
      //2.准备发送指定数据
      xmlHttpRequest.open("GET","http://localhost:8080/servlet/checkUserServlet?userName="+userName,true);


      //在 send 函数调用前，给 xmlHttpRequest 绑定一个事件 onreadystatechange 该事件可以指定一个函数，当数据变化时触发
      //每当 xmlHttpRequest 对象的 readyState 改变时，就会触发 onreadystatechange
      xmlHttpRequest.onreadystatechange=function (){
        //如果请求已完成且响应以就绪(即 readyState=4)，并状态码成功（即status:200）
        if(xmlHttpRequest.readyState==4 && xmlHttpRequest.status==200){

          //得到返回的数据 (业务处理页面 checkUserServlet 处返回的数据)
          var responseText = xmlHttpRequest.responseText;
          //判断返回的数据
          if(responseText!=""){
            document.getElementById("error").value="用户名不存在";
            return;
          }
          document.getElementById("error").value="用户名存在";
        }
      }

      //3.发送数据
      xmlHttpRequest.send();
    }
  </script>

</head>
<body>
<h1>用户登录</h1>
<form action="http://localhost:8080/servlet/checkUserServlet" method="post">
  u: <input type="text" name="userName" id="userName"/>
  <input type="button" onclick="checkUser();" value="用户名验证">
    
    <!--接收局部刷新的数据-->
  <input style="border-width: 0;color: red" type="text" id="error"><br><br>
  p: <input type="password" name="userPwd"/><br><br>
  <br/>
  <input type="submit" value="登录"/>
</form>
</body>
</html>
```

**后端业务处理-CheckUserServlet.java**

```java
@WebServlet("/checkUserServlet")
public class CheckUserServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //设置中文
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");

        //接受ajax提交的数据  [和ajax（GET/POST）提交的名字一致  ?userName= ]
        String userName = req.getParameter("userName");
        System.out.println(userName);

        //判断 设用户名非 root，就不可用
        if(!userName.equals("root")){ //不可用
            
            //不可用的用户 （应该从DB中匹配，这里直接手动创建）
            User notRootUser=new User(userName,"000000");
            //转json
            String userJson = new Gson().toJson(notRootUser);

            //返回
            resp.getWriter().write(userJson);
            return;
        }
        //可用 返回空
        resp.getWriter().write("");
    }
}
```







# JQuery操作Ajax：后续补充





