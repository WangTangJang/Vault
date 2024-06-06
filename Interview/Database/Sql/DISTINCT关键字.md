在 MySQL 中,`DISTINCT` 关键字可以用于对查询结果中的重复行**进行去重**。它的使用方法如下:

1. 对整个结果集去重:
```sql
SELECT DISTINCT column1, column2, ... 
FROM table_name;
```
这将返回表中每个独特的行,去掉重复的记录。

2. 对部分列去重:
```sql
SELECT column1, DISTINCT column2, column3
FROM table_name;
```
这将只对 `column2` 进行去重,返回的结果集中 `column1` 和 `column3` 可能会包含重复值。

3. 组合使用 `DISTINCT` 和 `GROUP BY`:
```sql
SELECT column1, COUNT(DISTINCT column2) 
FROM table_name
GROUP BY column1;
```
这将先对 `column2` 进行去重,然后再统计每个 `column1` 对应的不同 `column2` 的数量。

4. 与聚合函数一起使用:
```sql
SELECT MAX(DISTINCT column1), MIN(DISTINCT column2)
FROM table_name;
```
这将分别求 `column1` 和 `column2` 的最大值和最小值,只考虑不重复的值。