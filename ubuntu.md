
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
    /etc/init.d/ssh restart
    // 认证日志
    grep sshd /var/log/auth.log.0

## 帐号管理
    useradd -m -s /bin/bash newuser
    passwd newuser
    groupadd ftp                          // 添加组
    usermod -g www newuser                // 添加帐号到组
    usermod -G www,ftp,backup newuser     // 添加帐号到多个组
    id newuser && groups newuser          // 验证
    // sudoer和权限
    vim /etc/sudoers
    newuser ALL=(ALL:root) /usr/bin/find, /bin/rm
    // TODO 别名设置
    // 删除
    userdel newuser

## 安装LAMP
    apt-get install apache2
    apt-get install mysql-server
    apt-get install php5
    apt-get install php5-mysql
    
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

## 启用rewrite
    a2enmod rewrite
    vim /etc/apache2/sites-available/www.test.com
    RewriteEngine on
    RewriteCond $1 !^(\/index\.php|\/img|\/assets|\/js|\/css|\/robots\.txt|\/favicon\.ico|\/crossdomain\.xml)
    RewriteRule ^(.*)$ /index.php$1 [L]

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


## 网上资料
[《Ubuntu Server最佳方案》]


[百度百科：ubuntu](http://baike.baidu.com/view/4236.htm "ubuntu")

[forum.ubuntu.org.cn](http://forum.ubuntu.org.cn/ "forum.ubuntu.org.cn")

[Linux命令----分析CPU的瓶颈](http://space.itpub.net/8554499/viewspace-580300 "http://space.itpub.net/8554499/viewspace-580300")
