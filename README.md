# E-commerce-website-server-development

1. TestWebsites:
    frontend: www.happymmall.com
    backend: admintest.happymmall.com
    materials: learning.happymmal.com
    
2. CentOS 6.8 环境：
    yum 装载： https://blog.csdn.net/qq_40907977/article/details/110792105
            阿里云11/30/2020停止维护CentOS 6.8 的yum repo， 使用官方repo， wget 之后进行 yum makecache
            
    下载新的jdk， 修改环境， etc/profile, 添加JAVA_HOME 路径， source etc/profile， 执行命令
    
3. Tomcat: Tomcat7
     tomcat 安装，环境 /ect/profile CALALINA_HOME=home/yuhao/apache.....
     启动： apache..../bin/ -> ./startup.sh
     ****虚拟机内能访问，本地不行****：虚拟机设置防火墙端口 8080 open， 本地访问 192.168.1.59:8080
     
     
### Develop:

#### 1. vsftpd:

• commands:  
    vim /etc/vsftpd/vsftpd.conf     
    service vsftpd restart    
    useradd ftpuser -d /ftpfile -s /sbin/nologin   -----添加用户    
    passwd ftpuser   ----修改用户密码      
    userdel ftpuser  ----删除用户 
    id ftpuser      -----查询用户     
    whereis vsftp    
    vim /etc/sysconfig/iptables    
    service iptables restart      

    
