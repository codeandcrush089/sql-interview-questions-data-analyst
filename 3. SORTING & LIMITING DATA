<div align="center">


# 🔽📊 SORTING & LIMITING DATA
**Sorting & Limiting Data** help organize query results and control how many rows are returned. 🔽📊

</div>

---
## Q 1. What is ORDER BY?

`ORDER BY` is used to **sort query results** based on one or more columns.

**Key Points**

* Sorts data in **ascending or descending order**
* Default order is **ascending (ASC)**
* Can sort by multiple columns

**Example**

```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC;
```

This query returns employees sorted by **highest salary first**.

---
## Q 2. Difference between ASC and DESC.

Both are used with `ORDER BY` to control how results are sorted.

**ASC (Ascending)**

* Sorts data from **lowest to highest**
* Default sorting order

Example

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

**DESC (Descending)**

* Sorts data from **highest to lowest**

Example

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

**Quick Difference**

* `ASC` → Low → High (A → Z, 0 → 9)
* `DESC` → High → Low (Z → A, 9 → 0)

---
## Q 3. How do you fetch the latest 10 records from a table?

Sort the records by a **date or ID column in descending order** and limit the result.

**MySQL / PostgreSQL**

```sql
SELECT *
FROM orders
ORDER BY created_at DESC
LIMIT 10;
```

**SQL Server**

```sql
SELECT TOP 10 *
FROM orders
ORDER BY created_at DESC;
```

**Key Points**

* `ORDER BY ... DESC` → latest records first
* `LIMIT / TOP` → returns only 10 rows.

---
## Q 4. Difference between TOP, LIMIT, and FETCH FIRST.

All are used to **restrict the number of rows returned** by a query, but they belong to different SQL systems.

**TOP**

* Used in **SQL Server**
* Written right after `SELECT`

Example

```sql id="sz4p4p"
SELECT TOP 5 *
FROM employees;
```

**LIMIT**

* Used in **MySQL, PostgreSQL**
* Written at the end of the query

Example

```sql id="v1a0n4"
SELECT *
FROM employees
LIMIT 5;
```

**FETCH FIRST**

* Standard SQL, used in **Oracle, PostgreSQL, DB2**

Example

```sql id="5h3q1j"
SELECT *
FROM employees
FETCH FIRST 5 ROWS ONLY;
```

**Quick Difference**

| Command     | Commonly Used In        |
| ----------- | ----------------------- |
| TOP         | SQL Server              |
| LIMIT       | MySQL, PostgreSQL       |
| FETCH FIRST | Oracle, DB2, PostgreSQL |

---
## Q 5. How do you get the second highest salary?

Use a subquery to find the maximum salary less than the highest salary.

**Query**

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);
```

**Key Points**

* First `MAX()` finds the highest salary
* Second query returns the next highest value
* Common SQL interview question.

---
## Q 6. How to retrieve the Nth highest salary?

You can use `ORDER BY` with `LIMIT` and `OFFSET`.

**Example (3rd highest salary)**

```sql
SELECT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 2;
```

**Key Points**

* `ORDER BY salary DESC` → highest salaries first
* `OFFSET` skips rows
* Works in MySQL / PostgreSQL

**General Idea**

Nth highest salary → `OFFSET N-1`.

---
## Q 7. Can you sort data using column position?

Yes. SQL allows sorting using the **column position number** in the `SELECT` list.

**Example**

```sql
SELECT name, salary
FROM employees
ORDER BY 2 DESC;
```

**Explanation**

* `2` refers to the **second column** in the SELECT statement (`salary`).
* Results will be sorted by salary in descending order.

**Note**

Although valid, using **column names is recommended** because it makes queries easier to read and maintain.

---
## Q 8. What happens if ORDER BY is not used?

If `ORDER BY` is not used, the database returns results in **no guaranteed order**.

**Key Points**

* Rows may appear in **random or storage order**
* Order can change between queries
* Not reliable for reports or analysis

**Example**

```sql
SELECT *
FROM employees;
```

The result may not be sorted by **ID, name, or salary** unless `ORDER BY` is specified.

---
## Q 9. Sort employees by department and salary descending.

Use `ORDER BY` with multiple columns.

**Query**

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

**Key Points**

* First sorts by **department**
* Within each department, sorts by **salary (highest first)**
* Multiple columns can be used in `ORDER BY`.

---
## Q 10. Why is sorting important in reports?

Sorting organizes data in a **clear and meaningful order**, making reports easier to read and analyze.

**Key Points**

* Helps quickly identify **top or lowest values**
* Improves **readability of reports**
* Makes comparisons easier
* Common in dashboards and business reports

**Example**

```sql
SELECT name, sales
FROM employees
ORDER BY sales DESC;
```

This shows the **highest performers first**, which is useful in business reports. 📊
