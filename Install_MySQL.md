# Install Mysql #
## 安装MySql  ##
首先从官网下载rpm包
```
[vincent@master ~]$ wget https://repo.mysql.com//mysql57-community-release-el6-11.noarch.rpm
```
添加MySQL源
```
[vincent@master ~]$ sudo rpm -ivh mysql57-community-release-el6-11.noarch.rpm 

也可以

[vincent@master ~]$ sudo yum localinstall mysql57-community-release-el6-11.noarch.rpm 
```
生成yum缓存
```
[vincent@master ~]$ yum makecache
```
安装MySQL
```
[vincent@master ~]$ sudo yum install -y mysql mysql-server
```
启动MySQL服务
```
[vincent@master ~]$ sudo service mysqld start
```
设置mysqld服务自启动
```
[vincent@master ~]$ sudo chkconfig mysqld on
```
至此，MySQL已经安装好了。  
默认情况下，系统会创建一个root用户。我们需要获得root的临时密码。
```
[vincent@master ~]$ sudo grep 'temporary password' /var/log/mysqld.log
```
![](pic/configure-os/temporary-passwd.png)  
接着，利用获得的临时密码登陆MySQL。
```
[vincent@master ~]$ mysql -uroot -p
```
![](pic/configure-os/mysql-login-root.png)  
更改root用户密码
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '123456Asd!';
```
>注意密码要稍微复杂点，不然会因为不合要求而设置失败。

添加新用户test
```
mysql> create user 'test'@'%' identified by '123456Asd!';
```
刷新权限
```
mysql> flush privileges;

```
输入exit退出MySQL shell。 

mysql_secure_install一些安全配置。  
```
[vincent@master ~]$ sudo mysql_secure_installation
```
按照需求来，建议禁止MySQL远程root用户登陆。
### mysql字符集的配置 ###
![](pic/mysql-set/mysql字符集.png)