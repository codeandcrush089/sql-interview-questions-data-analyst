<div align="center">


# 🧹📊 DATA CLEANING & HANDLING NULLS 
**Data Cleaning & Handling NULLs ensures** your dataset is accurate by fixing errors, removing duplicates, and managing missing values. 🧹📊

</div>

## Q 1. How do you handle NULL values?

NULL values represent **missing or unknown data**. SQL provides functions and conditions to manage them.

**1️⃣ Filter NULL values**

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

**2️⃣ Replace NULL values**

```sql
SELECT COALESCE(salary, 0) AS salary
FROM employees;
```

**3️⃣ Ignore NULL in calculations**

Aggregate functions like `SUM()` and `AVG()` automatically **ignore NULL values**.

**Key Points**

* Use `IS NULL` or `IS NOT NULL` for filtering
* Use `COALESCE()` or `ISNULL()` to replace NULL values
* Important for **data cleaning and accurate reports**.

---
## Q 2. What is COALESCE?

`COALESCE` is a SQL function used to **return the first non-NULL value** from a list of values.

**Key Points**

* Helps replace `NULL` values
* Checks values from left to right
* Returns the **first non-NULL value**

**Example**

```sql
SELECT COALESCE(salary, 0) AS salary
FROM employees;
```

If `salary` is `NULL`, it will return **0 instead**.

**Another Example**

```sql
SELECT COALESCE(phone, mobile, 'Not Available') AS contact_number
FROM customers;
```

This returns the **first available contact number**.

---
## Q 3. Difference between COALESCE and ISNULL.

Both functions are used to **replace NULL values**, but they work slightly differently.

**COALESCE**

* Standard SQL function
* Can handle **multiple values**

Example

```sql id="s7t1nz"
SELECT COALESCE(phone, mobile, 'Not Available')
FROM customers;
```

**ISNULL**

* Specific to **SQL Server**
* Works with **only two values**

Example

```sql id="v5r2jd"
SELECT ISNULL(salary, 0)
FROM employees;
```

**Quick Difference**

* `COALESCE` → supports **multiple arguments**
* `ISNULL` → supports **only two arguments**
* `COALESCE` → **ANSI standard SQL**
* `ISNULL` → mainly used in **SQL Server**

---
## Q 4. Replace NULL salary with 0.

You can replace `NULL` values using `COALESCE()` or `ISNULL()`.

**Using COALESCE**

```sql id="3vtb5t"
SELECT COALESCE(salary, 0) AS salary
FROM employees;
```

**Using ISNULL (SQL Server)**

```sql id="vdudxq"
SELECT ISNULL(salary, 0) AS salary
FROM employees;
```

**Key Points**

* Replaces `NULL` salary with **0**
* Useful for **reports and calculations** where NULL values cause issues.

---
## Q 5. Remove duplicate records.

Duplicates can be removed using **`ROW_NUMBER()` with a CTE or subquery**.

**Example**

```sql id="1h9gkq"
WITH cte AS (
    SELECT *,
           ROW_NUMBER() OVER (PARTITION BY name, email ORDER BY id) AS rn
    FROM customers
)
DELETE FROM cte
WHERE rn > 1;
```

**Key Points**

* `ROW_NUMBER()` assigns a number to duplicate rows
* `PARTITION BY` identifies duplicates
* Rows with `rn > 1` are deleted.

---
## Q 6. How do you identify duplicates?

Duplicates can be identified using `GROUP BY` and `HAVING`.

**Example**

```sql id="jnk0dx"
SELECT email, COUNT(*) AS duplicate_count
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

**Key Points**

* `GROUP BY` groups rows by the selected column
* `COUNT(*)` counts occurrences
* `HAVING COUNT(*) > 1` shows duplicate values.

---
## Q 7. Trim spaces from a column.

Use the `TRIM()` function to remove **extra spaces from the beginning and end** of a string.

**Example**

```sql id="4t5n7p"
SELECT TRIM(name) AS cleaned_name
FROM customers;
```

**Other Functions**

* `LTRIM()` → removes spaces from the **left side**
* `RTRIM()` → removes spaces from the **right side**

Example

```sql id="8w9k2m"
SELECT LTRIM(name), RTRIM(name)
FROM customers;
```

**Key Point**

Trimming spaces helps **clean text data before analysis or reporting**.

---
## Q 8. Convert text to upper/lower case.

Use the `UPPER()` and `LOWER()` functions to change the case of text.

**Convert to Upper Case**

```sql id="5r8t2v"
SELECT UPPER(name) AS upper_name
FROM customers;
```

**Convert to Lower Case**

```sql id="k4m1np"
SELECT LOWER(name) AS lower_name
FROM customers;
```

**Key Points**

* `UPPER()` converts text to **uppercase**
* `LOWER()` converts text to **lowercase**
* Useful for **data cleaning and standardization**.

---
## Q 9. Data cleaning importance in BI.

Data cleaning is important in Business Intelligence (BI) because it ensures **accurate, reliable, and meaningful insights**.

**Key Points**

* **Improves data accuracy** by removing errors and duplicates
* **Ensures consistency** in formats and values
* **Handles missing or NULL values** properly
* **Enhances report quality** in BI tools like Power BI or Tableau
* Helps make **better business decisions**

**Example**

```sql id="u8x9ks"
SELECT TRIM(UPPER(customer_name))
FROM customers;
```

This cleans data by **removing extra spaces and standardizing text format**.

---
## Q 10. Real-world data cleaning example.

In real projects, raw data often contains **duplicates, NULL values, and inconsistent formats**. Data cleaning prepares it for analysis.

**Scenario**

A sales dataset has:

* Duplicate customer records
* NULL values in sales
* Extra spaces in customer names

**Example Query**

```sql
SELECT 
    TRIM(UPPER(customer_name)) AS customer_name,
    COALESCE(sales_amount, 0) AS sales_amount
FROM sales_data;
```

**What this cleaning does**

* `TRIM()` → removes extra spaces
* `UPPER()` → standardizes text format
* `COALESCE()` → replaces NULL sales with 0

**Result**

Clean and consistent data ready for **Power BI dashboards or reports**.
