# Q 1. Write a query to fetch all records from a table.

To retrieve all rows and columns from a table, we use the `SELECT` statement with `*`.

**Query**

```sql
SELECT *
FROM employees;
```

**Explanation**

* `SELECT *` → selects all columns
* `FROM employees` → specifies the table to fetch data from

This query returns **every record stored in the table**.

# Q 2. How do you select distinct values from a column?

Use the `DISTINCT` keyword to return **unique values** from a column.

**Query**

```sql
SELECT DISTINCT department
FROM employees;
```

**Key Points**

* Removes duplicate values
* Returns only unique records
* Can be used with one or multiple columns

**Example (Multiple Columns)**

```sql
SELECT DISTINCT department, job_title
FROM employees;
```

# Q 3. Difference between = and IN.

Both are used to filter data in SQL, but they work differently.

**`=` Operator**

* Compares a column with **one specific value**

Example

```sql
SELECT *
FROM employees
WHERE department = 'Sales';
```

**`IN` Operator**

* Checks if a value matches **any value in a list**

Example

```sql
SELECT *
FROM employees
WHERE department IN ('Sales', 'HR', 'IT');
```

**Quick Difference**

* `=` → Single value comparison
* `IN` → Multiple possible values in one condition

# Q 4. What is BETWEEN and when would you use it?

`BETWEEN` is used to filter values **within a specific range**.
It includes both the starting and ending values.

**When to use**

* Filtering numbers within a range
* Filtering dates
* Salary or price ranges

**Example**

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 60000;
```

**Key Points**

* Inclusive range (includes both values)
* Works with numbers, dates, and text
* Makes range conditions easier to read

# Q 5. How does LIKE work? Explain % and _.

`LIKE` is used in SQL to search for a **pattern in text data**.

**Wildcards**

* `%` → Matches **any number of characters**
* `_` → Matches **exactly one character**

**Examples**

Search names starting with "A"

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Search names where the second letter is "a"

```sql
SELECT *
FROM employees
WHERE name LIKE '_a%';
```

**Key Points**

* Used with `WHERE` clause
* Helpful for pattern matching
* Common in search and filtering text data 🔎

# Q 16. Write a query to fetch employees whose salary is between 30,000 and 60,000.

Use the `BETWEEN` operator to filter values within a range.

**Query**

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 60000;
```

**Key Points**

* `BETWEEN` includes both 30000 and 60000
* Useful for filtering ranges like salary, dates, or prices.

# Q 7. How do you filter records with NULL values?

In SQL, `NULL` values cannot be checked using `=`.
We use `IS NULL` or `IS NOT NULL`.

**Example (Find NULL values)**

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

**Example (Exclude NULL values)**

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

**Key Points**

* Use `IS NULL` to find missing values
* Use `IS NOT NULL` to filter valid data
* `=` does not work with `NULL` values.

# Q 8. What happens if you use WHERE on an aggregate function?

You **cannot use aggregate functions** like `COUNT()`, `SUM()`, `AVG()` directly in the `WHERE` clause.
This will cause an **error** because `WHERE` filters rows **before aggregation**.

**Incorrect Example**

```sql
SELECT department, COUNT(*)
FROM employees
WHERE COUNT(*) > 5
GROUP BY department;
```

**Correct Way (Use HAVING)**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Key Point**

* `WHERE` → filters rows
* `HAVING` → filters aggregated results.

# Q 9. Fetch top 5 highest-paid employees.

To get the highest-paid employees, sort salaries in **descending order** and limit the results.

**MySQL / PostgreSQL**

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

**SQL Server**

```sql
SELECT TOP 5 *
FROM employees
ORDER BY salary DESC;
```

**Key Points**

* `ORDER BY salary DESC` → highest salaries first
* `LIMIT / TOP` → restricts results to top 5 rows.

# Q 10. Difference between AND and OR with examples.

Both are logical operators used in the `WHERE` clause to filter data.

**AND**

* Returns results only when **all conditions are true**

Example

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
AND salary > 50000;
```

**OR**

* Returns results when **any one condition is true**

Example

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
OR department = 'HR';
```

**Quick Difference**

* `AND` → All conditions must be true
* `OR` → At least one condition must be true
