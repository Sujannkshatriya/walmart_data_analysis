## Walmart Data Analysis using Python and SQL


```select * from walmart_data;```

```select count(*) from walmart_data```

###--Analyze Payment Methods and Sales

```select payment_method,
count(*) as no_payment,
sum(quantity) as no_of_sold
from walmart_data
group by payment_method;
```

###--Which category received the highest average rating in each branch?

```select
"Branch",
category,
avg(rating) as avg_rate,
rank() over(partition by "Branch" order by avg(rating) desc) as rank
from walmart_data
group by 1,2;
```
###--What is the busiest day of the week for each branch based on transaction volume?

```select
"Branch",
to_char(to_date(date, 'dd/mm/yy'), 'day') as day_name,
count(*) as no_of_transactions
from walmart_data
group by 1,2
order by 1,3 desc
```
###--How many items were sold through each payment method?

```select
payment_method,
count(*) as no_of_payment,
sum(quantity) as no_qty_sold
from walmart_data
group by payment_method
```
###--What are the average, minimum, and maximum ratings for each category ineach city?

```select
"City",
category,
min(rating) as min_rating,
max(rating) as max_rating,
avg(rating) as avg_rating
from walmart_data
group by 1,2
```
###--What is the total profit for each category, ranked from highest to lowest?

```select
category,
sum(total) as total_revenue,
sum(total * profit_margin) as profit
from walmart_data
group by 1
```
###--What is the most frequently used payment method in each branch?

```select 
"Branch",
payment_method,
count(*) as total_transaction
from walmart_data
group by 1,2
```
###--How many transactions occur in each shift (Morning, Afternoon, Evening)across branches?

```select
 case 
     when extract(hour from(time::time))< 12 then 'Morning'
	 when extract(hour from(time::time)) between 12 and 17 then 'Afternoon'
	 else 'Evening'
	end day_time,
count(*)
from walmart_data
gro```up by 1
