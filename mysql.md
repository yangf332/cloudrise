
mysql
============================
记录mysql安装学习的点滴

## install
    yum install mysql
    yum install mysql-server
    yum install mysql-devel

## 启动
    /etc/init.d/mysqld start
    chkconfig -add mysqld

## 登录
    mysql -uusername -ppassword -Pport

## show
    show databases; use databasename;
    show tables;
    show columns from tablename;
    show create table talename;

## create
    create database databasename;
    create table tablename (
        id int(11) NOT NULL AUTO_INCREMENT,
        email varchar(255) NOT NULL,
        time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPATE CURRENT_TIMESTAMP,
        PRIMARY KEY ('id'),
    ) ENGINE=InnoDB  DEFAULT CHARSET=utf8


## use
    select * from tablename;
    select * from tablename where a = 1;
    select * from tablename order by columns desc;
    insert into tablename(field1, field2) values (1, 2);
    update tablename set field1 = 1 where field2 = 2;
    replace into tablename(field1, field2) values (1, 2);

## modify
    alter table tablename rename tableothername;
    alter table tablename modify a char(20);
    alter table tablename add addfield timestamp;
    alter table tablename drop column b;

## 时间戳
    select current_timestamp, current_timestamp();
    
## 导出导入数据库
    mysqldump -uuser -p databasename > /tmp/databasename.sql
    source /tmp/databasename.sql

## 修改密码
    SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpwd');


## 启用慢查询
    set global  slow_query_log  = on;
    +---------------------+---------------------------------+
    | Variable_name       | Value                           |
    +---------------------+---------------------------------+
    | log_slow_queries    | ON                              |
    | slow_launch_time    | 2                               |
    | slow_query_log      | ON                              |
    | slow_query_log_file | /var/run/mysqld/mysqld-slow.log |
    +---------------------+---------------------------------+

## 网上资料
[画图解释SQL联合语句](http://http://blog.jobbole.com/40443/ "画图解释SQL联合语句")

