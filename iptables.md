iptables
============================

## 安装
    yum install iptables
    
### 查看状态
* service iptables status
* /etc/init.d/iptabls status
* iptables -L -n    

### 清除已有规则
* iptables -F // 清除所有规则
* iptables -X // 清除操作者定义规则

### 规则
    iptables
      -A  // -A add 添加到规则列表最末尾； -I insert 插入到规则最前
      INPUT  // INPUT|OUTPUT|FORWARD 数据流方向流入|流出|转发
      -p tcp  // tcp|udp|icmp|!tcp  -icimp-type 8
      -s [ip]  // !(10.1.0.0/16)
      --dport 80 // 端口
      -m limit -limit 300/hour
      -j ACCEPT  // ACCEPT 开放；DROP 关闭
      
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT     // 开放端口段

### 删除规则
    iptables -L -n --line-numbers
    iptables -D INPUT 8 // 8号规则

### 保存
* iptables save
* iptables restart

### 配置文件
* /etc/sysconfig/iptables

## 网上资料
[iptables基本配置](http://www.vpser.net/security/linux-iptables.html "iptables基本配置")

