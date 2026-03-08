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

---
# Q 4. Can subquery return multiple rows?

---
# Q 5. Subquery vs JOIN – which is better?

---
# Q 6. Find employees earning more than average salary.

---
# Q 7. Find departments with highest average salary.

---
# Q 8. Use subquery in SELECT clause.

---
# Q 9. Can we use subquery in WHERE?

---
# Q 10. Common performance issues with subqueries.
