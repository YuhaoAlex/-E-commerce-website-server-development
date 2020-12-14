chmod -R 777 /var/home/userid/cc     #文件夹权限

passwd username  #用户密码
 
sudo vim /etc/sudoers -> /root -> noh  #设置用户root 权限  

useradd ftpuser -d userpath(/ftpfile) -s /sbin/nologin  #创建用户,以及用户的路径

chown -R ftpuser.ftpuser /ftpfile/   #把文件夹赋给ftpuser

cd /etc/vsftpd -> vim chroot_list -> ftpuser #添加FTP的chroot_list 用户

vim  /etc/selinux/config -> SELINUX=disable 

sudo setsebool -P ftp_home_dir 1

## nginx    
Nginx是一款自由的、开源的、高性能的HTTP服务器和反向代理服务器；同时也是一个IMAP、POP3、SMTP代理服务器；Nginx可以作为一个HTTP服务器进行网站的发布处理，另外Nginx可以作为反向代理进行负载均衡的实现.  
客户端是无感知代理的存在的，反向代理对外都是透明的，访问者并不知道自己访问的是一个代理。因为客户端不需要任何配置就可以访问.  
反向代理，"它代理的是服务端，代服务端接收请求"，主要用于服务器集群分布式部署的情况下，反向代理隐藏了服务器的信息。  
load balance, safety  
https://www.cnblogs.com/wcwnina/p/8728391.html#:~:text=Nginx%E6%98%AF%E4%B8%80%E6%AC%BE%E8%87%AA%E7%94%B1,%E8%BF%9B%E8%A1%8C%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%E7%9A%84%E5%AE%9E%E7%8E%B0%E3%80%82

wget http://learning.happymmall.com/nginx/linux-nginx-1.10.2.tar.gz #下载ngix

sudo yum install gcc #安装依赖环境

sudo yum -y install zlib zlib-devel pcre-devel openssl openssl-devel #安装依赖环境

sudo tar zxvf linux-nginx-1.10.2.tar.gz #nginx 解压

sudo ./configure

sudo make

sudo make install

