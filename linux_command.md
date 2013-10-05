
Linux Command
============================

## 文件管理
    cat -n filename  // 输出行号
    chmod -R 777 filename
    ln -s source link

## 文档编辑

## 查找替换
    grep 'strinng' -r *
    find . -name 'filename'
    find . -mtime -1 // 1天以内修改的文件
    find . -cmin -1  // 1分钟以内修改的文件
    find . -user root // 查找owner是root的文件
    find . !-user root 
    find . -group root // 查找group是root的文件
    find . -maxdepth 1 -name '*'
    // 过滤目录
    find . -path './dontsearchpath' -prune -o -name 'a.txt'
    find . -size +4k 
    

    sed -i 's/str1/str2/g' `grep str1 -RL ./`  // ./是当前目录

## 传输
    上传：rz -bey // receive
    下载：sz filename // send
    scp /path/file name@ip:/path/file

## 打包
    zip -r file.zip folename/*
    unzip file.zip

## 查看log
    tail -f filename | grep 'match'
    tail -f filename | grep -v 'not match'

## 查看目录及子目录大小
    du -sh *

## 比较
    vimdiff file1 file2

## curl
    curl -v http://www.xxx.com?p1=1&p2=2
    curl --data 'data=xxx' http://www.xxx.com
    curl -X DELETE www.xxx.com
    curl --form upload=@localfilename --form press=ok www.xxx.com
    curl --cookie 'name=xxx' www.xxx.com
    curl --header 'xxx: xxxx' www.xxx.com
    echo '<?xml version="1.0"><xxx></xxx></xml>' | curl -X POST -H 'Content-type:text/xml' -d @- www.xxx.com

## base64
    echo 'string' | base64
    echo 'coding' | base64 -D
    base64 file
    cat file | base64


## 网上资料
[linux](http://www.linux.org/ "linux")

[curl网站开发指南](http://www.ruanyifeng.com/blog/2011/09/curl.html "curl网站开发指南")

[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

