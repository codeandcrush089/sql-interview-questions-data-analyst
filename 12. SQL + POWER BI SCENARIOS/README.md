<div align="center">


# 📊⚡  SQL + POWER BI SCENARIOS
**SQL + Power BI Scenarios** show how SQL queries are used to prepare and analyze data for Power BI dashboards and reports. 📊⚡

</div>

---
## Q 1. How SQL is used in Power BI?

SQL is used in Power BI to **retrieve, filter, and prepare data from databases** before creating reports and dashboards.

**Key Uses**

**1️⃣ Data Extraction**
SQL queries pull data from databases into Power BI.

```sql
SELECT customer_id, sales_amount
FROM sales;
```

**2️⃣ Data Filtering**
Filter only the required data before loading it into Power BI.

```sql
SELECT *
FROM orders
WHERE order_date >= '2025-01-01';
```

**3️⃣ Data Aggregation**
Summarize data using functions like `SUM`, `COUNT`, or `AVG`.

```sql
SELECT department, SUM(sales_amount)
FROM sales
GROUP BY department;
```

**Key Point**

Using SQL before loading data helps **reduce data size and improve Power BI dashboard performance**.

---
## Q 2. Difference between SQL aggregation and DAX aggregation.

Both SQL and DAX are used to aggregate data, but they work at different stages.

**SQL Aggregation**

* Performed **in the database before data is loaded**
* Uses functions like `SUM()`, `COUNT()`, `AVG()`

Example

```sql
SELECT department, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY department;
```

**DAX Aggregation**

* Performed **inside Power BI after data is loaded**
* Uses functions like `SUM()`, `COUNT()`, `AVERAGE()`

Example

```DAX
Total Sales = SUM(Sales[sales_amount])
```

**Quick Difference**

* **SQL** → aggregation happens in the **database**
* **DAX** → aggregation happens in **Power BI model**
* **SQL** → reduces data before loading
* **DAX** → used for calculations in reports.

---
## Q 3. When do you push logic to SQL vs Power BI?

Deciding where to apply logic depends on **performance and use case**.

**Push Logic to SQL**

* For **data cleaning and transformations**
* For **large datasets**
* For **joins, filtering, and aggregations**

Example

```sql id="g4i7ds"
SELECT department, SUM(sales_amount)
FROM sales
GROUP BY department;
```

**Push Logic to Power BI (DAX)**

* For **dynamic calculations in reports**
* For **user-driven metrics and measures**
* For **dashboard-level calculations**

Example

```DAX id="r5k8lm"
Total Sales = SUM(Sales[sales_amount])
```

**Key Point**

* **SQL** → heavy data processing before loading
* **Power BI (DAX)** → interactive calculations in reports.

---
## Q 4. Write SQL for running total and compare with DAX.

A running total calculates the **cumulative sum of values over time**.

**SQL Example**

```sql
SELECT order_date,
       sales_amount,
       SUM(sales_amount) OVER (ORDER BY order_date) AS running_total
FROM sales;
```

**Key Point**

* `SUM() OVER (ORDER BY order_date)` calculates cumulative sales.

---

**DAX Example (Power BI)**

```DAX
Running Total =
CALCULATE(
    SUM(Sales[sales_amount]),
    FILTER(
        ALL(Sales[order_date]),
        Sales[order_date] <= MAX(Sales[order_date])
    )
)
```

**Quick Comparison**

| SQL                       | DAX                          |
| ------------------------- | ---------------------------- |
| Runs in the **database**  | Runs in **Power BI model**   |
| Used before loading data  | Used for report calculations |
| Uses **window functions** | Uses **CALCULATE + FILTER**  |

---
## Q 5. How SQL helps reduce Power BI model size?

SQL can reduce Power BI model size by **preparing and filtering data before loading it into Power BI**.

**Key Ways**

**1️⃣ Filter Unnecessary Data**
Load only the required rows.

```sql id="ux2q9n"
SELECT *
FROM sales
WHERE order_date >= '2024-01-01';
```

**2️⃣ Select Required Columns**
Avoid loading unnecessary columns.

```sql id="n5d8zy"
SELECT customer_id, sales_amount
FROM sales;
```

**3️⃣ Pre-Aggregate Data**
Summarize data before importing.

```sql id="g2q7fs"
SELECT department, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY department;
```

**Key Point**

Using SQL for **filtering, selecting, and aggregating data** reduces the amount of data loaded, which **improves Power BI performance and reduces model size**.

