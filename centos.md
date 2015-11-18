
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
    // 查看语言环境变量
    locale
    cat /etc/default/locale

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
    
## 安装开发工具包
    These tools include core development tools such as automake, gcc, perl, python and debuggers which is required to compile software and build new rpms
    // 命令
    yum groupinstall 'Development Tools'

## 安装cacti
    rpm -ivh http://apt.sw.be/redhat/el6/en/i386/rpmforge/RPMS/rpmforge-release-0.5.2-2.el6.rf.i686.rpm
    yum install rrdtool -y
    yum install net-snmp net-snmp-libs net-snmp-utils
    service snmpd start
    下载安装cacti: http://www.cacti.net/downloads/
    添加自动任务
    echo "*/5 * * * * cactiuser php /var/www/html/cacti/poller.php > /dev/null 2>&1">>/etc/crontab
    
## 安装git服务器
    sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
    cd /usr/local/src
    wget http://code.google.com/p/git-core/git-1.9.0.tar.gz
    sudo tar -zxvf git-1.9.0.tar.gz
    cd git-1.9.0
    sudo make prefix=/usr/local/git all
    sudo make prefix=/usr/local/git install
    sudo ln -s /usr/local/git/bin/* /usr/bin/
    git --version  #显示版本号，表示成功
    sudo yum install python python-setuptools
    cd /usr/local/src
    git clone git://github.com/res0nat0r/gitosis.git
    cd gitosis
    python setup.py install  #显示Finished processing dependencies for gitosis==0.2即表示成功
    # 开发机上
    scp id_rsa.pub username@ip:/tmp
    # server
    su - username
    gitosis-init < /tmp/id_rsa.pub
    # 开发机
    git clone username@ip/gitosis-admin.git
    vim gitosis.conf
    mkdir test-git
    cd test-git
    git init
    git add .
    git commit -m 'init'
    git remote add origin username@ip:test-git.git
    git push origin master
    

## FAQ
* 运行phpize时出现：Cannot find autoconf. Please check your autoconf installation
  - 解决
    - yum install m4
    - yum install autoconf
  - 解释
    - autoconf 是 用来生成自动配置软件源代码脚本（configure）的 工具.configure脚本能独立于autoconf运行,且在 运行的 过程中,不需要用户的 干预.
    - autoconf从configure.in这个列举编译软件时所需要各种参数的 模板文件中创建configure
    - autoconf需要GNU m4宏处理器来处理aclocal.m4,生成configure脚本.m4是 一个宏处理器.将输入拷贝到输出,同时将宏展开.宏可以是 内嵌的 ,也可以是 用户定义的 .除了可以展开宏,m4还有一些内建的 函数,用来引用文件,执行命令,整数运算,文本操作,循环等.m4既可以作为编译器的 前端,也可以单独作为一个宏处理器.

## 网上资料
[linux](http://www.linux.org/ "linux")

[《Ubuntu Server最佳方案》]

[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

[cacti install](http://baike.baidu.com/link?url=CtWOY3jK8-GvY3tKG5gjJ7CAo8cM-YT0BwCUkB3q5TzLGa1sRS29H-Uji_9M-6bvnx2JeSQbvGCCAaksmmdBha "cacti install")

[git server](https://github.com/jackliu2013/recipes/blob/master/doc/linux/CentOS_6.4_git%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%90%AD%E5%BB%BA.md)


