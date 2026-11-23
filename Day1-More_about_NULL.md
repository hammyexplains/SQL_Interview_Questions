# SQL NULL Comparison – TRUE, FALSE, or UNKNOWN?

## 1. What happens when NULL = NULL in SQL?

In SQL, when we compare `NULL` with another `NULL` using the equality operator (`=`), the result is **UNKNOWN**, not TRUE or FALSE.

```sql
SELECT
    CASE
        WHEN NULL = NULL THEN 'TRUE'
        ELSE 'FALSE'
    END AS result;
```

**Output:**

| result |
|---|
| FALSE |

**Why does it return FALSE here?**

Although `NULL = NULL` evaluates to UNKNOWN, the `WHEN` condition in a `CASE` statement executes only when the condition is TRUE.

Since UNKNOWN is not TRUE, SQL executes the `ELSE` block and returns FALSE.

> Important: The actual result of `NULL = NULL` is UNKNOWN. The CASE expression above displays FALSE because of its ELSE condition.

## 2. Understanding NULL in SQL

`NULL` represents a missing, unknown, or unavailable value.

It is not the same as:
- `0` (Zero)
- `''` (Empty string)
- `'NULL'` (String containing the word NULL)

## 3. SQL NULL Comparison Results

| SQL Expression | Result |
|---|---|
| `NULL = NULL` | UNKNOWN |
| `NULL != NULL` | UNKNOWN |
| `NULL = 10` | UNKNOWN |
| `10 = 10` | TRUE |
| `10 = 20` | FALSE |
| `NULL > 10` | UNKNOWN |

## 4. How to Check NULL Values?

We should never use `= NULL` or `!= NULL` to check for NULL values.

Instead, SQL provides two special operators:

### IS NULL

```sql
SELECT NULL IS NULL;
```

Result: `TRUE`

### IS NOT NULL

```sql
SELECT NULL IS NOT NULL;
```

Result: `FALSE`

## 5. Understanding Three-Valued Logic

Unlike normal comparisons that produce TRUE or FALSE, SQL supports three logical outcomes:

1. **TRUE** – The condition is satisfied.
2. **FALSE** – The condition is not satisfied.
3. **UNKNOWN** – The condition cannot be evaluated because of NULL.

## 6. Practical Example Using a Table

Consider an employee table:

| id | name |
|---|---|
| 1 | Alice |
| 2 | Bob |
| 3 | NULL |
| NULL | NULL |

### Query 1: Using = NULL

```sql
SELECT *
FROM employees
WHERE name = NULL;
```

**Result:** Zero rows.

Reason: `name = NULL` evaluates to UNKNOWN, and the WHERE clause returns only rows where the condition is TRUE.

### Query 2: Using IS NULL

```sql
SELECT *
FROM employees
WHERE name IS NULL;
```

**Result:** Two rows.

| id | name |
|---|---|
| 3 | NULL |
| NULL | NULL |

Reason: `IS NULL` correctly identifies NULL values.

## 7. Important SQL Interview Takeaways

- `NULL = NULL` returns UNKNOWN, not TRUE.
- `NULL != NULL` also returns UNKNOWN.
- Use `IS NULL` to check for NULL values.
- Use `IS NOT NULL` to check for non-NULL values.
- SQL uses TRUE, FALSE, and UNKNOWN (Three-Valued Logic).
- The WHERE clause selects only rows for which the condition evaluates to TRUE.

**Remember:** NULL means unknown. Therefore, SQL cannot assume that one NULL value is equal to another NULL value.