---
## Q 6. Import vs DirectQuery impact on SQL.

Power BI supports two main data connection modes: **Import** and **DirectQuery**.

**Import Mode**

* Data is **loaded into Power BI memory**
* SQL runs **only during data refresh**
* Faster dashboard performance

Example

```sql id="h4b9tk"
SELECT customer_id, sales_amount
FROM sales;
```

**DirectQuery Mode**

* Data stays in the **database**
* SQL queries run **every time a report is used**
* Depends heavily on database performance

Example

```sql id="v7y2qp"
SELECT *
FROM sales
WHERE order_date >= '2025-01-01';
```

**Quick Difference**

* **Import** → SQL runs during refresh, faster reports
* **DirectQuery** → SQL runs live for every interaction

**Key Point**

DirectQuery requires **well-optimized SQL queries and indexes** for good performance.

---
## Q 7. How to debug SQL query used in Power BI?

Debugging SQL queries helps identify **errors or performance issues** in Power BI reports.

**1️⃣ Check the Query in Power Query**
Open **Power Query Editor** and review the SQL or transformation steps.

**2️⃣ Test Query in Database Tool**
Run the same SQL in tools like **SSMS, MySQL Workbench, or PostgreSQL client** to verify results.

```sql
SELECT *
FROM sales
WHERE order_date >= '2025-01-01';
```

**3️⃣ Check Query Performance**
Use **Execution Plan** to identify slow operations.

**4️⃣ Enable Query Diagnostics**
Power BI provides **Query Diagnostics** to analyze query execution.

**Key Point**

Always test SQL queries **directly in the database first** to ensure they work correctly and run efficiently.

---
## Q 8. SQL vs Power Query – where to clean data?

Data cleaning can be done in **SQL or Power Query**, depending on the situation.

**SQL (Recommended for Large Data)**

* Clean data **before loading into Power BI**
* Faster for large datasets
* Reduces Power BI model size

Example

```sql id="e8u5mq"
SELECT TRIM(UPPER(customer_name)) AS customer_name,
       COALESCE(sales_amount, 0) AS sales_amount
FROM sales;
```

**Power Query (Recommended for Small Transformations)**

* Used inside **Power BI Power Query Editor**
* Good for quick transformations and data shaping

Examples:

* Removing columns
* Changing data types
* Splitting columns

**Quick Comparison**

* **SQL** → heavy data cleaning and large datasets
* **Power Query** → small transformations inside Power BI

**Best Practice**

Perform **major cleaning in SQL**, and use **Power Query for minor transformations**.

---
## Q 9. Real production SQL issue you faced.

A common real-world SQL issue occurs when **duplicate records or incorrect joins cause wrong report results**.

**Scenario**

In a sales report, the **total sales were showing higher than expected** because the query joined two tables incorrectly, causing duplicate rows.

**Problem Query**

```sql
SELECT c.customer_name, SUM(o.sales_amount)
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id;
```

Without proper grouping, totals can become incorrect.

**Fixed Query**

```sql
SELECT c.customer_name, SUM(o.sales_amount) AS total_sales
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_name;
```

**Lesson**

* Always check **joins and aggregations**
* Verify results to avoid **duplicate counting in reports**.

---
## Q 10. End-to-end SQL → Power BI reporting flow.

This describes how data moves from a **database to a Power BI dashboard**.

**1️⃣ Data Source**
Data is stored in databases like **MySQL, SQL Server, PostgreSQL**.

**2️⃣ Data Extraction with SQL**
SQL queries retrieve required data.

```sql
SELECT customer_id, order_date, sales_amount
FROM sales;
```

**3️⃣ Data Cleaning & Transformation**
Clean data using SQL or Power Query.

Example tasks:

* Handle NULL values
* Remove duplicates
* Standardize formats

**4️⃣ Load Data into Power BI**
Connect Power BI to the database using **Import or DirectQuery**.

**5️⃣ Data Modeling**
Create relationships between tables and build a data model.

**6️⃣ Create Measures with DAX**
Define calculations like totals or averages.

Example

```DAX
Total Sales = SUM(Sales[sales_amount])
```

**7️⃣ Build Visualizations**
Create charts, dashboards, and reports in Power BI.

**Key Flow**

Database → SQL Query → Data Cleaning → Power BI Import → Data Model → DAX Measures → Dashboard 📊
