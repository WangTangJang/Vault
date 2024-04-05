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

#表中添加列
ALTER TABLE your_table_name ADD COLUMN new_column_name data_type;
#修改列
ALTER TABLE your_table_name MODIFY COLUMN column_name new_data_type;
#删除列
ALTER TABLE your_table_name DROP COLUMN column_name;

#更新数据
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;

# 删库
drop database 库名;

# 删表
drop table 表名；

# 清表
delete from 表名;

# 显示表中数据
select * from 表名;

# 查看当前密码验证插件和安全策略
SHOW VARIABLES LIKE 'validate_password%';

# 创建用户, %表示允许用户从任何主机连接
CREATE USER 'Username'@'%' IDENTIFIED BY 'PassWord';

# 赋予用户权限
GRANT ALL PRIVILEGES ON your_database.* TO 'your_username'@'%';

GRANT SUPER ON *.* TO 'your_user'@'your_host';


# 退出
exit;
```