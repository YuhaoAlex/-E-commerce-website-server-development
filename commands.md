passwd username  #用户密码
 
sudo vim /etc/sudoers -> /root -> noh  #设置用户root 权限  

useradd ftpuser -d userpath(/ftpfile) -s /sbin/nologin  #创建用户,以及用户的路径

chown -R ftpuser.ftpuser /ftpfile/   #把文件夹赋给ftpuser

cd /etc/vsftpd -> vim chroot_list -> ftpuser #添加FTP的chroot_list 用户

vim  /etc/selinux/config -> SELINUX=disable 

sudo setsebool -P ftp_home_dir 1

### nginx  
Nginx是一款自由的、开源的、高性能的HTTP服务器和反向代理服务器；同时也是一个IMAP、POP3、SMTP代理服务器；Nginx可以作为一个HTTP服务器进行网站的发布处理，另外Nginx可以作为反向代理进行负载均衡的实现。

wget http://learning.happymmall.com/nginx/linux-nginx-1.10.2.tar.gz #下载ngix

sudo yum install gcc #安装依赖环境

sudo yum -y install zlib zlib-devel pcre-devel openssl openssl-devel #安装依赖环境

sudo tar zxvf linux-nginx-1.10.2.tar.gz #nginx 解压

sudo ./configure

sudo make

sudo make install

whereis nginx -> cd ...../nginx -> cd conf -> vim nginx.conf ->  include vhost/*.conf -> mkdir vhost -> cd vhost -> wget http://learning.happymmall.com/nginx/linux_conf/vhost/ 里面内容

cd .. cd .. ->cd sbin-> ./nginx -> error:/usr/local/nginx/conf/nginx.conf -> vin /usr/local/nginx/conf/nginx.conf -> :set number -> include.....; (少一个分号)
