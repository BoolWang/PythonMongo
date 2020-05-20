# PythonMongo
在服务器上配置mongo，并使用python远程连接

1.服务器配置  
Centos7
已配置外网访问，可ping百度  
已关闭防火墙，Selinx  
(见https://github.com/BoolWang/HotLinux)  

2.mongodb版本  
mongodb-org-4.0  

3.创建.repo文件，生成mongodb的源  
vi /etc/yum.repos.d/mongodb-org-4.0.repo  
写入：  
[mongodb-org-4.0]  
name=MongoDB Repository  
baseurl=https://repo.mongodb.org/yum/redhat/#releasever/mongodb-org/4.0/x86_64/  
gpgcheck=1  
enabled=1  
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc  
yum安装：yum install -y mongodb-org  

