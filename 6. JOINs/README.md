<div align="center">


# 🔗📊 JOIN
**JOIN** is used to combine data from two or more tables based on a related column. 🔗📊

</div>

## Q 1. What is a JOIN?

A `JOIN` is used to **combine rows from two or more tables** based on a related column.

**Key Points**

* Connects data from multiple tables
* Usually uses **Primary Key and Foreign Key**
* Common in relational databases

**Example**

```sql id="qg4yhm"
SELECT employees.name, departments.department_name
FROM employees
JOIN departments
ON employees.department_id = departments.id;
```

This query combines **employees** and **departments** tables to show each employee's department.

---
## Q 2. Types of joins in SQL.

Joins are used to **combine data from multiple tables**. The main types of joins are:

**1️⃣ INNER JOIN**
Returns only the rows that have matching values in both tables.

```sql
SELECT *
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

**2️⃣ LEFT JOIN (LEFT OUTER JOIN)**
Returns all rows from the left table and matching rows from the right table.

```sql
SELECT *
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id;
```

**3️⃣ RIGHT JOIN (RIGHT OUTER JOIN)**
Returns all rows from the right table and matching rows from the left table.

```sql
SELECT *
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

**4️⃣ FULL JOIN (FULL OUTER JOIN)**
Returns all rows from both tables, matching where possible.

**5️⃣ CROSS JOIN**
Returns the **Cartesian product** (every row from one table combined with every row from another table).

---
## Q 3. Difference between INNER JOIN and LEFT JOIN.

Both are used to combine data from two tables, but they return different results.

**INNER JOIN**

* Returns only rows that have **matching values in both tables**

Example

```sql id="vqu3g2"
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.id;
```

**LEFT JOIN**

* Returns **all rows from the left table**
* Returns matching rows from the right table
* If no match exists, the result is **NULL**

Example

```sql id="fcd6ec"
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.id;
```

**Quick Difference**

* `INNER JOIN` → Only matching records
* `LEFT JOIN` → All records from left table + matching from right table

---
## Q 4. When will LEFT JOIN return NULL?

`LEFT JOIN` returns `NULL` when there is **no matching record in the right table**.

**Key Points**

* All rows from the **left table** are returned
* If no match is found in the **right table**, its columns show `NULL`

**Example**

```sql id="l82c4h"
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.id;
```

If an employee has **no matching department**, `department_name` will appear as **NULL**.

---
## Q 5. Difference between LEFT JOIN and RIGHT JOIN.

Both joins return matching rows from two tables, but they differ in **which table's unmatched rows are kept**.

**LEFT JOIN**

* Returns **all rows from the left table**
* Matching rows from the right table
* If no match → right table columns show `NULL`

Example

```sql id="o6u5p8"
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.id;
```

**RIGHT JOIN**

* Returns **all rows from the right table**
* Matching rows from the left table
* If no match → left table columns show `NULL`

Example

```sql id="h1h3g2"
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.id;
```

**Quick Difference**

* `LEFT JOIN` → keeps all rows from **left table**
* `RIGHT JOIN` → keeps all rows from **right table**

---
## Q 6. What is a FULL OUTER JOIN?

A **FULL OUTER JOIN** returns **all rows from both tables**.
If there is a match, the rows are combined. If there is no match, the missing side returns **NULL**.

**Key Points**

* Includes **matching rows from both tables**
* Includes **unmatched rows from left and right tables**
* Unmatched columns appear as **NULL**

**Example**

```sql id="t9g3x1"
SELECT e.name, d.department_name
FROM employees e
FULL OUTER JOIN departments d
ON e.department_id = d.id;
```

This query returns **all employees and all departments**, even if there is no match between them.

---
## Q 7. What is a SELF JOIN? Give example.

A **SELF JOIN** is a join where a table is joined **with itself**.
It is useful when rows in the same table are related.

**Key Points**

* Uses the same table twice with **different aliases**
* Common for **hierarchical data** (like employee–manager relationships)

**Example**

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.id;
```

This query shows **each employee with their manager** from the same table.

---
## Q 8. What is a CROSS JOIN?

A **CROSS JOIN** returns the **Cartesian product** of two tables.
Each row from the first table is combined with **every row from the second table**.

**Key Points**

* No matching condition is required
* Total rows = rows in table1 × rows in table2
* Rarely used in large datasets

**Example**

```sql id="1deyr0"
SELECT *
FROM colors
CROSS JOIN sizes;
```

If `colors` has **3 rows** and `sizes` has **4 rows**, the result will have **12 rows**.

---
## Q 9. Difference between JOIN and SUBQUERY.

Both are used to retrieve data from multiple tables, but they work differently.

**JOIN**

* Combines rows from **two or more tables**
* Usually faster for large datasets

Example

```sql id="s8q3m4"
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.id;
```

**SUBQUERY**

* A query written **inside another query**
* Often used in `WHERE` or `SELECT`

Example

```sql id="9m7v2p"
SELECT name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE department_name = 'Sales'
);
```

**Quick Difference**

* `JOIN` → combines tables directly
* `SUBQUERY` → query inside another query

---
## Q 10. Fetch employee name and department name from two tables.

Use a `JOIN` to combine data from the **employees** and **departments** tables.

**Query**

```sql id="h7s2qa"
SELECT e.name AS employee_name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.id;
```

**Key Points**

* `JOIN` connects two tables
* `e` and `d` are table aliases
* `department_id` links employees with their departments.