whereis nginx -> cd ...../nginx -> cd conf -> vim nginx.conf ->  include vhost/*.conf -> mkdir vhost -> cd vhost -> wget http://learning.happymmall.com/nginx/linux_conf/vhost/ 里面内容

cd .. cd .. ->cd sbin-> ./nginx -> error:/usr/local/nginx/conf/nginx.conf -> vin /usr/local/nginx/conf/nginx.conf -> :set number -> include.....; (少一个分号)

## MySQL

yum -y install mysql-server  

vim /etc/my.cnf -> character-set-server=utf8 , default-character-server=utf8

chkconfig mysqld on  #mysql自启动

chkconfig --list mysqld  #查看自启动

-----------------------------------------------------------  
#### errors
>MySQL Daemon failed to start.
>Starting mysqld:   

cd /var/log -> vim mysqld.log

>/usr/libexec/mysqld: Table 'mysql.plugin' doesn't exist
>201213 15:10:42 [ERROR] Can't open the mysql.plugin table. Please run mysql_upgrade to create it.
>201213 15:10:42  InnoDB: Initializing buffer pool, size = 8.0M
>201213 15:10:42  InnoDB: Completed initialization of buffer pool
>InnoDB: Log scan progressed past the checkpoint lsn 0 37356

mysql_upgrade

>Looking for 'mysql' as: mysql
>Looking for 'mysqlcheck' as: mysqlcheck
>Running 'mysqlcheck with default connection arguments
>mysqlcheck: Got error: 2002: Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2) when trying to connect
>FATAL ERROR: Upgrade failed

cd /var/lib/mysql 发现没有 mysql.sock

查找https://blog.csdn.net/FrankieHello/article/details/78304092

>mysql> use mysql;  
>mysql> update user set password=password("你的新密码") where user="root";  
>mysql> flush privileges;  
>mysql> quit   

service mysqld restart -> 成功

-----------------------------------------------------------  

select user, host, password from mysql.user;  

set password for root@localhost=password('950723')   #更新用户密码

delete from mysql.user where user='';

flush privileegs;   #刷新

create database `mmall` default character set utf8 COLLATE utf8_general_ci;  #创建数据库

grant all privileges on mmall.* to yuhao@localhost identified by '950723';   #赋予用户管理数据库权限

#### 导入数据库

exit-> cd developer -> wget http://learning.happymmall.com/mmall.sql     #下载数据库文件

mysql -u root -p

use mmall -> source /developer/mmall.sql     #导入数据库

select * from mmall_user\G;    #\G 格式化


## git

mkdir /setup -> cd setup

wget http://learning.happymmall.com/git/git-v2.8.0.tar.gz

sudo yum -y install zlib-devel openssl-devel cpio expat-devel gettext-devel curl-devel perl-ExtUtils-CBuilder perl-ExtUtils- MakeMaker     #git 安装依赖

tar -zxvf git-v2.8.0.tar.gz 

cd git-2.8.0/

make

make prefix=/usr/local/git all

sudo make prefix=/usr/local/git install

git version -> no such .... -> sudo vim /etc/profile -> PATH 末尾加/usr/local/git/bin: -> source /etc/profile -> git --version   #在path中配置git的路径

git config --global user.name "imooc"     
git config --global user.email "imooc@163.com"    
git config --global core.autocrlf false       #ignore windows, linux 的换行符转换   
git config --global core.quotepath off        #避免中文乱码   
git config --global gui.encoding utf-8        #配置gui   
ssh-keygen -t rsa -C "imooccode@163.com"      #ssh

eval `ssh-agent`  
ssh-add ~/.ssh/id_rsa   
 
cat ~/.ssh/id_rsa.pub    #获取公共密钥  
>ssh-rsaAAAAB3NzaC1yc2EAAAABIwAAAQEAqLIEDoOuJBcxkp6lhTof7phT1ksE34IJHJGVkZfhJWD5FFkzvYR+jqBx1yh6ECfvWpSUGOXTyRfQLXBhgBAeXdwqO3PZ85Zmuq2SCE6CDhowirmkAFUl9kCxNCdukDK/whYu1CrctPOS0tzFXeaz7MI/zJuZ/GB83CxhYa6xrhcQUl/awXq613p44sBxcQ735ocN3uiEOnutJ9SoaCLMC/4SN9pnlb3PYcPI+GSgVRmIjCw2w0D7pzoSU8K7rk5WkmYbW2ly8eeMT+6l2/0W8mTBC1E4xAwoqG6t95X0090Vj5CHfOHKTR1hYTfupWR2YF8eHwPadQB828hC3jFhgw== imooccode@163.com

git-> addnew ssh key-> 把公钥粘贴 -> 完成


## Firewall

cd /etc/sysconfig/  -> 只有iptables.config -> iptables -P OUTPUT ACCEPPT（随便写一条规则） -> service iptables save

wget http://learning.happymmall.com/env/iptables 

vim iptables: 注释掉3306 端口， 注释8080端口， 5005端口（tomcat远程debug端口）  
              开放80端口--网站访问
              
service iptables restart 

## 自动化脚本

cd /developer -> wget http://learning.happymmall.com/deploy/deploy.sh -> vim deploy.sh -> 



# 详解---开发

## Nginx

•可直接支持Rails 和PHP 程序  
•HTTP反向代理服务器  
•负载均衡服务器  
•邮件代理服务器  
•帮助前端实现动静分离

### 命令  

/nginx/sbin/nginx -t   #测试配置文件 

/nginx/sbin/nginx     #启动

/nginx/sbin/nginx -s stop 或者  nginx -s quit         #停止命令

/nginx/sbin/nginx -s reload        #重启

ps -ef|grep nginx        #查看进程

kill -HUP 【Nginx主进程号】     #平滑重启

lsof -i :port  #查看端口状态

### Nginx虚拟域名配置及测试验证

cd /usr/local/nginx/conf/vhost/ -> vim learning.happymmall.com.conf -> proxy_pass http://192.168.1.59:8080;

cd .../nginx/sbin -> nginx -s reload

打开www.imooc.com 即可




### 配置linux域名

sudo vim /etc/hosts  
添加对应的域名即ip  
![image](https://github.com/YuhaoAlex/-E-commerce-website-server-development/blob/main/images/WX20201214-085007%402x.png)
 
 
 
## apache-tomcat-7.0.73

cd /home/yuhao/Desktop/apache-tomcat-7.0.73/bin ->./startup.sh






















