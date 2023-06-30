## Sales Insights Data Analysis Project

1. Import SQL database dump file named as 'db_dump.sql' in your DataBase.  

### Data Analysis Using SQL

use sales;
show tables;

# 1.Show all customer and transaction records

select * from customers;
select * from transactions;

# 2.Show total number of customers and transactions 

select count(*) from sales.customers;
select count(*) from sales.transactions;

# 3.Show transactions for Chennai market (market code for chennai is Mark001
select * from transactions where market_code='Mark001';

# 4.Show distinct product codes that were sold in chennai

select distinct product_code from transactions where market_code='Mark001';

# 5.Show transactions where currency is US dollar

select * from transactions where currency='USD';

# 6.Show transactions in 2020 join by date table

select * from transactions 
inner join date 
on transactions.order_date=date.date
where date.year='2020';
 
 # 7.Show total revenue in year 2020

select sum(transactions.sales_amount) as "Total Revenue" from transactions 
inner join date 
on transactions.order_date=date.date
where date.year='2020';

# 8.Show total revenue in year 2020, January Month

select sum(transactions.sales_amount) as "Total Revenue in Jan 2020" 
from transactions 
inner join date 
on transactions.order_date=date.date
where date.year='2020' and date.month_name="January";

# 9.Show total revenue in year 2020 in Chennai

select sum(transactions.sales_amount) as "Total Revenue" from transactions 
inner join date 
on transactions.order_date=date.date
where date.year='2020' and transactions.market_code="Mark001";

# 10. Avarage Revenue 

select round(avg(transactions.sales_amount) ,2) as "Avarage Revenue" 
from transactions 
inner join date 
on transactions.order_date=date.date
where date.year='2020' and transactions.market_code="Mark001";

Data Analysis Using Power BI
============================

1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`

