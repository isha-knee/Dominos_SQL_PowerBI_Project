# Dominos Sales Report Analysis (MySQL and Power BI)

![Dominos logo](https://github.com/isha-knee/Dominos_SQL_PowerBI_Project/blob/main/logo.png)

## Overview
This project presents a comprehensive sales analysis for Domino’s Pizza, using SQL for data preparation and Power BI for building interactive visualizations. The aim is to identify key sales trends and product performance insights to support strategic decision-making.

## Objective

The objective of this project is to analyze Domino’s sales data to uncover meaningful business insights through SQL and Power BI. This includes:

-Identifying daily and monthly order trends, understanding product performance by category and size

-Evaluating top and bottom-selling items based on revenue, quantity sold, and total orders

-The final dashboard serves as a decision-support tool to help improve sales strategy, product mix, and operational efficiency.

## Dataset

The data for this project is sourced from Kaggle dataset:

- **Dataset Link:** [Pizza Sales](https://www.kaggle.com/datasets/purusachdeva/dominos-pizza-sales)

## Dashboard Highlights
The Power BI dashboard provides a clear, interactive overview of Domino’s sales performance, with visuals designed to support data-driven decisions. Key highlights include:

-📅Sales Trends Analysis: Displaying daily and monthly trends in total orders and revenue to monitor business growth and seasonality.

-📦Product Performance Breakdown: Offers insights into customer preferences.

-🏆 Top & Bottom Performers: Helps identify high-performing products and underperforming items that may need promotion or replacement.

*These visuals help stakeholders understand demand patterns, optimize inventory, and tailor promotions based on product performance.*

## Dashboard
![Domino's Power BI Dashboard](https://github.com/isha-knee/Dominos_SQL_PowerBI_Project/blob/main/Screenshot%202025-04-30%20211600.png)

![Domino's Power BI Dashboard](https://github.com/isha-knee/Dominos_SQL_PowerBI_Project/blob/main/Screenshot%202025-04-30%20211619.png)

## Business Problems and Solutions

### 1. Total Revenue:

```sql
select sum(total_price) as Total_Revenue from pizza_sales;
```

### 2. Average Order Value:
```sql
select sum(total_price)/ count(distinct order_id) as Average_Order_Value 
from pizza_sales;
```

### 3. Total Pizza Sold:
```sql
select sum(quantity) as Total_pizza_sold from pizza_sales;
```

### 4. Total Orders:
```sql
select count(distinct order_id) as Total_Orders from pizza_sales;
```

### 5. Average Pizza per Order:
```sql
select cast(cast(sum(quantity) as decimal(10,2)) / cast(count(distinct order_id) as decimal(10,2)) as decimal(10,2)) as Avg_pizza_per_Order from pizza_sales;
```

### 6. Daily Trend for Total Orders: Distinct no of orders, over the weekdays (Mon-Sun)
```sql
select datename(dw, order_date) as order_day, count(distinct order_id) as Total_orders 
from pizza_sales
group by datename(dw, order_date)
```

### 7. Monthly Trend for Total Orders: Peak of months of orders being placed
```sql
select datename(month, order_date) as order_month, count(distinct order_id) as Total_orders
from pizza_sales
group by datename(month, order_date)
order by Total_orders desc
```

### 8. Percentage of Sales by Pizza Category: Overall sales contribution based on category of pizza
```sql
select pizza_category, round(sum(total_price) * 100 / (select sum(total_price) from pizza_sales),2) as Total_sales
from pizza_sales
group by pizza_category
```

### 9. Percentage of Sales by Pizza Size: 
```sql
select pizza_size, round(sum(total_price) * 100 / (select sum(total_price) from pizza_sales),2) as percentage_sales
from pizza_sales
group by pizza_size
order by percentage_sales desc;
```

### 10. Total Orders by Pizza Category:
```sql
select pizza_category, sum(quantity) as no_of_pizza_sold
from pizza_sales
group by pizza_category
order by no_of_pizza_sold desc;
```

### 11.	Top 5 Pizza’s by Revenue:
```sql
select top 5 pizza_name, sum(total_price) as Total_revenue
from pizza_sales
group by pizza_name
order by Total_revenue desc
```

### 12.	Bottom 5 Pizza’s by Revenue:
```sql
select top 5 pizza_name, sum(total_price) as Total_revenue
from pizza_sales
group by pizza_name
order by Total_revenue asc
```

### 13.	Top 5 Pizza’s by Qty:
```sql
select top 5 pizza_name, sum(quantity) as Total_Qty
from pizza_sales
group by pizza_name
order by Total_Qty desc
```

### 14.	Bottom 5 Pizza’s by Qty:
```sql
select top 5 pizza_name, sum(quantity) as Total_Qty
from pizza_sales
group by pizza_name
order by Total_Qty asc
```

### 15.	Top 5 Pizza’s by Total Orders:
```sql
select top 5 pizza_name, count(distinct order_id) as Total_Orders
from pizza_sales
group by pizza_name
order by Total_Orders desc
```

### 16.	Bottom 5 Pizza’s by Total Orders:
```sql
select top 5 pizza_name, count(distinct order_id) as Total_Orders
from pizza_sales
group by pizza_name
order by Total_Orders asc
```

## 📈 Key Learnings

-Applied SQL techniques for real-world data transformation and analysis

-Designed insight-driven dashboards using DAX and Power BI visual elements

-Gained understanding of sales performance metrics and business KPIs


