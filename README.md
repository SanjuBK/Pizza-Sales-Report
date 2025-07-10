# Pizza Sales Report Project
## Overview
This project analyzes pizza sales data from January 2015 to December 2015 using SQL and Power BI. The goal is to provide actionable business insights by calculating key performance indicators (KPIs), analyzing sales trends, and identifying best and worst-selling pizzas.

## Project Features

### Dashboards
- **Home Screen:**
  - KPIs: Total Revenue, Average Order Value, Total Pizza Sold, Total Orders, Average Pizza per Order
  - Daily and Monthly sales trends
  - Percentage of sales by Pizza Category and Pizza Size
  - Analysis of busiest days and sales performance
  - Navigation buttons for easy access to other pages

- **Best/Worst Sellers Page:**
  - Same KPIs as Home
  - Top 5 pizzas by revenue, quantity, and total orders
  - Bottom 5 pizzas by revenue, quantity, and total orders
  - Insights on best and worst sellers
  - Navigation buttons for Home and Best/Worst Sellers pages

## SQL Queries
The `SQL/pizza_sales_queries.sql` file contains all the SQL queries used to extract and calculate KPIs and trends from the pizza sales dataset.
## Pizza Sales SQL Queries:
A.KPI’s
1. Total Revenue: 
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
¬ 
2. Average pizza value by order: 
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
 
3. Total Pizza sold: 
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
 
4. Total  Orders: 
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
 
5. Average Pizza per Order: 
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;
 
B. Daily Trend of Order: 
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
 
C.  Monthly trend for total orders: 
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date);
 
D. Percentage of sales by Pizza category: 
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
 
E. Percentage of sales by Pizza size: 
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
 
F. Total Pizzas Sold by Pizza Category: 
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
 
G. Top 5 Pizzas by Revenue:
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
 
H. Bottom 5 Pizzas by Revenue: 
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
 
I. Top 5 Pizzas by Quantity: 
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
 
J. Bottom 5 Pizzas by Quantity: 
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
 
K. Top 5 Pizzas by Total Orders: 
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;
 
L. Bottom 5 Pizzas by Total Orders: 
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
 
## Tools Used
- SQL (MySQL / SQL Server)
- Power BI Desktop for dashboard creation

## How to Use
1. Load the pizza sales dataset into your SQL database.
2. Run the SQL queries in `pizza_sales_queries.sql` to generate the necessary aggregated data.
   
4. Open the Power BI dashboard file `PowerBI/PizzaSalesDashboard.pbix` to explore the interactive visualizations.
![Pizza Sales Report - Fri](https://github.com/user-attachments/assets/6bf2c226-7184-4392-a72d-9503caca479e)

![Pizza Sales Report - Best - Worst- Saller](https://github.com/user-attachments/assets/4443c76f-0d95-476b-98c0-52a165917d7b)

## Demo Video: 
https://www.loom.com/share/1d6fbd5db27742708a4225e0324d00f0?sid=00db31ee-e1af-4ddb-85fe-6beaf09a900e

## Contact
Feel free to reach out for questions or collaboration!

---

*This project demonstrates my skills in data querying, aggregation, and visualization, showcasing how data-driven insights can support business decisions in the food retail industry.*
