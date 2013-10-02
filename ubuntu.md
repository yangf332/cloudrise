
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
    sudo apt-get install openssh-server
    ssh localhost   // 测试可用
    ssh user@host
    // 禁用密码，使用公钥登录
    ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
    or
    ssh-copy-id -i .ssh/id_rsa.pub user@host
    sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
    sudo vim /etc/ssh/sshd_config
        PermitRootLogin no
        PasswordAuthentication no
        UsePAM no
    sudo /etc/init.d/ssh restart
    // 认证日志
    grep sshd /var/log/auth.log.0

## 



## 网上资料
[《Ubuntu Server最佳方案》]


[百度百科：ubuntu](http://baike.baidu.com/view/4236.htm "ubuntu")

[forum.ubuntu.org.cn](http://forum.ubuntu.org.cn/ "forum.ubuntu.org.cn")


