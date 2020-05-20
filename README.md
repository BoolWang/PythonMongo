# PythonMongo
在服务器上配置mongo，并使用python远程连接

1.服务器配置  
Centos7
已配置外网访问，可ping百度  
已关闭防火墙，Selinx  
(见https://github.com/BoolWang/HotLinux)  

2.mongodb版本  
[mongodb-org-3.2]

3.创建.repo文件，生成mongodb的源
yum update  
vi /etc/yum.repos.d/mongodb-org-3.2.repo  
写入：  
[mongodb-org-3.2]  
name=MongoDB Repository  
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/  
gpgcheck=1  
enabled=1  
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc  
安装：sudo yum install mongodb-org  

4.初始配置  
4.1 配置/etc/mongod.conf  
vi /etc/mongod.conf
修改：net:->bindip:0.0.0.0  
添加：security:authorization: enabled  
4.2 添加管理用户  
打开mongo shell：mongo  
>use admin  
>db.creatUser(    
... {  
... user:"root",  
... pwd:"**********",   #密码  
... roles:[{role:"userAdminAnyDatabase",db:"admin"}]  
... }  
... )  

测试用户登录：mongo -u root -p --authenticationDatabase admin  
输入密码即可登录，但root用户没有数据库的操作权限  
4.3 添加可操作数据库的管理用户  
$root用户登录  
>use admin  
>db.creatUser(  
... {  
... user:"admin",  
... pwd:"*********",  
... roles:[{role:"readWriteAnyDatabase",db:"admin"}]  
... }  
... )  

5.远程连接  
使用robomongo连接  

6.pymongo远程连接  
安装pymongo：pip install pymongo  
>import pymongo  
>myclient = pymongo.MongoClient(host='192.168.43.123', port=27017, username='admin', password='csu3216300.', authSource='admin')  
>dblist = myclient.list_database_names()  
>dblist  #即可看到数据库列表  

7.使用pymongo操作数据库


