mysql
============================

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
    * 注意int(11),在int类型中参数11为最大显示宽度，不影响取值范围
    -- 复制表结构
    create table [newtablename] like [oldtablename];
    -- 复制所有或部分字段，或者改名
    create table [newtablename] as ( select * from [oldtablename] );


## use
    select version(), current_date, now(), user();
    select * from tablename;
    select * from tablename where a = 1;
    select * from tablename order by columns desc;
    select * from tablename where filed1 like 'a%';
    select * from tablename where filed1 like '___';       ---- 三个长度
    select * from tablename where filed1 regexp '^.{5}$';  ---- 正则
    select * from tablename where MATCH(column) AGAINST (keyword);
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

## 权限相关
    use mysql;
    SELECT User, Password, Host from user;
    GRANT ALL ON database.* TO 'username'@'host' IDENTIFIED BY 'password';
    SHOW GRANTS;
    SHOW GRANTS FOR 'username'@'host';
    REVOKE ALL ON database.* FROM 'username'@'host';
    RENAME USER 'username'@'host' TO 'newusername'@'host';
    SET PASSWORD FOR 'username'@'host' = PASSWORD('XX');
    DROP USER 'username'@'host';
    FLUSH PRIVILEGES;
    =====
    HOST值的意义：
    % 匹配所有的主机
    localhost 不会被解析成IP地址，直接通过UNIX Socket连接
    127.0.0.1 通过TCP/IP访问，并且只能在本地访问
    ::1 兼容支持ipv6，表示同ipv4的127.0.0.1
    =====
    权限分配相关表：user=>db=>tables_priv=>columns_priv

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
    show engines;        -- 查看引擎信息，从ver5.5开始，默认为InnoDB
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
* utf8_general_ci 与 utf8_unicode_ci的区别
  - ci是case insensitive，大小写不敏感,a与A一样；cs区分大小写；bin是二进制，大小写敏感，可存二进制内容
  - utf8_unicode_ci的最主要的特色是支持扩展，即当把一个字母看作与其它字母组合相等时。例如，在德语和一些其它语言中‘ß'等于‘ss'。
  - utf8_unicode_ci和utf8_general_ci对中、英文来说没有实质的差别。
  - utf8_general_ci校对速度快，但准确度稍差。utf8_unicode_ci准确度高，但校对速度稍慢。
  - 如果你的应用有德语、法语或者俄语，请一定使用utf8_unicode_ci

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

## 索引
    ALTER TABLE {tablename} ADD INDEX {indexname} ('{column}');
    SHOW INDEX FROM {tablename}
    DROP INDEX {indexname} ON {tablename}

## Explain
* id - 查询序列号，值越大优先执行级越高；id相同则按顺序执行
* select_type
    - SIMPLE 不使用union及子查询
    - PRIMARY
    - UNION
    - DEPENDENT UNION
    - SUBQUERY
    - DEPENDENT SUBQUERY
    - DERIVED
    - UNCACHEABLE SUBQUER
    - UNCACHEABLE UNION
* table
* type 非常重要，显示连接使用的类型，按最优到最差
    - system 表仅有一行(=系统表)
    - const
    - eq_ref
    - ref 可能查到多条记录
    - ref_or_null 如同ref，但会在二次查询中找出null条目
    - index_merge 使用了索引合并优化
    - unique_subquery
    - index_subquery
    - range 只检索给定范围的行，使用索引选择行
    - index 全表扫描，按索引次序，避免了排序，开销仍然很大
    - all 全表扫描
* possible_keys 指出能在表中使用哪些索引有助于查询
* key 
* key_len
* ref 显示索引的哪一列被使用了
* rows 返回请求数据的行数
* extra 
    - Using filesort 使用外部索引排序，可能在内存或者磁盘上，效率受重大影响
    - Using temporary  对查询结果排序时使用临时表，常见于order by和group by，效果受重大影响


### 全文索引
* 特点
  - 性能比like强很多
  - 仅InnoDB和MyISAM引擎支持（InnoDB在mysql5.6.4开始支持）
  - 对汉语日语支持不好（没有空格之类的单词定界符）
  - 最小长度（InnoDB默认3个字符，MyISAM默认4个字符）
* 语法
  - MATCH(col1,col2,…) AGAINST (expr[search_modifier])
  - search_modifier
    - IN NATURAL LANGUAGEMODE （默认）
    - IN NATURAL LANGUAGE MODE WITH QUERY EXPANSION
    - IN BOOLEAN MODE 
      - ( '+MySQL -YourSQL' IN BOOLEAN MODE ) -排除单词      
      - ('MySQL YourSQL' IN BOOLEAN MODE); 空格后单词是可选的
      - ">" 增加相关性贡献 "<" 减少相关性贡献 "()"分组 
      - "~" 相关性为负  
    - WITH QUERY EXPANSION
      - 查询扩展：执行两次搜索
         - 第一次用给定短语搜索
         - 第二次用第一次返回结果中相关性高的词搜索
      - 会显著地引入噪声
