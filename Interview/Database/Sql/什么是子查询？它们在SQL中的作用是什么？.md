子查询是在 SQL 查询语句内部嵌套的一个查询，它被包含在主查询的条件或表达式中。子查询可以在其他查询中使用，并且返回的结果集可以用于进一步的过滤、比较或计算。

### 子查询的语法：
在主查询的 WHERE 子句、FROM 子句、SELECT 子句或 HAVING 子句中嵌套一个完整的查询。

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name operator (SELECT column_name FROM another_table WHERE condition);
```

### 子查询的作用：
1. **过滤数据：** 子查询可以用于过滤主查询的结果。例如，你可以使用子查询在 WHERE 子句中查找符合某个条件的行。

    ```sql
    SELECT emp_name, salary
    FROM employees
    WHERE salary > (SELECT AVG(salary) FROM employees);
    ```

2. **比较操作：** 子查询可以与比较运算符一起使用，用于比较主查询中的值与子查询的结果。

    ```sql
    SELECT emp_name
    FROM employees
    WHERE emp_id = (SELECT manager_id FROM departments WHERE dept_name = 'HR');
    ```

3. **IN 和 NOT IN 操作：** 子查询可以用于检查一个值是否存在于另一个查询的结果集中。

    ```sql
    SELECT emp_name
    FROM employees
    WHERE emp_id IN (SELECT emp_id FROM sales_team);
    ```

4. **EXISTS 和 NOT EXISTS 操作：** 子查询可以用于检查是否存在符合条件的记录。

    ```sql
    SELECT emp_name
    FROM employees e
    WHERE EXISTS (SELECT 1 FROM sales_team s WHERE s.emp_id = e.emp_id);
    ```

5. **在 SELECT 子句中使用：** 子查询可以在 SELECT 子句中返回一个标量值，用于计算或显示。

    ```sql
    SELECT emp_name, (SELECT MAX(salary) FROM employees) AS max_salary
    FROM employees;
    ```

使用子查询可以使 SQL 查询更加灵活，能够处理更复杂的条件和逻辑。然而，需要注意使用子查询可能会对性能产生影响，因此在编写复杂查询时要谨慎使用。