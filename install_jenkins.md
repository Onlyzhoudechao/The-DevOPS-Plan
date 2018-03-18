# jenkins的安装 #

一、进入jenkins的官网如下图所示
![](pic/install-jenkins/jenkinsweb.PNG)

点击Download然后跳转到下面的页面，选择centos的链接
![](pic/install-jenkins/centoslink.PNG)

跳转到下面的页面：
![](pic/install-jenkins/select.PNG)

安装图中的步骤安装jenkins
```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

yum install jenkins
此步骤为上图中的代码
```

二、检查jenkins是否配置jdk，在candidates后面加上自己的jdk路径，如下：
```
vi /etc/rc.d/init.d/jenkins
```
![](pic/install-jenkins/java.PNG)

这里我安装jdk的路径为默认的，jenkins已经默认配置了，需要注意的是如果你在安装jdk时在上图中的路径没有，需要自己加上。

三、启动jenkins

```
java -jar /usr/lib/jenkis/jenkins.war  --httpPort='端口号'

用上面的安装方法，目录默认是这里，注意后面要加上端口号，避免和其他端口冲突
```
这里需要注意一点，不要忘记在 /etc/hosts这个配置文件中加上你的主机名    127.0.0.1   master （这里master是我的主机名）

这里还要注意的是centos必须对外开放一些端口，否则远程访问不到，以下是开放端口的语句
```
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
然后保存并重新启动
sudo service iptables save && sudo service iptables restart
再通过查看哪些端口已经对外开放
/etc/init.d/iptables status
```