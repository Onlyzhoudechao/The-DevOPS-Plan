# Install SonarQube #
## 安装SonarQube ##
1. 下载SonarQube  
最新的LTS版本6.7.2。[点击查看支持和依赖](https://docs.sonarqube.org/display/SONARQUBE67/Requirements)
```
[vincent@master ~]$ wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-6.7.2.zip
```
2. 解压  
要先安装unzip
```
[vincent@master ~]$ sudo yum install -y unzip
```
使用unzip解压.zip文件，并重命名
```
[vincent@master ~]$ unzip sonarqube-6.7.2.zip 
[vincent@master ~]$ mv sonarqube-6.7.2 sonarqube
```
<!-- 3. 更改sonarqube文件权限和所属用户组
```
[vincent@master ~]$ cd /opt/
[vincent@master opt]$ sudo chown -R vincent:vincent sonarqube-6.7.2
``` -->
3. 启动SonarQube
```
[vincent@master ~]$ ./sonarqube/bin/linux-x86-64/sonar.sh console
```
或
```
[vincent@master ~]$ ./sonarqube/bin/linux-x86-64/sonar.sh start
```
4. 开启9000端口
注意要开启SonarQube的运行端口9000