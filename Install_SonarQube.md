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
使用unzip解压.zip文件，解压到/opt/下
```
[vincent@master ~]$ sudo unzip sonarqube-6.7.2.zip -d /opt/
```
