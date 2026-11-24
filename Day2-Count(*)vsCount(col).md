
# SQL: Difference Between COUNT(*) and COUNT(column_name)

## Question
Does `COUNT(*)` give the same result as `COUNT(column_name)` in SQL?

## Answer
No, they do not always return the same result.

- `COUNT(*)` counts **all rows** in a table, including rows containing NULL values.
- `COUNT(column_name)` counts only the **non-NULL values** in the specified column.

Both return the same result only when the specified column does not contain any NULL values.

---

## Example

Consider the following `employees` table:

| id | name |
|---|---|
| 1 | Hameed |
| 2 | Rahul |
| 3 | NULL |
| 4 | Priya |
| 5 | NULL |

There are 5 rows in total, but only 3 non-NULL values in the `name` column.

### SQL Query

```sql
SELECT
    COUNT(*) AS total_rows,
    COUNT(name) AS total_names
FROM employees;
```

### Output

| total_rows | total_names |
|---|---|
| 5 | 3 |

### Explanation

**1. COUNT(*)**

```sql
SELECT COUNT(*) FROM employees;
```

Result: `5`

It counts every row in the table, regardless of whether the columns contain NULL values.

**2. COUNT(name)**

```sql
SELECT COUNT(name) FROM employees;
```

Result: `3`

It counts only the rows where the `name` column has a non-NULL value.

---

## When Do Both Return the Same Result?

Consider a table where the specified column contains no NULL values.

| id | name |
|---|---|
| 1 | Hameed |
| 2 | Rahul |
| 3 | Priya |
| 4 | Tarun |

Query:

```sql
SELECT
    COUNT(*) AS total_rows,
    COUNT(name) AS total_names
FROM employees;
```

Output:

| total_rows | total_names |
|---|---|
| 4 | 4 |

In this case, both return the same result because there are no NULL values in the `name` column.

---

## Key Differences

| Feature | COUNT(*) | COUNT(column_name) |
|---|---|---|
| Counts all rows | Yes | No |
| Counts rows with NULL values | Yes | No |
| Ignores NULL values | No | Yes |
| Returns same result when column has no NULLs | Yes | Yes |

## Important Takeaway

- `COUNT(*)` = Total number of rows.
- `COUNT(column_name)` = Total number of non-NULL values in that column.
- If a column contains NULL values, the results can differ.
- If a column has no NULL values, both return the same result.

**Interview Tip:** Whenever you are asked about the difference between `COUNT(*)` and `COUNT(column_name)`, remember that `COUNT(*)` counts rows, whereas `COUNT(column_name)` counts non-NULL values.
