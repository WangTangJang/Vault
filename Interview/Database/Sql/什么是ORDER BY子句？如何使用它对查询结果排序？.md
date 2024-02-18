`ORDER BY`子句用于对查询结果进行排序。通过使用`ORDER BY`，你可以指定一个或多个列，以确定返回的数据集的顺序。在默认情况下，查询结果是无序的，但通过使用`ORDER BY`，你可以按升序（ASC）或降序（DESC）的方式对结果进行排序。

### 语法：
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...;
```

- `column1, column2, ...`: 要检索的列。
- `table_name`: 要从中检索数据的表。
- `ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...`: 指定用于排序的列和排序顺序。默认是升序（ASC），如果需要降序，则使用`DESC`。

### 示例：
假设有一个名为 `employees` 的表，包含 `employee_id`、`first_name` 和 `salary` 列，你可以使用`ORDER BY`对查询结果进行排序：

```sql
-- 按照 first_name 列升序排序
SELECT employee_id, first_name, salary
FROM employees
ORDER BY first_name ASC;
```

```sql
-- 按照 salary 列降序排序
SELECT employee_id, first_name, salary
FROM employees
ORDER BY salary DESC;
```

你还可以使用多个列进行排序。在这种情况下，首先按第一个列排序，然后在相同值的情况下按第二个列排序：

```sql
-- 按照 salary 列降序排序，然后按照 first_name 列升序排序
SELECT employee_id, first_name, salary
FROM employees
ORDER BY salary DESC, first_name ASC;
```

使用`ORDER BY`子句时，确保在查询中的`SELECT`和`FROM`子句之后使用，并在`WHERE`和`LIMIT`之前使用。这样可以确保在应用筛选条件和限制行数之前对结果进行正确的排序。