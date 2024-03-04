



# 系统常用命令

> 关机与重启

```shell
sync  #将数据由内存同步到硬盘

shutdown   #关机

shutdown -h 10  #十分钟后关机

shutdown -h 10：00  #今天10：00关机

shutdown -h now  #立即关机

reboot  #重启

shutdown -r now  #立即重启

shutdown -r +10  #十分钟后重启

halt   #关闭系统



#启动开机自启命令
systemctl start [软件名]
systemctl enable [软件名]
```



# 系统目录详解

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7LDkhrDl4H9TqZhwyeNSeaNibQYW2xbQIL38lrCCSPEzFKJhCiau0FvQMFSa37NQxTTbbo3PrpjJic5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

- **/bin**：bin是Binary的缩写, 这个目录存放着最经常使用的命令。
- **/boot：** 这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。
- **/dev ：** dev是Device(设备)的缩写, 存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。
- **/etc：** 这个目录用来存放所有的系统管理所需要的配置文件和子目录。
- **/home**：用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。
- **/lib**：这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。
- **/lost+found**：这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。
- **/media**：linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。
- **/mnt**：系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。
- **/opt**：这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。
- **/proc**：这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
- **/root**：该目录为系统管理员，也称作超级权限者的用户主目录。
- **/sbin**：s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。
- **/srv**：该目录存放一些服务启动之后需要提取的数据。
- **/sys**：这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。
- **/tmp**：这个目录是用来存放一些临时文件的。   
- **/usr**：这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。
- **/usr/bin：** 系统用户使用的应用程序。
- **/usr/sbin：** 超级用户使用的比较高级的管理程序和系统守护程序。
- **/usr/src：** 内核源代码默认的放置目录。
- **/var**：这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。
- **/run**：是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。





# 目录管理

> 处理目录的常用命令

接下来我们就来看几个常见的处理目录的命令吧：

- ls: 列出目录
- cd：切换目录
- pwd：显示目前所在的目录
- mkdir：创建一个新的目录
- rmdir：删除一个空的目录
- cp: 复制文件或目录
- rm: 移除文件或目录
- mv: 移动文件与目录，或修改文件与目录的名称

---

## ls 查目录

> ls （列出目录）

语法：

```
[root@www ~]# ls [-aAdfFhilnrRSt] 目录名称
```

选项与参数：

- -a ：全部的文件，连同隐藏文件( 开头为 . 的文件) 一起列出来(常用)
- -l ：长数据串列出，包含文件的属性与权限等等数据；(常用)

将目录下的所有文件列出来(含属性与隐藏档)

```
[root@www ~]# ls -al ~
```

## mkdir （创建新目录）

> mkdir （创建新目录）

如果想要创建新的目录的话，那么就使用mkdir (make directory)吧。

```
mkdir [-mp] 目录名称
```

选项与参数：

- -m ：配置文件的权限喔！直接配置，不需要看默认权限 (umask) 的脸色～
- -p ：帮助你直接将所需要的目录(包含上一级目录)递归创建起来！

```shell
# 创建多层级目录
[root@kuangshen home]# mkdir test1/test2/test3/test4
mkdir: cannot create directory ‘test1/test2/test3/test4’:
No such file or directory  # <== 没办法直接创建此目录啊！

# 加了这个 -p 的选项，可以自行帮你创建多层目录！
[root@kuangshen home]# mkdir -p test1/test2/test3/test4

# 创建权限为 rwx--x--x 的目录。
[root@kuangshen home]# mkdir -m 711 test2
```

## rmdir ( 删除空的目录 )

> rmdir ( 删除空的目录 )

语法：

```
rmdir [-p] 目录名称
```

选项与参数：**-p ：**连同上一级『空的』目录也一起删除

## cp ( 复制文件或目录 )

> cp ( 复制文件或目录 )

语法：

```
[root@www ~]# cp [-adfilprsu] 来源档(source) 目标档(destination)
[root@www ~]# cp [options] source1 source2 source3 .... directory
```

选项与参数：

- **-a：**相当於 -pdr 的意思，至於 pdr 请参考下列说明；(常用)
- **-p：**连同文件的属性一起复制过去，而非使用默认属性(备份常用)；
- **-d：**若来源档为连结档的属性(link file)，则复制连结档属性而非文件本身；
- **-r：**递归持续复制，用於目录的复制行为；(常用)
- **-f：**为强制(force)的意思，若目标文件已经存在且无法开启，则移除后再尝试一次；
- **-i：**若目标档(destination)已经存在时，在覆盖时会先询问动作的进行(常用)
- **-l：**进行硬式连结(hard link)的连结档创建，而非复制文件本身。
- **-s：**复制成为符号连结档 (symbolic link)，亦即『捷径』文件；
- **-u：**若 destination 比 source 旧才升级 destination ！

```shell
# 找一个有文件的目录，我这里找到 root目录
[root@kuangshen home]# cd /root
[root@kuangshen ~]# ls
install.sh
[root@kuangshen ~]# cd /home

# 复制 root目录下的install.sh 到 home目录下
[root@kuangshen home]# cp /root/install.sh /home
[root@kuangshen home]# ls
install.sh

# 再次复制，加上-i参数，增加覆盖询问？
[root@kuangshen home]# cp -i /root/install.sh /home
cp: overwrite ‘/home/install.sh’? y # n不覆盖，y为覆盖
```

## rm ( 移除文件或目录 )

> rm ( 移除文件或目录 )

语法：

```
rm [-fir] 文件或目录
```

选项与参数：

- -f ：就是 force 的意思，忽略不存在的文件，不会出现警告信息；
- -i ：互动模式，在删除前会询问使用者是否动作
- -r ：递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！

## mv  ( 移动文件与目录，或修改名称 )

> mv  ( 移动文件与目录，或修改名称 )

语法：

```
[root@www ~]# mv [-fiu] source destination
[root@www ~]# mv [options] source1 source2 source3 .... directory
```

选项与参数：

- -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；
- -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖！
- -u ：若目标文件已经存在，且 source 比较新，才会升级 (update)



# 文件基本属性

Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。

在Linux中我们可以使用`ll`或者`ls –l`命令来显示一个文件的属性以及文件所属的用户和组

实例中，boot文件的第一个属性用"d"表示。"d"在Linux中代表该文件是一个目录文件。

在Linux中第一个字符代表这个文件是目录、文件或链接文件等等：

- 当为[ **d** ]则是目录
- 当为[ **-** ]则是文件；
- 若是[ **l** ]则表示为链接文档 ( link file )；
- 若是[ **b** ]则表示为装置文件里面的可供储存的接口设备 ( 可随机存取装置 )；
- 若是[ **c** ]则表示为装置文件里面的串行端口设备，例如键盘、鼠标 ( 一次性读取装置 )。

接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。

其中，[ r ]代表可读(read)、[ w ]代表可写(write)、[ x ]代表可执行(execute)。

要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号[ - ]而已。

每个文件的属性由左边第一部分的10个字符来确定（如下图）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JGpeIS4j9q3B4LQhsQkFiauEybzG2XIdlOMLyO13lMfPKUWRpGJGgyxCAJ9mics9dTZ1qrWDIvleYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从左至右用0-9这些数字来表示。

第0位确定文件类型，第1-3位确定属主（该文件的所有者）拥有该文件的权限。第4-6位确定属组（所有者的同组用户）拥有该文件的权限，第7-9位确定其他用户拥有该文件的权限。

其中：

第1、4、7位表示读权限，如果用"r"字符表示，则有读权限，如果用"-"字符表示，则没有读权限；

第2、5、8位表示写权限，如果用"w"字符表示，则有写权限，如果用"-"字符表示没有写权限；

第3、6、9位表示可执行权限，如果用"x"字符表示，则有执行权限，如果用"-"字符表示，则没有执行权限。



## 修改文件属性

> 修改文件属性

**1、chgrp：更改文件属组**

```
chgrp [-R] 属组名 文件名
```

-R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。

**2、chown：更改文件属主，也可以同时更改文件属组**

```
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```

**3、chmod：更改文件9个属性**

```
chmod [-R] xyz 文件或目录
```

Linux文件属性有两种设置方法，一种是数字，一种是符号。

Linux文件的基本权限就有九个，分别是owner/group/others三种身份各有自己的read/write/execute权限。

先复习一下刚刚上面提到的数据：文件的权限字符为：『-rwxrwxrwx』， 这九个权限是三个三个一组的！其中，我们可以使用数字来代表各个权限，各权限的分数对照表如下：

```
r:4     w:2         x:1
```

每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为：[-rwxrwx---] 分数则是：

- owner = rwx = 4+2+1 = 7
- group = rwx = 4+2+1 = 7
- others= --- = 0+0+0 = 0

```
chmod 770 filename
```







# vim

**第一部分：一般模式可用的光标移动、复制粘贴、搜索替换等**

| 移动光标的方法     |                                                              |
| :----------------- | ------------------------------------------------------------ |
| h 或 向左箭头键(←) | 光标向左移动一个字符                                         |
| j 或 向下箭头键(↓) | 光标向下移动一个字符                                         |
| k 或 向上箭头键(↑) | 光标向上移动一个字符                                         |
| l 或 向右箭头键(→) | 光标向右移动一个字符                                         |
| [Ctrl] + [f]       | 屏幕『向下』移动一页，相当于 [Page Down]按键 (常用)          |
| [Ctrl] + [b]       | 屏幕『向上』移动一页，相当于 [Page Up] 按键 (常用)           |
| [Ctrl] + [d]       | 屏幕『向下』移动半页                                         |
| [Ctrl] + [u]       | 屏幕『向上』移动半页                                         |
| +                  | 光标移动到非空格符的下一行                                   |
| -                  | 光标移动到非空格符的上一行                                   |
| n< space>          | 那个 n 表示『数字』，例如 20 。按下数字后再按空格键，光标会向右移动这一行的 n 个字符。 |
| 0 或功能键[Home]   | 这是数字『 0 』：移动到这一行的最前面字符处 (常用)           |
| $ 或功能键[End]    | 移动到这一行的最后面字符处(常用)                             |
| H                  | 光标移动到这个屏幕的最上方那一行的第一个字符                 |
| M                  | 光标移动到这个屏幕的中央那一行的第一个字符                   |
| L                  | 光标移动到这个屏幕的最下方那一行的第一个字符                 |
| G                  | 移动到这个档案的最后一行(常用)                               |
| nG                 | n 为数字。移动到这个档案的第 n 行。例如 20G 则会移动到这个档案的第 20 行(可配合 :set nu) |
| gg                 | 移动到这个档案的第一行，相当于 1G 啊！(常用)                 |
| n< Enter>          | n 为数字。光标向下移动 n 行(常用)                            |





| 搜索替换 |                                                              |
| :------- | ------------------------------------------------------------ |
| /word    | 向光标之下寻找一个名称为 word 的字符串。例如要在档案内搜寻 vbird 这个字符串，就输入 /vbird 即可！(常用) |
| ?word    | 向光标之上寻找一个字符串名称为 word 的字符串。               |
| n        | 这个 n 是英文按键。代表重复前一个搜寻的动作。举例来说， 如果刚刚我们执行 /vbird 去向下搜寻 vbird 这个字符串，则按下 n 后，会向下继续搜寻下一个名称为 vbird 的字符串。如果是执行 ?vbird 的话，那么按下 n 则会向上继续搜寻名称为 vbird 的字符串！ |
| N        | 这个 N 是英文按键。与 n 刚好相反，为『反向』进行前一个搜寻动作。例如 /vbird 后，按下 N 则表示『向上』搜寻 vbird 。 |



| 删除、复制与粘贴 |                                                              |
| :--------------- | ------------------------------------------------------------ |
| x, X             | 在一行字当中，x 为向后删除一个字符 (相当于 [del] 按键)， X 为向前删除一个字符(相当于 [backspace] 亦即是退格键) (常用) |
| nx               | n 为数字，连续向后删除 n 个字符。举例来说，我要连续删除 10 个字符， 『10x』。 |
| dd               | 删除游标所在的那一整行(常用)                                 |
| ndd              | n 为数字。删除光标所在的向下 n 行，例如 20dd 则是删除 20 行 (常用) |
| d1G              | 删除光标所在到第一行的所有数据                               |
| dG               | 删除光标所在到最后一行的所有数据                             |
| d$               | 删除游标所在处，到该行的最后一个字符                         |
| d0               | 那个是数字的 0 ，删除游标所在处，到该行的最前面一个字符      |
| yy               | 复制游标所在的那一行(常用)                                   |
| nyy              | n 为数字。复制光标所在的向下 n 行，例如 20yy 则是复制 20 行(常用) |
| y1G              | 复制游标所在行到第一行的所有数据                             |
| yG               | 复制游标所在行到最后一行的所有数据                           |
| y0               | 复制光标所在的那个字符到该行行首的所有数据                   |
| y$               | 复制光标所在的那个字符到该行行尾的所有数据                   |
| p, P             | p 为将已复制的数据在光标下一行贴上，P 则为贴在游标上一行！举例来说，我目前光标在第 20 行，且已经复制了 10 行数据。则按下 p 后， 那 10 行数据会贴在原本的 20 行之后，亦即由 21 行开始贴。但如果是按下 P 呢？那么原本的第 20 行会被推到变成 30 行。(常用) |
| J                | 将光标所在行与下一行的数据结合成同一行                       |
| c                | 重复删除多个数据，例如向下删除 10 行，[ 10cj ]               |
| u                | 复原前一个动作。(常用)                                       |
| [Ctrl]+r         | 重做上一个动作。(常用)                                       |





