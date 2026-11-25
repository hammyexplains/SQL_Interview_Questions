
# SQL: Difference Between WHERE and HAVING

## Question
What is the difference between `WHERE` and `HAVING` in SQL?

## Answer

Both `WHERE` and `HAVING` are used to filter data in SQL.

However, they are used at different stages of query execution.

- `WHERE` filters individual rows before grouping.
- `HAVING` filters groups after the `GROUP BY` operation.

---

## 1. WHERE Clause

The `WHERE` clause is used to filter individual rows based on a condition.

It is executed before the `GROUP BY` operation.

### Example

Consider the following `employees` table:

| employee_id | name | department | salary |
|---|---|---|---|
| 1 | Hameed | IT | 50000 |
| 2 | Rahul | IT | 60000 |
| 3 | Priya | HR | 40000 |
| 4 | Tarun | HR | 45000 |
| 5 | Arjun | IT | 70000 |

### SQL Query

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### Output

| employee_id | name | department | salary |
|---|---|---|---|
| 2 | Rahul | IT | 60000 |
| 5 | Arjun | IT | 70000 |

### Explanation

The `WHERE` clause checks each employee's salary and returns only the rows where the salary is greater than 50000.

---

## 2. HAVING Clause

The `HAVING` clause is used to filter groups created by the `GROUP BY` operation.

It is commonly used with aggregate functions such as:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`

### Example

Find departments whose average salary is greater than 50000.

### SQL Query

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Output

| department | average_salary |
|---|---|
| IT | 60000 |

### Explanation

First, SQL groups employees by department.

Then it calculates the average salary for each department.

Finally, the `HAVING` clause filters the groups and returns only departments whose average salary is greater than 50000.

---

## 3. Using WHERE and HAVING Together

You can use both clauses in the same query.

### Question

Find departments whose average salary is greater than 50000, considering only employees whose salary is greater than 45000.

### SQL Query

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE salary > 45000
GROUP BY department
HAVING AVG(salary) > 50000;
```

### Output

| department | average_salary |
|---|---|
| IT | 60000 |

### Explanation

**Step 1: WHERE**

```sql
WHERE salary > 45000
```

Filters individual employees and removes employees whose salary is 45000 or less.

**Step 2: GROUP BY**

```sql
GROUP BY department
```

Groups the remaining employees by department.

**Step 3: HAVING**

```sql
HAVING AVG(salary) > 50000
```

Filters the departments based on their average salary.

---

## 4. Difference Between WHERE and HAVING

| Feature | WHERE | HAVING |
|---|---|---|
| Filters | Individual rows | Groups |
| Execution | Before GROUP BY | After GROUP BY |
| Used with aggregate functions | Cannot directly filter using aggregate functions | Can filter using aggregate functions |
| Can be used without GROUP BY | Yes | Yes, depending on the SQL query |
| Example | `WHERE salary > 50000` | `HAVING AVG(salary) > 50000` |

---

## 5. Important Interview Question

### Can we use HAVING without GROUP BY?

Yes.

Example:

```sql
SELECT COUNT(*) AS total_employees
FROM employees
HAVING COUNT(*) > 3;
```

Output:

| total_employees |
|---|
| 5 |

Here, the entire table is treated as one group, and the `HAVING` clause filters that group.

### Can we use WHERE with aggregate functions?

Generally, no.

This query is invalid:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE AVG(salary) > 50000
GROUP BY department;
```

Because `WHERE` filters rows before the aggregate calculation.

Use `HAVING` instead:

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

## Key Takeaway

Remember this simple rule:

**WHERE filters rows, whereas HAVING filters groups.**

- Use `WHERE` to filter records before grouping.
- Use `HAVING` to filter aggregated results after grouping.
- Use both when you need to filter rows first and then filter the resulting groups.
