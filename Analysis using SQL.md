# Superstore Sales Analysis Using SQL

**Project Title:** Superstore Sales & Profitability Analysis Using SQL  
**Done By:** Shivanand Metri

---

## 1. Problem Statement

Retail organizations collect large volumes of transactional data, but raw data alone does not provide business value unless it is properly analyzed. The Superstore dataset contains detailed information about customer orders, products, regions, sales, discounts, and profits.

The main problem is to **identify sales patterns, profitability drivers, customer behavior, and operational inefficiencies** using SQL-based data analysis. Without this analysis, the business risks offering excessive discounts, continuing loss-making products, and misallocating resources across regions and customer segments.

### Objective
To use SQL queries on the Superstore dataset to:
- Evaluate overall business performance
- Identify profitable and loss-making areas
- Understand customer and product behavior
- Support data-driven decision-making

---

## 2. Dataset Description

The analysis is performed on a **single Superstore table** with all column names in **lowercase**.

### Key Columns
- order_id
- order_date
- ship_date
- ship_mode
- customer_id
- customer_name
- segment
- country
- region
- state
- city
- category
- sub_category
- product_name
- sales
- quantity
- discount
- profit

---

## 3. Business Questions (15)

### Sales & Profit Performance
1. What are the total sales and total profit of the Superstore?
2. How do sales and profit vary by year?
3. Which regions generate the highest sales and profit?
4. Which states contribute the most to overall sales?
5. What are the monthly sales trends?

### Product Analysis
6. Which product categories are most profitable?
7. Which sub-categories are consistently loss-making?
8. What are the top 10 products by total sales?
9. Which products have the highest profit margins?

### Customer Analysis
10. Which customer segment generates the highest revenue?
11. Who are the top 10 customers by sales value?
12. What is the average order value per customer?

### Discount & Operations
13. How does discount level impact profitability?
14. What is the average profit per order?
15. Which shipping mode is used most frequently and is most profitable?

---

## 4. SQL Methods and Queries

### 1. Total Sales and Profit
```sql
select 
    sum(sales) as total_sales,
    sum(profit) as total_profit
from superstore;
```

### 2. Sales and Profit by Year
```sql
select 
    year(order_date) as order_year,
    sum(sales) as total_sales,
    sum(profit) as total_profit
from superstore
group by year(order_date)
order by order_year;
```

### 3. Sales and Profit by Region
```sql
select 
    region,
    sum(sales) as total_sales,
    sum(profit) as total_profit
from superstore
group by region
order by total_sales desc;
```

### 4. Top States by Sales
```sql
select 
    state,
    sum(sales) as total_sales
from superstore
group by state
order by total_sales desc;
```

### 5. Monthly Sales Trend
```sql
select 
    year(order_date) as year,
    month(order_date) as month,
    sum(sales) as total_sales
from superstore
group by year, month
order by year, month;
```

### 6. Sales and Profit by Category
```sql
select 
    category,
    sum(sales) as total_sales,
    sum(profit) as total_profit
from superstore
group by category;
```

### 7. Loss-Making Sub-Categories
```sql
select 
    sub_category,
    sum(profit) as total_profit
from superstore
group by sub_category
having sum(profit) < 0
order by total_profit;
```

### 8. Top 10 Products by Sales
```sql
select 
    product_name,
    sum(sales) as total_sales
from superstore
group by product_name
order by total_sales desc
limit 10;
```

### 9. Products with Highest Profit Margin
```sql
select 
    product_name,
    sum(profit) / sum(sales) as profit_margin
from superstore
group by product_name
order by profit_margin desc;
```

### 10. Sales by Customer Segment
```sql
select 
    segment,
    sum(sales) as total_sales
from superstore
group by segment;
```

### 11. Top 10 Customers by Sales
```sql
select 
    customer_name,
    sum(sales) as total_sales
from superstore
group by customer_name
order by total_sales desc
limit 10;
```

### 12. Average Order Value per Customer
```sql
select 
    customer_id,
    avg(sales) as avg_order_value
from superstore
group by customer_id;
```

### 13. Discount Impact on Profit
```sql
select 
    discount,
    sum(profit) as total_profit
from superstore
group by discount
order by discount;
```

### 14. Average Profit per Order
```sql
select 
    avg(profit) as avg_profit_per_order
from superstore;
```

### 15. Shipping Mode Analysis
```sql
select 
    ship_mode,
    count(order_id) as total_orders,
    sum(profit) as total_profit
from superstore
group by ship_mode
order by total_orders desc;
```

---

## 5. Analysis Summary

- **Overall Performance:** The Superstore achieves strong revenue, but profit margins vary significantly across products and regions.
- **Regional Performance:** A few regions and states dominate sales contribution, while others underperform or generate losses.
- **Product Insights:** Technology and Office Supplies categories tend to be more profitable, whereas certain Furniture sub-categories consistently incur losses.
- **Customer Insights:** Consumer and Corporate segments contribute the majority of revenue. A small group of customers accounts for a large portion of total sales.
- **Discount Strategy:** Higher discounts are strongly associated with reduced or negative profits, highlighting the need for controlled discounting.
- **Operational Efficiency:** Standard shipping is the most frequently used shipping mode, while faster shipping methods do not always result in higher profit.

---

## 6. Business Recommendations

1. Reduce or restructure discounts on low-margin products.
2. Discontinue or reprice consistently loss-making sub-categories.
3. Focus sales and marketing efforts on high-profit regions and customer segments.
4. Optimize shipping strategies to balance cost and customer satisfaction.
5. Monitor top customers and introduce loyalty programs to retain high-value clients.

---

## 7. Conclusion

This SQL-based Superstore analysis demonstrates how structured querying can convert raw transactional data into actionable business insights. The findings support strategic decision-making in pricing, product management, customer targeting, and operational optimization.

---

**End of Project**
