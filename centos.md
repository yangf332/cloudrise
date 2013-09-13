
CentOS 和 Ubuntu学习
============================
记录CentOS和 Ubuntu安装学习的点滴

## VitualBox安装CentOS
    下载了VitualBox和CentOS ios文件安装。
    前几次都错选了从光盘启动，每次进入都是新系统。这才发现根本就没有安装过，我说怎么感觉哪里不对呢。
    重新安装分区配置。

## 查看系统信息
    // lsb是Linux Standard Base的缩写，lsb_release命令用来显示LSB和特定版本的相关信息
    lsb_release -a  
    // Linux查看版本当前操作系统内核信息
    uname -a
    // 查看版本当前操作系统发行版信息
    cat /etc/issue
    cat /proc/version
    // 查看CPU信息
    cat /proc/cpuinfo | grep name
    cat /proc/cpuinfo | grep physical
    // 系统运行位数
    getconf LONG_BIT

## sudo提权提示“xx用户不在sudoers文件中，此事将被报告”
    解决方法：用root编辑/etc/sudoers文件，添加一行：
    username ALL=(ALL) ALL
    解决

## 安装httpd, php
    yum install httpd
    /etc/init.d/httpd start
    可以用浏览器打开localhost，看到主页了
    yum install php
    /etc/init.d/httpd restart
    在/var/www/html下添加php文件，写入phpinfo();可以看到内容了
    但是不知道为什么，本机还是无法访问虚拟主机的web应用

## 引导时启动httpd
    chkconfig --list
    chkconfig --add httpd
    chkconfig --level 2345 httpd on

## mysql
    yum install mysql
    yum install mysql-server
    yum install php-mysql
    /etc/init.d/mysqld start
    chkconfig --list
    chkconfig --add mysqld
    chkconfig --level 2345 mysqld on

## mysql自动备份
    vim bakmysql
    mysqldump -uroot -ppasswd databasename | gzip > /var/www/html/mysqldata/`date +%Y-%m-%d_%H%M%S`.sql.gz
    chmod +x bakmysql
    vim /etc/crontab
    01 3 * * * root /usr/sbin/bakmysql // 每天3点执行
    service crond start
    chkconfig --level 2345 crond on

## 配置sshd
    vim /etc/ssh/sshd_config
    Protocol 2,1 允许SSH1和SSH2连接，建议设置成 Protocal 2
    vim /etc/hosts.deny
    sshd:All
    vim /etc/hosts.allow
    sshd:All
    启动：/etc/init.d/sshd start
    ssh localhost 成功
    [参考](http://www.cnblogs.com/trams/archive/2012/04/29/2476175.html "参考")

## 安装rzsz
    yum install lrzsz


## [U]ubuntu安装apache, php
    sudo apt-get update

## [U]ubuntu安装curl
    sudo apt-get install curl libcurl3 libcurl3-dev php5-curl
    *** curl.ini (Y/I/N/O/D/Z) [default=N] ? Y
    Installing new version of config file /etc/php5/conf.d/curl.ini ...
    重启apache

## [U]ubuntu安装gd2
    sudo apt-get install php5-gd 
    重启apache

## [U]ubuntu启用rewrite
    sudo a2enmod rewrite
	vim /etc/apache2/sites-available/default
	RewriteEngine on
    RewriteCond $1 !^(\/index\.php|\/img|\/assets|\/js|\/css|\/robots\.txt|\/favicon\.ico|\/crossdomain\.xml)
    RewriteRule ^(.*)$ /index.php$1 [L]

## [U]ubuntu开启80端口
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT

## 网上资料
[linux](http://www.linux.org/ "linux")
[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

