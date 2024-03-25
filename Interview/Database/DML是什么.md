DML，即数据操纵语言（Data Manipulation Language），是SQL（Structured Query Language，结构化查询语言）中用于管理和操作数据库中数据的一套命令。DML提供了一系列的语句，允许用户插入、查询、更新和删除数据库中的数据。以下是DML的主要组成部分：

1. **SELECT**：用于从数据库表中检索数据。这是最常用的DML语句，可以简单查询单列或多列数据，也可以使用复杂的条件和排序。

   示例：
   ```sql
   SELECT column1, column2 FROM table_name;
   ```

2. **INSERT INTO**：用于向数据库表中添加新的数据行。你可以为表中的每一行指定列的值。

   示例：
   ```sql
   INSERT INTO table_name (column1, column2) VALUES (value1, value2);
   ```

3. **UPDATE**：用于修改数据库表中的现有数据。可以使用条件来指定哪些行应该被更新。

   示例：
   ```sql
   UPDATE table_name SET column1 = value1 WHERE condition;
   ```

4. **DELETE**：用于从数据库表中删除数据。同样，可以使用条件来指定哪些行应该被删除。

   示例：
   ```sql
   DELETE FROM table_name WHERE condition;
   ```

DML语句是数据库用户与数据库交互的基础，无论是数据分析师、开发人员还是数据库管理员，都需要熟练掌握这些语句来有效地处理数据。DML与数据定义语言（DDL）相对，DDL用于定义、修改和删除数据库和表结构，如CREATE、ALTER和DROP等命令。而**DML专注于数据本身的操作，不涉及数据库结构的改变。**