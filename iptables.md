
iptables
============================

## 安装
    yum install iptables


## 命令
    iptables -L -n                                    // 查看已有规则
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT     // 开放端口
    iptables -I INPUT -s [ip] -j DROP                 // 屏蔽IP
    iptables -I INPUT -s [ip]/8 -j DROP               // 屏蔽IP段

    iptables save


## 网上资料
[iptables基本配置](http://www.vpser.net/security/linux-iptables.html "iptables基本配置")