# 用户管理

> 添加账号 useradd

```
useradd 选项 用户名
```

参数说明：

- 选项 :

- - -c comment 指定一段注释性描述。
  - -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
  - -g 用户组 指定用户所属的用户组。
  - -G 用户组，用户组 指定用户所属的附加组。
  - -m　使用者目录如不存在则自动建立。
  - -s Shell文件 指定用户的登录Shell。
  - -u 用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。

测试：

```
# 此命令创建了一个用户kuangshen，其中-m选项用来为登录名kuangshen产生一个主目录 /home/kuangshen
[root@kuangshen home]# useradd -m kuangshen
```

增加用户账号就是在/etc/passwd文件中为新用户增加一条记录，同时更新其他系统文件如/etc/shadow, /etc/group等。



> Linux下如何切换用户

1.切换用户的命令为：su username 【username是你的用户名哦】

2.从普通用户切换到root用户，还可以使用命令：sudo su

3.在终端输入exit或logout或使用快捷方式ctrl+d，可以退回到原来用户，其实ctrl+d也是执行的exit命令

4.在切换用户时，如果想在切换用户之后使用新用户的工作环境，可以在su和username之间加-，例如：【su - root】

$表示普通用户

\#表示超级用户，也就是root用户



> 删除帐号

如果一个用户的账号不再使用，可以从系统中删除。

删除用户账号就是要将/etc/passwd等系统文件中的该用户记录删除，必要时还删除用户的主目录。

删除一个已有的用户账号使用userdel命令，其格式如下：

```
userdel 选项 用户名
```

常用的选项是 **-r**，它的作用是把用户的主目录一起删除。

```
[root@kuangshen home]# userdel -r kuangshen
```

此命令删除用户kuangshen在系统文件中（主要是/etc/passwd, /etc/shadow, /etc/group等）的记录，同时删除用户的主目录。



> 修改帐号

修改用户账号就是根据实际情况更改用户的有关属性，如用户号、主目录、用户组、登录Shell等。

修改已有用户的信息使用usermod命令，其格式如下：

```
usermod 选项 用户名
```

常用的选项包括-c, -d, -m, -g, -G, -s, -u以及-o等，这些选项的意义与useradd命令中的选项一样，可以为用户指定新的资源值。

例如：

```
# usermod -s /bin/ksh -d /home/z –g developer kuangshen
```

此命令将用户kuangshen的登录Shell修改为ksh，主目录改为/home/z，用户组改为developer。



> 用户口令的管理

用户管理的一项重要内容是用户口令的管理。用户账号刚创建时没有口令，但是被系统锁定，无法使用，必须为其指定口令后才可以使用，即使是指定空口令。

指定和修改用户口令的Shell命令是passwd。超级用户可以为自己和其他用户指定口令，普通用户只能用它修改自己的口令。

命令的格式为：

```
passwd 选项 用户名
```

可使用的选项：

- -l 锁定口令，即禁用账号。
- -u 口令解锁。
- -d 使账号无口令。
- -f 强迫用户下次登录时修改口令。

如果默认用户名，则修改当前用户的口令。

例如，假设当前用户是kuangshen，则下面的命令修改该用户自己的口令：

```
$ passwd
Old password:******
New password:*******
Re-enter new password:*******
```

如果是超级用户，可以用下列形式指定任何用户的口令：

```
# passwd kuangshen
New password:*******
Re-enter new password:*******
```

普通用户修改自己的口令时，passwd命令会先询问原口令，验证后再要求用户输入两遍新口令，如果两次输入的口令一致，则将这个口令指定给用户；而超级用户为用户指定口令时，就不需要知道原口令。

为了系统安全起见，用户应该选择比较复杂的口令，例如最好使用8位长的口令，口令中包含有大写、小写字母和数字，并且应该与姓名、生日等不相同。

为用户指定空口令时，执行下列形式的命令：

```
# passwd -d kuangshen
```

此命令将用户 kuangshen的口令删除，这样用户 kuangshen下一次登录时，系统就不再允许该用户登录了。

passwd 命令还可以用 -l(lock) 选项锁定某一用户，使其不能登录，例如：

```
# passwd -l kuangshen
```



# 用户组管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group文件的更新。

> 增加一个新的用户组使用groupadd命令

```
groupadd 选项 用户组
```

可以使用的选项有：

- -g GID 指定新用户组的组标识号（GID）。
- -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。

实例1：

```
# groupadd group1
```

此命令向系统中增加了一个新组group1，新组的组标识号是在当前已有的最大组标识号的基础上加1。

实例2：

```
# groupadd -g 101 group2
```

此命令向系统中增加了一个新组group2，同时指定新组的组标识号是101。



> 如果要删除一个已有的用户组，使用groupdel命令

```
groupdel 用户组
```

例如：

```
# groupdel group1
```

此命令从系统中删除组group1。



> 修改用户组的属性使用groupmod命令

```
groupmod 选项 用户组
```

常用的选项有：

- -g GID 为用户组指定新的组标识号。
- -o 与-g选项同时使用，用户组的新GID可以与系统已有用户组的GID相同。
- -n新用户组 将用户组的名字改为新名字

```
# 此命令将组group2的组标识号修改为102。
groupmod -g 102 group2

# 将组group2的标识号改为10000，组名修改为group3。
groupmod –g 10000 -n group3 group2
```



> 切换组

如果一个用户同时属于多个用户组，那么用户可以在用户组之间切换，以便具有其他用户组的权限。

用户可以在登录后，使用命令newgrp切换到其他用户组，这个命令的参数就是目的用户组。例如：

```
$ newgrp root
```

这条命令将当前用户切换到root用户组，前提条件是root用户组确实是该用户的主组或附加组。



> /etc/passwd

完成用户管理的工作有许多种方法，但是每一种方法实际上都是对有关的系统文件进行修改。

与用户和用户组相关的信息都存放在一些系统文件中，这些文件包括/etc/passwd, /etc/shadow, /etc/group等。

下面分别介绍这些文件的内容。

**/etc/passwd文件是用户管理工作涉及的最重要的一个文件。**

Linux系统中的每个用户都在/etc/passwd文件中有一个对应的记录行，它记录了这个用户的一些基本属性。

这个文件对所有用户都是可读的。它的内容类似下面的例子：

```
＃ cat /etc/passwd

root:x:0:0:Superuser:/:
daemon:x:1:1:System daemons:/etc:
bin:x:2:2:Owner of system commands:/bin:
sys:x:3:3:Owner of system files:/usr/sys:
adm:x:4:4:System accounting:/usr/adm:
uucp:x:5:5:UUCP administrator:/usr/lib/uucp:
auth:x:7:21:Authentication administrator:/tcb/files/auth:
cron:x:9:16:Cron daemon:/usr/spool/cron:
listen:x:37:4:Network daemon:/usr/net/nls:
lp:x:71:18:Printer administrator:/us
r/spool/lp:
```



# 磁盘管理

> 概述

Linux磁盘管理好坏直接关系到整个系统的性能问题。

Linux磁盘管理常用命令为 df、du。

- df ：列出文件系统的整体磁盘使用量
- du：检查磁盘空间使用量



> df

df命令参数功能：检查文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

语法：

```
df [-ahikHTm] [目录或文件名]
```

选项与参数：

- -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
- -k ：以 KBytes 的容量显示各文件系统；
- -m ：以 MBytes 的容量显示各文件系统；
- -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
- -H ：以 M=1000K 取代 M=1024K 的进位方式；
- -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
- -i ：不用硬盘容量，而以 inode 的数量来显示



> du

Linux du命令也是查看使用空间的，但是与df命令不同的是Linux du命令是对文件和目录磁盘使用的空间的查看，还是和df命令有一些区别的，这里介绍Linux du命令。

语法：

```
du [-ahskm] 文件或目录名称
```

选项与参数：

- -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已。
- -h ：以人们较易读的容量格式 (G/M) 显示；
- -s ：列出总量而已，而不列出每个各别的目录占用容量；
- -S ：不包括子目录下的总计，与 -s 有点差别。
- -k ：以 KBytes 列出容量显示；
- -m ：以 MBytes 列出容量显示；



> 磁盘挂载与卸除

根文件系统之外的其他文件要想能够被访问，都必须通过“关联”至根文件系统上的某个目录来实现，此关联操作即为“挂载”，此目录即为“挂载点”,解除此关联关系的过程称之为“卸载”

Linux 的磁盘挂载使用mount命令，卸载使用umount命令。

磁盘挂载语法：

```
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n] 装置文件名 挂载点
```

测试：

```
# 将 /dev/hdc6 挂载到 /mnt/hdc6 上面！
[root@www ~]# mkdir /mnt/hdc6
[root@www ~]# mount /dev/hdc6 /mnt/hdc6
[root@www ~]# df
Filesystem           1K-blocks     Used Available Use% Mounted on
/dev/hdc6              1976312     42072   1833836   3% /mnt/hdc6
```

磁盘卸载命令 umount 语法：

```
umount [-fn] 装置文件名或挂载点
```

选项与参数：

- -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；
- -n ：不升级 /etc/mtab 情况下卸除。

卸载/dev/hdc6

```
[root@www ~]# umount /dev/hdc6
```







# 题目

## yum源管理

```
新建文件夹
mkdir [文件夹名]
删除文件夹
rm -rf

新建文件
touch [文件名]
删除文件
rm -i

挂载文件
mount [需要挂载的文件] [挂载到的地址]

配置yum
vi/etc/yum.reops.d/local.repo

查看yum格式
cat  /etc/yum.reops.d/ CentOS-Media.repo
```





## Lvm

```
查看磁盘(第一块默认sda，第二块默认sdb）
fdisk -l

给磁盘分区
fdisk /dev/sdb
n
p
1
回车
+5G

保存退出
q
w

将分区混合创建物理卷（先融合再分配）
pvcreate /dev/sdb[1-3]

创建卷组（卷组从物理卷中来）
vgcreate [卷组名] /dev/sdb[1-3]

创建逻辑卷（逻辑卷从卷组中来）
 lvcreate -L [逻辑卷大小] -n [逻辑卷名] [卷组名]

查看
pvscan
lvscan

xfs格式化逻辑卷
mkfs.xfs [逻辑卷地址（例：/dev/xcloudvg/xcloudlv）]

xfs逻辑卷挂载到指定目录
mount -t xfs [逻辑卷地址（例：/dev/xcloudvg/xcloudlv）] [挂载的指定目录]

查看
df -h (必须查看)
```



## 配置ftp
```
yum -y install iaas-xiandian vsftpd
vi /etc/vsftpd/vsftpd.conf 

加入anon_root=/opt
systemctl restart vsftpd
systemctl enable vsftpd
```





## 防火墙

【fa yi wang de】

```
# 查看firewall服务状态
systemctl status firewalld   

# 开启、重启、关闭、firewalld.service服务
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop

# 查看防火墙规则
firewall-cmd --list-all    # 查看全部信息
firewall-cmd --list-ports  # 只看端口信息

# 开启端口
开端口命令：firewall-cmd --zone=public --add-port=80/tcp --permanent
重启防火墙：systemctl restart firewalld.service

命令含义：
--zone #作用域
--add-port=80/tcp  #添加端口，格式为：端口/通讯协议
--permanent   #永久生效，没有此参数重启后失效
```





## jdk安装（rpm安装）

1、rpm下载地址http://www.oracle.com/technetwork/java/javase/downloads/index.html

2、如果有安装openjdk 则卸载

```
[root@kuangshen ~]# java -version
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
# 检查
[root@kuangshen ~]# rpm -qa|grep jdk
jdk1.8.0_121-1.8.0_121-fcs.x86_64
# 卸载 -e --nodeps 强制删除
[root@kuangshen ~]# rpm -e --nodeps jdk1.8.0_121-1.8.0_121-fcs.x86_64
[root@kuangshen ~]# java -version
-bash: /usr/bin/java: No such file or directory  # OK
```

3、安装JDK

```
# 安装java rpm
[root@kuangshen kuangshen]# rpm -ivh jdk-8u221-linux-x64.rpm

# 安装完成后配置环境变量 文件：/etc/profile
JAVA_HOME=/usr/java/jdk1.8.0_221-amd64
CLASSPATH=%JAVA_HOME%/lib:%JAVA_HOME%/jre/lib
PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin
export PATH CLASSPATH JAVA_HOME
# 保存退出

# 让新增的环境变量生效！
source /etc/profile

# 测试 java -version
[root@kuangshen java]# java -version
java version "1.8.0_221"
Java(TM) SE Runtime Environment (build 1.8.0_221-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.221-b11, mixed mode)
```



## Tomcat安装（解压缩安装）

1、安装好了Java环境后我们可以测试下Tomcat！准备好Tomcat的安装包！

2、将文件移动到/usr/tomcat/下，并解压！

```
[root@kuangshen kuangshen]# mv apache-tomcat-9.0.22.tar.gz /usr
[root@kuangshen kuangshen]# cd /usr
[root@kuangshen usr]# ls
apache-tomcat-9.0.22.tar.gz
[root@kuangshen usr]# tar -zxvf apache-tomcat-9.0.22.tar.gz   # 解压
```

