## Tool chain v1 ##
1. 安装java
```
wget --no-cookie --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.rpm

sudo rpm -ivh jdk-8u161-linux-x64.rpm

sudo alternatives --config java

sudo alternatives --config javac
```

2. 安装Jenkins
```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum -y install jenkins

sudo service jenkins start
或
sudo java -jar /usr/lib/jenkins/jenkins.war
```


3. 安装mysql
```
wget https://repo.mysql.com//mysql57-community-release-el6-11.noarch.rpm

sudo yum localinstall mysql57-community-release-el6-11.noarch.rpm 

yum makecache

sudo yum -y install mysql mysql-server

sudo service mysqld start

//开机自启MySQL服务
sudo chkconfig mysqld on

sudo grep 'temporary password' /var/log/mysqld.log

mysql -uroot -p 

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '123456Asd!';    //更改root密码

mysql> create user 'test'@'%' identified by '123456Asd!';   //添加新用户

mysql> flush privileges;    //刷新权限
```


4. 安装sonarqube
>默认用户admin
>默认密码admin
```
wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-6.7.2.zip

unzip sonarqube-6.7.2.zip 

mv sonarqube-6.7.2 sonarqube

./sonarqube/bin/linux-x86-64/sonar.sh start

可能要设置mysql，可跳过
mysql> create user 'sonarqube'@'%' identified by '123456Asd!';
mysql> create database sonarqube-test;
mysql> grant all privileges on sonarqube_test.* to 'sonarqube';

sonarqube配置，可跳过
vi sonarqube/conf/sonar.properties
    修改下列
sonar.jdbc.username=sonarqube
sonar.jdbc.password=123456Asd!

sonar.jdbc.url=jdbc:mysql://localhost:3306/sonarqube_test?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false

```


5. 下载maven

```
cd /usr/local

sudo wget http://mirrors.hust.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz

sudo tar zxvf apache-maven-3.5.2-bin.tar.gz

sudo mv apache-maven-3.5.2 maven

如果权限不够
sudo chown -R jenkins:jenkins maven
```


6. 安装git
```
sudo yum -y install git
```

7. 安装ansible
```
sudo yum -y install epel-release

yum makecache

sudo yum -y install ansible
```


8. 安装gitlab社区版
>默认端口80  
>默认用户root
```
前期准备
sudo yum install -y curl policycoreutils-python openssh-server cronie
sudo lokkit -s http -s ssh

sudo yum install postfix
sudo service postfix start
sudo chkconfig postfix on

新建 /etc/yum.repos.d/gitlab-ce.repo，内容为
[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1

再执行
sudo yum makecache
sudo yum install gitlab-ce

gitlab初始化
sudo gitlab-ctl reconfigure


配置文件目录
/etc/gitlab/gitlab.rb
```

9. 安装Nexus  
>默认端口8081  
>默认用户名 admin 密码 admin123
```
wget https://sonatype-download.global.ssl.fastly.net/repository/repositoryManager/3/nexus-3.9.0-01-unix.tar.gz
tar xvf nexus-3.9.0-01-unix.tar.gz
mv nexus-3.9.0-01 nexus
./nexus/bin/nexus start  //选项： {start|stop|run|run-redirect|status|restart|force-reload}
```
10. 安装JIRA
```
wget https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.8.1-x64.bin
chmod a+x atlassian-jira-software-7.8.1-x64.bin
sudo ./atlassian-jira-software-7.8.1-x64.bin
接下来进行软件安装
注意查看说明，尤其是端口配置
```
