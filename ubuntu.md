
Ubuntu
============================
记录学习Ubuntu的点滴

## 简介
    Ubuntu（乌班图）是基于Debian GNU/Linux，支持x86、amd64（即x64）和ppc架构，由全球化的专业开发团队（Canonical Ltd）打造的开源GNU/Linux操作系统。
    Ubuntu每6个月发布一个新版本，而每个版本都有代号和版本号，其中有LTS是长期支持版。版本号基于发布日期，例如第一个版本，4.10，代表是在2004年10月发行的。

## 官方下载
    http://releases.ubuntu.com/


## 安装

## 远程管理
    apt-get install openssh-server
    ssh localhost   // 测试可用
    ssh user@host
    // 禁用密码，使用公钥登录
    ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
    or
    ssh-copy-id -i .ssh/id_rsa.pub user@host
    cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
    vim /etc/ssh/sshd_config
        PermitRootLogin no
        PasswordAuthentication no
        UsePAM no
        // 保持连接状态
        TCPKeepAlive yes
        ClientAliveCountMax 360
    /etc/init.d/ssh restart
    // 认证日志
    grep sshd /var/log/auth.log.0

## 帐号管理
    useradd -d /home/[newuser] -s /bin/bash -m [newuser] // m表示如果目录不存在则创建
    passwd [newuser]
    groupadd ftp                          // 添加组
    usermod -g www newuser                // 添加帐号到组
    usermod -G www,ftp,backup newuser     // 添加帐号到多个组
    id newuser && groups newuser          // 验证
    // sudoer和权限
    vim /etc/sudoers                      // or `visudo`
    [newuser] ALL=(ALL:root) /usr/bin/find, /bin/rm
    [newuser] ALL=(ALL) NOPASSWD: ALL     // sudo时不需要密码
    // TODO 别名设置
    // 删除
    userdel -r [newuser]

## 运行环境配置
    locale
    sudo locale-gen en_US en_US.UTF-8 en_CA.UTF-8
    sudo dpkg-reconfigure lcales
    sudo apt-get update
    sudo apt-get upgrade

## 安装LAMP
    apt-get install apache2
    apt-get install mysql-server
    apt-get install php5
    apt-get install php5-mysql

## 安装LNMP
    apt-get install nginx
    /etc/init.d/nginx start | service nginx start
    vim /etc/nginx/sites-available/default 
    # location ~ .php${} 打开
    apt-get install mysql-server mysql-client
    apt-get install pp5-fpm
    vim /usr/share/nginx/html/test.php  
    service php5-fpm start     
    service nginx -t // 测试配置文件
    service php5-fpm -t // 测试配置文件

## 安装chkconfig
    apt-get install chkconfig
    chkconfig --level 2345 apache2 on
    chkconfig --level 2345 mysql on    

## 配置目录权限
    chown -R user:www-data /var/www
    chmod -R 774 /var/www 

## 配置Apache
    a2enmod        // 配置模块
    a2dismod       // 关闭配置模块
    cd /etc/apache2/sites-available/
    cp default www.test.com
    vim www.test.com
    a2dissite default && a2ensite www.test.com
    /etc/init.d/apache2 start

## 增加新的端口
    vim /etc/apache2/ports.conf
    NameVirtualHost *:80
    NameVirtualHost *:8080
    Listen 80
    Listen 8080
    vim /etc/apache2/sites-available/[xxx]
    <VirutalHost *:8080>
    ...
    </VirutalHost>
    重启apache2

## 启用rewrite
    a2enmod rewrite
    vim /etc/apache2/sites-available/www.test.com
    RewriteEngine on
    RewriteCond $1 !^(\/index\.php|\/img|\/assets|\/js|\/css|\/robots\.txt|\/favicon\.ico|\/crossdomain\.xml)
    RewriteRule ^(.*)$ /index.php$1 [L]
    AND
    <Directory />
    Options -Indexes FollowSymLinks #-Indexes表示不允许目录浏览
    AllowOverride None | All | AuthConfig | FileInfo | Indexes | Limit | Options
    </Directory>
    设置为None时完全忽略.htaccess文件
    禁止目录浏览，还可以在.htaccess文件中输入
    <Files *>
    Options -Indexes
    </Files>

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
    // 查看语言环境变量
    locale
    cat /etc/default/locale


## [U]ubuntu安装apache, php
    apt-get update
    apt-get install apache2
    apt-get install mysql-server
    apt-get install php5, php5-mysql, php5-gd

## [U]ubuntu启动apache
    sudo /etc/init.d/apache2 start

## [U]Apache创建一个新的虚拟主机(复制default并启用)
    cd /etc/apache2/sites-available/
    sudo cp default www.test.com
    vim www.test.com
    sudo a2dissite default && sudo a2ensite www.test.com
    sudo /etc/init.d/apache2 restart

## [U]ubuntu安装curl
    sudo apt-get install curl libcurl3 libcurl3-dev php5-curl
    *** curl.ini (Y/I/N/O/D/Z) [default=N] ? Y
    Installing new version of config file /etc/php5/conf.d/curl.ini ...
    重启apache

