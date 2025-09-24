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
```
![Gender Distribution](Images/Picture1.png)

### 2. Customer Count per Age Group
```sql
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

```
![Customer Count per Age Group](Images/Picture2.png)

### 3. Total Revenue
```sql
SELECT SUM(total_sale) AS total_revenue
FROM sales;

```
![Total Revenu](Images/Picture3.png)

### 4. Revenue by Category
```sql
SELECT category, SUM(total_sale) AS revenue
FROM sales
GROUP BY category
ORDER BY revenue DESC;

```
![Revenue by Category](Images/Picture4.png)

### 5. Average Order Value (AOV)
```sql
SELECT AVG(total_sale) AS average_order_value
FROM sales;

```
![Average Order Value (AOV)](Images/Picture5.png)

### 6. Top 10 Customers by Sales
```sql
SELECT customer_id, SUM(total_sale) AS total_spent
FROM sales
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 10;

```
![Top 10 Customers by Sales](Images/Picture6.png)

### 7. Top Products by Sales Volume
```sql
SELECT product_id, SUM(quantity) AS total_units_sold
FROM sales
GROUP BY product_id
ORDER BY total_units_sold DESC
LIMIT 10;

```
![Top Products by Sales Volume](Images/Picture8.png)


## 3.0 Project Questions and SQL Solutions
### Q1: Retrieve all columns for sales made on '2022-11-05'
```sql
SELECT *
FROM sales
WHERE sale_date = '2022-11-05';
```
![ Retrieve all columns for sales made on '2022-11-05](Images/Picture9.png)

### Q2: Retrieve transactions where category = 'Clothing' and quantity > 4 in November 2022
```sql
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
```
![Retrieve transactions where category = 'Clothing' and quantity > 4 in November 2022](Images/Picture10.png)

### Q3: Calculate total sales for each category
```sql
SELECT category, SUM(total_sale) AS total_sales
FROM sales
GROUP BY category;
```
![ Calculate total sales for each category](Images/Picture11.png)

### Q4: Average age of customers buying 'Beauty' products
```sql
SELECT AVG(age) AS avg_age
FROM customers c
JOIN sales s ON c.customer_id = s.customer_id
WHERE s.category = 'Beauty';
```
![ Average age of customers buying 'Beauty' products](Images/Picture12.png)

### Q5: Transactions with total sale > 1000
```sql
SELECT *
FROM sales
WHERE total_sale > 1000;
```
![Transactions with total sale > 1000](Images/Picture13.png)

### Q6: Number of transactions by gender per category
```sql
SELECT c.gender, s.category, COUNT(s.transaction_id) AS total_transactions
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
GROUP BY c.gender, s.category;
```
![ Number of transactions by gender per category](Images/Picture10.png)
