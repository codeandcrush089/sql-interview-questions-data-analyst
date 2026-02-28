# Q 1. What is SQL and why is it important for Data Analysts?

**SQL (Structured Query Language)** is a programming language used to communicate with relational databases. It allows users to **store, retrieve, filter, update, and analyze data** efficiently.

### Why SQL is important for Data Analysts

**1️⃣ Data Extraction**
Analysts use SQL to pull specific data from large databases.

```sql
SELECT *
FROM sales
WHERE order_date >= '2025-01-01';
```

**2️⃣ Data Filtering & Cleaning**
SQL helps filter incorrect or unnecessary data before analysis.

```sql
SELECT *
FROM customers
WHERE email IS NOT NULL;
```

**3️⃣ Data Aggregation**
Analysts summarize data using functions like **SUM, COUNT, AVG**.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

**4️⃣ Joining Multiple Tables**
Business data is usually stored in multiple tables. SQL helps combine them.

```sql
SELECT o.order_id, c.customer_name
FROM orders o
JOIN customers c
ON o.customer_id = c.customer_id;
```

**5️⃣ Faster Decision Making**
SQL enables analysts to quickly generate reports and insights for business decisions.

### Simple Summary

SQL is the **core skill for Data Analysts** because it helps them access, analyze, and transform raw data into meaningful insights. 📊

# Q 2. Difference between SQL and MySQL.

**SQL (Structured Query Language)** is a standard language used to query and manage data in relational databases.
**MySQL** is a database management system that uses SQL to store and manage data.

**Key Differences**

* **SQL:** A language used to interact with databases.
* **MySQL:** Software (RDBMS) that implements SQL.
* **SQL:** Used across many databases like PostgreSQL, SQL Server, Oracle.
* **MySQL:** One specific database system developed by Oracle.

**Example**

```sql
SELECT * FROM customers;
```

This SQL query can run in **MySQL, PostgreSQL, SQL Server,** and other SQL-based databases.

# Q 3. What are DDL, DML, DCL, TCL commands? Give examples.

These are categories of SQL commands used to manage and control databases.

**1️⃣ DDL (Data Definition Language)**
Used to define or modify database structure.

Common commands:

* `CREATE`
* `ALTER`
* `DROP`
* `TRUNCATE`

Example

```sql
CREATE TABLE employees (
  id INT,
  name VARCHAR(50)
);
```


**2️⃣ DML (Data Manipulation Language)**
Used to work with data inside tables.

Common commands:

* `SELECT`
* `INSERT`
* `UPDATE`
* `DELETE`

Example

```sql
INSERT INTO employees (id, name)
VALUES (1, 'Rahul');
```


**3️⃣ DCL (Data Control Language)**
Used to control user access and permissions.

Common commands:

* `GRANT`
* `REVOKE`

Example

```sql
GRANT SELECT ON employees TO user1;
```


**4️⃣ TCL (Transaction Control Language)**
Used to manage transactions in a database.

Common commands:

* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`

Example

```sql
ROLLBACK;
```

# Q 4. What is a primary key? Can it contain NULL values?

A **Primary Key** is a column (or set of columns) that uniquely identifies each row in a table.

**Key Points**

* Values must be **unique**
* Cannot contain **NULL values**
* Each table can have **only one primary key** (can include multiple columns)

**Example**

```sql
CREATE TABLE employees (
  id INT PRIMARY KEY,
  name VARCHAR(50),
  department VARCHAR(50)
);
```

Here, `id` uniquely identifies every employee and **cannot be NULL or duplicated**.


# Q 5. What is a foreign key and why is it used?

A **Foreign Key** is a column in one table that refers to the **Primary Key of another table**. It creates a relationship between the two tables.

**Why it is used**

* Maintains **data integrity**
* Connects related tables
* Prevents invalid data from being inserted

**Example**

```sql
CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

Here, `customer_id` links the **orders** table to the **customers** table.

# Q 6. Difference between DELETE, TRUNCATE, and DROP.

These commands are used to remove data or database objects, but they work differently.

**DELETE**

* Removes specific rows from a table
* Can use `WHERE` condition
* Table structure remains

Example

```sql
DELETE FROM employees
WHERE department = 'Sales';
```

**TRUNCATE**

* Removes **all rows** from a table
* Faster than DELETE
* Cannot use `WHERE`

Example

```sql
TRUNCATE TABLE employees;
```

**DROP**

* Deletes the **entire table** including structure and data

Example

```sql
DROP TABLE employees;
```

**Quick Summary**

| Command  | Removes Data        | Removes Table Structure | WHERE Allowed |
| -------- | ------------------- | ----------------------- | ------------- |
| DELETE   | Yes (selected rows) | No                      | Yes           |
| TRUNCATE | Yes (all rows)      | No                      | No            |
| DROP     | Yes                 | Yes                     | No            |


