## Nmap

nmap 被誉为“扫描器之王”：免费，跨平台，速度快

![image-20240403180753246](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403180753246.png)

![image-20240403180805923](https://typora-picgo-push.oss-cn-hangzhou.aliyuncs.com/img-for-typora/image-20240403180805923.png)

> 实例

```sh
nmap -sP 192.168.1.0/24  # ping 扫描主机
nmap -iL C:\Users\smk\Desktop\targets.txt  #扫描文件中的所有目标地址
nmap 192.168.0.100/24 -exclude 192.168.0.1  #扫描除某一个目标地址之外的所有目标地址
nmap 192.168.0.100/24 -excludefile C:\Users\smk\Desktop\targets.txt #扫描除某一文件中的目标地址之外的目标地址
nmap 192.168.0.6 -p 135,443,445  #扫描某一目标地址的21、22、23、80端口
nmap --traceroute 192.168.0.6 #对目标地址进行路由跟踪
nmap -O 192.168.0.6 #通过指纹识别技术识别目标地址的操作系统的版本
```

---

