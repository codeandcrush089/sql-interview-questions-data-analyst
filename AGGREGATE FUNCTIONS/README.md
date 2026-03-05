# Q 1. What are aggregate functions in SQL?

Aggregate functions perform **calculations on multiple rows of data** and return a **single summarized value**.

**Common Aggregate Functions**

* `COUNT()` → counts rows
* `SUM()` → total of values
* `AVG()` → average value
* `MAX()` → highest value
* `MIN()` → lowest value

**Example**

```sql
SELECT AVG(salary)
FROM employees;
```

This query returns the **average salary of all employees**.

# Q 2. Difference between COUNT(*) and COUNT(column).

Both are used to count rows, but they treat **NULL values differently**.

**COUNT(*)**

* Counts **all rows** in a table
* Includes rows with `NULL` values

Example

```sql
SELECT COUNT(*)
FROM employees;
```

**COUNT(column)**

* Counts **only non-NULL values** in a specific column

Example

```sql
SELECT COUNT(manager_id)
FROM employees;
```

**Quick Difference**

* `COUNT(*)` → counts every row
* `COUNT(column)` → ignores `NULL` values in that column

# Q 3. What does SUM() return if all values are NULL?

If all values in a column are `NULL`, the `SUM()` function returns **NULL**.

**Key Points**

* `SUM()` ignores `NULL` values during calculation
* If **no non-NULL values exist**, the result is `NULL`

**Example**

```sql
SELECT SUM(bonus)
FROM employees;
```

If every `bonus` value is `NULL`, the result will be **NULL**.

**Tip**

You can replace `NULL` with 0 using `COALESCE`.

```sql
SELECT COALESCE(SUM(bonus), 0)
FROM employees;
```

# Q 4. Difference between AVG() and SUM()/COUNT().

Both are used to calculate the **average value**, but they are written differently.

**AVG()**

* Built-in function to calculate the average
* Automatically ignores `NULL` values

Example

```sql
SELECT AVG(salary)
FROM employees;
```

**SUM()/COUNT()**

* Manual way to calculate the average
* Divides total sum by the number of values

Example

```sql
SELECT SUM(salary) / COUNT(salary)
FROM employees;
```

**Key Point**

* `AVG()` is simpler and commonly used
* `SUM()/COUNT()` gives the same result but is written manually


# Q 5. Write a query to calculate total sales per customer.

Use the `SUM()` function with `GROUP BY` to calculate total sales for each customer.

**Query**

```sql
SELECT customer_id, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY customer_id;
```

**Key Points**

* `SUM()` calculates total sales
* `GROUP BY` groups results for each customer
* Returns total sales per customer.


# Q 6. Find average salary department-wise.

Use `AVG()` with `GROUP BY` to calculate the average salary for each department.

**Query**

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Key Points**

* `AVG()` calculates the average salary
* `GROUP BY department` groups employees by department
* Returns the average salary for each department.

# Q 7. Why can’t we use aggregate functions in WHERE?

Aggregate functions cannot be used in `WHERE` because `WHERE` filters rows **before aggregation happens**.

**Key Points**

* `WHERE` works on **individual rows**
* Aggregate functions like `COUNT()`, `SUM()`, `AVG()` are calculated **after grouping**
* To filter aggregated results, use `HAVING`

**Incorrect Example**

```sql
SELECT department, COUNT(*)
FROM employees
WHERE COUNT(*) > 5
GROUP BY department;
```

**Correct Example**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

# Q 8. What is the use of HAVING?

`HAVING` is used to **filter grouped data after aggregation**.

**Key Points**

* Used with `GROUP BY`
* Works with aggregate functions like `COUNT()`, `SUM()`, `AVG()`
* Filters results **after grouping**

**Example**

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Explanation**

* Groups employees by department
* Shows only departments with **more than 5 employees**.

# Q 9. HAVING vs WHERE with example.

Both are used to filter data, but they work at different stages of a query.

**WHERE**

* Filters rows **before grouping**
* Cannot use aggregate functions

Example

```sql id="3ldg0b"
SELECT *
FROM employees
WHERE salary > 50000;
```

**HAVING**

* Filters data **after GROUP BY**
* Works with aggregate functions

Example

```sql id="h7ezcd"
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Quick Difference**

* `WHERE` → filters individual rows
* `HAVING` → filters grouped/aggregated results


# Q 10. Count number of orders per customer.

Use `COUNT()` with `GROUP BY` to calculate the number of orders for each customer.

**Query**

```sql
SELECT customer_id, COUNT(order_id) AS total_orders
FROM orders
GROUP BY customer_id;
```

**Key Points**

* `COUNT(order_id)` counts the orders
* `GROUP BY customer_id` groups orders by each customer
* Returns total orders per customer.
