# Q 1. What is a subquery?

A **subquery** is a query written **inside another SQL query**.
It is used to retrieve data that will be used by the main query.

**Key Points**

* Also called an **inner query**
* Usually used in `WHERE`, `SELECT`, or `FROM`
* Executes **before the main query**

**Example**

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

This query finds employees whose salary is **higher than the average salary**.

 ---
# Q 2. Types of subqueries.

Subqueries are mainly classified based on how they return results.

**1️⃣ Single-row Subquery**
Returns only **one row**.

Example

```sql id="x0j0xj"
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

**2️⃣ Multiple-row Subquery**
Returns **multiple rows** and often uses `IN`, `ANY`, or `ALL`.

Example

```sql id="r8qj8v"
SELECT name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
);
```

**3️⃣ Correlated Subquery**
Depends on the **outer query** and runs once for each row.

Example

```sql id="3t0g6v"
SELECT e.name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

---
# Q 3. Difference between correlated and non-correlated subquery.

Subqueries can be classified based on whether they depend on the outer query.

**Correlated Subquery**

* Depends on the **outer query**
* Executes **once for each row**

Example

```sql id="h5k7dm"
SELECT e.name
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE department_id = e.department_id
);
```

**Non-Correlated Subquery**

* Independent of the outer query
* Executes **only once**

Example

```sql id="c7x2fw"
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

**Quick Difference**

* Correlated → runs for each row
* Non-correlated → runs once

---
# Q 4. Can subquery return multiple rows?

Yes, a subquery can return **multiple rows**.

**Key Points**

* When a subquery returns multiple rows, it is called a **multi-row subquery**
* Usually used with operators like `IN`, `ANY`, or `ALL`
* Cannot be used with `=` because `=` expects a single value

**Example**

```sql id="z7y3wr"
SELECT name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
);
```

This subquery returns **multiple department IDs**, and the main query selects employees from those departments.

---
# Q 5. Subquery vs JOIN – which is better?
### Subquery vs JOIN – which is better?

Both are used to retrieve data from multiple tables, but **JOIN is usually preferred for performance**.

**JOIN**

* Combines tables directly
* Generally **faster for large datasets**
* Commonly used in data analysis

Example

```sql id="z8h0qs"
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.id;
```

**Subquery**

* Query inside another query
* Easier for some logical conditions

Example

```sql id="t0y7lz"
SELECT name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
);
```

**Key Point**

* `JOIN` → better for performance and complex queries
* `SUBQUERY` → simpler for nested logic.

---
# Q 6. Find employees earning more than average salary.

Use a **subquery** to calculate the average salary and compare it with each employee's salary.

**Query**

```sql id="n3x2kp"
SELECT name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

**Key Points**

* Subquery calculates the **average salary**
* Main query returns employees earning **above average**.

---
# Q 7. Find departments with highest average salary.

Use `GROUP BY` to calculate the average salary per department and select the highest one.

**Query**

```sql id="yrp57b"
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
ORDER BY avg_salary DESC
LIMIT 1;
```

**Key Points**

* `AVG(salary)` calculates average salary per department
* `GROUP BY` groups employees by department
* `ORDER BY ... DESC` returns the department with the highest average salary.

---
# Q 8. Use subquery in SELECT clause.
### Use subquery in `SELECT` clause

A subquery can be used in the `SELECT` clause to return a **calculated value** for each row.

**Example**

```sql
SELECT name,
       salary,
       (SELECT AVG(salary) FROM employees) AS avg_salary
FROM employees;
```

**Key Points**

* Subquery runs to compute a value (like average salary)
* Result is shown as an additional column
* Useful for comparisons and reports.

---
# Q 9. Can we use subquery in WHERE?
### Can we use subquery in `WHERE`?

Yes, a subquery can be used in the `WHERE` clause to filter results based on another query.

**Example**

```sql
SELECT name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE department_name = 'Sales'
);
```

**Key Points**

* Subquery runs first
* The result is used by the main query to filter rows
* Commonly used with `IN`, `EXISTS`, `=`, `ANY`, `ALL`.

---
# Q 10. Common performance issues with subqueries.
### Common performance issues with subqueries

Subqueries can sometimes slow down queries if not used properly.

**1️⃣ Correlated Subqueries**
Run once for **each row**, which can be slow on large tables.

**2️⃣ Nested Subqueries**
Multiple levels of subqueries increase complexity and execution time.

**3️⃣ Large Result Sets**
If a subquery returns many rows, filtering becomes slower.

**4️⃣ Missing Indexes**
Queries on non-indexed columns can reduce performance.

**Tip**

In many cases, using a **JOIN** instead of a subquery can improve performance.
