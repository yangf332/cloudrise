
构建高性能Web站点
============================

## 服务器并发处理能力
    吞吐率(Throughput)，单位是reqs/s(requests/sec)，描述Web服务器单位时间内处理的请求数
	
## 开启Apache Server Status
    修改httpd.conf，打开server-status的注释
    Allow from ip
    service httpd restart
    访问localhost/server-status

## 进行ab测试
    ab -V
    // -n请求数 -c
    ab -n1000 -c10 http://localhost/test.php


## 网上资料
[linux](http://www.linux.org/ "linux")
[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

