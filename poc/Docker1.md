# Docker使用笔记 #
## 1. Install docker ##
>操作系统：Fedora 27  
参考教程: [Get Docker CE for Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)  

+ 移除旧的docker
```
$ sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```
+ 安装docker-ce
```
$ sudo dnf -y install dnf-plugins-core

$ sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo


$ sudo dnf install docker-ce
```
+ 启动docker
```
$ sudo systemctl start docker
```
+ 设置docker命令免sudo
>此时应该已经能正常使用docker命令了，但是需要sudo，比较麻烦。解决方法是将当前用户加入doker组。

```
如果还没有 docker group 就添加一个：
sudo groupadd docker

将用户加入该 group 内
sudo gpasswd -a ${USER} docker

重启 docker 服务
sudo service docker restart
```