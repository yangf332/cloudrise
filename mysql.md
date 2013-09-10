
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

## show
    show variables;      -- 查看配置信息
    show global status;  -- 查看MySQL服务器运行的各种状态值
    show variables like 'max_connections';  
    show global status like 'max_used_connections';  
    show variables like 'key_buffer_size';  
    +-----------------+----------+  
    | Variable_name   | Value    |  
    +-----------------+----------+  
    | key_buffer_size | 67108864 |  
    +-----------------+----------+  
    show global status like 'key_read%'; 
    +-------------------+----------+  
    | Variable_name     | Value    |  
    +-------------------+----------+  
    | Key_read_requests | 25629497 |  
    | Key_reads         | 66071    |  
    +-------------------+----------+  
    key_cache_miss_rate ＝ Key_reads / Key_read_requests * 100% =0.27% 
    show variables like 'thread_cache_size';
    show global status like 'qcache%';
    show global status like 'sort%';
    show global status like 'open_files';
    show variables like 'open_files_limit';
    show global status like 'table_locks%';

## 表扫描情况
    show global status like 'handler_read%';  
    +-----------------------+-----------+  
    | Variable_name         | Value     |  
    +-----------------------+-----------+  
    | Handler_read_first    | 108763    |  
    | Handler_read_key      | 92813521  |  
    | Handler_read_next     | 486650793 |  
    | Handler_read_prev     | 688726    |  
    | Handler_read_rnd      | 9321362   |  
    | Handler_read_rnd_next | 153086384 |  
    +-----------------------+-----------+  
    show global status like 'com_select';  
    +---------------+---------+  
    | Variable_name | Value   |  
    +---------------+---------+  
    | Com_select    | 2693147 |  
    +---------------+---------+  
    表扫描率 ＝ Handler_read_rnd_next / Com_select 
    如果表扫描率超过4000，说明进行了太多表扫描，很有可能索引没有建好


## 启用慢查询
    show variables like '%slow%';
    show global status like '%slow%';  
    set global  slow_query_log  = on;
    +---------------------+---------------------------------+
    | Variable_name       | Value                           |
    +---------------------+---------------------------------+
    | log_slow_queries    | ON                              |
    | slow_launch_time    | 2                               |
    | slow_query_log      | ON                              |
    | slow_query_log_file | /var/run/mysqld/mysqld-slow.log |
    +---------------------+---------------------------------+

## 报错问题
    1.  The used SELECT statements have a different number of columns
    在使用union查询时，多个查询语句的查询字段不一致

## 网上资料
[通过show status优化mysql](http://lxneng.iteye.com/blog/451985 "通过show status优化mysql")

[画图解释SQL联合语句](http://blog.jobbole.com/40443/ "画图解释SQL联合语句")

