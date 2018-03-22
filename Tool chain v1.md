## Tool chain v1 ##
安装java
```
wget --no-cookie --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.rpm

sudo rpm -ivh jdk-8u161-linux-x64.rpm

sudo alternatives --config java

sudo alternatives --config javac
```

安装Jenkins
```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum -y install jenkins

sudo service jenkins start
或
sudo java -jar /usr/lib/jenkins/jenkins.war
```
安装mysql
```
wget https://repo.mysql.com//mysql57-community-release-el6-11.noarch.rpm

sudo yum localinstall mysql57-community-release-el6-11.noarch.rpm 

yum makecache

sudo service mysqld start

sudo chkconfig mysqld on

sudo grep 'temporary password' /var/log/mysqld.log

mysql -uroot -p 

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '123456Asd!';    //更改root密码

mysql> create user 'test'@'%' identified by '123456Asd!';   //添加新用户

mysql> flush privileges;    //刷新权限
```
安装sonarqube
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

下载maven

```
cd /usr/local

sudo wget http://mirrors.hust.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz

sudo tar zxvf apache-maven-3.5.2-bin.tar.gz

sudo mv apache-maven-3.5.2 maven

如果权限不够
sudo chown -R jenkins:jenkins maven
```


安装git
```
sudo yum -y install git
```

安装ansible
```
sudo yum -y install epel-release

yum makecache

sudo yum -y install ansible
```
