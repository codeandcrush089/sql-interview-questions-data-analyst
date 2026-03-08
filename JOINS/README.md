# Q 1. What is a JOIN?

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

# Q 2. Types of joins in SQL.
### Types of Joins in SQL

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

# Q 3. Difference between INNER JOIN and LEFT JOIN.

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

# Q 4. When will LEFT JOIN return NULL?

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

