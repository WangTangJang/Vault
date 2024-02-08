
```mysql
# 连接数据库
mysql -uroot -pmysql;

# 展示数据库
show databases;

# 使用数据库
use 库名;

# 展示库中表
show tables;

# 展示表的状态
show table status like 'Table_Name';

# 展示表结构
describe 表名;

# 建立数据库
create database 库名;

#建表
create table 表名 (字段设定列表)；

# 删库
drop database 库名;

# 删表
drop table 表名；

# 清表
delete from 表名;

# 显示表中数据
select * from 表名;

# 退出
exit;
```