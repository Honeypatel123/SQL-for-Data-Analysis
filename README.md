# 📊 SQL for Data Analysis - Warehouse & Retail Sales

This PostgreSQL project explores warehouse and retail sales data through a series of SQL queries to answer key business questions.

---

## 🔹 Questions and Queries

### 1. Total Retail Sales for Each Supplier

```sql
SELECT supplier, SUM(retailsales) AS total_retail_sales
FROM project
GROUP BY supplier;
```

---

### 2. Total Retail Sales by Supplier and Month

```sql
SELECT supplier, year, month, SUM(retailsales) AS total_retail_sales
FROM project
GROUP BY supplier, year, month;
```

---

### 3. Maximum Warehouse Sales per Item Description

```sql
SELECT itemdescription, MAX(retailsales) AS max_warehouse_sales
FROM project
GROUP BY itemdescription;
```

---

### 4. Average Retail Transfers by Year

```sql
SELECT year, AVG(retailtransfers) AS avg_retail_transfers
FROM project
GROUP BY year;
```

---

### 5. Difference Between Maximum and Minimum Retail Sales per Item

```sql
SELECT itemdescription, MAX(retailsales) - MIN(retailsales) AS diff_max_min_retail_sales
FROM project
GROUP BY itemdescription;
```

---

### 6. Total Retail Sales for Each Supplier (Broken Down by Year and Month)

```sql
SELECT year, month, supplier,
       SUM(retailsales) OVER (PARTITION BY supplier, year, month) AS total_retail_sales
FROM project;
```

---

### 7. Running Total of Retail Sales for Each Item Type (Ordered by Month)

```sql
SELECT year, month, itemtype,
       SUM(retailsales) OVER (PARTITION BY itemtype ORDER BY month) AS running_total_retail_sales
FROM project;
```

---

### 8. Difference in Retail Sales Between Each Month and Previous Month (For Each Supplier and Item Type)

```sql
SELECT year, month, supplier, itemtype,
       retailsales - LAG(retailsales) OVER (PARTITION BY supplier, itemtype ORDER BY year, month) AS diff_retail_sales
FROM project;
```

---

## 🔹 Further Questions to Explore (Upcoming)

- Average retail sales per item type compared to the overall yearly average.
- Percentage of retail sales per supplier, compared to the total sales across all suppliers by year and month.
- Identify the month with the highest retail transfer for each supplier over the past 12 months.

---

> **Note:**  
> This is a sample of SQL queries and ideas for analyzing warehouse and retail sales data. Results depend on the specific structure and values in your database.