## [U]ubuntu安装ssg
    sudo apt-get install openssh-server
    /etc/init.d/ssh start
    ssh localhost

## [U]HTTPS的实现

## [U]启用压缩

## [U]使用缓存（mod_cache）

## [U]不要以root身份运行Apache

## [U]ubuntu启用rewrite
    sudo a2enmod rewrite
    vim /etc/apache2/sites-available/default
    RewriteEngine on
    RewriteCond $1 !^(\/index\.php|\/img|\/assets|\/js|\/css|\/robots\.txt|\/favicon\.ico|\/crossdomain\.xml)
    RewriteRule ^(.*)$ /index.php$1 [L]

## [U]ubuntu开启默认关闭的80端口
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT

## [U]ufw防火墙
    apt-get install ufw
    ufw enable
    ufw default deny
    ufw allow 22/tcp
    ufw allow from 10.0.0.1
    ufw deny 80
    ufw delete deny 80/tcp
    ufw status

## [U]用Apache支持Python
    sudo apt-get intall libapache2-mod-python
    支持Python有两种方式：后者支持html中嵌入py代码
        Publisher Handler:
            <Directory /var/www/>
                AddHandler mod python .py
                PythonHandler mod_python.publisher
                PythonDebug On
            </Directory>
        PSP Handler:
            <Directory /var/www/>
                AddHandler mod python .psp
                PythonHandler mod_python.psp
                PythonDebug On
            </Directory>
    sudo /etc/init.d/apache2 restart

## [U]用Django开发Web应用
    sudo apt-get install python-django
    django-admin startproject mysite
    
## [U]locale-gen
    locale-gen zh_CN.UTF-8  // 编译本地定义文件的一个列表
    环境变量：
    LC_CTYPE     - Character classification and case conversion.
    LC_COLLATE   - Collation order.
    LC_TIME      - Date and time formats.
    LC_NUMERIC   - Non-monetary numeric formats.
    LC_MONETARY  - Monetary formats.
    LC_MESSAGES  - Formats of informative and diagnostic messages and interactive responses.


## locale-gen
    locale-gen zh_CN.UTF-8  // 编译本地定义文件的一个列表
    环境变量：
    LC_CTYPE     - Character classification and case conversion.
    LC_COLLATE   - Collation order.
    LC_TIME      - Date and time formats.
    LC_NUMERIC   - Non-monetary numeric formats.
    LC_MONETARY  - Monetary formats.
    LC_MESSAGES  - Formats of informative and diagnostic messages and interactive responses.

## 分析CPU瓶颈
    apt-get install sysstat
    mpstat         // mpstat 不但能查看所有CPU的平均信息，还能查看指定CPU的信息。
    vmstat         // 只能查看所有CPU的平均信息；查看cpu队列信息；
    iostat         // 只能查看所有CPU的平均信息。
    sar
    uptime 
    w
    top

## 工具
    iftop - 网络流量监控工具 
        sudo apt-get install iftop
        sudo iftop
    nethogs - 网络流量监控工具
        sudo apt-get install nethogs
        sudo nethogs




## 其它

#### 其它命令
    lscpu  # 查询cpu信息
    lshw   # 查询硬件信息
    lspci  # 查询pci总线相关信息
    lsusb  # 查询usb信息
    lsblk  # 查询块设备信息，包括硬盘分区

#### 理解inode
    inode是Unix/Linux文件系统和硬盘存储的基础
    inode包含信息：文件的字节数、UID、GID、权限、三个时间戳、链接数、block位置
    stat filename  // 查看inode
    每个inode大小为128字节或256字节。每1-2KB设置一个inode。
    df -i          // 查看inode总数
    dumpe2fs -h /dev/hda | grep "Inode size"   // 查看每个inode节点大小
    由于每个文件都必须有一个inode，因此有可能发生inode已经用光，但是硬盘还未存满的情况。这时，就无法在硬盘上创建新文件。
    每个inode都有一个号码，操作系统用inode号码来识别不同的文件。
    ls -i filename  // 查看文件名对应的inode编号
    作用：
        1. find . -inum INODE_NUM -delete   // 通过inode号删除文件
        2. 移动或重命名文件，只改变文件名，不影响inode号
        3. 通过inode识别文件，实现运行中更新


## 错误解决
    1. apache2: Could not reliably determine the server 's fully qualified domain name, using 127.0.1.1 for ServerName
    vim /etc/apache2/httpd.conf
    ServerName localhost


## 网上资料
[《Ubuntu Server最佳方案》]


[百度百科：ubuntu](http://baike.baidu.com/view/4236.htm "ubuntu")

[forum.ubuntu.org.cn](http://forum.ubuntu.org.cn/ "forum.ubuntu.org.cn")

[Linux命令----分析CPU的瓶颈](http://space.itpub.net/8554499/viewspace-580300 "http://space.itpub.net/8554499/viewspace-580300")

[inode](http://www.ruanyifeng.com/blog/2011/12/inode.html "inode")

[Apache - AllowOverride](http://www.chinaz.com/server/2010/0129/105397.shtml "Apache - AllowOverride")
