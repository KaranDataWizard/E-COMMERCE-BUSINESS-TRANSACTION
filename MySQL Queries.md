


# 🛒 E-Commerce Transaction Data Analysis using MySQL

This project involves a comprehensive analysis of e-commerce transaction data using MySQL. The goal is to derive actionable insights regarding sales performance, customer behavior, and product trends.

---

## 🗂️ Dataset Overview

The dataset contains the following columns:

- `TransactionNo`
- `Date`
- `ProductNo`
- `ProductName`
- `Price`
- `Quantity`
- `CustomerNo`
- `Country`
- `TotalRevenue`

---

## 📁 Database and Table Creation

```sql
CREATE DATABASE Transaction_analysis;
USE transaction_analysis;

CREATE TABLE ecommerce (
  TransactionNo VARCHAR(50),
  Date DATE,
  ProductNo VARCHAR(50),
  ProductName VARCHAR(255),
  Price DECIMAL(10,2),
  Quantity INT,
  CustomerNo VARCHAR(50),
  Country VARCHAR(100),
  TotalRevenue DECIMAL(10,2)
);

LOAD DATA INFILE "D:\\E-COMMERCE.csv"
INTO TABLE ecommerce
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

---

## 🔍 Basic Analysis

```sql
-- 1. Total Revenue Generated
SELECT SUM(TotalRevenue) AS Revenue FROM ecommerce;

-- 2. Number of Unique Products Sold
SELECT COUNT(DISTINCT ProductName) AS Unique_Product FROM ecommerce;

-- 3. Transactions per Day
SELECT Date, COUNT(DISTINCT TransactionNo) AS Transaction_count
FROM ecommerce
GROUP BY Date;

-- 4. Average Quantity per Transaction
SELECT TransactionNo, ROUND(AVG(Quantity), 2) AS Avg_quantity
FROM ecommerce
GROUP BY TransactionNo
ORDER BY Avg_quantity DESC;

-- 5. Unique Countries
SELECT DISTINCT Country FROM ecommerce
WHERE TransactionNo IS NOT NULL;
```

---

## 🧪 Intermediate Analysis

```sql
-- 6. Top 5 Best-Selling Products by Quantity
SELECT ProductName, SUM(Quantity) AS TotalQuantity
FROM ecommerce
GROUP BY ProductName
ORDER BY TotalQuantity DESC
LIMIT 5;

-- 7. Product with Highest Revenue
SELECT ProductName, SUM(TotalRevenue) AS Revenue
FROM ecommerce
GROUP BY ProductName
ORDER BY Revenue DESC;

-- 8. Monthly Revenue Trend
SELECT YEAR(Date) AS Year, MONTHNAME(Date) AS Month, SUM(TotalRevenue) AS Revenue
FROM ecommerce
GROUP BY YEAR(Date), MONTHNAME(Date)
ORDER BY Year, Month;

-- 9. Customer with Most Purchases by Quantity
SELECT CustomerNo, SUM(Quantity) AS Quantity
FROM ecommerce
GROUP BY CustomerNo
ORDER BY Quantity DESC;

-- 10. Average Order Value
SELECT ROUND(SUM(TotalRevenue) / COUNT(DISTINCT TransactionNo), 2) AS AOV
FROM ecommerce;
```

---

## 💡 Advanced Analysis

```sql
-- 11. Countries with Highest Revenue and Their Contribution %
SELECT Country,
       SUM(TotalRevenue) AS Revenue,
       ROUND(SUM(TotalRevenue) / (SELECT SUM(TotalRevenue) FROM ecommerce) * 100, 2) AS Percentage
FROM ecommerce
GROUP BY Country
ORDER BY Revenue DESC;

-- 12. Customers Who Purchased the Same Product More Than Once
SELECT CustomerNo, ProductNo, COUNT(*) AS Product_Count
FROM ecommerce
GROUP BY CustomerNo, ProductNo
HAVING COUNT(*) > 1
ORDER BY Product_Count DESC;

-- 13. Average Revenue Per Product Across Countries
SELECT Country, ProductName, ROUND(AVG(TotalRevenue), 2) AS Avg_Revenue
FROM ecommerce
GROUP BY Country, ProductName
ORDER BY Avg_Revenue DESC;

-- 14. Product with Highest Revenue Per Unit Sold
SELECT ProductName,
       ROUND(SUM(TotalRevenue) / SUM(Quantity), 2) AS Revenue_Per_Unit
FROM ecommerce
GROUP BY ProductName
ORDER BY Revenue_Per_Unit DESC;

-- 15. Cumulative Revenue Month-Over-Month
SELECT YEAR(Date) AS Year, 
       MONTH(Date) AS Month,
       SUM(TotalRevenue) AS Revenue,
       SUM(SUM(TotalRevenue)) OVER (ORDER BY YEAR(Date), MONTH(Date)) AS Cumulative_Revenue
FROM ecommerce
GROUP BY YEAR(Date), MONTH(Date)
ORDER BY Cumulative_Revenue DESC;

-- 16. Top 5 Products Showing Most Revenue Growth MoM
WITH monthly_product_revenue AS (
  SELECT ProductNo, 
         YEAR(Date) AS Year, 
         MONTH(Date) AS Month, 
         SUM(TotalRevenue) AS Revenue
  FROM ecommerce
  GROUP BY ProductNo, YEAR(Date), MONTH(Date)
),
growth_calc AS (
  SELECT *,
         Revenue - LAG(Revenue) OVER (PARTITION BY ProductNo ORDER BY Year, Month) AS Revenue_Growth
  FROM monthly_product_revenue
)
SELECT *
FROM growth_calc
ORDER BY Revenue_Growth DESC
LIMIT 5;
```

---

## 📊 Results & Insights

- 💰 **Total Revenue**: 6,29,65,892.34
- 🔝 **Top-Selling Product**: Paper Craft Little Birdie
- 🌍 **Highest Spending Country**: United Kingdom
- 🧍‍♂️ **Top Customer by quantity(customer no)**: 14646
- 📈 **Revenue Trends**: Jan-2018

---

## ✅ Conclusion

This analysis helps understand:
- What products and customers drive revenue
- Which regions are most profitable
- Seasonal trends in revenue
- Key performance metrics like AOV, revenue per product, and product growth

🔍 These insights can help stakeholders with decisions around **inventory**, **marketing**, and **customer engagement strategies**.

---

## 📌 Tools Used

- MySQL
- CSV file import
- Window functions, CTEs, aggregation, filtering
