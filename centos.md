
CentOS
============================
记录CentOS安装学习的点滴

## VitualBox安装CentOS
    下载了VitualBox和CentOS ios文件安装。
    前几次都错选了从光盘启动，每次进入都是新系统。这才发现根本就没有安装过，我说怎么感觉哪里不对呢。
    重新安装分区配置。

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
    chkconfig --add httpd
    没成功，还不知道原因


## 网上资料
[linux](http://www.linux.org/ "linux")
[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

