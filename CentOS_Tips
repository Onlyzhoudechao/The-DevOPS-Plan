# CentOS一些小笔记 #
***************
## 关闭selinux ##
### 1. CentOS6 ###
* 查看selinux模式
```
getenfore
```
开启为：Enforcing；关闭为:Permissive
* 临时关闭selinx，立即生效，服务器重启则失效
```
setenforce 0（关闭）
setenforce 1（开启）
```
* 永久关闭，需要重启服务器后生效
```
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```
也可以用vim开启/etc/selinux/config文件啊，将SELINUX=enforcing改为SELINUX=disabled  

### 2. CenOS7 ###
同CentOS6  
  
