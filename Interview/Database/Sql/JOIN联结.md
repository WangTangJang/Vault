在数据库中，JOIN 是用于将两个或多个表中的行**联结**起来的操作。JOIN 通过**指定连接条件**，将满足条件的行合并到一起，形成一个来自多个表的结果集。
## INNER JOIN：
![image.png](http://img.briar.ink/20240414205126.png)
INNER JOIN 用于返回两个表中满足连接条件的行。如果两个表中的某行在连接条件下匹配，那么这一行将包含在结果集中。
```sql
SELECT * 
FROM table1
INNER JOIN table2 ON table1.column = table2.column;
```

内联结存在隐式形式：没有`JOIN`关键字，条件使用`WHERE`指定
## ## FULL JOIN (FULL OUTER JOIN)：
![image.png](http://img.briar.ink/20240414204559.png)
FULL JOIN 返回左表和右表中的所有行，如果没有匹配的行，将用 NULL 值填充。
```sql
SELECT * 
FROM table1
FULL JOIN table2 ON table1.column = table2.column;
```

## LEFT JOIN (LEFT OUTER JOIN)：
![image.png](http://img.briar.ink/20240414205229.png)
LEFT JOIN 返回左表中的**所有行**，以及右表中满足连接条件的行。如果右表中没有匹配的行，那么结果集中右表的列将包含 NULL 值。
```sql
SELECT * 
FROM table1
LEFT JOIN table2 ON table1.column = table2.column;
```
## RIGHT JOIN (RIGHT OUTER JOIN)：
RIGHT JOIN 返回右表中的所有行，以及左表中满足连接条件的行。如果左表中没有匹配的行，那么结果集中左表的列将包含 NULL 值。
```sql
SELECT * 
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

