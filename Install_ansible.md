# Install ansible #
## 安装ansible ##
1. 配置epel源  
ansible是有源的，不过是在epel源中。CentOS6配置epel源在[CentOS6 configure](CentOS_configure.md)有讲到
```
[vincent@master ~]$ sudo yum install epel-release
[vincent@master ~]$ sudo mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
[vincent@master ~]$ sudo mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
[vincent@master ~]$ sudo curl -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
[vincent@master ~]$ sudo yum clean all && yum makecache
```
2. 安装ansible
```
[vincent@master ~]$ sudo yum install ansible
```