# 工具链搭建（一） #
## 安装CentOS 6.9 minimal 后的基本配置 ##
1. root登陆后添加新用户
```
[root@master ~]# useradd vincent //添加新用户vincent
[root@master ~]# passwd vincent //设置vincent密码
[root@master ~]# visudo //将vincent添加到sudors
```
>visudo中更改如下图  
>![](pic/configure-os/visudo.png)  
>保存并退出
>然后终端输入exit退出登陆，改用用户vincent登陆

2. 网络配置，设置固定ip
默认情况下时上不了网的，因为还没有配置网络。
```
[vincent@master ~]$ sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
>将ifcfg-eth0更改为  
![](pic/configure-os/modified-ifcfg-eth0.png)  
>其中关键是设置IPADDR、GATEWAY、PREFIX、DNS1、DNS2，另外将ONBOOT设置为yes可以自启动，BOOTPROTO设为none不用dhcp来自动获取ip

然后重启network服务
```
[vincent@master ~]$ sudo service network restart
```
重启成功效果如下图  
![](pic/configure-os/network-service-restart.png)

3. 配置阿里源
首先备份repo文件
```
[vincent@master ~]$ sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```
然后下载并替换repo配置文件
```
[vincent@master ~]$ sudo curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```
生成缓存
```
[vincent@master ~]$ yum makecache
```
效果如下  
![](pic/configure-os/yum-makecache.png)  
建议最后更新一下系统
```
[vincent@master ~]$ sudo yum -y update
```
3. 安装JDK8
使用官方的rpm安装方式方便快捷且易于维护  
首先下载JDK
```
[vincent@master ~]$ sudo yum  install -y wget    //安装下载工具wget
[vincent@master ~]$ wget --no-cookie --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.rpm //接受协议并下载java 1.8.161
```
安装JDK
```
[vincent@master ~]$ sudo rpm -ivh jdk-8u161-linux-x64.rpm
```
![](pic/configure-os/rpm-jdk.png)  

使用alternatives配置JAVA环境  
配置java
```
[vincent@master ~]$ sudo alternatives --config java
```
![](pic/configure-os/alternatives-java.png)   

配置javac
```
[vincent@master ~]$ sudo alternatives --config javac
```
![](pic/configure-os/alternatives-javac.png)   

>使用这种方法安装的好处是当有多个java版本时可以很方便地选取我们需要的版本。

