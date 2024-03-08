# 1.项目配置

所需软件：VMware Workstation Pro

所需镜像文件：VMware-VMvisor-Installer-6.5.0.update02-8294253.x86_64.iso

---



# 2.安装步骤

打开VMware workstation 15.5 pro虚拟机软件

步骤一：单击“创建新的虚拟机”

![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image002.png)
 步骤二：选择“典型（推荐）”，单击“下一步”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image004.png)
 步骤三：选择“稍后安装操作系统”，单击“下一步”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image006.png)

步骤四：选择相应的安装版本，单击“下一步”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image008.png)
 步骤五：自定义esxi主机名，并选择合适的安装位置。
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image010.png)
 步骤六：添加适合的磁盘大小，根据实际情况选择虚拟磁盘文件存储方式。
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image012.png)

步骤七：确认相关配置信息，然后单击“自定义硬件”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image014.png)
 步骤八：选择合适的内存大小、vCPU大小、以及添加iso映像文件，操作完成后，点击“关闭”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image016.png)
 步骤九：回到此页面，单击“完成即可”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image018.png)

# 3.配置步骤



步骤十：单击“开启此虚拟机”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image020.png)
 步骤十一：等待加载
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image022.png)
 步骤十二：敲击回车键，继续下一步

步骤十三：敲击回车键，继续下一步
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image024.png)
 步骤十四：按“F11”，表示“接收协议并进行下一步操作”
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image026.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image027.png)
 步骤十五：选择安装到的磁盘，敲击“回车键”，继续下一步。
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image029.png)

步骤十六：选择键盘布局，默认即可，敲击“回车键”，继续
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image031.png)
 步骤十七：为esxi主机设置密码（注意：密码设置要符合复杂性），敲击“回车键”，继续
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image033.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image034.png)
 步骤十八：按“F11”键，开始安装，
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image035.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image036.png)

步骤十九：按回车键，重启（注意：重启前，先移除挂载的iso文件）
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image038.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image039.png)
 步骤二十：配置IP地址的网络相关信息。按“F2”键，进入配置界面。输入root密码
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image041.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image043.png)

选择“Configure Management Network”选项，配置网络信息
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image045.png)
 配置ip地址、子网掩码、网关等信息
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image047.png)
 按“ESC”键退出，按“y”键，表示确认并退出此界面
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image049.png)
 继续按“ESC”键，退出此配置界面
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image051.png)

完成IP地址配置
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image053.png)
 使用浏览器登录此esxi主机进入web控制台，进行操作管理。输入http://192.168.200.10
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image055.png)
 进入此界面，点击“高级”——>“继续前往192.168.200.10（不安全）”（注意：其他浏览器同理）
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image057.png)

进入此界面，输入用户名、密码
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image059.png)单击确认即可
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image061.png)
 ![在这里插入图片描述](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image063.png)
 至此，esxi主机在VM workstation安装完成。

 

# 4.虚拟机导入到ESXi

**VMware Workstation** **与 ESXi 的主要区别**

VMware Workstation是直接在windows系统下安装软件，安装后再在软件里面安装虚拟机，而ESXi相当于一个linux操作系统，直接像安装linux系统一样安装后，再在另一台windows电脑上通过web或者安装vcenter连接访问esxi，然后再安装和管理虚拟机。

---



1、先在Vmware workstation工作站上导出虚拟机为vof文件

导出前，要先关闭虚拟机，然后右键–》文件–》导出为OVF(E)…

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image065.jpg)

导出完成后，得到4个文件，如下图所示，其中红色圈起的是需要用到的文件

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image067.jpg)

2、打开exsi管理web后台，需要上传两个文件,扩展名为ovf和vmdk的文件,然后下图操作即可,最后启动电源开机。

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image069.jpg)

 

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image071.jpg)

 

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image073.jpg)

 

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image075.jpg)

 

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image077.jpg)

![img](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/clip_image079.jpg)