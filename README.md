# 🛍️ Sales Dataset

## 📘 Overview

This dataset contains detailed sales transaction records for various products across multiple regions, channels, and customer types. It can be used for sales analysis, business forecasting, dashboard creation, and machine learning applications such as revenue prediction or customer segmentation.

## 📂 File Information

* **Filename:** `sales.csv`
* **Total Rows:** 2,738
* **Total Columns:** 8
* **File Format:** CSV (Comma-Separated Values)
* **Encoding:** UTF-8

## 🧩 Columns Description

| Column Name       | Description                                                          |
| ----------------- | -------------------------------------------------------------------- |
| **Date**          | Transaction date in YYYY-MM-DD format.                               |
| **Product**       | Name of the product sold (e.g., Almonds, Cashews, Walnuts).          |
| **Region**        | Geographic region where the sale occurred (e.g., East, West, South). |
| **Units_Sold**    | Number of units sold for the transaction.                            |
| **Revenue**       | Total revenue generated (in local currency).                         |
| **Salesperson**   | Name of the salesperson responsible for the sale.                    |
| **Channel**       | Mode of sale — either Online or Offline.                             |
| **Customer_Type** | Type of customer — typically Retail or Wholesale.                    |

## 🧠 Example Preview

| Date       | Product | Region | Units_Sold | Revenue | Salesperson | Channel | Customer_Type |
| ---------- | ------- | ------ | ---------- | ------- | ----------- | ------- | ------------- |
| 2022-01-01 | Almonds | West   | 37         | 295.16  | Meena       | Online  | Retail        |
| 2022-01-01 | Raisins | East   | 14         | 218.39  | Raj         | Online  | Wholesale     |
| 2022-01-01 | Walnuts | West   | 45         | 642.71  | Anita       | Online  | Retail        |


## 📊 Potential Use Cases

use mnp;        

select * from `Sales data`;
rename table sales to S2022;
select *from sales;

#1.Write a query to display total sales revenue for each year.
#(Use the Date column to group by year)

select year(date),sum(Revenue) as total_revenue
from sales
group by year(date);

#2.Retrieve the top 3 products based on total units sold across all 3 years.

select Product,sum(Units_Sold) as total_sold 
from sales
group by Product 
order by  total_sold desc
limit 3;

#3.Display year-wise revenue generated from each Sales Channel (Online vs Offline).
select year(date),Channel,sum(Revenue) as total_revenue
from sales
group by year(date),Channel;

#4.List the top-performing salesperson for each year based on revenue.
select salesperson, years ,sum(Revenue) as total_revenue
from sales
group by years,salesperson;
select * from sales;

alter table sales add column years int;
update sales
set years=year(date);

set sql_safe_updates=0;

#5.Write a query to show total revenue by region, sorted from highest to lowest.

select Region,sum(Revenue) as total_revenue 
from sales 
group by Region 
order by total_revenue desc;

#6.Retrieve unique Customer Types and the count of orders for each type.
select * from sales;
select Customer_Type,count(Units_Sold) as total_order 
from sales 
group by Customer_Type;

#7.Find the product with the maximum revenue generated in 2023.
select years,Product,max(Revenue) as max_revenue  
from sales 
group by Product,years
having years = '2023'
order by max_revenue desc;

select * from sales;
alter table sales add column months int;
update sales
set months= month(date);


#8.Show monthly sales trend of 2024
#(Extract month from Date column and sum revenue)

select years,months,sum(Revenue) as total_reveneu
from sales 
group by months,years
having years='2024';

#9.Display total units sold for each product in North region only.

select Product,sum(Units_Sold) as total_sold
from sales 
where Region ='North'
group by Product;

#10. Count the number of Online vs Offline orders in the entire dataset.

select Channel,count(Units_Sold) as total_order 
from sales
group by Channel;




## ✍️ Author

Created and curated by [Your Name].
Feel free to contribute or report issues in the repository.

---

**Tags:** `sales` · `retail` · `analytics` · `forecasting` · `business-intelligence`
