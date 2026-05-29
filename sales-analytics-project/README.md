# Sales Analytics Project (SQL + Python)

## Project Overview

This project simulates a real-world sales analytics workflow using Python, SQL, and SQLite.

The objective is to analyze customer orders, product performance, and revenue trends using multi-table SQL analysis and data visualization techniques.

---

## Objectives

- Generate synthetic business data
- Build relational database tables
- Perform SQL JOIN analysis
- Analyze revenue and customer behavior
- Identify top-performing product categories
- Create business visualizations and insights

---

## Tools & Technologies

- Python (Pandas, NumPy, Matplotlib)
- SQL (SQLite)
- Jupyter Notebook

---

## Database Structure

The project contains three relational tables:

### customers
- customer_id
- age
- country

### products
- product_id
- category
- price

### orders
- order_id
- customer_id
- product_id
- quantity

---

##  Project Workflow

### 1. Data Generation

Synthetic sales data was generated using Python and NumPy.

---

### 2. Database Creation

All tables were loaded into SQLite:

python
customers.to_sql("customers", conn, if_exists="replace", index=False)
products.to_sql("products", conn, if_exists="replace", index=False)
orders.to_sql("orders", conn, if_exists="replace", index=False)
3. SQL JOIN Analysis

The project uses multi-table JOIN operations to combine customer, product, and order information.

Example JOIN Query

SELECT o.order_id,
       c.country,
       p.category,
       p.price,
       o.quantity,
       (p.price * o.quantity) AS revenue
FROM orders o
JOIN customers c
ON o.customer_id = c.customer_id
JOIN products p
ON o.product_id = p.product_id;

### Business Analysis
#### Revenue by Product Category
SELECT p.category,
       SUM(p.price * o.quantity) AS revenue
FROM orders o
JOIN products p
ON o.product_id = p.product_id
GROUP BY p.category
ORDER BY revenue DESC;

#### Top Customers
SELECT c.customer_id,
       c.country,
       SUM(p.price * o.quantity) AS total_spent
FROM orders o
JOIN customers c
ON o.customer_id = c.customer_id
JOIN products p
ON o.product_id = p.product_id
GROUP BY c.customer_id, c.country
ORDER BY total_spent DESC
LIMIT 20;

#### Which country contributes the most revenue?
SELECT c.country,
       SUM(p.price * o.quantity) AS total_revenue
FROM orders o
JOIN customers c
ON o.customer_id = c.customer_id
JOIN products p
ON o.product_id = p.product_id
GROUP BY c.country
ORDER BY total_revenue DESC

### Visualization

A bar chart was created to visualize revenue by product category.

### Key Insights
Certain product categories generate significantly higher revenue
Revenue distribution differs across customer groups
Top customers contribute disproportionately to total sales
SQL JOIN operations enable deeper business analysis across multiple tables

### Skills Demonstrated
SQL JOIN operations
Revenue and KPI analysis
Relational database design
Business analytics
Data visualization
Python + SQL workflow

### Future Improvements
Add transaction dates for time-series analysis
Build dashboard using Tableau or Power BI
Add customer segmentation analysis
Introduce machine learning for sales forecasting

## Author Yue Sheng
