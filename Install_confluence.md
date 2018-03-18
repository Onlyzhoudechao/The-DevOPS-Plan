# confluence的安装 #

一、安装confluence6.5.0（在my.cnf的[mysqld]下面加一行transaction_isolation = READ-COMMITTED设置事务隔离策略，confluence需要这种事务隔离策略，否则数据库连接的时候会报错）

1.下载并解压confluence到/tmp目录
```
wget -c -P /tmp https://downloads.atlassian.com/software/confluence/downloads/atlassian-confluence-6.5.0.tar.gz
cd /tmp
tar zxvf atlassian-confluence-6.5.0.tar.gz
cp -rv atlassian-confluence-6.5.0/ /opt/
```
2.创建软链接，注意confluence目录后不要带“/”，/opt/confluence就作为confluence的安装目录
```
ln -sv /opt/atlassian-confluence-6.5.0 /opt/confluence
- 创建confluence用户并设置密码为”123456“
/usr/sbin/useradd --create-home --comment "Account for running confluence" --shell /bin/bash confluence
echo "123456" | passwd --stdin confluence
```
3.设置confluence目录只允许jira用户访问
```
chown -R confluence.confluence /opt/confluence/
chmod -R 700 /opt/confluence/
```
4.创建confluence家目录，用于log、搜索索引等文件的存储，并限制只允许confluence用户访问
```
mkdir /home/confluence/confluence-home
chown -R confluence.confluence /home/confluence/confluence-home
chmod -R 700 /home/confluence/confluence-home
```
5.设置/opt/confluence/confluence/WEB-INF/classes/confluence-init.properties文件，在末尾去除注释并修改为上面设置的confluence家目录路径
```
confluence.home=/home/confluence/confluence-home
```
6.检查端口是否被占用，confluence默认运行的端口有8000和8090， Change the Server port (8000) and the Connector port (8090)，如果被占用，可打开/opt/confluence/conf/server.xml文件修改端口，如果防火墙打开，则放行修改后的端口，下面的例子是修改成Server port to 6006 and the Connector port to 6060
```
<Server port="6006" shutdown="SHUTDOWN" debug="0">
    <Service name="Tomcat-Standalone">
        <Connector port="6060" connectionTimeout="20000" redirectPort="8443"
                maxThreads="48" minSpareThreads="10"
                enableLookups="false" acceptCount="10" debug="0" URIEncoding="UTF-8"
                protocol="org.apache.coyote.http11.Http11NioProtocol" />
```
7.下载mysql数据库连接confluence包并拷贝到jira的lib目录下
```
wget -c -P /tmp wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.45.tar.gz
cd /tmp
tar zxvf mysql-connector-java-5.1.45.tar.gz
cd mysql-connector-java-5.1.45
\cp mysql-connector-java-5.1.45-bin.jar /opt/confluence/confluence/WEB-INF/lib/
```
8.可以切换到confluence用户并启动jira工程，检查6060端口。并将启动命令加入到/etc/rc.local文件中
```
[root@master ~]# /bin/sh /opt/confluence/bin/start-confluence.sh

To run Confluence in the foreground, start the server with start-confluence.sh -fg
executing as current user
If you encounter issues starting up Confluence, please see the Installation guide at http://confluence.atlassian.com/display/DOC/Confluence+Installation+Guide

Server startup logs are located in /opt/confluence/logs/catalina.out
---------------------------------------------------------------------------
Using Java: /usr/bin/java
2018-03-19 00:23:55,184 INFO [main] [atlassian.confluence.bootstrap.SynchronyProxyWatchdog] A Context element for ${confluence.context.path}/synchrony-proxy is found in /opt/confluence/conf/server.xml. No further action is required
---------------------------------------------------------------------------
Using CATALINA_BASE:   /opt/confluence
Using CATALINA_HOME:   /opt/confluence
Using CATALINA_TMPDIR: /opt/confluence/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /opt/confluence/bin/bootstrap.jar:/opt/confluence/bin/tomcat-juli.jar
Using CATALINA_PID:    /opt/confluence/work/catalina.pid
Tomcat started.
```
以上的过程来自于[点击查看]http://blog.51cto.com/net881004/2054131()

