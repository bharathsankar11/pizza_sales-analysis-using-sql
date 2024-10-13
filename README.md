----Table View---- 
select*from pizza_sales;
----Retrieve the total number of orders placed----
select count(distinct order_id) as 'Total Orders' from pizza_sales;
----Calculate the total revenue generated from pizza sales----
select cast(sum(quantity*total_price) as decimal(10,2)) as 'Total Revenue' from pizza_sales;
----Identify the highest-priced price----
select pizza_name,max(total_price) from pizza_sales;
----Identify the most common pizza size ordered----
select pizza_size,count(distinct order_id) as 'No of Orders',sum(quantity) as 'Total Quantity Ordered' from pizza_sales 
group by pizza_size
order by count(distinct order_id) desc;
----List the top 5 most ordered pizza types along with their quantities----
select pizza_name,sum(quantity) as 'Total Ordered' from pizza_sales
group by pizza_name
order by sum(quantity) desc
limit 5;
----Find the category-wise distribution of pizzas----
select pizza_category,count(distinct order_id) as 'No of pizzas' from pizza_sales
group by pizza_category
order by 'No of pizzas';
----Determine the top 3 most ordered pizza types based on revenue----
select pizza_name,sum(quantity*total_price) as 'Revenue from pizza' from pizza_sales
group by pizza_name
order by 'Revenue from pizza'
limit 3;
----Calculate the average number of pizzas ordered per day----
with cte as(
select order_date as 'Date',sum(quantity) as 'Total Pizza Ordered that day' from pizza_sales
group by order_date
)
select avg([Total Pizza Ordered that day]) as 'Avg Number of pizzas ordered per day' from cte;
----Retrieve all orders placed between 20-02-2015 and 20-10-2015-----
select order_id as 'Order',order_date from pizza_sales where order_date between '20-02-2015' and '20-10-2015';