3、运行Tomcat，进入bin目录，和我们以前在Windows下看的都是一样的

```
# 执行：startup.sh -->启动tomcat
# 执行：shutdown.sh -->关闭tomcat
./startup.sh
./shutdown.sh
```



## 安装Docker（yum安装）



> 基于 CentOS 7 安装

1. 官网安装参考手册：https://docs.docker.com/install/linux/docker-ce/centos/

2. 确定你是CentOS7及以上版本

   ```
   [root@192 Desktop]# cat /etc/redhat-release
   CentOS Linux release 7.2.1511 (Core)
   ```

3. yum安装gcc相关（需要确保 虚拟机可以上外网 ）

   ```
   yum -y install gcc
   yum -y install gcc-c++
   ```

4. 卸载旧版本

   ```
   yum -y remove docker docker-common docker-selinux docker-engine
   # 官网版本
   yum remove docker \
             docker-client \
             docker-client-latest \
             docker-common \
             docker-latest \
             docker-latest-logrotate \
             docker-logrotate \
             docker-engine
   ```

5. 安装需要的软件包

   ```
   yum install -y yum-utils device-mapper-persistent-data lvm2
   ```

6. 设置stable镜像仓库

   ```
   # 错误
   yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
   ## 报错
   [Errno 14] curl#35 - TCP connection reset by peer
   [Errno 12] curl#35 - Timeout
   
   # 正确推荐使用国内的
   yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
   ```

7. 更新yum软件包索引

   ```
   yum makecache fast
   ```

8. 安装Docker CE

   ```
   yum -y install docker-ce docker-ce-cli containerd.io
   ```

9. 启动docker

   ```
   systemctl start docker
   ```

10. 测试

    ```
    docker version
    
    docker run hello-world
    
    docker images
    ```



![image-20230607164651721](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20230607164651721.png)











# ###################################



# 常见的操作系统：

•Windows

•Mac （Unix内核的桌面版）

Unix

UNIX的前身是由贝尔实验室利用汇编语言写成的，由于汇编语言要基于cpu的指令集来运行，不同的CPU指令集不同，所以可移植性差；后来在1971-1973年间由Dennis Ritchie以C语言改写，才称为UNIX；

•Linux

## unix和Linux区别和联系：

1）UNIX系统大多是与硬件配套的，而Linux则可运行在多种硬件平台上.

2）UNIX是商业软件，而Linux是自由软件，免费、公开源代码的.

3）Unix的历史久于linux. Linux的思想源于Unix；

4）在使用上，linux相对没有unix那么复杂；

# Linux发展

![image-20220219135854534](E:/typora/install/Typora/data_text/images/image-20220219135854534.png)

## 发展总结

1）Unix的前身是由贝尔实验室（Bell lab.）的Ken Thompson利用组合语言写成的， 后来在1971-1973年间由Dennis Ritchie以**C程序语**言进行改写，才称为Unix。

2）1977年由Bill Joy释出BSD （Berkeley Software Distribution），这些称为Unix-like的操作系统。

3）1984年由Andrew Tanenbaum开始制作Minix操作系统，该系统可以提供源代码以及软件；

4）**1984**年由Richard Stallman提倡**GNU计划**，倡导自由软件（Free software）， 强调其软件可以“自由的取得、复制、修改与再发行”，并规范出GPL授权模式， 任何GPL（General Public License）软件均不可单纯仅贩卖其软件，也不可修改软件授权。

5）1991年由芬兰人Linus Torvalds开发出Linux操作系统。简而言之，Linux成功的地方主要在于： Minix、Unix）, GNU, Internet, POSIX 及虚拟团队的产生。

 6）符合 Open source 理念的授权相当多，比较知名的如 Apache / BSD / GPL / MIT 等。

7）Linux本身就是个最阳春的操作系统，其开发网站设立在http://www.kernel.org，我们亦称Linux操作系统最底层的数据为“核心（Kernel）”。

 8）从 Linux kernel 3.0 开始，已经舍弃奇数、偶数的核心版本规划，新的规划使用主线版本（MainLine） 为依据， 并提供长期支持版本 （longterm） 来加强某些功能的持续维护。

9）Linux distributions的组成含有：“Linux Kernel + Free Software +Documentations（Tools） + 可完整安装的程序”所制成的一套完整的系统。

10）常见的 Linux distributions 分类有“商业、社群”分类法，或“RPM、DPKG”分类法



## 流行的Linux发行版本

目前世界上大概有三百多种Linux发行版本，其中流行的主要有：

+ Red Hat: ![image-20220301102653150](E:/typora/install/Typora/data_text/images/image-20220301102653150.png)     http://www.redhat.com

  企业版本，收费。

+ centos![image-20220301102948523](E:/typora/install/Typora/data_text/images/image-20220301102948523.png) : https://www.centos.org/

  **C**ommunity **Ent**erprise **O**perating **S**ystem，中文意思是社区企业操作系统

  是rhe 的克隆版本，免费。

+ Fedora:      http://frdora.redhat.com https://getfedora.org/zh_Hans_CN/server/

  发音：英 [fɪ'dɔːrə]费朵拉，Fedora ---发布于2003年，社区开发的免费版，定位于桌面版本

+ Ubuntu![image-20220301103435618](E:/typora/install/Typora/data_text/images/image-20220301103435618.png):      https://www.ubuntu.com

 	乌班图，安装简单，以桌面应用为主的Linux操作系统。其名称来自非洲南部祖鲁语或豪萨语的“*ubuntu*"一词，意思是“人性”“我的存在是因为大家的存在"，是非洲传统的一种价值观

+ Novell SuSE:  http://www.novell.com

  发音/zuzə/，意思为"Software- und System-Entwicklung"，那是一句德文，英文为"Software and system development"。	德国著名的linux版本，最早通过oracle认证的版本。

  https://www.dell.com/support/contents/zh-cn/article/product-support/self-support-knowledgebase/operating-systems/linux-operating-systems/suse-linux

+ Debian![image-20220301105234991](E:/typora/install/Typora/data_text/images/image-20220301105234991.png):      http://www.debian.org

  Deb'-ee-en ，“得比恩”。大便![img](E:/typora/install/Typora/data_text/images/05A87953.png)。

​	最遵循GNU规范的版本，拥有最强大的软件包管理工具dpkg(类型于reh中的rpm)

redhat 9(2003个人版)以后， redhat转型了，将重心转移到可以带来更多利润的商业版——redhat enterprise，可以为用户提供定制化服务。 然后redhat又推出了专注于桌面的版本，也就是个人版。



## Linux应用领域

+ 1、因特网应用架构与网络服务

​	LAMP、J2EE、.NET

​	WWW、DNS、FTP、MAIL、防火墙

+ 2、数据库服务器

  Mysql、Oracle、DB2

+ 3、软件开发

  C、C++、PHP、JAVA+JSP

## Linux的优点和缺点

8、Linux的优点：

1) 具有强大的并行处理能力，稳定性好；

2）免费或少许费用

3）安全性、漏洞的快速修补

4）多用户、多任务

5）用户与用户组的规划

6）相对比较不耗资源的系统

7）整合度佳且多样的图形用户界面等等；

8）强大的网络支持，具有完善的安全保护机制；

缺点：

1） 没有特定的支持厂商

2） 游戏的支持度不足

3） 专业软件的支持度不足等





# 安装CentOS

## VMware使用

