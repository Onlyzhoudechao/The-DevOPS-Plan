# Install ansible #
## 安装ansible ##
1. 配置epel源  
ansible是有源的，不过是在epel源中。CentOS6配置epel源在[CentOS6 configure](CentOS_configure.md)有讲到
```
[vincent@master ~]$ sudo yum install epel-release
[vincent@master ~]$ sudo mv /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel.repo.backup
[vincent@master ~]$ sudo mv /etc/yum.repos.d/epel-testing.repo /etc/yum.repos.d/epel-testing.repo.backup
[vincent@master ~]$ sudo wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
[vincent@master ~]$ sudo yum clean all && yum makecache
```
2. 安装ansible
```
[vincent@master ~]$ sudo yum install ansible
```
**********************************
# Ansible基本使用方法 ##
### 1. Ad-Hoc命令  ###
算是Ansible最直白，最简单的用法。用例如下  
>直接在终端输入
```
ansible webservsers -i hosts -m ping
```
就是利用ansible对inventory组webservers使用ping模块(module)。  
* 其中**webservers**是记录在hosts下。
* **-i hosts**就是根据当前目录下的hosts文件来确定webservers组。一个经典的hosts文件的写法如下
```
[webservers]
192.168.132.22
192.145.235.4

[database]
120.78.135.143
```
很明显，通过hosts文件将三台服务器分成了两个组。注意如果没有指明hosts文件，默认的hosts文件为/etc/ansible/hosts  
* **-m** 用于指明module。ansible有很多module，每个module有不同的功能，有些module使用时需要参数。上面的例子使用的module是“ping”，用来测试服务器的连接。  

下面是一个更为复杂的例子
```
ansible webservers -i hosts -u vince -m module yum -a "name=git state=present" -b
```
* **-u** 指定连接的用户
* **yum** 是yum模块，用于通过yum管理webservers的软件
* **-a** 即args提供了yum模块使用的时候所需要的参数，分别是name和state
* **-b** 即become
### 2. Playbook ###
Ansible的“剧本”，类似一个脚本，使用.yml文件。一个简单的playbook如下：  
```
---
- name: This is a play
  hosts: webservers
  remote_user: vince
  sudo: yes
  connection: ssh
  vars:
    http_port: 80
    cache_dir: /opt/cache
  tasks:
    - name: create cache dir
      file: path={{cache_dir}} state=directory
    - name: install nginx
      yum: name=httpd state=installed
      when: ansible_os_family=="Red Hat"
```
* **- name** 是一个项目或task的名字，在playbook运行时会显示出来。可以随便取。
* **vars** 变量声明，比如cache_dir，在下面的task的{{cache_dir}}就是对应这个cache_dir的值
* **file、yum** 两个module分别用来在目标服务器创建文件和使用yum。
* **when** 条件，这里ansible_os_family=="Red Hat"意味着当目标节点的操作系统是Red Hat系（CentOS、Fedora等）时，运行这个task。

playbook的使用方法是：
```
# ansible-playbook -i hosts site.yml
```
site.yml是当前路径下的playbook，-i指明使用的hosts是当前路径下的hosts。没有-i则默认使用/etc/ansible/hosts。

### 3. Roles ###
在playbook（剧本）下，不同的role（角色）各司其职，有着不同的功能。可能有些role用来初始化gitlab服务器，有些role用来创建数据库。  
创建一个role的方法如下：
```
# ansible-galaxy init gitlab
```
就在当前路径下创建一个叫gitlab的角色。