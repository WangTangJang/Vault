SQL（Structured Query Language）是一种用于管理和处理关系型数据库的标准化语言。它允许用户查询、插入、更新、删除和管理数据库中的数据。
以下是一些常见的 SQL 基本命令：
## SELECT - 查询数据
   `SELECT` 语句用于从一个或多个表中检索数据。
   ```sql
   SELECT column1, column2, ...
   FROM table_name
   WHERE condition;
   ```
## INSERT - 插入数据
   `INSERT` 语句用于将新记录插入到表中。
   ```sql
   INSERT INTO table_name (column1, column2, ...)
   VALUES (value1, value2, ...);
   ```
## UPDATE - 更新数据
   `UPDATE` 语句用于更新表中的记录。
   ```sql
   UPDATE table_name
   SET column1 = value1, column2 = value2, ...
   WHERE condition;
   ```

## DELETE - 删除数据
   `DELETE` 语句用于从表中删除记录。
   ```sql
   DELETE FROM table_name
   WHERE condition;
   ```
## CREATE - 创建表
   `CREATE` 语句用于创建新表。
   ```sql
   CREATE TABLE table_name (
      column1 datatype,
      column2 datatype,
      ...
   );
   ```
## ALTER - 修改表结构
   `ALTER` 语句用于修改现有表的结构，如添加、修改或删除列。
   ```sql
   ALTER TABLE table_name
   ADD column_name datatype;
   ```
## DROP - 删除表
   `DROP` 语句用于删除整个表。
   ```sql
   DROP TABLE table_name;
   ```
## GRANT - 授权
   `GRANT` 语句用于赋予用户或用户组数据库操作的权限。
   ```sql
   GRANT permission
   ON object_name
   TO user_name;
   ```
## REVOKE - 撤销权限
   `REVOKE` 语句用于撤销用户或用户组的数据库操作权限。
   ```sql
   REVOKE permission
   ON object_name
   FROM user_name;
   ```
### 10. **WHERE - 过滤条件**
`WHERE` 子句用于过滤从表中检索的数据，指定检索的条件。
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
