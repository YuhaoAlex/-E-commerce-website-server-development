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

#### errors
>MySQL Daemon failed to start.
>Starting mysqld: 


