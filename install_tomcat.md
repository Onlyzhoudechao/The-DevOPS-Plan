# tomcat 的安装过程 #

(在Tomcat的安装过程中，最好把它安装在/usr/local下面，不然在后面jenkins的启动过程中会没有权限来访问war包，maven的安装目录也是这样的)

1.安装包的下载
```
wget http://mirror.bit.edu.cn/apache/tomcat/tomcat-7/v7.0.85/bin/apache-tomcat-7.0.85.tar.gz
```

2.解压tomcat到指定目录
```
tar zxvf apache-tomcat-7.0.85.tar.gz -C /usr/local
```

3.打开tomcat的解压目录，进入到conf目录中，修改server.xml这个配置文件，把<connector port="8080"/>改为8090，并且修改
 <!-- Define an AJP 1.3 Connector on port 8009 -->
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />  中的端口号为8012

4.进入tomcat的bin目录下，通过 ./startup.sh来启动tomcat。

5.在浏览器中输入http:40.125.215.65:8090来访问tomcat访问器。

