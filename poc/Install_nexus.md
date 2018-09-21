# Install nexus #
## nexus安装与使用 ##
1. 下载nexus
```
# cd ~
# wget https://sonatype-download.global.ssl.fastly.net/repository/repositoryManager/3/nexus-3.9.0-01-unix.tar.gz
```
2. 安装并运行
```
# tar xvf nexus-3.9.0-01-unix.tar.gz
# mv nexus-3.9.0-01 nexus
# ./nexus/bin/nexus start  //选项： {start|stop|run|run-redirect|status|restart|force-reload}
```
3. 登陆
nexus默认端口8081。  
浏览器输入http://（yourip）:8081  
默认用户名 admin 密码 admin123