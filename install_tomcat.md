# tomcat 的安装过程 #

(在Tomcat的安装过程中，最好把它安装在/usr/local下面，不然在后面jenkins的启动过程中会没有权限来访问war包，maven的安装目录也是这样的)

1.安装包的下载
```
wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-7/v7.0.85/bin/apache-tomcat-7.0.85.tar.gz
```

2.解压tomcat到指定目录
```
tar zxvf 
```