# SQL Retail Sales Analysis Project  

## 📑 Outline  
1. Introduction  
2. Exploratory Analysis  
3. Project Questions and SQL Solutions  
4. Conclusion  
5. Recommendations  

---

## 1.0 Introduction  
This project conducts a detailed analysis of a **Retail Sales Dataset** to derive actionable insights using SQL.  
The dataset contains customer transactions with details such as transaction ID, sale date, customer demographics, product categories, quantity, price per unit, and total sales value.  

Key metrics explored:  
- Gender distribution of customers  
- Customer count per age group  
- Total revenue and revenue by category  
- Average Order Value (AOV)  
- Top 10 customers by sales  
- Top 10 products by sales volume  

Project workflow:  
1. **Database Setup** – Creating and populating a retail sales database  
2. **Data Cleaning** – Removing missing/null records  
3. **Exploratory Data Analysis (EDA)** – Exploring dataset characteristics  
4. **Business Analysis** – Answering business questions with SQL  

Tool used: **MySQL Workbench**  

---

## 2.0 Exploratory Analysis  

### 1. Gender Distribution of Customers  
```sql
SELECT gender, COUNT(customer_id) AS total_customers
FROM customers
GROUP BY gender;
![Sales by Region](sales_by_region.png)

SELECT 
  CASE 
    WHEN age BETWEEN 18 AND 25 THEN '18-25'
    WHEN age BETWEEN 26 AND 35 THEN '26-35'
    WHEN age BETWEEN 36 AND 45 THEN '36-45'
    WHEN age BETWEEN 46 AND 55 THEN '46-55'
    ELSE '56+'
  END AS age_group,
  COUNT(customer_id) AS total_customers
FROM customers
GROUP BY age_group;
![Sales by Region](sales_by_region.png)

### 2.Customer Count per Age Group 
SELECT SUM(total_sale) AS total_revenue
FROM sales;
![Sales by Region](sales_by_region.png)

SELECT category, SUM(total_sale) AS revenue
FROM sales
GROUP BY category
ORDER BY revenue DESC;
![Sales by Region](sales_by_region.png)

SELECT AVG(total_sale) AS average_order_value
FROM sales;
![Sales by Region](sales_by_region.png)

SELECT customer_id, SUM(total_sale) AS total_spent
FROM sales
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 10;
![Sales by Region](sales_by_region.png)

SELECT product_id, SUM(quantity) AS total_units_sold
FROM sales
GROUP BY product_id
ORDER BY total_units_sold DESC
LIMIT 10;
![Sales by Region](sales_by_region.png)
