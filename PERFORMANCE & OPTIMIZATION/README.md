<div align="center">


# ⚡🚀 PERFORMANCE & OPTIMIZATION
**Performance & Optimization** focuses on improving query speed and efficiency to handle large datasets better. ⚡🚀

</div>

## Q 1. What is indexing?

Indexing is a database technique used to **improve the speed of data retrieval** from a table.

**Key Points**

* Works like an **index in a book**
* Helps the database **find data faster**
* Created on one or more columns

**Example**

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

**Explanation**

* Creates an index on the `name` column
* Queries searching by `name` will run **faster**.

---
## Q 2. Types of indexes.

Indexes are used to **speed up data retrieval** in a database. The main types are:

**1️⃣ Clustered Index**

* Sorts and stores the table data physically
* A table can have **only one clustered index**

Example

```sql id="h7p2qk"
CREATE CLUSTERED INDEX idx_emp_id
ON employees(id);
```

**2️⃣ Non-Clustered Index**

* Stores index separately from the table data
* A table can have **multiple non-clustered indexes**

Example

```sql id="j9m3rv"
CREATE INDEX idx_emp_name
ON employees(name);
```

**3️⃣ Unique Index**

* Ensures all values in the indexed column are **unique**

Example

```sql id="s1d7kp"
CREATE UNIQUE INDEX idx_email
ON users(email);
```

**Key Point**

Indexes improve **query performance**, especially for large tables.

---
## Q 3. When not to use indexes?

Indexes improve query performance, but in some cases they should be avoided.

**1️⃣ Small Tables**
Indexes are unnecessary for very small tables because the database can scan them quickly.

**2️⃣ Columns with Frequent Updates**
Indexes slow down `INSERT`, `UPDATE`, and `DELETE` operations.

**3️⃣ Columns with Many Duplicate Values**
Indexes are less effective on columns with **low selectivity** (many repeated values).

**4️⃣ Columns Rarely Used in Queries**
If a column is not used in `WHERE`, `JOIN`, or `ORDER BY`, indexing is unnecessary.

**Key Point**

Use indexes mainly on columns frequently used in **searching, filtering, or joining data**.

---
## Q 4. How do indexes improve performance?

Indexes improve query performance by allowing the database to **locate data quickly without scanning the entire table**.

**Key Points**

* Reduce the need for **full table scans**
* Provide **faster data retrieval** for queries
* Improve performance for `WHERE`, `JOIN`, and `ORDER BY` operations
* Work like a **book index**, pointing directly to the data location

**Example**

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

Now queries like this run faster:

```sql
SELECT *
FROM employees
WHERE name = 'Rahul';
```

Because the database can **use the index to find rows quickly**.

---
## Q 5. What is query optimization?

Query optimization is the process of **improving SQL queries so they run faster and use fewer resources**.

**Key Points**

* Reduces **query execution time**
* Uses **indexes and efficient query structure**
* Avoids unnecessary operations like full table scans
* Improves overall **database performance**

**Example**

Inefficient query

```sql
SELECT *
FROM employees;
```

Optimized query

```sql
SELECT name, salary
FROM employees
WHERE department = 'Sales';
```

**Tip**

Use **indexes, proper filtering, and optimized joins** to improve query performance.

---
## Q 6. Difference between clustered and non-clustered index.

Both indexes improve query performance, but they store data differently.

**Clustered Index**

* Physically sorts and stores the table data
* A table can have **only one clustered index**

Example

```sql
CREATE CLUSTERED INDEX idx_emp_id
ON employees(id);
```

**Non-Clustered Index**

* Stores index separately from the table data
* A table can have **multiple non-clustered indexes**

Example

```sql
CREATE INDEX idx_emp_name
ON employees(name);
```

**Quick Difference**

| Clustered Index             | Non-Clustered Index           |
| --------------------------- | ----------------------------- |
| Data stored in sorted order | Separate structure from table |
| Only one per table          | Multiple allowed              |
| Faster for range queries    | Faster for specific lookups   |

---
## Q 7. How to improve slow SQL query?

Slow queries can be improved by optimizing how the database retrieves and processes data.

**Key Methods**

**1️⃣ Use Indexes**
Create indexes on columns used in `WHERE`, `JOIN`, or `ORDER BY`.

```sql
CREATE INDEX idx_customer_id
ON orders(customer_id);
```

**2️⃣ Avoid `SELECT *`**
Retrieve only the required columns.

```sql
SELECT name, salary
FROM employees;
```

**3️⃣ Optimize Joins**
Use proper join conditions and indexed columns.

**4️⃣ Filter Early**
Use `WHERE` to reduce the number of rows processed.

```sql
SELECT *
FROM orders
WHERE order_date >= '2025-01-01';
```

**5️⃣ Analyze Execution Plan**
Check how the database executes the query and optimize accordingly.

**Key Point**

Efficient indexing, proper filtering, and optimized joins can **significantly improve query performance**.

---
## Q 8. Explain execution plan.

An **execution plan** shows how the database engine **executes a SQL query step by step**.

**Key Points**

* Displays the **operations used to retrieve data**
* Helps identify **performance issues**
* Shows whether the database uses **indexes or full table scans**

**Example**

```sql
EXPLAIN
SELECT *
FROM employees
WHERE department = 'Sales';
```

**What it shows**

* How tables are accessed
* Which indexes are used
* Estimated cost and number of rows processed

**Use**

Developers use execution plans to **optimize slow SQL queries**.

---
## Q 9. Why SELECT * is bad?

Using `SELECT *` retrieves **all columns from a table**, which can reduce query performance and clarity.

**Key Points**

* Retrieves **unnecessary data**
* Increases **memory and network usage**
* Makes queries **slower on large tables**
* Breaks queries if table structure changes

**Bad Practice**

```sql id="7i3lva"
SELECT *
FROM employees;
```

**Better Practice**

```sql id="m9p2se"
SELECT name, salary
FROM employees;
```

**Tip**

Always select **only the required columns** for better performance.

---
## Q 10. SQL best practices for BI reports.

Following SQL best practices helps create **faster and more reliable BI reports**.

**1️⃣ Select Only Required Columns**
Avoid `SELECT *` to reduce unnecessary data.

```sql
SELECT customer_id, sales_amount
FROM sales;
```

**2️⃣ Use Indexes**
Index columns used in `WHERE`, `JOIN`, and `ORDER BY`.

**3️⃣ Filter Data Early**
Use `WHERE` to reduce the dataset before processing.

```sql
SELECT *
FROM orders
WHERE order_date >= '2025-01-01';
```

**4️⃣ Use Aggregation in SQL**
Pre-aggregate data before loading into BI tools.

```sql
SELECT department, SUM(sales)
FROM sales
GROUP BY department;
```

**5️⃣ Clean Data in SQL**
Handle NULL values and duplicates before reporting.

**Key Point**

Optimized SQL queries help **reduce Power BI model size and improve dashboard performance**.
