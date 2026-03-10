# Q 1. What are window functions?

Window functions perform **calculations across a set of rows related to the current row** without grouping the result.

**Key Points**

* Operate on a **window of rows**
* Do not reduce the number of rows like `GROUP BY`
* Often used for ranking and running totals

**Common Window Functions**

* `ROW_NUMBER()`
* `RANK()`
* `DENSE_RANK()`

**Example**

```sql id="f8d2zs"
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

This query ranks employees based on **salary**.

---
# Q 2. Difference between GROUP BY and WINDOW functions.
### Difference between `GROUP BY` and Window Functions

Both are used for calculations on data, but they behave differently.

**GROUP BY**

* Groups rows and returns **one result per group**
* Reduces the number of rows

Example

```sql id="5f29qk"
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

**Window Functions**

* Perform calculations **without grouping rows**
* Original rows remain in the result

Example

```sql id="7ap7dp"
SELECT name, department,
       AVG(salary) OVER (PARTITION BY department) AS avg_salary
FROM employees;
```

**Quick Difference**

* `GROUP BY` → aggregates and reduces rows
* Window functions → calculate values while keeping all rows intact

---
# Q 3. What is OVER() clause?
### What is `OVER()` clause?

The `OVER()` clause is used with **window functions** to define the **set of rows (window)** on which the function operates.

**Key Points**

* Used with functions like `RANK()`, `ROW_NUMBER()`, `SUM()`
* Defines how rows are **partitioned or ordered**
* Does not group rows like `GROUP BY`

**Example**

```sql id="z1c6nf"
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

This query ranks employees based on **salary without grouping the rows**.

---
# Q 4. Difference between ROW_NUMBER, RANK, DENSE_RANK.

These are **window functions** used to assign rankings to rows.

**ROW_NUMBER()**

* Assigns a **unique number** to each row
* No duplicate ranks

Example

```sql id="gn3uxv"
SELECT name, salary,
       ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_num
FROM employees;
```

**RANK()**

* Gives the **same rank to equal values**
* Skips the next rank

Example

```sql id="abdcsp"
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS rank_num
FROM employees;
```

**DENSE_RANK()**

* Gives the **same rank to equal values**
* Does **not skip ranks**

Example

```sql id="d7hpu9"
SELECT name, salary,
       DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank
FROM employees;
```

**Quick Difference**

* `ROW_NUMBER()` → unique rank for each row
* `RANK()` → same rank but **skips numbers**
* `DENSE_RANK()` → same rank **without skipping numbers**

---
# Q 5. Find running total of sales.

A running total shows the **cumulative sum of sales** as rows progress.

**Query**

```sql id="k1m4ts"
SELECT order_date,
       sales_amount,
       SUM(sales_amount) OVER (ORDER BY order_date) AS running_total
FROM sales;
```

**Key Points**

* `SUM()` calculates the total
* `OVER(ORDER BY order_date)` defines the order for cumulative calculation
* Each row shows the **total sales up to that point**.

---
# Q 6. Find highest salary per department using window function.

Use a window function with `PARTITION BY` to calculate the highest salary within each department.

**Query**

```sql id="d6z0s8"
SELECT name, department, salary,
       MAX(salary) OVER (PARTITION BY department) AS highest_salary
FROM employees;
```

**Key Points**

* `PARTITION BY department` creates a window for each department
* `MAX(salary)` finds the highest salary within that department
* Each row shows the employee salary and the department’s highest salary.

---
# Q 7. What is PARTITION BY?

`PARTITION BY` is used in **window functions** to divide rows into groups (partitions) so calculations are performed **within each group**.

**Key Points**

* Similar to `GROUP BY` but **does not reduce rows**
* Used with window functions like `RANK()`, `SUM()`, `AVG()`
* Calculates results **separately for each partition**

**Example**

```sql id="gk2w9t"
SELECT name, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_in_dept
FROM employees;
```

This query ranks employees **within each department**.

---
# Q 8. Can we use window functions in WHERE?

No, window functions **cannot be used directly in the `WHERE` clause**.

**Reason**

* `WHERE` is executed **before window functions**
* Window functions are calculated **after SELECT**

**Solution**

Use a **subquery or CTE**.

**Example**

```sql
SELECT *
FROM (
    SELECT name, salary,
           RANK() OVER (ORDER BY salary DESC) AS salary_rank
    FROM employees
) t
WHERE salary_rank <= 5;
```

**Key Point**

* Window functions must be used **in SELECT or ORDER BY**, not in `WHERE`.

---
# Q 9. Use case of window functions in Power BI.

Window functions are used in SQL to **prepare data before loading it into Power BI** for analysis and reporting.

**Common Use Cases**

**1️⃣ Ranking Data**
Find top products, customers, or employees.

```sql
SELECT product_name, sales,
       RANK() OVER (ORDER BY sales DESC) AS sales_rank
FROM sales;
```

**2️⃣ Running Totals**
Calculate cumulative sales for trend analysis.

```sql
SELECT order_date, sales,
       SUM(sales) OVER (ORDER BY order_date) AS running_total
FROM sales;
```

**3️⃣ Department-wise Analysis**
Compare values within groups.

```sql
SELECT department, salary,
       AVG(salary) OVER (PARTITION BY department) AS avg_salary
FROM employees;
```

**Key Point**

Using window functions in SQL helps **reduce Power BI calculations and improves performance**.

---
# Q 10. Why window functions are faster?

Window functions are often faster because they **perform calculations without grouping or reducing rows**.

**Key Points**

* Avoid multiple joins or subqueries
* Process data in a **single query pass**
* Use efficient internal database algorithms
* Keep the original rows while calculating results

**Example**

```sql
SELECT name, salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

**Tip**

Window functions are commonly used for **ranking, running totals, and comparisons** in analytical queries.
