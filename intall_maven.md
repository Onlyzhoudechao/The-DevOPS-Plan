# maven的安装 #

一.下载maven的tar包
```
wget http://mirrors.hust.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
```

二.解压缩maven
```
tar zxvf apache-maven-3.5.2-bin.tar.gz -C software
```
我这里将maven解压缩之后的路径为:/home/zhoudechao/software/

三.配置环境变量
```
vi /etc/profile

新增行MAVEN_HOME,等于号后面是maven解压的文件夹地址
export MAVEN_HOME=/home/zhoudechao/software/apache-maven-3.5.2
找到PATH行,追加$MAVEN_HOME/bin
例如
PATH=$MAVEN_HOME/bin:$PATH
//重新刷新配置文件
source /etc/profile
```
四.测试安装
```
mvn -v
```