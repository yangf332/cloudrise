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
        PRIMARY KEY (id),
    ) ENGINE=InnoDB  DEFAULT CHARSET=utf8


## use
    select version(), current_date, now(), user();
    select * from tablename;
    select * from tablename where a = 1;
    select * from tablename order by columns desc;
    select * from tablename where filed1 like 'a%';
    select * from tablename where filed1 like '___';       ---- 三个长度
    select * from tablename where filed1 regexp '^.{5}$';  ---- 正则
    update tablename set field1 = 1 where field2 = 2;
    update tablename set field1 = substring(field1, 3);
    update tablename set field1 = concat('pre', field1);
    replace into tablename(field1, field2) values (1, 2);

## insert 
    insert into tablename(field1, field2) values (1, 2);
    insert into table2(fileld1, filed2, ...) select value1, value2, ... from table1;
    select value1, value2, ... into table2 from table1; 

## union、union all
    select * from tb union select * from tb1;      -- 会筛选掉重复的记录
    select * from tb union all select * from tb1;  -- 仅仅简单合并，会返回重复记录

## modify
    alter table tablename rename tableothername;
    alter table tablename modify a char(20);
    alter table tablename add addfield timestamp;
    alter table tablename drop column b;
    alter table tablename auto_increment = 100;

## delete
    -- 可以选择删除；返回删除记录数；
    delete from tablename;
    -- 只能全部删除；返回0；自增字段恢复成初始值；快；
    truncate tablename;

## 时间戳
    select current_timestamp, current_timestamp();

## 用户变量
    set @a = 1, @b = 2;
    select @a, @b;    

## 其它
    select lpad('100015', 8, 0);
    select rpad('100015', 8, 0);
    select LAST_INSERT_ID(); ---- 查询auto_increment的最新值

## 导出导入数据库
    mysqldump -uuser -p databasename > /tmp/databasename.sql
    source /tmp/databasename.sql
    load data local infile '/path/file.txt' into table TABLENAME
    导出excel
    select * into outfile '/path/filename.xls' from TABLENAME

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

## 查看和设置编码格式
    show variables like 'character%';
    mysql> show variables like 'character%';
    +--------------------------+--------------------------------------------------------+
    | Variable_name            | Value                                                  |
    +--------------------------+--------------------------------------------------------+
    | character_set_client     | utf8                                                   |
    | character_set_connection | utf8                                                   |
    | character_set_database   | latin1                                                 |
    | character_set_filesystem | binary                                                 |
    | character_set_results    | utf8                                                   |
    | character_set_server     | latin1                                                 |
    | character_set_system     | utf8                                                   |
    设置：
    set character_set_client=utf8;
    set character_set_connection=utf8;
    set character_set_database=utf8;
    set character_set_results=utf8;
    set character_set_server=utf8;
    或者：
    set names utf8;

## History
    cat ~/.mysql_history
    show variables like 'log_bin';  -- 看是否启用了日志
    show master status;
    show variables like 'expire_logs_days';
    set global expire_logs_days = 20 ;

## 外键
    InnoDB引擎类型的表支持外键约束
    外键列必须建立索引（MysQL 4.1.2以后版本会自动生成）
    外键关系的两个表的列必须数据类型相似
    使两张表关联，保证数据的一致性和实现一些级联操作
    外键的定义语法：
    [CONSTRAINT symbol] FOREIGN KEY [id] (index_col_name, ...)
    REFERENCES tbl_name (index_col_name, ...)
    [ON DELETE {RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT}]
    [ON UPDATE {RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT}]

## InnoDB和MyISAM
    MyISAM优点:
        是MySQL中默认的存储引擎
        设计的目的是使用唯一的键在读取操作中快速检查。适合95%的操作为读操作
        支持全文索引
        磁盘空间占用较少
    MyISAM缺点:
        表级别锁定，如果写操作超过5%，速度变慢
        不支持事务，没有回滚能力
        持久性有问题，崩溃恢复操作慢
    InnoDB优点：
        支持事务，回滚。崩溃不会导致数据损坏
        行级锁定，并发写入同一表的不同行不会被序列化
        支持全部ACID功能的版本控制
        支持多种联机备份策略
        提高了并发能力
        具有提交，回滚和崩溃恢复的能力。处理大数据量性能好。
    InnoDB缺点：
        没有全文索引
        占用更多磁盘空间
        简单查询速度低于MyISAM
    MyISAM的索引和数据是分开的，并且索引是有压缩的，内存使用率对应提高了不少。而Innodb是索引和数据是紧密捆绑的，没有使用压缩从而会造成Innodb比MyISAM体积庞大不小。
    InnoDB 中不保存表的具体行数。执行select count(*) from table时，InnoDB要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可。DELETE FROM table时，InnoDB不会重新建立表，而是一行一行的删除。
    MyISAM的insert性能高；InnoDB针对索引的update性能高

## 分库分表
    垂直切分：关系紧密的表放在一个库里
    水平切分：适合单表数据多的情况。将数据按规则切分到多个server上。
    混和切分：可无限扩充的server阵列
    切分策略：先垂直再水平


## 报错问题
    1.  The used SELECT statements have a different number of columns
    在使用union查询时，多个查询语句的查询字段不一致
    2. 找不到mysql.sock，使用find / 也不行
    /etc/init.d/mysql stop
    mysql -uroot -p
    报错:Can not connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock'
    找到文件所在位置
    3. 编码格式为latin1，设置为utf8后，重新登录又恢复
    解决方法是修改配置:
    vim /etc/mysql/my.cnf
    在client节点下添加：  default-character-set=utf8 
    在mysqld节点下添加：   character-set-server=utf8 ；  collation-server=utf8_general_ci
    保存后重启mysql

## 数据库范式
    第一范式(1NF)：数据库的每个字段都只能存放单一值，而且每笔记录都要能利用一个惟一的主键来加以识别
    第二范式(2NF)：数据表里的所有数据都要和该数据表的主键有完全依赖关系；如果有哪些数据只和主键的一部份有关的话，就得把它们独立出来变成另一个数据表。
    第三范式(3NF)：用来检验是否所有非键属性都只和候选键有相关性，也就是说所有非键属性互相之间应该是无关的。

## 网上资料
[InnoDB 还是 MyISAM?](http://www.cnblogs.com/villion/archive/2009/07/09/1893762.html "InnoDB 还是 MyISAM?")

[通过show status优化mysql](http://lxneng.iteye.com/blog/451985 "通过show status优化mysql")

[画图解释SQL联合语句](http://blog.jobbole.com/40443/ "画图解释SQL联合语句")

[手册](http://dev.mysql.com/doc/refman/5.1/zh/index.html "手册")

[数据库规范化](http://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A7%84%E8%8C%83%E5%8C%96 "数据库规范化")

[数据库分库分表(sharding)系列](http://blog.csdn.net/column/details/sharding.html "数据库分库分表(sharding)系列")
