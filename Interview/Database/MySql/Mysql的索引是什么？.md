在MySQL中，索引（Index）是一种数据结构，用于提高数据库表的查询性能。索引类似于书籍的目录，通过索引，数据库系统可以更快速地定位并访问数据。默认的索引类型是[[B树]]。
## 创建索引：
```sql
CREATE INDEX index_name ON table_name (column1, column2, ...);
```
索引在数据库中的使用通常是由DBMS自动处理的，而不需要手动干预。当执行查询时，数据库系统会根据查询条件和表的索引情况来**自动选择**是否使用索引以及选择哪些索引。
## 删除索引：
```sql
DROP INDEX index_name ON table_name;

-- 删除表的主键索引
ALTER TABLE table_name DROP PRIMARY KEY;
```
## 展示索引：
```sql
SHOW INDEX FROM table_name;
```
### 输出内容：
![[20240208230509.png]]
1. **Table：** 表示索引所属的表。
2. **Non_unique：** 表示索引是否是==唯一索引==。0 表示唯一索引，1 表示非唯一索引。
3. **Key_name：** 表示索引的名称。
4. **Seq_in_index：** 表示索引中的==列序号==，对于==复合索引==，表示列在索引中的位置。
5. **Column_name：** 表示索引包含的列名。
6. **Collation：** 表示索引的排序规则（升序为 `A`，降序为 `D`）。
7. **Cardinality：** 表示索引的基数，即不同值的数量。
8. **Sub_part：** 对于部分索引，表示索引的长度；对于整体索引，为 `NULL`。
9. **Packed：** 显示索引的==压缩方式==，对于不压缩的索引，为 `NULL`。
10. **Null：** 表示索引中的列是否可以包含 `NULL` 值。
11. **Index_type：** 表示索引的类型，这里是 `BTREE`，表示B树索引。
12. **Comment：** 注释，此处为空。