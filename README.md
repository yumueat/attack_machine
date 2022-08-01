# attack_machine
## 简介
+ 该项目包含shell脚本和docker镜像，通过这个脚本可以快速部署一台渗透测试用的机器。原理是：利用docker搭建了一台渗透测试机器并打包为镜像，然后再利用shell脚本进行一键快速部署，首先安装docker，然后拉取镜像并创建容器。
+ 项目诞生：一方面：该项目中的镜像基于kali的官方docker镜像，但是kali官方的docker镜像是最小化安装的，基本不含渗透测试工具，于是就需要自己进行部署，于是我便打算在部署完成后进行打包，以方便再次部署；另一方面：部署工具的过程是一个不断踩坑的过程，有可能部署一个工具中途会遇到很多问题，花费很多时间却仍然得不到解决。这个项目诞生的一个很大的原因就是为了节省时间，利用docker镜像可以实现快速且无错误的部署。
+ 本项目中的脚本在Debian 10 CentOS7 Ubuntu 20.04上测试均通过
## 工具列表
在docker官方镜像的基础上安装了Top 10 Kali Linux Toolkit
|工具名称 |版本 |
|---------|----|
burpsuite |2021.10.3-10704 Burp Suite Community Edition
sqlmap |1.6.6#stable
Nmap |version 7.92
Wireshark |3.6.5 (Git v3.6.5 packaged as 3.6.5-1)
metasploit |v6.2.2-dev
Aircrack-ng |1.6
Hydra |v9.3
crackmapexec |Version : 5.2.2
Responder |3.1.1.0
John the Ripper |1.9.0-jumbo-1+bleeding-aec1328d6c

其余安装的工具如下（包含安装的环境）
> 下面附上这些工具的官网或者github地址，方便大家学习，其中很多项目是开源的，感谢这些大佬的无私奉献

|工具名称 |版本 |官网|
|---------|----|----|
Wget |1.21.3 built on linux-gnu.
gcc |(Debian 11.3.0-3) 11.3.0
git |version 2.35.1
autoconf |(GNU Autoconf) 2.71
java |openjdk 11.0.14.1 2022-02-08
Python |3.10.4 (main, Mar 24 2022, 13:07:27) [GCC 11.2.0] on linux（该版本为默认，其中还有3.9.12和3.9.6）
ruby |3.0.3p157 (2021-11-24 revision 3fb7d2cadc) [x86_64-linux-gnu]
pip |22.2 from /usr/local/lib/python3.10/dist-packages/pip (python 3.10)
OneForAll |v0.4.5 #dev |https://github.com/shmilylty/OneForAll
JSFinder |commit 7c129b9 on May 1, 2020 |https://github.com/Threezh1/JSFinder
Dirmap |v1.0 |https://github.com/H4ckForJob/dirmap
dirsearch |v0.4.2.6 |https://github.com/maurosoria/dirsearch
Ehole |version: 3.0 |https://github.com/EdgeSecurityTeam/EHole
WhatWeb |version 0.5.5 |https://github.com/urbanadventurer/WhatWeb
xray |Version: 1.8.4/a47961e0/COMMUNITY |https://github.com/chaitin/xray
水泽 |2022.7.5 |https://github.com/0x727/ShuiZe_0x727
nuclei |2.7.4 |https://github.com/projectdiscovery/nuclei
nessusd |10.3.0-debian9_amd64 （开放于8834端口） |https://www.tenable.com/products/nessus
## 使用方法
**运行脚本即可（不会的看下面的详细操作），运行结束后会直接进入容器中，脚本中已经对不同主流Linux操作系统做了区别处理，所以这个脚本在不同主流Linux操作系统是通用的**

+ 安装git

CentOs

```
yum -y install git
```
Ubuntu/Debian
```
apt -y install git
```
![image-20220801043655084](https://user-images.githubusercontent.com/87589322/182175017-98c5ed4b-85e7-4691-8ef8-cd27043a2a9c.png)


+ 拉取项目

```
git clone https://github.com/yumueat/attack_machine
```
![image-20220801043536998](C:\Users\yumu\AppData\Roaming\Typora\typora-user-images\image-20220801043536998.png)

+ 给脚本执行权限

```
cd attack_machine && chmod +x install.sh 
```
![image-20220801043435956](C:\Users\yumu\AppData\Roaming\Typora\typora-user-images\image-20220801043435956.png)

+ 执行脚本

```
./install.sh 
```

![image-20220801043310167](C:\Users\yumu\AppData\Roaming\Typora\typora-user-images\image-20220801043310167.png)

+ 脚本结束后会直接进入容器，我设置的root用户的默认密码为root，输入密码即可进入

![image-20220801043937073](C:\Users\yumu\AppData\Roaming\Typora\typora-user-images\image-20220801043937073.png)

+ Enjoy it

## 一些需要知道的事情（注意事项/温馨提示）

### 提交建议

+ 如果在使用的时候或者安装的时候出现错误，可以在Issues中提出
+ 如果有好的工具推荐（希望加入到镜像中）或者对本项目有什么建议/提醒，都可以在Issues中提出

### 工具的使用

我已经通过脚本的方式对使用工具的命令进行了简化

原来是这样的（需要在工具相关目录下）

```shell
python3 dirmap.py --help
```

现在可以直接使用简化后的命令 

```shell
dirmap --help
```

其中nessus比较特殊，是用systemctl命令控制开和停的，使用它需要访问vps的8834端口，然后按照要求进行安装，网上都有教程（因为这个需要登录，我就没安装）

### 关于docker的使用

退出后再次进入

```shell
docker attach kali #或者其他的都可以（看需要）
```

退出

```
Ctrl + P + Q
```

如果进入kali时没有显示，可以多敲几下回车



