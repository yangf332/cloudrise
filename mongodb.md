MongoDB
====================

## 特点
* 面向文档（对象），类似于行
* 集合（表）
* 自带JavaScript shell
* 每个文档有一个唯一的特殊键"_id"

## 文档
* 键值对
* 有序
* 区分大小写和类型

## 命令
    help
    use [dbname]
    db
    db.version();
    db.[dbname].insert({...});
    db.[dbname].find({...});
    db.[dbname].findOne({...});
    db.[dbname].update({...}, {...});
    db.[dbname].remove({...});
    db.[dbname].[function_name];  // 显示方法源码

## 相关书籍
* 《MongoDB权威指南》

## 相关资料
[MongoDB工具](http://www.robomongo.org/)