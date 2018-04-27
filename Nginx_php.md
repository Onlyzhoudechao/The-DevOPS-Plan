# Nginx支持php #
************************
## 基本方法 ##
1. 安装php、php-fpm、php-devel  
2. 配置/etc/nginx下的nginx.conf或者/etc/nginx/config.d/default.conf  
>在配置文件server{ }中添加
>```
>    location ~ \.php?.*$ {  
        root           /share/test;  
        fastcgi_pass   127.0.0.1:9000;  
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;  
        include        fastcgi_params;  
    }
>```   
大致上讲就是配置php-cgi，当打开php文件时，将该文件传递到php解释器。
## 问题 ##
1. nignx跳转到php页面时变成下载  
查看php-cgi和php-fpm是否正确运行，并监听相应的端口（默认是9000）   
2. 端口冲突，服务器上9000端口已经被占用，要更改php-fpm的监听端口  
分四个步骤：   
步骤一、配置nginx，将上文中的fastcgi_pass 127.0.0.1:9000改为你需要的端口，如127.0.0.1:9002   
  
步骤二、配置php-fpm，找到php-fpn.conf文件（这要看版本，有些不是配置php-fpm.conf，而是它引用的在/etc/php-fpm.d下的www.conf文件)，更改listen = 127.0.0.1:9000
为 listen = 127.0.0.1:9002   
  
步骤三、这两个配置好后，还有一个问题，就是要(关闭selinux)[CentOS_Tips.md]，不然访问php文件nginx会报错permission denied。  
  
步骤四、重启nginx