安装centOS

 VMware Workstation是一款功能强大的桌面[虚拟计算机](http://baike.baidu.com/view/1041209.htm)软件，能够虚拟化出好几台逻辑独立的系统，虚拟化系统可以很简单的制作出相仿的硬件资源;提供用户可在单一的桌面上同时运行不同的操作系统和进行开发、测试 、部署新的应用程序的最佳解决方案。

 

1）VMware快照：创建快照可以将系统的当前状态进行备份，以便随时还原，一般是在进行一项有一定风险的操作之前，可以对系统创建快照；

![img](E:/typora/install/Typora/data_text/images/clip_image002.jpg)

2）虚拟机克隆：搭建网络实验环境一般需要多台虚拟机，通过克隆，可以快速得到任意数量的相同配置的虚拟机，省去了系统安装的过程；克隆操作必须在虚拟机关机的状态下进行。在linux图形界面中点击右上角的下拉箭头，然后点击关机按钮，将系统关机；如果选择链接克隆,如果母盘有问题了，那么克隆的子盘也没法使用，但是这种节省磁盘空间；如果选择完整克隆，就不存在这个问题了；

 

第一步：图形化关机（也可以命令行关机）：

![img](E:/typora/install/Typora/data_text/images/clip_image004.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image006.jpg)

 

第二步：克隆

![img](E:/typora/install/Typora/data_text/images/clip_image008.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image010.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image012.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image014.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image016.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image018.jpg)

 

## 网络适配器的三种网络连接说明：

![img](E:/typora/install/Typora/data_text/images/clip_image020.jpg)

 

### 1、桥接模式：

在桥接模式下，虚拟机就像是一台独立主机，与物理主机是同等地位，可以通过物理主机的网卡访问外网，外部网络中的计算机也可以访问此虚拟机。为虚拟机设置一个与物理网卡在同一网段的IP，则虚拟机就可以与物理主机以及局域网中的所有主机之间进行自由通信；

桥接模式对应的虚拟网络名称为**VMnet0**，在桥接模式下，虚拟机其实是**通过物理主机的网卡进行通信**的，如果物理主机有多块网卡（比如一块有线网卡和一块无线网卡），那么还需要注意虚拟机实际是桥接到了那块物理网卡上；

![img](E:/typora/install/Typora/data_text/images/clip_image022.jpg)

 

启用桥接模式后：

1）将虚拟机的IP地址更改为和主机在同一网段；

[root@lixia ~]# ifconfig ens33 192.168.0.102/24 是子网掩码

2）虚拟机需要用主机的网卡连接网络，所以要将桥接模式的网络设置到主机的无线网卡上；

  ![img](E:/typora/install/Typora/data_text/images/clip_image024.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image026.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image028.jpg)

主机的无线网卡，可以从网络连接中查看：

![img](E:/typora/install/Typora/data_text/images/clip_image030.jpg)

 

3）重启网络服务：[root@lixia ~]# systemctl restart network

4）ping 主机

 

### 2、仅主机（host-only）模式

仅主机模式对应的是虚拟网络VMnet1，是一个独立的虚拟网络，它**与物理网络之间是隔离**开的。也就是说，所有设为仅主机模式下的虚拟机之间以及虚拟机与物理主机之间可以互相通信，但是他们**与外部网络中的主机之间无法通信**；

安装了VMware之后，在物理主机中会添加俩块虚拟网卡：VMnet1和VMnet8，其中VMnet1虚拟网卡对应了VMnet1虚拟网络。也就是说，物理主机如果要与仅主机模式下的虚拟机之间进行通信，那么就得保证虚拟机的IP要与物理主机VMnet1网卡的IP在同一网段；

![img](E:/typora/install/Typora/data_text/images/clip_image032.jpg)

具体配置如下：

 

![img](E:/typora/install/Typora/data_text/images/clip_image034.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image036.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image038.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image040.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image042.jpg)

![img](E:/typora/install/Typora/data_text/images/clip_image044.jpg)

 

### 3、网络地址转换（NAT）模式

NAT模式对应的虚拟网络是VMnet8，这**也是一个独立的网络**。在此模式下，物理主机就像一台支持NAT功能的代理服务器，而虚拟机就像NAT的客户端一样，虚拟机可以使用物理主机的IP地址直接访问外部网络中的计算机，但是由于NAT技术（网络地址转换）的特点，外部网络中的计算机无法主动与NAT模式下的虚拟机进行通信，也就是说，**只能是由虚拟机到外部网络计算机的单向通信。**

当然，物理主机与NAT模式下的虚拟机之间是可以互相通信的，前提是虚拟机的IP要与VMnet8网卡的IP在同一网段。如果物理主机已经接入到了internet，那么只需将虚拟机的网络设为NAT模式，虚拟机就可以自动接入到internet，所以如果虚拟机需要上网，那么非常适合设置为NAT模式；

可以手动配置IP

![img](E:/typora/install/Typora/data_text/images/clip_image046.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image048.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image050.jpg)

 

## 安装步骤

 

![img](E:/typora/install/Typora/data_text/images/clip_image001.png)

 

![img](E:/typora/install/Typora/data_text/images/clip_image002.png)

 

![img](E:/typora/install/Typora/data_text/images/clip_image004-16452578035601.jpg)

此处同时设置Root用户密码

 

![img](E:/typora/install/Typora/data_text/images/clip_image005.png)

 

![img](E:/typora/install/Typora/data_text/images/clip_image006.png)

 

![img](E:/typora/install/Typora/data_text/images/clip_image007.png)

 

![img](E:/typora/install/Typora/data_text/images/clip_image009.jpg)

 

![img](E:/typora/install/Typora/data_text/images/clip_image011.jpg)

 

 

![img](E:/typora/install/Typora/data_text/images/clip_image013.jpg)

 

 

## 基本配置

### 日期和时间

#### 查看

```sh
[wxl@192 ~]$ date
Fri Feb 18 21:20:38 PST 2022
[wxl@192 ~]$ timedatectl status
      Local time: Fri 2022-02-18 21:21:21 PST
  Universal time: Sat 2022-02-19 05:21:21 UTC
        RTC time: Sat 2022-02-19 05:21:21
       Time zone: America/Los_Angeles (PST, -0800)

```

#### 查看时区

```sh
[wxl@192 ~]$ timedatectl status
      Local time: Fri 2022-02-18 21:21:21 PST
  Universal time: Sat 2022-02-19 05:21:21 UTC
        RTC time: Sat 2022-02-19 05:21:21
       Time zone: America/Los_Angeles (PST, -0800)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: no
      DST active: no
 Last DST change: DST ended at
                  Sun 2021-11-07 01:59:59 PDT
                  Sun 2021-11-07 01:00:00 PST
 Next DST change: DST begins (the clock jumps one hour forward) at
                  Sun 2022-03-13 01:59:59 PST
                  Sun 2022-03-13 03:00:00 PDT

```

#### 修改时区

```sh
[wxl@192 ~]$ timedatectl set-timezone AsiaAsia/Shanghai
[wxl@192 ~]$ date
Sat Feb 19 13:23:22 CST 2022

```

#### 修改时间

```sh
[root@192 wxl]# date -s '2022-02-19 13:35:40'
Sat Feb 19 13:35:40 CST 2022

```

#### 环境变量配置和查看

```shell
vi /etc/profile
添加如下内容：
export REDIS_HOME=/mnt/lucky/redis6.2.6/redis-6.2.6
export PATH=REDIS_HOME:REDIS_HOME/src:$PATH
保存退出，使环境变量生效
source /etc/profile


[root@iZuf6gjqwln3sm6qg7g32eZ src]# echo $PATH
REDIS_HOME:REDIS_HOME/src:/user/java/jdk1.8.0_11/bin:/user/java/jdk1.8.0_11/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/opt/yys/redis5/bin:/root/bin
[root@iZuf6gjqwln3sm6qg7g32eZ src]# echo $REDIS_HOME
/mnt/lucky/redis6.2.6/redis-6.2.6

```

##  环境安装版本查看

```sh
[root@192 etc]# ls /etc/*release
/etc/centos-release  /etc/os-release  /etc/redhat-release  /etc/system-release

[root@192 etc]# cat /etc/centos-release
CentOS Linux release 7.9.2009 (Core)

```



![image-20220219144351602](E:/typora/install/Typora/data_text/images/image-20220219144351602.png)

# 远程连接工具使用

+ MobaXterm

[参考文章]: https://zhuanlan.zhihu.com/p/56341917

## 报错1：

![image-20220301140000828](E:/typora/install/Typora/data_text/images/image-20220301140000828.png)

把安装包文件，拷贝到d:\重新安装。

## 报错2：

![image-20220301135647003](E:/typora/install/Typora/data_text/images/image-20220301135647003.png)

![image-20220301135620103](E:/typora/install/Typora/data_text/images/image-20220301135620103.png)

## 报错3

![image-20220301135816127](E:/typora/install/Typora/data_text/images/image-20220301135816127.png)

![image-20220301135845470](E:/typora/install/Typora/data_text/images/image-20220301135845470.png)

![image-20220301141448846](E:/typora/install/Typora/data_text/images/image-20220301141448846.png)

+ putty
+ SecureCRT



![image-20220301143206158](E:/typora/install/Typora/data_text/images/image-20220301143206158.png)

命令提示符

+ root用户#

+ 普通用户$

## 复制和黏贴

鼠标左键划选复制文件，右键粘贴文本。但在Moba中右键粘贴功能默认不打开，我们可以手动打开。

在菜单栏点击 「settings」 --> 「Configuration」，在弹出的对话框中选择 「terminal」，再将 「paste using right-click」 打上对勾即可。

![image-20220301151536795](E:/typora/install/Typora/data_text/images/image-20220301151536795.png)



# 目录介绍

![image-20220219134006127](E:/typora/install/Typora/data_text/images/image-20220219134006127.png)

![image-20220301143744243](E:/typora/install/Typora/data_text/images/image-20220301143744243.png)

# 了解系统启动的过程

![image-20220219162430270](E:/typora/install/Typora/data_text/images/image-20220219162430270.png)



•计算机的整个启动过程分成四个阶段。

## **第一阶段：*BIOS

   上个世纪70年代初，rom被发明出来，开机程序被刷入ROM芯片，计算机通电后，第一件事就是读取它。这块芯片里的程序叫做"基本輸出輸入系統"（Basic Input/Output System），简称为[BIOS](http://en.wikipedia.org/wiki/BIOS)。

> ROM：read only memery  只读存储器
>
> 

•1.1硬件自检

•    BIOS程序首先检查，计算机硬件能否满足运行的基本条件，这叫做"硬件自检"（Power-On Self-Test），缩写为[POST](http://en.wikipedia.org/wiki/Power-on_self-test)。

•如果硬件出现问题，主板会发出不同含义的[蜂鸣](http://en.wikipedia.org/wiki/Power-on_self-test)，启动中止。如果没有问题，屏幕就会显示出CPU、内存、硬盘等信息

•1.2启动顺序

•   硬件自检完成后，BIOS把控制权转交给下一阶段的启动程序。

•这时，BIOS需要知道，"下一阶段的启动程序"具体存放在哪一个设备。也就是说，BIOS需要有一个外部储存设备的排序，排在前面的设备就是优先转交控制权的设备。这种排序叫做"启动顺序"（Boot Sequence）。



## 第二阶段：主引导记录

•BIOS按照"启动顺序"，把控制权转交给排在第一位的储存设备。

•这时，计算机读取该设备的第一个扇区，也就是读取最前面的512个字节。如果这512个字节的最后两个字节是0x55和0xAA，表明这个设备可以用于启动；如果不是，表明设备不能用于启动，控制权于是被转交给"启动顺序"中的下一个设备。

•这最前面的512个字节，就叫做["](http://en.wikipedia.org/wiki/Master_boot_record)[主引导记录](http://en.wikipedia.org/wiki/Master_boot_record)["](http://en.wikipedia.org/wiki/Master_boot_record)（Master boot record，缩写为MBR）。



•**2.1** **主引导记录的结构**

•"主引导记录"只有512个字节，放不了太多东西。它的主要作用是，告诉计算机到硬盘的哪一个位置去找操作系统。

•主引导记录由三个部分组成：

•　　（1） 第1-446字节：调用操作系统的机器码。

•　　（2） 第447-510字节：分区表（Partition table）。

•　　（3） 第511-512字节：主引导记录签名（0x55和0xAA）。

•其中，第二部分"分区表"的作用，是将硬盘分成若干个区。

## **第三阶段：硬盘启动**

​     计算机的控制权就要转交给硬盘的某个分区了，找到操作系统。

## 第四阶段：操作系统

​      控制权转交给操作系统后，**操作系统的内核**首先被载入内存。

•    以Linux系统为例，先载入/boot目录下面的kernel。内核加载成功后，第一个运行的程序是/sbin/init。它根据配置文件/etc/inittab产生init进程。这是Linux启动后的第一个进程，pid进程编号为1，其他进程都是它的后代。然后，init线程加载系统的各个模块，比如窗口程序和网络程序，直至执行/bin/login程序，跳出登录界面，等待用户输入用户名和密码。

•   至此，全部启动过程完成。

> Pid: process ID



# 命令

## 基本操作

1. 提示符

![image-20220219221513947](E:/typora/install/Typora/data_text/images/image-20220219221513947.png)

2. 按[向上箭头]和[向下箭头]键可以滚动以前使用过的命令

​     键入了文件名、命令、或路径名的一部分，然后按 [Tab] 键 ，会把文件或路径名的剩余部分补全

3. 复制

   选中文本

   黏贴：Shift+Ins键

4. 

5. cd：改变目录，如cd /home，表示由当前目录进入home目录。

​      pwd：显示目前的目录。



## 查看命令帮助

man 命令名

查找 /需要查找的字符

定位到下面一个位置，n

退出：ESC键，q



## ls查看文件目录信息

ls[命令](https://www.linuxcool.com/)可以在[Linux](https://www.linuxprobe.com/)中显示出当前目录下有哪些文件和目录

![image-20220219180411068](E:/typora/install/Typora/data_text/images/image-20220219180411068.png)

 

1、 Ls命令

1）ls[命令](https://www.linuxcool.com/)可以在[Linux](https://www.linuxprobe.com/)中显示出当前目录下有哪些文件和目录

![img](E:/typora/install/Typora/data_text/images/clip_image002-16452793566012.jpg)

2）ls -l，使用长清单模式来列出文件和目录，可以详细的看出文件或文件夹的大小、权限、时间戳、所有者等信息

![img](E:/typora/install/Typora/data_text/images/clip_image004-16452793566013.jpg)

3） ls -lh显示文件的大小，上图中都是字节数，下面通过ls -lh来直接显示文件大小

![img](E:/typora/install/Typora/data_text/images/clip_image005-16452793566024.png)

4） ls –lhS对上面结果进行排序，使用ls -lhS

![img](E:/typora/install/Typora/data_text/images/clip_image007.jpg)

5） ls -al显示隐藏文件，通过ls -al输出，如需要列表显示后面加上l即可

![img](E:/typora/install/Typora/data_text/images/clip_image009-16452793566035.jpg)

6） ls -d */ 列出当前路径下的所有目录（不要列出文件）

![img](E:/typora/install/Typora/data_text/images/clip_image011-16452793566036.jpg)

7）如何不显示所有者信息和组信息呢，也就是上图中的两个root，前面一个为用户后面一个为组，通过ls -g可以隐藏用户信息，通过ls -G可以隐藏组信息，也可以组合起来

![img](E:/typora/install/Typora/data_text/images/clip_image013-16452793566037.jpg)

8） 列出父目录，ls还可以通过下图的操作来列出上一层，也可以通过ls ~来列出用户的主目录

![img](E:/typora/install/Typora/data_text/images/clip_image015.jpg)

9） ls -i显示文件索引节点号（inode）。一个索引节点代表一个文件；

![img](E:/typora/install/Typora/data_text/images/clip_image017.jpg)

-a 列出所有的文件和目录，包括以“.”号开头的；

-c   按文件修改时间排序，可以使用“-l”选项显示创建时间；

-d   列出目录的信息，而不是列出命令里面的内容；

-G 不显示文件的用户组；

-h 自动将文件大小使用方便阅读的方式表示，如：1.23K, 2.4M, 9G;

-k   以K为单位显示文件大小，相当于“--block-size=1024”；

-l 以长列表的形式显示文件的详细信息；

-S 根据文件大小排序；

-t   使用修改时间排序；

-u 按最后访问时间排序； 使用“-l”显示最后访问时间；

--help 显示帮助信息；

--version 输出版本号；

 10)查看pid对应的程序文件(xxx是pid)

ls -l /proc/xxx/exe

![image-20220901160517211](E:/typora/install/Typora/data_text/images/image-20220901160517211.png)

##  date 命令

1） date 查看当前服务器时间

![img](E:/typora/install/Typora/data_text/images/clip_image019.jpg)

2） date -s 时分秒 ：修改时间

![img](E:/typora/install/Typora/data_text/images/clip_image021.jpg)

3） hwclock -w 时间写入bios避免重启失效。

![img](E:/typora/install/Typora/data_text/images/clip_image023.jpg)

4）查看系统版本

![img](E:/typora/install/Typora/data_text/images/clip_image025.jpg)

## Linux文件属性权限说明

![img](E:/typora/install/Typora/data_text/images/clip_image027.jpg)

说明：d代表目录，- 代表是文件

1） 目录/文件权限

![img](E:/typora/install/Typora/data_text/images/clip_image029.jpg)

 

2） 每个目录/文件都有ugo；比如如下a目录属主有 读+写+执行的权限，组用户有读+执行的权限，其他用户有读+执行的权限；r w x 对应的数值分别为 4 2 1 ，如果转换成数值就是 755

![img](E:/typora/install/Typora/data_text/images/clip_image031.jpg)

 

##  用户/组说明：

程序运行与权限有关，而权限与GID、UID有关，

每个文件都具有“所有者与所属用户组”的属性；每个登录的用户至少会取得2个ID，一个是用户ID，（UID）另一个是用户组ID（GID）；用户和组信息都存在 /etc/passwd文件里；有些是系统账号如：bin,daemon,adm,nobody等不要随意删除；系统运行所必须要的，删掉会导致系统不能正常运行；，每个用户信息都有7个字段：如下：

cat /etc/passwd

![img](E:/typora/install/Typora/data_text/images/clip_image033.jpg)

 

1）账号名称：就是账号，用来对应UID的，例如：root的UID对应就是0，第三个字段；

2）密码：这里显示一个X，可以到/etc/shadow中查看；

3）UID：用户标识符，UID为0时，就是root

4）GID：在/ect/group里查看；

5）用户信息说明列

6）主文件夹：也叫用户家目录，root用户登录后就跑到/root里面，普通用户登录后会到/home/username目录下；

7）shell：当用户登录系统后就会取得一个shell来与系统的内核通信以进行用户的操作任务，那为何默认shell会使用bash呢？就是在这个字段指定的；

 

/etc/shadow

![img](E:/typora/install/Typora/data_text/images/clip_image035.jpg)

\1)   账号名称

\2)   密码

\3)   最近更动密码的日期

\4)   密码不可被更动的天数

\5)   密码需要重新更改的天数

\6)   密码需要更改期限的警告天数

