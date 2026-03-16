<div align="center">


# 📅⏱️ DATE & TIME FUNCTIONS
**Date & Time Functions** help you extract, manipulate, and analyze date or time values in a dataset. 📅⏱️

</div>

## Q 1. How do you extract year from date?

You can extract the **year part from a date** using the `YEAR()` function.

**Example (MySQL / SQL Server)**

```sql id="o38wrs"
SELECT YEAR(order_date) AS order_year
FROM orders;
```

**Key Points**

* `YEAR()` extracts the year from a date column
* Useful for **year-wise reports and analysis**

**Example Output**

| order_date | order_year |
| ---------- | ---------- |
| 2025-03-10 | 2025       |

---
## Q 2. Difference between GETDATE() and CURRENT_DATE.

Both are used to get the **current date**, but they are used in different database systems.

**GETDATE()**

* Used in **SQL Server**
* Returns **current date and time**

Example

```sql
SELECT GETDATE();
```

**CURRENT_DATE**

* Used in **MySQL, PostgreSQL**
* Returns **only the current date**

Example

```sql
SELECT CURRENT_DATE;
```

**Quick Difference**

* `GETDATE()` → date + time (SQL Server)
* `CURRENT_DATE` → only date (MySQL, PostgreSQL)

---
## Q 3. Find records from last 30 days.

Use date functions to filter records from the **last 30 days**.

**Example (MySQL / PostgreSQL)**

```sql id="n3k6qz"
SELECT *
FROM orders
WHERE order_date >= CURRENT_DATE - INTERVAL 30 DAY;
```

**Example (SQL Server)**

```sql id="p6k1ds"
SELECT *
FROM orders
WHERE order_date >= DATEADD(DAY, -30, GETDATE());
```

**Key Points**

* Filters records from the **past 30 days**
* Common in **sales and activity reports**.

---
## Q 4. Calculate age from DOB.

Use date functions to calculate the **age from a date of birth (DOB)**.

**Example (MySQL)**

```sql id="u3c2kq"
SELECT name,
       TIMESTAMPDIFF(YEAR, dob, CURDATE()) AS age
FROM employees;
```

**Example (SQL Server)**

```sql id="c6y4mz"
SELECT name,
       DATEDIFF(YEAR, dob, GETDATE()) AS age
FROM employees;
```

**Key Points**

* `dob` → date of birth column
* Calculates the **age in years** based on the current date.

---
## Q 5. Difference between DATE and DATETIME.

Both are data types used to store date values, but they store different levels of detail.

**DATE**

* Stores **only the date**
* Format: `YYYY-MM-DD`

Example

```sql
SELECT DATE('2025-03-11');
```

**DATETIME**

* Stores **date and time**
* Format: `YYYY-MM-DD HH:MM:SS`

Example

```sql
SELECT DATETIME('2025-03-11 10:30:00');
```

**Quick Difference**

* `DATE` → stores only **date**
* `DATETIME` → stores **date + time**

---
## Q 6. Find month-wise sales.

Use date functions with `GROUP BY` to calculate total sales for each month.

**Query**

```sql id="9kveqp"
SELECT MONTH(order_date) AS month,
       SUM(sales_amount) AS total_sales
FROM sales
GROUP BY MONTH(order_date);
```

**Key Points**

* `MONTH()` extracts the month from the date
* `SUM()` calculates total sales
* `GROUP BY` groups results by each month.

---
## Q 7. How do you handle time zones?

Time zones are handled by **converting timestamps from one time zone to another** using built-in SQL functions.

**Example (MySQL)**

```sql id="g7t1hp"
SELECT CONVERT_TZ(order_time, 'UTC', 'Asia/Kolkata')
FROM orders;
```

**Example (PostgreSQL)**

```sql id="2k1eap"
SELECT order_time AT TIME ZONE 'UTC' AT TIME ZONE 'Asia/Kolkata'
FROM orders;
```

**Key Points**

* Store timestamps in **UTC**
* Convert to the **user's local time zone** when displaying data
* Prevents issues with global applications.

---
## Q 8. What is DATEDIFF?

`DATEDIFF` is a SQL function used to **calculate the difference between two dates**.

**Key Points**

* Returns the difference in **days, months, or years**
* Commonly used for **age, duration, or time gap calculations**

**Example (SQL Server)**

```sql id="x2j7bn"
SELECT DATEDIFF(DAY, '2025-03-01', '2025-03-11') AS days_difference;
```

**Example Use Case**

```sql id="y6q9fh"
SELECT order_id,
       DATEDIFF(DAY, order_date, delivery_date) AS delivery_days
FROM orders;
```

This calculates **how many days it took to deliver each order**.

---
## Q 9. Find difference between two dates.

Use the `DATEDIFF` function to calculate the **difference between two dates**.

**Example (SQL Server)**

```sql id="m0k3sn"
SELECT DATEDIFF(DAY, '2025-03-01', '2025-03-11') AS date_difference;
```

**Example (MySQL)**

```sql id="u3k7ez"
SELECT DATEDIFF('2025-03-11', '2025-03-01') AS date_difference;
```

**Key Points**

* Calculates the **number of days between two dates**
* Commonly used for **delivery time, age, or duration calculations**.

---
## Q 10. Common date issues in SQL reports.

Date-related problems are common in reporting and data analysis.

**1️⃣ Time Zone Differences**
Data stored in different time zones can produce incorrect report results.

**2️⃣ Incorrect Date Format**
Different formats like `MM-DD-YYYY` vs `DD-MM-YYYY` may cause errors.

**3️⃣ Missing Time Component**
Using `DATE` instead of `DATETIME` can remove important time details.

**4️⃣ NULL Date Values**
Missing dates can affect calculations and reports.

**5️⃣ Date Filtering Errors**
Incorrect use of date ranges can return wrong records.

**Tip**

Always store dates in **standard format (YYYY-MM-DD)** and preferably in **UTC** for consistent reporting.