* 相关选项：
  - 控制最大最小词长：修改后需要重建索引（drop index && add index 或者 repair table {tablename} QUICK）
    - innodb: innodb_ft_min_token_size, innodb_ft_max_token_size
    - MyISAM: ft_min_word_len, ft_max_word_len
    - 上面内容需要修改配置文件，在[mysqld]之下
  - 相关库表
    - Information_schema
      - INNODB_SYS_INDEXES：提供了InnoDB索引的状态信息
      - INNODB_FT_CONFIG：显示一个InnoDB表的FULLTEXT索引及其相关处理的元数据
      - INNODB_FT_INDEX_TABLE：转化后的索引信息用于处理基于InnoDB表FULLTEXT索引的文本搜索
      - INNODB_FT_INDEX_CACHE
      - INNODB_FT_DEFAULT_STOPWORD
      - INNODB_FT_DELETED
      - INNODB_FT_BEING_DELETED
      


## InnoDB和MyISAM
    MyISAM优点:
        是MySQL中默认的存储引擎，ver5.5之前
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

## 主从复制
* 保持主从版本一致
* 修改master配置文件
  - vim /etc/my.cnf
  - [mysqld]
  - log-bin=mysql-bin // 必须启用二进制日志
  - server-id=1       // 必须设置唯一ID
* 修改slave配置文件
  - vim /etc/my.cnf
  - [mysqld]
  - log-bin=mysql-bin
  - server-id=2
* 重启mysql
  - /etc/init.d/mysqld restart
* 在master上创建帐号
  - GRANT REPLICATION SLAVE ON *.* TO 'SYNC'@'%' IDENTIFIED BY 'PASSWORD'
* 查询master状态
  - show master status;
  - File:mysql-bin.000001
  - Position: 308
* 配置slave
  - change master to master_host='{ip}',master_user='SYNC',master_password='PASSWORD',master_log_file='mysql-bin.00001',master_log_pos=308;
  - start slave;
  - show slave status\G; // 检查状态
  - Slave_IO_Running： Yes  // 为No则有错误，可定时检测此参数发送警报
  - Slave_SQL_Running: Yes  // 为No则有错误，可定时检测此参数发送警报
  

## 锁
* 锁是计算机协调多个进程或线程并发访问某一资源的机制
* 不同的存储引擎支持不同的锁机制
  - MyISAM和MEMORY存储引擎采用的是表级锁（table-level locking）
  - BDB存储引擎采用的是页面锁（page-level locking），但也支持表级锁
  - InnoDB存储引擎既支持行级锁（row-level locking），也支持表级锁，但默认情况下是采用行级锁
* 不同级别锁对比
  - 表级锁：开销小，加锁快；不会出现死锁；锁定粒度大，发生锁冲突的概率最高,并发度最低
  - 行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低,并发度也最高
  - 页面锁：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般
* 查询锁
  - show status like 'table%';
  - Table_locks_waited 值较高，则表级锁争用严重
  - show atatus like 'innodb_row_lock%'
  - InnoDB_row_lock_waits, InnoDB_row_lock_time_avg较高，则锁争用严重
* 命令
  - lock table {tablename} {locktype}
  - locktype四种
    - read         // 只能读，不可写
    - read local   // 可以insert
    - write        // 当前用户可读写，其它用户完全阻止
    - low priority write  // 
  - unlock table
* MyISAM锁调度
  - 那么，一个进程请求某个 MyISAM表的读锁，同时另一个进程也请求同一表的写锁，MySQL如何处理呢？答案是写进程先获得锁。不仅如此，即使读请求先到锁等待队列，写请求后到，写锁也会插到读锁请求之前！这是因为MySQL认为写请求一般比读请求要重要。这也正是MyISAM表不太适合于有大量更新操作和查询操作应用的原因，因为，大量的更新操作会造成查询操作很难获得读锁，从而可能永远阻塞。这种情况有时可能会变得非常糟糕！幸好我们可以通过一些设置来调节MyISAM 的调度行为。 
  - max_write_lock_count
   
  

## 分库分表
    垂直切分：关系紧密的表放在一个库里
    水平切分：适合单表数据多的情况。将数据按规则切分到多个server上。
    混和切分：可无限扩充的server阵列
    切分策略：先垂直再水平


## 报错问题
* The used SELECT statements have a different number of columns
  - 在使用union查询时，多个查询语句的查询字段不一致
* 找不到mysql.sock，使用find / 也不行
  - /etc/init.d/mysql stop
  - mysql -uroot -p
  - 报错:Can not connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock'
    找到文件所在位置
* 编码格式为latin1，设置为utf8后，重新登录又恢复
  - 解决方法是修改配置:
  - vim /etc/mysql/my.cnf
    - 在client节点下添加：  default-character-set=utf8
    - 在mysqld节点下添加：   character-set-server=utf8 ；    collation-server=utf8_general_ci
    保存后重启mysql
* This version of MySQL doesn’t yet support ‘LIMIT & IN/ALL/ANY/SOME subquery’ 
  - select * from table where id in (select id from table limit 10); // 这样就会报错
  - 解决方法：再套一层 select * from table where id in (select t.id from (select * from table limit 10)as t)