\7)   密码过期后的账号宽限时间

\8)   账号失效日期

\9)   保留（扩展字段）

/etc/group

![img](E:/typora/install/Typora/data_text/images/clip_image037.jpg)

\1)   用户组名

\2)   用户组密码

\3)   GID

 

## useradd

格式：useradd  【-u UID】【-g 初始用户组】【-mM】【-c 说明栏】【-d 主文件夹绝对路径】【-s shell】用户账号名

参数：

-u：后面接的是UID，是一组数字，直接指定一个特定的UID给这个账号

-g：指定用户所属的群组。值可以使组名也可以是GID。用户组必须已经存在的，默认值为100，即users。

-G：指定用户所属的附加群组

-M：不要创建用户主文件夹

-m：自动建立用户的登入目录。

-c：说明（etc/passwd第五个字段的内容）

-d：指定用户登入时的主目录，替换系统默认值/home/<用户名>

-r：创建一个系统账号

-s：后面接一个shell，若没有指定则默认/bin/bash

-e：日期格式，设置账号的实效日；

-f：后面接shadow的第七个字段选项，指定密码是否会失效，0为立刻失效；-1为永不失效；

范例一：完全参考默认值新建一个用户，名为vbird1

默认会创建用户主文件夹，且权限为700；

![img](E:/typora/install/Typora/data_text/images/clip_image039.jpg)

![img](E:/typora/install/Typora/data_text/images/clip_image041.jpg)

![img](E:/typora/install/Typora/data_text/images/clip_image043.jpg)

范例2：假设已知道我的系统中有个用户名组名为users,且UID 700并不存在，请用users为初始用户组，以及uid为700创建一个名为vbird2的账号；

![img](E:/typora/install/Typora/data_text/images/clip_image045.jpg)

范例3：创建一个系统账号，名为vbird3

![img](E:/typora/install/Typora/data_text/images/clip_image047.jpg)

范例4：建立一个新用户账户testuser1，并设置UID为544，主目录为/usr/testuser1，属于users组：

useradd -u 544 -d /usr/testuser1 -g users -m testuser1

![img](E:/typora/install/Typora/data_text/images/clip_image049.jpg)

[root@localhost ~]# id testuser1 查看用户信息

![img](E:/typora/install/Typora/data_text/images/clip_image051.jpg)

## passwd

6、 passwd 该命令用于修改用户的密码，使用方法：passwd 用户名

![img](E:/typora/install/Typora/data_text/images/clip_image053.jpg)

## usermod 可用来修改用户帐号的各项设定

语法：usermod -参数 [用户帐号]

参数说明：

-c<备注> 修改用户帐号的备注文字。 

-d<登入目录> 修改用户登入时的目录。 

-e<有效期限> 修改帐号的有效期限，格式：YYYY-MM-DD

-f<缓冲天数> 修改在密码过期后多少天即关闭该帐号。 

-g<群组> 修改用户所属的群组。 

-G<群组> 修改用户所属的附加群组。 

-l<帐号名称> 修改用户帐号名称。

-L 锁定用户密码，使密码无效。 

-s<shell> 修改用户登入后所使用的shell。

-u<uid> 修改用户ID。 

-U 解除密码锁定。

 

范例1：将testuser1用户所属组改为root（创建testuser1用户时该用户默认组是users）

![img](E:/typora/install/Typora/data_text/images/clip_image055.jpg)

范例2：修改用户testuser1的说明列，加上“testuser1 is test”的说明

![img](E:/typora/install/Typora/data_text/images/clip_image057.jpg)

范例3：用户testuser1密码在2022/12/20号失效

![img](E:/typora/install/Typora/data_text/images/clip_image059.jpg)

##  Userdel  可删除用户帐号与相关的文件。

若不加参数，则仅删除用户帐号，而不删除相关文件。

语法：userdel [-r][用户帐号]

参数说明：-r　删除用户及其home目录。

范例：删除test1用户及其主目录

![image-20220302111631369](E:/typora/install/Typora/data_text/images/image-20220302111631369.png)

[root@localhost ~]# userdel -r test1

![image-20220302111740180](E:/typora/install/Typora/data_text/images/image-20220302111740180.png)

![image-20220302111721700](E:/typora/install/Typora/data_text/images/image-20220302111721700.png)

![image-20220302111702145](E:/typora/install/Typora/data_text/images/image-20220302111702145.png)

 

##  groupadd 建立用户组。

groupadd [-g gid] [-o]] [-r] [-f] groupname

参数说明：

-g gid：指定组ID号

-o：允许创建ID重复的用户组

-r：创建系统用户组，低于499系统账号

-f：结合-g一起使用，当-g指定的uid已存在，系统自动重新选择一个可用的uid

​    来建立新的组。

查询组员用/etc/group即可查询组员

[root@localhost ~]# cat /etc/group

范例：添加一个testgroup群组：

![img](E:/typora/install/Typora/data_text/images/clip_image062.png)

 

##  groupmod 功能说明：更改群组识别码或名称。

语法：groupmod [-g <群组识别码> <-o>][-n <新群组名称>][群组名称]

参数说明：

-g <群组识别码> 修改组id。 

-o 重复使用群组识别码。 

-n <新群组名称> 设置欲使用的新的群组名称。（改名）

范例：将linuxtest用户组的组名改为linuxtest1

```shell
[root@localhost /]# groupmod -n testgroup1 testgroup
```

![image-20220302112254508](E:/typora/install/Typora/data_text/images/image-20220302112254508-16461913755371.png)

范例：将vbird3组的组id改为和testgroup1组号一致（testgroup1的群组号是1001）（-o参数的使用）

[root@localhost ~]# groupmod -g 1001 -o vbird3-o-o

![image-20220302112841093](E:/typora/install/Typora/data_text/images/image-20220302112841093.png)

 

##  groupdel 删除群组。

倘若该群组中仍包括某些用户，**则必须先删除这些用户后**，方能删除群组

语法：groupdel [群组名称]

范例：删除linuxtest1用户组

[root@localhosthome]# groupdel  linuxtest1

 先删除用户后，才能删除组，修改组id时，会同时修改用户的组id。

![image-20220302113624722](E:/typora/install/Typora/data_text/images/image-20220302113624722.png)

## chmod [-R] 给文件或者目录赋权限

**Change mode**

> vi test.txt
>
> 按i，进入编辑模式
>
> 输入内容
>
> 111
>
> aaa
>
> Esc 退出编辑模式
>
> :wq!
>
> 查看模式下，dd删除行，x是删除一个字符

文件拥有者仅有只读权限，而文件所属组用户具有读、写权限，其他用户具备读、写、执行三种权限可以写成下列命令：

•  chmod 467 test.txt 【**r=4、w=2、x=1**】

4+2+1=7 读写执行

4+2=6 读写

4+1=5 读执行

![image-20220302114537218](E:/typora/install/Typora/data_text/images/image-20220302114537218.png)

•  也可以使用下列方法为用户设定指定权限

•  +：添加权限（w、r、x）

•  -：删除权限（w、r、x）

•  u：文件拥有者  g：文件所属组  o：其他人  a：所有

•  [root@localhost]#chmod u+x 

•  [root@localhost]#chmod g+rx 

•  [root@localhost]#chmod a-r 

范例：给a.txt文件赋权：文件所有者可读+写+执行，文件所属组用户具有读+执行权限，其他用户有读写权限：

1）先看一下a.txt 文件的权限

```shell
[root@localhost wxl]# chmod 756 a.txt
[root@localhost wxl]#
[root@localhost wxl]# ll a.txt
-rwxr-xrw-. 1 root root 8 Mar  2 11:52 a.txt
[root@localhost wxl]#
[root@localhost wxl]#
[root@localhost wxl]# su wxl
[wxl@localhost ~]$ pwd
/home/wxl
[wxl@localhost ~]$ ll a.txt
-rwxr-xrw-. 1 root root 8 Mar  2 11:52 a.txt
[wxl@localhost ~]$ cat a.txt
111
aaa
[wxl@localhost ~]$ vi a.txt
[wxl@localhost ~]$
[wxl@localhost ~]$ cat a.txt
111
aaabbb

```



2）用符号赋权（了解）

注意，所有者、组、其他人之间用逗号分隔

![img](E:/typora/install/Typora/data_text/images/clip_image068.jpg)

3）也可以用数字赋权

![img](E:/typora/install/Typora/data_text/images/clip_image070.jpg)

4）还可以这样赋权

给组用户赋写的权限 

 ![img](E:/typora/install/Typora/data_text/images/clip_image072.jpg)

给所有all（用户+组+其他用户）去掉执行的权限

![img](E:/typora/install/Typora/data_text/images/clip_image074.jpg)

给目录赋权可以加上参数 -R

（了解）

![img](E:/typora/install/Typora/data_text/images/clip_image076.jpg)

给lx.txt文件赋权：文件属主执行权限，组读写权限，其他用户写权限；

![img](E:/typora/install/Typora/data_text/images/clip_image078.jpg)

 

## chown  修改文件或者目录所有者和所属组

 **Change owner**

**chown** **【-R】账号名称 文件或目录** 

**chown** **【-R】账号名称：组名  文件或目录**

参数：-R 递归修改目录以及其子目录下的所有文件

账号名称和组名之间用：冒号。

范例：将a.txt的所有者改为vbird1这个账号：

![image-20220302134124529](E:/typora/install/Typora/data_text/images/image-20220302134124529.png)

```shell
[root@localhost wxl]# chown wxl a.txt
```

![image-20220302134108481](E:/typora/install/Typora/data_text/images/image-20220302134108481.png)



范例2：将a.txt的所有者与用户组改为wxl

```shell
[root@localhost wxl]# chown wxl:wxl a.txt

```

![image-20220302134347749](E:/typora/install/Typora/data_text/images/image-20220302134347749.png)



## chgrp 修改文件所属用户组

语法：chgrp [-R] 组名 文件名

参数：-R 递归修改

```shell
[root@localhost wxl]# chgrp root a.txt
```

![image-20220302134630521](E:/typora/install/Typora/data_text/images/image-20220302134630521.png)



## diff 用来比较文件内容

different

1、 diff 用来比较文件内容

格式：diff [options] from-file to-file (a=add,c=change,d=delete)

1）Normal模式：**diff a.txt b.txt**

```shell
[wxl@localhost test2]$ cat a.txt
1
word
2
b
[wxl@localhost test2]$ cat b.txt
1
c
[wxl@localhost test2]$ diff a.txt b.txt
2,4c2
< word
< 2
< b
---
> c
```

![image-20220303090519097](E:/typora/install/Typora/data_text/images/image-20220303090519097.png)

 

2）Context模式：diff -c

 ![image-20220302094617531](E:/typora/install/Typora/data_text/images/image-20220302094617531.png)

3) Unified模式: diff -u

 ![image-20220302094625355](E:/typora/install/Typora/data_text/images/image-20220302094625355.png)

4) [root@localhost test]# diff --brief 1233.txt 1234.txt 比较2个文件是否一致；

Files 1233.txt and 1234.txt differ

 

## cd 切换 目录

**（change directory）**

cd 【相对路径或者绝对路径】

. 代表此层目录

.. 代表上一层目录

​    \- 代表前一个工作目录

​    ~代表当前用户的家目录

​    ~account 代表account这个用户的主文件夹（account是个账号名称）

​     ![image-20220302094730049](E:/typora/install/Typora/data_text/images/image-20220302094730049.png)

## mkdir【-p】 目录名称

创建一个目录

[root@localhost~]# mkdir test

创建一个名称为test 的目录

-p 参数，一次创建多级目录

[root@localhost~]# mkdir -p test/test1/test2

 ![image-20220302094741288](E:/typora/install/Typora/data_text/images/image-20220302094741288.png)

 ![image-20220302141928686](E:/typora/install/Typora/data_text/images/image-20220302141928686.png)

## rmdir【-p】目录名称

remove directory

删除一个或多个空目录

[root@localhost~]# rmdir test

递归删除目录

> Tips：需要写上子目录

   ![image-20220302094813328](E:/typora/install/Typora/data_text/images/image-20220302094813328.png)

##  pwd  显示当前所在的路径（我在哪？）

print working directory

##  mv（移动文件与目录，或更名）

move

1)重命名目录

用法：mv [原文件名] [新文件名]

[root@localhost~]# mv test test1

将test目录重命名为test1

2)移动文件

用法：mv [文件名] [目标路径]

[vbird1@localhost ~]$ mv 1.txst 2.txt c.txt lx1(目录)

 

## cp功能说明：将源文件拷贝至某处

语法：cp [-prsu] [来源文件] [目的文件] 

copy

参数说明： 

-p 或 --preserve  保留源文件或目录的属性，包括所有者、所属组、权限与时间

-r：递归处理，将指定目录下的文件与子目录一并处理 

-s：做成链接文件，而不 copy 之意！与 ln 指令相同功能！

-u, --update：如果来源文件比较新，或者是沒有目的文件，那么才会进行 copy 的动作

-v 或 --verbose   显示执行过程

 

##  ln 软硬链接

创建软链接 

语法： ln –s [来源文件]  [软链接文件] 

特点：相当于windows的快捷方式，原文件不存在，软链接文件失效。

 ![image-20220302095215088](E:/typora/install/Typora/data_text/images/image-20220302095215088.png)

