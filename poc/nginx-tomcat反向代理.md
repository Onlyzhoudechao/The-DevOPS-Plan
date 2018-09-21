# nginx集群tomcat的配置 #

```
/etc/nginx/nginx.conf    //这个是nginx的配置文件位置
/etc/init.d/nginx start
在http标签里面添加如下的内容：
upstream tomcat_server1{
	server 40.125.215.65:8090;       //tomcat的服务器和端口
	server 40.125.173.186:8090;
}

server{
	listen 80;          //80端口监听
	server_name 139.219.102.213;   //nginx的服务器的地址
	location / {
		proxy_pass http://tomcat_server1;     //所有访问server_name的都跳转到tomcat_server1 
	}
}


设置selinux临时关闭
setenforce 0

临时打开SELinux 
setenforce 1

查看SELinux状态 
getenforce
```