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

    sed -i 's/str1/str2/g' `grep str1 -rl ./`  // ./是当前目录
    
## for循环
    for i in {1..10}; do echo $i; done
    for i in 1 2 3;do echo $i; done
    for var in `cat filename.txt`; do echo $var; done
    // 批量修改文件名
    for var in *.txt; do mv $var `echo $var|tr a-z A-Z`;done // 大小写转换
    for var in *.txt; do mv $var `echo $var|sed s/abc/def/`;done // 正则替换
    
    

## 传输
    上传：rz -bey // receive
    下载：sz filename // send
    scp /path/file name@ip:/path/file

## 打包
    zip -r file.zip foldername/*
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

## 标准编译安装
    wget http://xxx/xxx.tar.gz
    tar -zxvf xxx.tar.gz
    tar -jxvf xxx.tar.bz2
    cd xxx/
    ./configure --prefix-/opt/xxx  // 配置软件特性，检查编译环境，生成 Makefile文件
    make                           // 根据 Makefile 编译源代码
    sudo make install              // 将编译完成的程序安装到系统中。通常需要 root权限
    make clean                     // 清除源代码目录中的编译结果

## 统计代码行数
    ls * | xargs wc -l
    find . -name '*.php' | xargs wc -l

## sed命令
* 打印
  - sed '/match/p' filename  // 默认打印所有内容
  - sed -n '/match/p' filename //  **取消默认打印**，只输出匹配的行
  - sed -n '/.*ing/p' filename
  - sed -n '2,5p' filename  //打印2到5行
  - sed '/[Aa]bc/p' filename // 正则匹配
* 修改
  - sed -i 直接修改文件内容
  - sed -i 's/gb2312/utf8/g' filename // 替换一个文件
  - sed -i 's/gb2312/utf8/g' `grep gb2312 -rl ./` // 批量替换
  - sed -i 's/<[^>]*>//g' filename // 去除html标签
  - sed '/test/a\ add to end' filename
  - sed '/test/i\ add to front' filename
  - sed '/test/c\ change' filename
  - sed 'y/1234/abcd/' filename
  - sed '1,10y/1234/abcd/' filename
  - sed 's/^/#/g' filename  // 每行最前面加内容
  - sed 's/$/#/g' filename  // 每行最后面加内容
  - sed 's/\</#/g' filename // 每个单词前面加内容
  - sed 's/\>/#/g' filename // 每个单词前面加内容
  - sed 's/s/S/2' filename  // 替换每行第二个s
  - sed 's/s/S/3g' filename // 替换每个第3个以后的s
  - sed 's/(cat), (dog)/\1, \2/g' filename
  - sed '1 i xxx' filename  // 第一行前插入
  - sed '/fish/a xxx' filename // 匹配到fish追加
  - sed '2,$d' filename
* 删除
  - sed '2d' filename
  - sed '2,$d' filename
  - sed '$d' filename // 删除最后一行
  - sed '/##/'d filename // 删除有##注释的行
  - sed '/abc/,/def/d' filename // 删除包含'abc'到'def'的行之间内容
  - sed '/abc/,10d' filename // 删除包含'abc'到第10行内容
* 多点编辑
  - sed -e '1,5d' -e 's/abc/012/' filename
  - sed -n '/test/w file' filename 
  - sed '2r c.txt' filename // 在filename第二行添加c.txt内容
  - sed '/^##/w file' filename // 把filename中匹配##开头的行保存在file
  - sed 's#10#100#g' filename // 紧跟着s命令的都被认为是分隔符，这里'#'替代了'/'
  
## awk

* 打印
  - awk '{print $1, $4}' f  // $1...$n表示第几列，$0表示整行
  - awk '{printf "%8s, %18s", $1, $4}' n // 格式化输出
* 内建变量
  - $0 当前记录 $1~$n 第n列
  - FS 字段分隔符 默认是空格或Tab
  - NR行号
  - NF字段个数
  - RS, FS, FILENAME
* 过滤
  - awk '$3==0 && $6 == "LISTEN"' n  // !=, >, <, >=, <=
  - awk '$3 >0 {print $0}' n
  - awk '$3==0 && $6=="LISTEN" || NR==1 ' n  // 打印出表头
  - awk '{printf NR, $1}' n // 打印行号
  - awk 'BEGIN{FS=":"} {print $1, $3}' /etc/passwd  // 指定分隔符  或者 awk -F:
* 匹配
  - awk '$6 ~ /FIN/ || NR==1 {print NR, $4, $5} OFS="\t" n
  - awk '$6 !~ /FIN/TIME/ || NR==1 {print NR, $4, $5} n
* 统计
  - ls -l *.php | awk '{sum+=$5} END {print sum}'   // 文件大小总和

 


### ifconfig
* ifconfig
* 启动关闭网卡
  - ifconfig eth0 up
  - ifconfig eth0 down
* 修改mac地址
  - ifconfig eth0 hw ether 00:AA:BB:CC:DD:EE
* 配置IP地址
  - ifconfig eth0 192.168.120.56 
  - ifconfig eth0 192.168.120.56 netmask 255.255.255.0 broadcast 192.168.120.255
* 启用和关闭ARP协议
  - ifconfig eth0 arp
  - ifconfig eth0 -arp
* 注意：ifconfig配置网卡，重启后配置消失。如果要保存，需要个性配置文件

## 其它
    cut -f1 -d" " ~/.bash_history | sort | uniq -c | sort -nr | head -n 30 看看你最常用的命令是什么
    回到刚才的目录
    cd - 
    找出10个大文件
    du -sh * | sort -rh | head
    设置文件密码
    vim -x
    生成.bak方式
    cp filename{,.bak}
    who -b   # Time of last system boot
    printenv # 打印所有环境变量
    创建虚拟文件
    -- dd if=/dev/zero of={filename} bs=1M count=10 // bs(block size)指定块大小，缺省单位为Byte
    -- du -h {filename}

## 网上资料
[linux](http://www.linux.org/ "linux")

[curl网站开发指南](http://www.ruanyifeng.com/blog/2011/09/curl.html "curl网站开发指南")

[linux command](http://linux.chinaitlab.com/special/linuxcom/ "linux command")

[标准编译安装](http://i.linuxtoy.org/docs/guide/ch18s02.html "标准编译安装")

[commandlinefu](http://beta.commandlinefu.cn/ "commandlineful")
