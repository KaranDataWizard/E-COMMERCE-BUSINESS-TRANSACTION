
---

# 📦 E-Commerce Sales Data Analysis (500K+ Records)  
**🔍 SQL-Based Business Insights | 🧹 Excel for Preprocessing**

---

## 🧠 Overview

This project is a comprehensive **data analytics case study** based on e-commerce sales data with over **500,000+ transaction records**. The goal is to generate **business-level insights** using **MySQL**, while **Microsoft Excel** was used strictly for **initial data cleaning and formatting**.

By writing structured SQL queries, this project extracts key performance metrics — such as revenue trends, best-selling products, customer loyalty, and monthly growth — that are critical for **business intelligence** and **strategic decision-making** in the e-commerce space.

---

## 🎯 Objectives

- 📊 Extract actionable KPIs using advanced SQL queries  
- 🧠 Identify top-performing products, loyal customers, and high-contributing countries  
- 📅 Analyze monthly revenue trends and cumulative growth  
- ⚙️ Use window functions to understand revenue growth and customer retention  
- 🏢 Create scalable and reusable SQL templates for real-world scenarios  

---

## 🧰 Tools & Technologies

| Tool / Technology   | Purpose                           |
|---------------------|-----------------------------------|
| **Microsoft Excel** | Data Cleaning & Preprocessing     |
| **MySQL**           | Data Analysis & Business Insights |

---

## 🗂️ Dataset Schema

The dataset includes the following columns:

- `TransactionNo` – Unique ID for each transaction  
- `Date` – Date of transaction  
- `ProductNo` – Product identifier  
- `ProductName` – Name of the product  
- `Price` – Unit price  
- `Quantity` – Number of units sold  
- `CustomerNo` – Customer identifier  
- `Country` – Country of purchase  
- `TotalRevenue` – Revenue generated (Price × Quantity)

---

## 📊 Key Metrics & KPIs

| Category     | KPIs / Analysis                                           |
|--------------|-----------------------------------------------------------|
| 🧾 Revenue    | Total Revenue, Average Order Value (AOV)                 |
| 📈 Trends     | Monthly Revenue, Cumulative Revenue (MoM)               |
| 📦 Products   | Top Products by Quantity & Revenue, Revenue per Unit    |
| 🧍 Customers  | Top Buyers, Repeat Purchases, Loyalty Indicators         |
| 🌍 Geography  | Revenue by Country, Country Contribution %              |
| 🧮 SQL Logic  | MoM Growth using Window Functions (`LAG()`)             |

---

## ⚙️ SQL Techniques Used

- 🔢 Aggregations: `SUM()`, `COUNT()`, `AVG()`  
- 📊 Grouping & Filtering: `GROUP BY`, `ORDER BY`, `HAVING`, `WHERE`  
- 🪟 Window Functions: `LAG()`, `OVER(PARTITION BY ...)`  
- 📄 CTEs: `WITH` clause for query structuring and readability  

---

## 💡 Business Questions Solved

1. 💰 What is the total revenue generated?  
2. 📦 Which products are the best sellers (by revenue and quantity)?  
3. 📅 How is monthly revenue growing over time?  
4. 🌍 Which countries contribute the most to total sales?  
5. 🔁 Are there any repeat customers with consistent purchasing behavior?  
6. 🚀 Which products show the highest month-over-month revenue growth?

---

## 📌 Sample Query: Month-over-Month Product Revenue Growth

```sql
WITH monthly_product_revenue AS (
    SELECT 
        ProductNo, 
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
SELECT * FROM growth_calc
ORDER BY Revenue_Growth DESC
LIMIT 5;
```

---

## 📊 Results & Insights

✅ **Top 5 Products by Quantity Sold**: Consistently high volume with stable pricing strategy  
✅ **Top Revenue-Generating Product**: One item alone drives a significant portion of revenue  
🌍 **Country Revenue Breakdown**: 3 countries contribute over 70% of total sales  
🔁 **Customer Loyalty**: Identified high-value, repeat buyers with strong product affinity  
📈 **MoM Revenue Growth**: Revenue rises steadily, with notable peaks during key seasons  
📦 **Revenue per Unit**: Helped optimize discounting and pricing strategies for profitability  

---

## 📌 Conclusion

This end-to-end analytics project showcases how structured **SQL** queries — combined with basic **Excel** cleanup — can deliver actionable, enterprise-ready insights. From identifying revenue-driving products to analyzing customer behavior and country-level contributions, this project is ideal for stakeholders and hiring managers looking to assess real-world data analysis skills.

> 🎯 Whether optimizing marketing efforts or planning product launches, SQL alone is powerful enough to provide meaningful business direction.

---

## 🤝 Connect with Me

**👨‍💼 Karan Kumar**  
🎓 BBA Student | 💻 Aspiring Data Analyst  
📊 Proficient in SQL • Excel • Power BI  
🔗 [LinkedIn – https://www.linkedin.com/in/contact-karankumar/ <!-- Replace with your real LinkedIn URL -->


⭐ *If you found this helpful, feel free to star the repo and share it with others!*  
🛠️ *Open to collaboration and suggestions — fork it, explore it, improve it!*