创建硬链接 

ln [来源文件]  [硬链接文件] 

特点：相当于源文件的**副本**，随原文件变化而变化

 ![image-20220302095226899](E:/typora/install/Typora/data_text/images/image-20220302095226899.png)

  **硬链接**：新建的文件是已经存在的文件的一个别名，当原文件删除时，**新建的文件仍然可以使用**.

**软链接**：也称为符号链接，新建的文件以“路径”的形式来表示另一个文件，和Windows的快捷方式十分相似，新建的软链接可以指向不存在的文件.

 

 

9、 文件操作

touch 

vi命令 

cp 

mv 

rm 

wc 

sort

find

grep

 

##  rm命令（★★慎重使用★★）

  

•  rm:删除文件或目录

-f force强制删除

-r recursive递归

•  rm -rf 强制删除目录或文件，同时略过不存在的文件，不显示任何信息

•  rm -ri 删除文件或目录时给予确认提示

•  rm filename直接删除掉文件，如果想删除文件夹，你就加参数 -r

 

##  WC命令

word count

统计出文件中字符行数、字节数、单词个数等

-c, --bytes：统计字节数

-m, --chars：统计字符数 

-l, --lines：  统计行数

-L, --max-line-length：打印最长行的长度

-w, --words： 统计单词个数（由空白、等分隔）

\#[root@localhost]#wc test.txt  **行数、word字符总数、字节数、**

![image-20220302160447382](E:/typora/install/Typora/data_text/images/image-20220302160447382.png)



\#[root@localhost]#wc -c test.txt  统计字节数

12 test.txt

\#[root@localhost]#wc -m test.txt 统计字符数

12 test.txt

\#[root@localhost]#wc -l test.txt   统计行数

6 test.txt



##  Vi命令：

 vim是unix系统上的第一个全屏模式编辑器，它用法简单，而且所占空间不大，操作灵活无比。

•    三种模式

•  命令行模式 （ command mode/一般模式）

•  文本输入模式 （ input mode/编辑模式）

•  末行模式 （ last line mode/指令列命令模式）

一般模式：vi 文件名 默认进入该文件的一般模式，可以上下移动光标、删除某个字符、删除某行以及复制或粘贴一行或者多行。

u  vi移动光标类命令 (命令行下)

•  l：光标右移一个字符

•  h：光标左移一个字符

•  space（空格建）：光标右移一个字符

•  Backspace：光标左移一个字符

•  j或Ctrl+n：光标下移一行

•  k或Ctrl+p：光标上移一行

•  Enter：光标下移一行



•  **w****或W：光标右移一个字至字首**

•  **b****或B：光标左移一个字至字首**

•  **e****或E：光标右移一个字至字尾**



•  H：光标移至屏幕顶行

•  M：光标移至屏幕中间行

•  L：光标移至屏幕最后行(光标移至当前页的最后一行)



•  **0****：（注意是数字零）光标移至当前行首或者（ ^ ）**

•  **$****：光标移至当前行尾** 

•  **nG****：光标移至第n行首， 文件首行（1G）**



•  G: 光标移至文件的最后一行行首（光标移至整个文件最后一行）

•  **X:** **删除一个字符**

 

•  显示行号  :set nu （末行模式）

•    末行模式 set nu! （取消显示行号）



u  vi插入文本类命令（编辑模式）

•  i：在光标前

•  I(大写的i)：在当前行首

•  a：光标后

•  A：在当前行尾

•  o：在当前行之下新开一行

•  O：在当前行之上新开一行



u  vi保存退出命令

•  :q ：退出vi

•  :wq ：保存并退出vi

•  :w  ：保存编辑内容

•  :q!  ：强制退出

•  :wq! ：强制保存并退出vi



+ 复制粘贴 （命令模式下）

•     yy复制一行

•    p 粘贴

•     [n]yy复制n行，3yy复制3行

•    p 粘贴



剪切与删除（命令模式下）

•    dd删除一行

•    ndd删除n行 2dd 删除2行

•    p粘贴上面的内容



•  搜索

•   命令模式下，键入 / 后面按搜索的内容

•    按 n 向后搜索

•    按 N 向前搜索



•  替换

•   末行模式下

 :%s/ABC/abc/g 全局替换
 :%s/ABC/abc 替换的是每行第一次出现的字符串
 :s/ABC/abc  替换的是第一行第一次出现的字符串

:1,10s/源/目标替换  替换文中1到10行的字符串

 

**•  撤销**

•   命令模式下，u 撤销至上一步

•   ctrl + r恢复至上一步撤销（再次执行）



•   显示当前文件名

•    末行模式 file

 

 

## 文本查看命令

### cat 

显示文件内容，并且支持将多个文件串连后输出

注意：该命令一次显示完整个文件，若想分页查看，需使用more

格式：  cat [ options ] filename1 … filename2 …

常用 options：

-n  对所有输出行进行编号

-b 与-n相似，  但空白行不编号 

例：$ cat file1 file2 file3    同时显示三个文件

 $ cat -b file1 file2 file3

 

[root@lixia lx]# cat a.txt b.txt c.txt >d.txt

解释：cat 命令显示文件内容，>为重定向命令，这里是将cat命令的输出重定向到新建文件abc.txt中，如果文件不存在则自动新建。

 

### head  查询前几行，默认显示10行

 -q 隐藏文件名

​    -v 显示文件名

​    -c<数目> 显示的字节数

​    -n<行数> 显示的行数

 

head /etc/passwd

 

显示 notes.log 文件的开头 5 行

head -n 5 runoob_notes.log

 显示文件前 20 个字节:

head -c 20 runoob_notes.log



### more

分页显示文件内容 （一页一页地显示，仅只能向前）

more [-dlfpcsu] [-num] [+/ pattern] [+ linenum] [file ...]

参数说明：

-num：每页显示多少行内容

+linenum：从多少行开始显示（跳过多少行开始显示）

[root@localhost]#more +2 -3 test.txt 

从第2行开始，每页显示3行数据阅读test.txt文件

 

•      -c    从顶部清屏，然后显示

-d    提示“Press space to continue，’q’ to quit（按空格键继续，按q键退出）”，禁用响铃功能

-l    忽略Ctrl+l（换页）字符

-p    通过清除窗口而不是滚屏来对文件进行换页，与-c选项相似

-s    把连续的多个空行显示为一行

-u    把文件内容中的下画线去掉

 

 

### tail

命令从指定点开始将文件写到标准输出.使用tail命令的-f选项可以方便的查阅正在改变的日志文件,tail -f filename会把filename里最尾部的内容显示在屏幕上,并且不断刷新,使你看到最新的文件内容.

tail [必要参数] [选择参数] [文件]

-f 循环读取 --follow

-q 不显示文件名信息

-v 显示文件名信息

-c<数目> 显示的字节数

**-n<行数> 显示行数**

--pid=PID 与-f合用,表示在进程ID,PID死掉之后结束. 

-s, --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒 

 

tail -f filename

tail -n 20 filename

tail -f -n 10 filename (tail -10f filename)

>  结合vi修改文件后，看输出内容。
>
>  

### less

分页浏览 （可以向前翻页与可以向后翻页）

less [参数] 文件

下翻页 d , 上翻页u,退出是q

动态打印F  （类似tail -f)

 

### find命令查找文件（grep 是查找文件的内容）

Linux find 命令用来在指定目录下查找文件。

任何位于参数之前的字符串都将被视为欲查找的目录名。如果使用该命令时，不设置任何参数，则 find 命令将在当前目录下查找子目录与文件。并且将查找到的子目录和文件全部进行显示。

> 语法：find path -option [ -print ]  [ -exec  -ok  command ]  {} \;

以 ; 为结束标志，由于各个系统中分号会有不同的意义，因此在前面加上反斜杠。

{} 代表前面find查找出来的文件名

-o 是或者的意思 or

-a 是而且的意思 and

-not 是相反的意思

 

1）常用的按文件名来查：

在根目录下查找文件名为pass打头的文件

[root@localhost ~]# find / -name "pass*"

```shell
[root@localhost ~]# find / -name 'pass*'
```

 ![image-20220302171916063](E:/typora/install/Typora/data_text/images/image-20220302171916063.png)

文件名不区分大小写：

[root@localhost ~]# find / -iname "passwd"

![image-20220302172139182](E:/typora/install/Typora/data_text/images/image-20220302172139182.png)

范例6：将当前目录及其子目录下所有文件后缀为 .c 的文件列出来:

\# find . -name "*.c"

 ![image-20220302172526898](E:/typora/install/Typora/data_text/images/image-20220302172526898.png)

2）按文件类型查：

范例7：将当前目录及其子目录下的所有普通文件列出来：

\# find . -type f

f指file

![image-20220302173027007](E:/typora/install/Typora/data_text/images/image-20220302173027007.png)

 

范例8：查找当前目录及子目录下所有的目录

\# find . -type d 

 ![image-20220302172821804](E:/typora/install/Typora/data_text/images/image-20220302172821804.png)

范例9：查找系统中所有文件长度为 0 的普通文件，并列出它们的完整路径：

\# find / -type f -size 0 -exec ls -l {} \;

```shell
find . -type d -exec ls -lh {} \;
```



![image-20220303112547896](E:/typora/install/Typora/data_text/images/image-20220303112547896.png)

#### exec

说明：**exec**：对匹配的文件执行该参数所给出的shell命令。 
    形式为command {} \;，注意{}与\;之间有空格

|xargs 与exec作用相同 ，起承接作用

区别在于 |xargs 主要用于承接删除操作 ，而 -exec 都可用 如复制、移动、重命名等

 

```shell
[root@localhost usr]# find /usr -size -10M -ctime 0 -type f -name '*.log' -exec ls -lh {} \;

```



```shell
[root@localhost usr]# find /usr -size -10M -ctime 0 -type f -name '*.log' -exec rm -rf {} \;

```



![image-20220303113645168](E:/typora/install/Typora/data_text/images/image-20220303113645168.png)

1、在/usr 目录下找出大小超过10M 的文件且创建时间为当天24小时之内的文件名以 .log 结尾的文件，如果找到删除它们。

  find /usr -size +10M -a -type f -a -ctime 0 -a -name "*.log" |xargs rm -rf

ctime 0代表，0点到23:59:59秒。

3)如何在/usr 目录下限定查找目录深度3层内，找出大小小于10M 的文件且创建时间为24小时之内的文件名以.log 结尾的文件，如果找到删除它们

find /usr -maxdepth 3 -size -10M -ctime -1 -name "*.log"|xargs rm -rf

>  -size 参数 注意容量计算差异



2、按文件大小和时间查：

范例1：查询文件大小大于1M的文件

find /usr/ -size +1M -a -type f （-a 指“与”的意思，两个条件同时满足，-a 可以省略） 

范例2：查询文件大小小于1M，或者文件的修改时间在24H之内的

find ./ -size -1M -o -mtime 0 或（ -o 指或）

范例3：将当前目录及其子目录下所有最近 20 天内创建的文件列出:

\# find . -ctime -20

范例4：寻找当前目录下文件大于1M的文件或者是目录。

  ```shell
[wxl@localhost ~]$ find . -size +1M -exec ls -lh {} \;
-rw-r--r--. 1 wxl wxl 1.6M Mar  1 12:00 ./.cache/tracker/meta.db
-rw-r--r--. 1 wxl wxl 1.3M Mar  3 08:56 ./.cache/tracker/meta.db-wal

  ```



3、按正则条件查：

范例10：按正则查找当前文件夹下的.txt文件

[root@localhost lx]# find . -regex '.*'\.txt

. 代表一定有一个任意字符的字符

\* 匹配任意个数

\ 转义字符，将特殊符号的特殊意义去除

​    

 

4、按文件从属关系查：

范例11: 查找当前目录及子目录下所有用户名为root的文件

 

5、按权限查：

范例12：精确查找当前目录及子目录下ugo权限为644的文件/文件夹

\#find . -perm 644 –print

 

范例13：精确查找当前目录及子目录下ugo用户中任意一类（或）有可执行权限的文件/文件夹（ugo 就是指 user(也称为 owner)、group 和 other 三个单词的首字母组合）

\# find . -perm  /111 -print

范例14：精确查找当前目录及子目录下ugo用户都拥有（与）可执行权限的文件/文件夹   

\# find . -perm -111 -print

  

   6、组合查：

  范例15：查找当前目录及子目录下格式为gif且权限为644的文件/文件夹

\# find . -name '*.gif' -a -perm 644

范例16：查找当前目录及子目录下格式为gif或jpg的文件/文件夹

\# find . -name '*.gif' -o -name '*.jpg'

范例17：查找当前目录及子目录下格式不为gif的文件/文件夹

\# find . -not -name '*.gif'

范例18：带括号的复杂查询， 查询jpg文件或空txt文件

\# find . -name '*.jpg' -o \( -name '*.txt' -a -empty \)

