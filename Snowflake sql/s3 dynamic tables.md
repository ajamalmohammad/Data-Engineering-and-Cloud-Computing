
```sql

use warehouse compute_wh;
use role TRAINING_ROLE;
use schema uniq_training.staging;


create or replace table sales (customerid int,product string,quantity int,price float);
create or replace table customers (customerid int,CustomerName string, city string);

insert into sales(customerid,product,quantity,price) values(1,'Shirt',2,20);
insert into sales(customerid,product,quantity,price) values(2,'Hat',1,15);
insert into sales(customerid,product,quantity,price) values(3,'Hat1',5,30);
insert into sales(customerid,product,quantity,price) values(3,'Hat1',5,30);

insert into customers(customerid,CustomerName,city) values(1,'John Doe','New York');
insert into customers(customerid,CustomerName,city) values(2,'Jane Smith','Seattle');
insert into customers(customerid,CustomerName,city) values(3,'Jane1 Smith1','Seattle1');

delete from sales where customerid=2;


CREATE OR REPLACE DYNAMIC TABLE Sales_By_Customer
    LAG = '1 MINUTE'
    WAREHOUSE=compute_wh
AS
SELECT 
  c.CustomerName,
  SUM(s.Quantity * s.Price) AS TotalSales
FROM sales s
JOIN customers c ON s.CustomerID = c.CustomerID
GROUP BY c.CustomerName;


alter dynamic table Sales_By_Customer refresh; 
select * from Sales_By_Customer;


--- Full refresh ETL 
delete from final_table;

insert into final_table
SELECT 
  c.CustomerName,
  SUM(s.Quantity * s.Price) AS TotalSales
FROM sales s
JOIN customers c ON s.CustomerID = c.CustomerID
GROUP BY c.CustomerName;



--- incremental 


-- backlog loading maintenace 


insert into final_table
SELECT 
  c.CustomerName,
  SUM(s.Quantity * s.Price) AS TotalSales
FROM sales s
JOIN customers c ON s.CustomerID = c.CustomerID
where batch_id> current_date -1 , sequence_id 
GROUP BY c.CustomerName;

```