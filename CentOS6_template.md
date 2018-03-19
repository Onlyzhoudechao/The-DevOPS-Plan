# CentOS6模板 #
## 说明 ##
在关机并Clone之前删除了/etc/udev/rules.d/70-persistent-net.rules避免出现中不到eth0的情况。  
在打开克隆的CentOS之后，在root的家目录下运行./configure.sh，会进行时间同步，新用户的创建和网络的设置。在选择（Y/N）时统一使用小写。