用()调整后面2个条件为且关系。注意，(后有个空格。

范例19：查找当前目录及子目录下txt文件并查找文件中包含certPrefix的行

\# find . -name '*.txt' -exec grep 'certPrefix' {} \;

 

查找并删除---面试题

``` shell
find -name 1.txt -exec rm -rf {} \;
find -name 1.txt -delete
find -name 'l*txt’ | xargs rm -rf
```

查找文件名或扩展名是txt的文件，并删除。

xargs 是给命令传递参数的一个过滤器,可以将管道或标准输入的数据转换成参数

```shell
find -name 1.txt -exec rm-rf {} \;
```

{}表示查找的结果。注意{}后面有空格，\;固定格式

 

#### find和grep区别

find 查找的是文件或目录。grep查找的是字符、文件内容

 

**which 显示命令全路径(从path中查找可执行文件所在路径)**

有的命令既是内部命令又是外部命令，如cd

**whereis 除了查找可执行程序位置，还查找帮助手册、库文件等**

**locate：从数据库查找文件，速度比find快（从硬盘一个个查找），但是只能按文件名查找，且已更新**

  

##   du 检查磁盘空间使用量

（英文全称：disk used）：

   查看当前路径下文件和目录的大小

 ![image-20220303095714212](E:/typora/install/Typora/data_text/images/image-20220303095714212.png)

查看当前目录下的总大小

 ![image-20220303095726751](E:/typora/install/Typora/data_text/images/image-20220303095726751.png)

查看当前目录下指定的文件大小

 ![image-20220303100713958](E:/typora/install/Typora/data_text/images/image-20220303100713958.png)

查看指定目录的大小：

[root@localhost /]# du -sh ./etc

223M ./etc

 

查看当前路径下的文件夹大小

-h或–human-readable 以K，M，G为单位

–max-depth=<目录层数> 表示目录的深度

-x 在一个文件系统目录下

 

 显示2级目录的使用量，自动单位转换

[wxl@localhost ~]$ du -d 2 -h

或者 [wxl@localhost ~]$ du --max-depth=2 -h

![image-20220306225047776](E:/typora/install/Typora/data_text/images/image-20220306225047776.png)



## sort命令

•      功能说明：将文本文件内容加以排序显示，不改变原文件中内容

•  [root@localhost]#sort test.txt

•  Test.txt文件内容为：

A

C

D

B

•  排序后为：a、b、c、d

•  sort -r test.txt (倒序排序)   

•  sort –n  (转化为数值进行排序)

>   转化为数值排序，字符不是转换成ASCII进行排序。

 

## grep 查找文件内容

•      grep指令用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的   范本样式，预设grep指令会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为“-”，则grep指令会从标准输入设备读取数据，grep还有强大的**正则表达式**处理方式.

•  用法： 

> grep 要过滤的字符 要过滤的文件

•  Grep命令：
 -c：只输出匹配行的计数。
 -i：不区分大小写
 -h：查询多文件时不显示文件名。
 -l：查询多文件时只输出包含匹配字符的文件名。
 -n：显示匹配行及行号。
 -s：不显示错误信息。
 -v：显示不包含匹配文本的所有行。

范例1：搜索/etc/passwd文件中包含字符串的行

   [vbird1@localhost ~]$ cat /etc/passwd

​      ![image-20220306225612671](E:/typora/install/Typora/data_text/images/image-20220306225612671.png)

![image-20220306225632945](E:/typora/install/Typora/data_text/images/image-20220306225632945.png)

范例2：下面来搜索不包含 lx字符串的行

​    ![image-20220306225822601](E:/typora/install/Typora/data_text/images/image-20220306225822601.png)

范例3：来看看包含 leo 的行位于文件的第几行

​    ![image-20220306225759571](E:/typora/install/Typora/data_text/images/image-20220306225759571.png)

范例4：另外一些时候，我们希望 grep 不要输出搜索到的行的内容，而是简单地告诉我们到底搜索到了多少行就好了

 ![image-20220306225903159](E:/typora/install/Typora/data_text/images/image-20220306225903159.png)

范例5：我想搜索包含 leo 的行，但 grep 在输出时，最好能把 leo 所在行的上面或下面相邻的行也都展示出来。

查vbird2上面（前）和下面（后）行都输出

```shell
[wxl@localhost ~]$ cat /etc/passwd|grep -B 1 -A 1 vbird2
```

-A 后面（下面），-B 前面（上面）

**或者：**

```shell
[wxl@localhost ~]$ cat /etc/passwd|grep -C 1 vbird2**
```

范例6：忽略大小写-i。不加参数，对大小写敏感。

![image-20220306230741516](E:/typora/install/Typora/data_text/images/image-20220306230741516.png)

范例7：找出内容中含有lx单词的文件都有哪些。我们希望得到的是一个文件列表

![image-20220306230908809](E:/typora/install/Typora/data_text/images/image-20220306230908809.png)

 范例8：找出不含 lx 单词的文件都有哪些

grep ‘error’ –L *.log

![image-20220306231011649](E:/typora/install/Typora/data_text/images/image-20220306231011649.png)

grep正则：

范例9：搜索a.txt文件中开头是 as的行

![image-20220306231045319](E:/typora/install/Typora/data_text/images/image-20220306231045319.png)

范例10：搜索 /etc/passwd 文件中行尾是 bash 的行

![image-20220306231100488](E:/typora/install/Typora/data_text/images/image-20220306231100488.png) 

范例11:以递归的方式查找符合条件的文件。例如，查找指定目录/home/wxl及其子目录（如果存在子目录的话）下所有文件中包含字符串"test"的文件：

```
grep -rl test . *.txt 
```

 ![image-20220306231119538](E:/typora/install/Typora/data_text/images/image-20220306231119538.png)

 **练习：**

个人用户的家目录下，建子目录：t1

创建文件 f1.txt

内容包含:

abc

def

123

456

请在个人用户的家目录下，用grep查找包含123内容的文件名。

 

## cmp(了解)-compare

  功能说明：比较两个文件是否有差异，byte to byte

语法：cmp [第一个文件][第二个文件]

用字节的方式，比较两个文件是否存在差异，但是不保存运算结果；

参数：

-b --print-bytes  打印差异字节

-c或--print-chars 　除了标明差异处的十进制字码之外，一并显示该字符所对应字符。

-i SKIP --ignore-initial=SKIP 跳过输入的第一个字节

-i SKIP1:SKIP2 --ignore-initial=SKIP1:SKIP2  跳过文件1的第一个SKIP1字节和文件2的第一个SKIP2字节

-l或--verbose 　标示出所有不一样的地方。

-s或--quiet或--silent 　不显示错误信息。

-v或--version 　显示版本信息。

--help 　在线帮助。

 

##  File

检测文件类型

[root@localhost]#file test.txt 

test.txt: ASCII text

![image-20220306231303747](E:/typora/install/Typora/data_text/images/image-20220306231303747.png)

 

## 查看内核版本号

[test@mylinux test]$ uname -a  

![image-20220306232401665](E:/typora/install/Typora/data_text/images/image-20220306232401665.png)

查看系统版本：

 ![image-20220306232407326](E:/typora/install/Typora/data_text/images/image-20220306232407326.png)

 练习：请查出/etc目录下，带release名字的文件或目录

[wxl@localhost etc]$ grep -rl . *release*

![image-20220306232542580](E:/typora/install/Typora/data_text/images/image-20220306232542580.png)

或者：[wxl@localhost etc]$ find . -name '*release*'

 ![image-20220306232557652](E:/typora/install/Typora/data_text/images/image-20220306232557652.png)

 

##  tar打包命令

文件打包语法：

\# tar -cvf 目标文件名.tar 源文件

文件解包语法：

\# tar -xvf 目标文件名.tar

文件压缩语法：

\# tar -zcvf 目标文件名.tar.gz  源文件

文件解压语法：

\# tar -zxvf 目标文件名.tar.gz

•  参数说明：

•  c，建立新的备份文件；

•  -C 切换到指定目录(tar -zxvf 1234.tar.gz -C 134，解压tar包到指定目录)

•  x，将备份文件解开；

•  t，列出备份文件的内容；

•  r，将文件附加在一个备份文件的后面；

•  u，将备份文件里的文件以较新的版本更新；

•  d，比较备份文件里的文件与文件系统中的文件；

•  v，在处理文件时显示更多的信息；

•  k，在解开文件时保留已存在的文件，也就是在备份文件中的文件不能覆盖已存在的文件；

•  f，指定文件

•  z，压缩文件。

•  zcvf  --打包同时实现压缩，生成.tar.gz; cvf ---只对文件进行打包，没压缩

•  zxvf --对压缩后的打包文件进行解压； xvf –对.tar 文件进行解包

 

 

 

范例0：[把一个目录下所有的子目录各自打包成tar文件](https://www.cnblogs.com/awpatp/p/13388890.html)

find . -maxdepth 1 -mindepth 1 -type d -exec tar cvf {}.tar {} \;

**范**例1：删除当前目录下除了.tar.gz的文件；

[root@192 wxl]# find . -name '*.gz' -exec rm -rf {} \;

或

 

 

范例1：将lx和lx1两个文件夹打包成img.tar，仅打包不压缩

```
tar -cvf img.tar lx lx1
```

 

范例2：将lx和lx1两个文件夹打包成img.tar.gz，打包后，以gzip压缩

```
   tar -zcvf img.tar.gz lx lx1
```

   

 

范例3：不解压的情况下查看img.tar和img.tar.gz的所有内容

 

 

范例4：将img.tar.gz 解压到a目录下（使用了-C参数改变目录为-C后面目录）

 

范例5：将img.tar包解压到当前目录

 

## zip打包

•  将文件打包为zip格式的压缩文件

•  zip -r filename.zip 源文件

•  -r递归压缩

•  zip -r filename.zip filesdir

•  unzip是从zip包中解压出某个文件

•  unzip filename.zip

​       

## gzip 压缩、gzip/gunzip 解压缩

>  gzip命令不会打包目录，而是把目录下所有的子文件分别压缩

​    ![image-20220303092720568](E:/typora/install/Typora/data_text/images/image-20220303092720568.png)

​    ![image-20220303092738023](E:/typora/install/Typora/data_text/images/image-20220303092738023.png)

## bzip2压缩、bzip2/bunzip2解压缩

​    ![image-20220303091533566](E:/typora/install/Typora/data_text/images/image-20220303091533566.png)

   

## which

 功能说明：which指令会在环境变量$PATH设置的目录里查找符合条件的文件。

语法：which [文件...]

 ![image-20220303091600739](E:/typora/install/Typora/data_text/images/image-20220303091600739.png)

范例：使用指令"which"查看指令"bash"的绝对路径

 ![image-20220303091608401](E:/typora/install/Typora/data_text/images/image-20220303091608401.png)

\#bash可执行程序的绝对路径

​       ![image-20220303091627534](E:/typora/install/Typora/data_text/images/image-20220303091627534.png)

​       ![image-20220303091636100](E:/typora/install/Typora/data_text/images/image-20220303091636100.png)

 

## alias 给命令起别名

[root@localhost]#alias rm=’rm -i’

表示为rm -i命令起一个简单的别名

  

查看别名：

 

设置别名

 

使用别名：

 

删除别名

[root@localhost]#unalias l

 

 

 

25、     echo

\1)   echo输出到终端

 

\2)   echo输出到文件

 

\3)   清空文件内容

 

 

\4)   追加内容

​    

 5）显示转义字符

​    

•     注：对于linux系统，必须使用-e选项来使转义符生效 （\t \n \c） 

• 例：$ echo -e “hello\tboy” 

$ hello  boy

 

26、     export 设置环境变量：

   var_name=value; export var_name

   或者：var_name=value

   export var_name

查看环境变量取值       #echo $var_name 

删除某个变量       #unset var_name 

查看环境变量： env

 注：该命令只是从当前用户进程中删除，不会从文件/etc/profile删除

   source 立即加载环境变量

 

 

 

source 命令可以强行让一个脚本去立即影响当前的环境

 

27、     ifconfig

\1)   显示网络设备信息

 

\2)   启动关闭指定网卡

 

\# ifconfig ens33 down

\# ifconfig ens33 up

\3)   配置静态IP地址

[root@localhost ~]# vi /etc/sysconfig/network-scripts/ifcfg-ens33

 

 

 

重启网络服务  systemctl restart network

完成

 

查看网关：

ip route show

 

 

28、     netconfig/setup(yum install setup -y)

29、     netstat

   Netstat 命令用于显示各种网络相关信息，如网络连接，路由表，接口状态 (Interface Statistics)，masquerade 连接，多播成员 (Multicast Memberships) 等等。

  参数：

-a (all)显示所有选项，默认不显示LISTEN相关

-t (tcp)仅显示tcp相关选项

-u (udp)仅显示udp相关选项

-n 拒绝显示别名，能显示数字的全部转化成数字。

-l 仅列出有在 Listen (监听) 的服務状态

-p 显示建立相关链接的程序名

-r 显示路由信息，路由表

-e 显示扩展信息，例如uid等

-s 按各个协议进行统计

-c 每隔一个固定时间，执行该netstat命令

实例：

   1、查看所有端口

[root@mylinux ~]# netstat -anp

   2、查看指定端口有没有被占用

netstat -anp |grep  端口号

 

30、     ping命令一般用于检测网络通与不通或者网络连接速度的命令，也叫时延，其值越大速度越慢

ping 127.0.0.1

ping www.baidu.com

 

 

31、     df 命令

功能：检查文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息

语法：df [选项]

参数：

-a: 显示所有文件系统信息，包括系统特有的 /proc、/sysfs 等文件系统；

-m: 以 MB 为单位显示容量；

-k: 以 KB 为单位显示容量，默认以 KB 为单位；

