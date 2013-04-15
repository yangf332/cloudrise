
Linux Command
============================

## 查找替换
    grep 'strinng' -r *
    find . -name 'filename'
    find . -mtime -1 // 1天以内修改的文件

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

## 网上资料
[linux](http://www.linux.org/ "linux")