## 数据库范式
    第一范式(1NF)：数据库的每个字段都只能存放单一值，而且每笔记录都要能利用一个惟一的主键来加以识别
    第二范式(2NF)：数据表里的所有数据都要和该数据表的主键有完全依赖关系；如果有哪些数据只和主键的一部份有关的话，就得把它们独立出来变成另一个数据表。
    第三范式(3NF)：用来检验是否所有非键属性都只和候选键有相关性，也就是说所有非键属性互相之间应该是无关的。

### 安装完MySQL后必须调整的10项配置
    * 一次只改变一个设置！这是测试改变是否有效的唯一方法。
    * 运行时可使用set global。需要永久生效，在配置文件里改动。
    * 改动配置后无法重启？确认使用了正确的单位。
    基本配置
    1. innodb_buffer_pool_size: 缓冲池是数据和索引缓存的地方：这个值越大越好，这能保证你在大多数的读取操作时使用的是内存而不是硬盘。
    2. innodb_log_file_size:
    3. max_connections: 解决“Too many connections”错误
    InnoDB配置
    4. innodb_file_per_table:
    5. innodb_flush_log_at_trx_commit:
    6. innodb_flush_method:
    7. innodb_log_buffer_size:
    其它设置
    query_cache_size:
    log_bin:
    expire_logs_days:
    skip_name_resolve: 跳过DNS查找

### Query Cache
    缓存客户端提交给MySQL的select(仅此类型)语句及结果集。
    注意：此缓存是mysql的缓存，在存储引擎之上。引擎、表、日志等都有各自的缓存。
    缓存原理：
        select语句通过一定的hash计算，存放在hash表里。结果集存放在内存中。
    失效机制：
        任何一个表或者数据、索引结构发生变化时，与此表关联的cache失效，并释放内存。
        所以数据变化频繁的sql就不要cache了。
    相关参数：
        SHOW VARIABLES LIKE '%query_cache%';
    确认query cache使用情况，命中率：
        show status like 'Qcache%';


### 数据库设计学习笔记 (http://www.imooc.com/view/117)
    根据业务需要，结合DBMS，构造数据存储模型。实现有效的存储及高效地访问。
    设计步骤：
        需求分析：
            数据是什么？
            数据属性？ 时效性？过期清理或归档：永久保存；数据过大？分库分表：单库单表
            存储特点？ 永久存储|过期清理
        逻辑设计： ER图逻辑建模
            设计范式
        物理设计： DBMS
            选择合适的数据库
            建库建表及命名规范
            字段类型： 优先考虑数字类型；其次是日期和二进制；最后是字符类型；相同级别选择占用空间小的
                字符串处理比数字慢
            反范式化设计： 为了性能和读取效率违反范式
            避免使用外键约束： 降低效率、高并发变慢
            避免使用触发器：  降低效率、可能出现异常、业务逻辑复杂
            严禁使用预留字段：
        维护优化：
            维护数据字典
                select a.table_name, b.TABLE_COMMENT, a.COLUMN_NAME, a.COLUMN_TYPE, a.COLUMN_COMMENT
                FROM information_schema.COLUMNS a
                JOIN information_schema.TABLES b
                ON a.table_schema = b.table_schema
                AND a.table_name = b.table_name
                WHERE a.table_name = '[tablename]';
            维护索引
            维护表结构
            表拆分

### 常用SQL
    /*
     * 查询一个表所有字段名
     */
    SELECT COLUMN_NAME
    FROM information_schema.COLUMNS
    WHERE TABLE_SCHEMA = '{databasename}'
    AND TABLE_NAME = '{tablename}'


## 网上资料
[InnoDB 还是 MyISAM?](http://www.cnblogs.com/villion/archive/2009/07/09/1893762.html "InnoDB 还是 MyISAM?")

[通过show status优化mysql](http://lxneng.iteye.com/blog/451985 "通过show status优化mysql")

[画图解释SQL联合语句](http://blog.jobbole.com/40443/ "画图解释SQL联合语句")

[手册](http://dev.mysql.com/doc/refman/5.1/zh/index.html "手册")

[数据库规范化](http://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A7%84%E8%8C%83%E5%8C%96 "数据库规范化")

[数据库分库分表(sharding)系列](http://blog.csdn.net/column/details/sharding.html "数据库分库分表(sharding)系列")

[安装完 MySQL 后必须调整的 10 项配置](http://www.oschina.net/translate/10-mysql-settings-to-tune-after-installation "安装完 MySQL 后必须调整的 10 项配置")

[query cache](http://blog.csdn.net/qiuyepiaoling/article/details/6004611 "query cache")

[mysql用户管理和权限设置](http://www.cnblogs.com/fslnet/p/3143344.html "mysql用户管理和权限设置")

[MySQL全文检索](http://blog.csdn.net/bbirdsky/article/details/45368897)

[Mysql中的排序规则utf8_unicode_ci、utf8_general_ci的区别总结](http://www.jb51.net/article/48775.htm)

[MySQL锁](http://blog.csdn.net/xifeijian/article/details/20313977)