-h: 使用人们习惯的 KB、MB 或 GB 等单位自行显示容量；

-T: 显示该分区的文件系统名称；

-i: 不用硬盘容量显示，而是以含有 inode 的数量来显示。 

​    

 

 

 

 

32、     top 能够实时显示系统中各个进程的资源占用状况

top 按q 退出，如果想要动态的显示进程信息，就可以使用top命令

​    

  系统当前的时间

  系统已经运行了2分钟了（在这期间没有重启过）

  当前有3个用户登录系统

 

 

load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。

 

Tasks — 任务（进程），系统现在共有204个进程，其中处于运行中的有1个，203个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个。

 

 --------------显示top中隐藏的进程-----------
服务器上有这个文件吗？  /etc/ld.so.preload
麻烦您先执行这个命令cp /etc/ld.so.preload /etc/ld.so.preload.bak

然后执行命令vi /etc/ld.so.preload   进去将所有内容都删除。后保存

再执行命令echo $LD_PRELOAD  显示为空，就可以了

执行完之后，再使用top命令查看

  

 

33、     ps 用来列出系统中当前运行的哪些进程；

   ps命令用来列出系统中当前运行的那些进程。ps命令列出的是当前那些进程的快照，就是执行

```
参数：
-A ：所有的 process 均显示出来，与 -e 具有同样的效用；
-a ：不与 terminal 有关的所有 process ；
-u ：有效使用者 (effective user) 相关的 process ；
x ：通常与 a 这个参数一起使用，可列出较完整信息。
输出格式规划：
l ：较长、较详细的将该 PID 的的信息列出；
j ：工作的格式 (jobs format)
-f ：做一个更为完整的输出。
    用户id，进程id，父进程id，最近CPU使用情况，进程开始时间等等
```

  ps命令的那个时刻的那些进程

   [root@mylinux ~]# ps -axjf | grep tomcat

   [root@mylinux ~]# ps -ef | grep tomcat

   [root@mylinux ~]# ps -aux | grep tomcat

​          

34、     hostname 查看主机名称

修改主机名

临时主机名修改，重启后失效

 

永久性修改主机名

  

   [root@#localhost ~]# hostnamectl set-hostname mylinux

​    

   然后再reboot重启

   

   查看主机名：[root@lixia ~]# hostname

   设置临时主机名，重启后失效 [root@lixia ~]# hostname 主机名

永久性修改主机名 [root@#localhost ~]# hostnamectl set-hostname 主机名

 

 

49 、centos7 关闭防火墙

查看防火墙状态 systemctl status firewalld.service 

执行后可以看到绿色字样标注的“active（running）”，说明防火墙是开启状态

使用命令：systemctl stop firewalld.service 关闭运行的防火墙

一旦重启操作系统，防火墙就自动开启了，

输入命令systemctl disable firewalld.service，永久关闭防火墙

 

firewall-cmd --zone=public --add-port=9001/tcp --permanent   # 开放9001端口
firewall-cmd --reload   # 配置立即生效
firewall-cmd --zone=public --remove-port=9001/tcp --permanent  #关闭9001端口
#查看有哪些端口开放
firewall-cmd --zone=public --list-ports

 

 

 

50、注销-重启-关机

1、注销（文本模式）

[root@localhost root]#logout \exit 退出登录

2、重启    reboot

[root@localhost root]#reboot 重启系统

3、关机    shutdown 

[root@localhost root]#shutdown now 立刻关机

[root@localhost root]#shutdown +5 5分钟后关机

[root@localhost root]#shutdown 10:30 在10:30时关机

[root@localhost root]#shutdown -r now 立刻关闭系统并重启

[root@localhost root]#shutdown -r 23:59 指定在23:59时重启动

 

查看当前哪个用户在登录 [lx@lixia ~]$ whoami

 

51、awk命令awk就是把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理

-F指定域分隔符为':'

 

输出账户信息：cat /etc/passwd

wxl:x:1000:1000:CentOS 7 64:/home/wxl:/bin/bash

vbird2:x:700:100::/home/vbird2:/bin/bash

 

范例：显示/etc/passwd的账户

 

输出冒号截取后的2个部分

cat /etc/passwd|awk -F ':' '{print $1,$2}'

 

范例2：显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以tab键分割

 

范例3：如果只是显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以逗号分割,而且在所有行添加列名name,shell,在最后一行添加"blue,/bin/nosh"。

[root@mylinux ~]# cat /etc/passwd | awk -F ':' 'BEGIN {print "name,shell"} {print $1","$7} END {print "blue,/bin/nosh"}'    

 

说明：awk工作流程是这样的：先执行BEGING，然后读取文件，读入有/n换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，$0则表示所有域,$1表示第一个域,$n表示第n个域,随后开始执行模式所对应的动作action。接着开始读入第二条记录······直到所有的记录都读完，最后执行END操作。

 

 

范例4：搜索/etc/passwd有root关键字的所有行

[root@mylinux ~]# awk -F: '/root/' /etc/passwd

 

 

范例5：搜索/etc/passwd有root关键字的所有行，并显示对应的shell

 

 此外,$0变量是指整条记录。$1表示当前行的第一个域,$2表示当前行的第二个域,......以此类推。

 awk编程: 变量和赋值

除了awk的内置变量，awk还可以自定义变量。

下面统计/etc/passwd的账户人数

awk '{count++;print $0;} END{print "user count is ",count}' /etc/passwd

 

 

 

52、su 切换用户

53、whereis  查找命令在哪

适用场合：二进制文件、源文件和帮助手册文件路径的查找

参数：

-b 　只查找二进制文件。

-B<目录> 　只在设置的目录下查找二进制文件。

-f 　不显示文件名前的路径名称。

-m 　只查找说明文件。

-M<目录> 　只在设置的目录下查找说明文件。

-s 　只查找原始代码文件。

-S<目录> 　只在设置的目录下查找原始代码文件。

-u 　查找不包含指定类型的文件。

 

范例：使用指令"whereis"查看指令"bash"的位置，输入如下命令：

 

注意：以上输出信息从左至右分别为查询的程序名、bash路径、bash的man 手册页路径。

如果用户需要单独查询二进制文件或帮助文件，可使用如下命令：

$ whereis -b bash        #显示bash 命令的二进制程序 

bash: /bin/bash /etc/bash.bashrc /usr/share/bash  # bash命令的二进制程序的地址 

$ whereis -m bash        #显示bash 命令的帮助文件 

bash: /usr/share/man/man1/bash.1.gz #bash命令的帮助文件地址 

 

55、free 命令显示系统内存的使用情况，包括物理内存、交换内存(swap)和内核缓冲区内存。

 

56、scp

**scp 跨服务拷贝（服务器必须能ping通）**

[root@lixia ~]# scp root@192.168.174.155:/home/lx/abc.txt ./

将远程主机的abc.txt文件复制到本地当前路径下；

[root@lixia ~]# scp abc.txt root@192.168.174.155:/home/lx/

将本地当前路径下的abc.txt文件反拷贝到远程主机的/home/lx/路径下；

在服务器间拷贝。

 

57、查看路由和DNS

![image-20220301231939790](E:/typora/install/Typora/data_text/images/image-20220301231939790.png)

# 了解shell脚本

![image-20220219134908569](E:/typora/install/Typora/data_text/images/image-20220219134908569.png)



Shell是工作在linux内核与用户之间的解释程序，相当于操作系统的外壳，向linux内核传达用户指令的“翻译官”，通常指bash（/bin/bash）,shell有多种：ksh,csh,bash，zsh,tcsh等

查看当前用户用到是哪种shell

​                               

范例：[root@localhost lx]# vi test.sh

 

\#!/bin/bash代表shell解释器使用的是bash，echo打印”hello world”

root@localhost lx]# chmod 777 test.sh

 

 

范例：while循环例子

 

第2、3行定义2个变量

Let 用于执行一个或多个表达式。

 

 

范例2：判断输入的内容

 

 

；；表示语句都结束了。

esac对应case

范例3：实现脚本test.sh：打印当前时间在/home/time.txt中，写出脚本至运行结果的过程及详细命令

 

运行结果：

 

 

# 七、Crontab任务

如果没有安装，可用命令先安装yum install crontabs

查看crontab服务状态（查看服务状态，方式二：systemctl status crond.service）

 

[root@localhost ~]# systemctl status crond

[root@localhost ~]# systemctl stop crond

[root@localhost ~]# systemctl start crond

参数：

• -u user：用于设定某个用户的crontab服务；

• file: file为命令文件名，表示将file作为crontab的任务列表文件并载入crontab；

• -e：编辑某个用户的crontab文件内容，如不指定用户则表示当前用户；

• -l：显示某个用户的crontab文件内容，如不指定用户则表示当前用户；

• -r：从/var/spool/cron目录中删除某个用户的crontab文件。

• -i：在删除用户的crontab文件时给确认提示。

 

**crontab 定时任务** 

crontab -l 查询任务

crontab -e 编辑任务

crontab -r 清除任务

crontab /home/hll/test.txt 直接把文件里的内容加到定时任务

（前提文件里写好了定时任务内容）

 

 

 

 

在以上各个字段中，还可以使用以下特殊字符：

"*"代表所有的取值范围内的数字，如月份字段为*，则表示1到12个月；

"/"代表每一定时间间隔的意思，如分钟字段为*/10，表示每10分钟执行1次。

"-"代表从某个区间范围，是闭区间。如“2-5”表示“2,3,4,5”，小时字段中0-23/2表示在0~23点范围内每2个小时执行一次。

","分散的数字（不一定连续），如1,2,3,4,7,9。

注：由于各个地方每周第一天不一样，因此Sunday=0（第一天）或Sunday=7（最后1天）。

[root@localhost home]# crontab -e

 

控制台回显“crontab：installing new crontab” 表示添加调度任务成功

crontab配置实例：

每一分钟执行一次command（因cron默认每1分钟扫描一次，因此全为*即可）

 

\*  *  *  *  *  command

每小时的第3和第15分钟执行command

 

3,15  *  *  *  * command

每天上午8-11点的第3和15分钟执行command：

 

3,15 8-11 * * * command

每隔2天的上午8-11点的第3和15分钟执行command：

 

3,15 8-11 */2 *  * command

每个星期一的上午8点到11点的第3和第15分钟执行command

 

3,15 8-11  *  * 1 command

每晚的21:30重启smb

 

30 21  *  * * /etc/init.d/smb restart

每月1、10、22日的4 : 45重启smb

 

45 4 1,10,22 * * /etc/init.d/smb restart

每周六、周日的1 : 10重启smb

 

10 1 * * 6,7 /etc/init.d/smb restart

每天18 : 00至23 : 00之间每隔30分钟重启smb

 

**0,30 18-23 \*** * * /etc/init.d/smb restart

***/30 18-23 \*** * * /etc/init.d/smb restart

 

每一小时重启smb

 

\* */1 * * * /etc/init.d/smb restart

晚上11点到早上7点之间，每隔一小时重启smb

\* 23-7/1 *  *  * /etc/init.d/smb restart

 

每月的4号与每周一到周三的11点重启smb

 

0 11 4 * mon-wed /etc/init.d/smb restart

每小时执行/etc/cron.hourly目录内的脚本

 

0 1  *  *  *   root run-parts /etc/cron.hourly

 

范:2：每分钟向文本写入当前日期

[root@wxllinux ~]# crontab -l

*/1 * * * * date >> /home/wxl/date_log.txt

 

[root@wxllinux ~]# tail -f /home/wxl/date_log.txt

Sun Feb 27 14:44:01 CST 2022

 

范例3：同步服务器时间

https://blog.csdn.net/wangmx1993328/article/details/81235245

手动更新时间：

[root@wxllinux ~]# date

Sun Feb 27 14:50:56 CST 2022

 

[root@wxllinux ~]# ntpdate -u pool.ntp.org

27 Feb 14:51:45 ntpdate[4581]: adjust time server 84.16.67.12 offset 0.007930 sec

 

[root@wxllinux ~]# date

Sun Feb 27 14:52:03 CST 2022

 

配置任务计划，每1小时更新一次时间，并将日志写入到 /home/wxl/ntpdate.log 文件中

\* */1 * * * /usr/sbin/ntpdate -u pool.ntp.org >> /home/wxl/ntpdate.log 2>&1。标准输出和错误都被写入到log文件中。

 

[root@wxllinux ~]# tail -f /home/wxl/ntpdate.log

27 Feb 15:00:10 ntpdate[4711]: adjust time server 84.16.73.33 offset 0.008471 sec

27 Feb 15:01:10 ntpdate[4741]: adjust time server 84.16.73.33 offset -0.004321 sec

27 Feb 15:02:09 ntpdate[4778]: adjust time server 84.16.73.33 offset 0.005522 sec

# shell



# FAQ

1） r w x 对应的数值分别为 4 2 1 ，如果转换成数值就是 755

范例13：精确查找当前目录及子目录下ugo用户中任意一类（或）有可执行权限的文件/文件夹（ugo 就是指 user(也称为 owner)、group 和 other 三个单词的首字母组合）

\# find . -perm  /111 -print

![image-20220220210325066](E:/typora/install/Typora/data_text/images/image-20220220210325066.png)

范例14：精确查找当前目录及子目录下ugo用户都拥有（与）可执行权限的文件/文件夹   

\# find . -perm -111 -print





source 加载环境变量

1、 df 命令
