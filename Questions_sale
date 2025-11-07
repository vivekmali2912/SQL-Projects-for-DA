#1.Write a query to display total sales revenue for each year.
select year(date),
sum(Revenue) as total_revenue 
from sale 
group by year(date);


#2.Retrieve the top 3 products based on total units sold across all 3 years.
select Product,
sum(Units_Sold) as total_Unitsold 
from sale 
group by Product 
order by  total_Unitsold desc 
limit 3;

#3.Display year-wise revenue generated from each Sales Channel. 
select year(date),
Channel,
sum(Revenue) as total_revenue 
from sale 
group by year(date),Channel;

alter table sale add column years int;
update sale
set years=year(date);

set sql_safe_updates=0;
select * from sale;
 

#4.List the top-performing salesperson for each year based on revenue.
select salesperson,
 years,
 sum(Revenue) as total_revenue
 from sale
 group by years,salesperson;
 
 #5.Using a window function, rank the products by revenue within each region.
  select Region,
 Product,
 sum(Revenue) as total_revenue,
 rank() over(partition by Region order by sum(Revenue) desc) as rank_wise_region 
 from sale
 group by Region,Product ;
 
 #6.Display each salesperson’s percent contribution to their region’s total sales using SUM() OVER.
select salesperson, 
region,
sum(revenue) as salesperson_revenue,
sum(sum(revenue)) over (partition by region) as region_total,
round(100 * sum(revenue) / sum(sum(revenue)) over (partition by region),2) as percent_contribution
from sale
group by salesperson, region;

#7.Find the top-performing region based on total revenue using a subquery.
select region,
 sum(revenue) as total_revenue 
 from sale 
 group by region having sum(revenue) = 
 (select max(region_total) from 
 (select region, 
 sum(revenue) as region_total
 from sale  
 group by region  
 ) t);
 
 #8.Create a view that stores average revenue per channel per customer type, and query it to find which combination gives the highest average.
 create view channel_performance as
 select channel,
 customer_type, 
 avg(revenue) as avg_revenue 
 from sale
 group by channel, customer_type;
 
 #9.Find products that perform better in online than offline channels.
 select  product,
sum(case when channel = 'online' then revenue else 0 end) as online_revenue,
sum(case when channel = 'offline' then revenue else 0 end) as offline_revenue 
from sale
group by product
having online_revenue > offline_revenue;


#10.Identify seasonal trends: find average monthly revenue by product to detect seasonality.
select product,
date_format(date,'%y-%m') as y_month,
avg(revenue) as average_revenue 
from sale 
group by product,y_month;
