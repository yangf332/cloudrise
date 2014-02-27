
构建高性能Web站点
============================


## 二、数据的网络传输
    带宽（band width）指在固定时间内可传输的资料数量。单位bps(bit/s)

## 三、服务器并发处理能力
    吞吐率(Throughput)，单位是reqs/s(requests/sec)，描述Web服务器单位时间内处理的请求数
    开启Apache Server Status
        修改httpd.conf，打开server-status的注释
        Allow from ip
        service httpd restart
        访问localhost/server-status
    进行ab测试
        ab -V
        // -n请求数 -c
        ab -n1000 -c10 http://localhost/test.php
    strace
        strace用来跟踪进程执行时的系统调用和所接收的信号。
        在Linux世界，进程不能直接访问硬件设备，当进程需要访问硬件设备(比如读取磁盘文件，接收网络数据等等)时，必须由用户态模式切换至内核态模式，通 过系统调用访问硬件设备。
        strace可以跟踪到一个进程产生的系统调用,包括参数，返回值，执行消耗的时间。
        strace cat /tmp/tmp
        strace -p pid

## 四、动态内容缓存
    缓存的目录就是把花费昂贵开销的计算结果保存起来，在需要的时候直接取出使用，避免重复计算。
    缓存最重要的是缓存命中率。
    smarty cache
    file cache
    APC cache
    XCache cache
    memcache cache

## 五、动态脚本加速
    opcode 
    函数跟踪
    xdebug

## 六、浏览器缓存
    header("HTTP/1.1 304");
    header("Last-Modified: " . gmdate("D, d M Y H:i:s") . " GMT");
    header("Expires: " . gmdate("D, d M Y H:i:s", time() + 3600) . " GMT")

## 七、Web服务器缓存
    .

## 八、反向代理缓存
    .

## 九、Web组件分离
    使用不同的域名对Web组件进行分离后，提高了浏览器下载并发数。


## 十、分布式缓存
    memcached

## 十一、数据库性能优化
    mysql> show status;
    mysql> show innodb status;
    第三方工具： mysqlreport
    explain select * from tablename where id = 1;
        在explain的分析结果中：
            type为const，意味着通过索引查询，所以时间复杂度为常量；
            type为ALL，意味着全表查询，
    组合索引：
    减少表锁定：
        show processlist\G;
    使用查询缓存：update时则更新缓存
        query_cache_size = xxx
        query_cache_type = 1
        query_cache_limit = xxx
    线程池： 尽量使用持久连接
        thread_cache_size = 100


## 十二、Web负载均衡
    HTTP重定向
    DNS负载均衡

## 十三、共享文件系统

## 十四、内容分发和同步
    主动分发：SCP, WebDAV, rsync
    被动同步

## 十五、分布式文件系统

## 十六、数据库扩展
    主从复制：1，开启主服务器上的二进制日志；2，在主从服务器上配置授权
    读写分离：1，更新操作必须作用于主服务器
    数据库反向代理： MySQL Proxy
    水平分区：分库分

## 十七、分布式计算

## 十八、性能监控


## 书外内容

### 互联网系统架构的演进
    1. 网站开发初期：短平快
        开发语言：PHP、Java为主力
        辅助框架：PHP的Yii，Python的Django等
        数据：    安全和备份
    2. 解决可用性问题：不能有单点失效
        前端采用LVS、HAProxy、Nginx等负载均衡/反向代理设备
        DB：DRDB+Heartbeat技术组合
        程序节点：
    3. 解决性能问题：水平扩展
        数据存储：硬盘读写、内存读写
        存储模型：结构化存储（传统DB）和NoSQL存储(HBase、Memcached、Redis)
        定制文件系统：GFS、TFS
        分库分表：水平切分、垂直切分
        缓存：本地缓存、分布式缓存
        

## 网上资料
[linux strace](http://www.cnblogs.com/ggjucheng/archive/2012/01/08/2316692.html "linux strace")

[linux](http://www.linux.org/ "linux")

[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

[互联网系统架构的演进](http://blog.csdn.net/heiyeshuwu/article/details/11862979 "互联网系统架构的演进")

