<div align="center">


# 📊🔎 GROUP BY & HAVING
**GROUP BY & HAVING** are used to group rows with similar values and filter aggregated results. 📊🔎

</div>

## Q 1. What is GROUP BY?

`GROUP BY` is used to **group rows with the same values** in a column and apply aggregate functions like `COUNT()`, `SUM()`, or `AVG()`.

**Key Points**

* Groups data based on a column
* Commonly used with aggregate functions
* Helps create summarized reports

**Example**

```sql id="e9o7r4"
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

This query returns the **number of employees in each department**.

---
## Q 2. What happens if you miss GROUP BY in aggregate query?

If you use aggregate functions with other columns **without `GROUP BY`**, the query will usually return an **error**.

**Key Points**

* SQL cannot determine how to group the non-aggregated columns
* All non-aggregated columns must be included in `GROUP BY`

**Incorrect Example**

```sql
SELECT department, COUNT(*)
FROM employees;
```

This will cause an error because `department` is not grouped.

**Correct Example**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```
---
## Q 3. Can we use GROUP BY on multiple columns?

Yes, `GROUP BY` can be used with **multiple columns** to group data based on the combination of those columns.

**Key Points**

* Groups rows using **multiple column values**
* Common in reports and analysis
* Often used with aggregate functions

**Example**

```sql
SELECT department, job_title, COUNT(*) AS total_employees
FROM employees
GROUP BY department, job_title;
```

This query returns the **number of employees for each job title within each department**.

---
## Q 4. Difference between GROUP BY and DISTINCT.

Both are used to remove duplicate values, but their purpose is different.

**DISTINCT**

* Returns **unique values** from a column
* Does not perform aggregation

Example

```sql
SELECT DISTINCT department
FROM employees;
```

**GROUP BY**

* Groups rows to perform **aggregate calculations**
* Used with functions like `COUNT()`, `SUM()`, `AVG()`

Example

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```

**Quick Difference**

* `DISTINCT` → removes duplicate values
* `GROUP BY` → groups data for aggregation

---
## Q 5. Find total sales by year and month.

Use date functions with `GROUP BY` to summarize sales by year and month.

**Query (MySQL)**

```sql id="t0l3nm"
SELECT YEAR(order_date) AS year,
       MONTH(order_date) AS month,
       SUM(sales_amount) AS total_sales
FROM sales
GROUP BY YEAR(order_date), MONTH(order_date);
```

**Key Points**

* `YEAR()` extracts the year from the date
* `MONTH()` extracts the month
* `SUM()` calculates total sales for each month.

---
## Q 6. Show departments having more than 10 employees.

Use `GROUP BY` with `HAVING` to filter departments based on the number of employees.

**Query**

```sql
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

**Key Points**

* `GROUP BY department` groups employees by department
* `COUNT(*)` counts employees in each department
* `HAVING` filters departments with more than 10 employees.

---
## Q 7. Can HAVING be used without GROUP BY?

Yes, `HAVING` can be used without `GROUP BY`, but it is typically used with **aggregate functions**.

**Key Points**

* `HAVING` filters aggregated results
* If `GROUP BY` is not used, the whole table is treated as **one group**

**Example**

```sql
SELECT COUNT(*) AS total_employees
FROM employees
HAVING COUNT(*) > 100;
```

This query returns the result only if the **total number of employees is greater than 100**.

---
## Q 8. GROUP BY execution order.

In SQL, queries are executed in a **logical order**, not the order they are written.

**Execution Order**

1. `FROM` → Selects the table
2. `WHERE` → Filters rows
3. `GROUP BY` → Groups rows
4. `HAVING` → Filters grouped results
5. `SELECT` → Chooses columns
6. `ORDER BY` → Sorts the final result

**Example**

```sql
SELECT department, COUNT(*)
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING COUNT(*) > 5
ORDER BY department;
```

**Key Point**

* `GROUP BY` happens **after WHERE but before HAVING**.

---
## Q 9. Find highest salary in each department.

Use the `MAX()` aggregate function with `GROUP BY` to find the highest salary in every department.

**Query**

```sql
SELECT department, MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

**Key Points**

* `MAX(salary)` returns the highest salary
* `GROUP BY department` groups employees by department
* Result shows the **top salary in each department**.

---
## Q 10. Common mistakes with GROUP BY.

These are common errors beginners make when using `GROUP BY`.

**1️⃣ Missing columns in GROUP BY**
All non-aggregated columns in `SELECT` must appear in `GROUP BY`.

Incorrect

```sql
SELECT department, salary
FROM employees
GROUP BY department;
```

**2️⃣ Using aggregate functions in WHERE**

Incorrect

```sql
SELECT department, COUNT(*)
FROM employees
WHERE COUNT(*) > 5
GROUP BY department;
```

Correct

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**3️⃣ Forgetting GROUP BY with aggregates**

Incorrect

```sql
SELECT department, COUNT(*)
FROM employees;
```

**Key Tip**

* Use `GROUP BY` when combining **aggregate functions with other columns**.
