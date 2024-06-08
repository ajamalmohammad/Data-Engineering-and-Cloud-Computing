
## Recap : Session 3

### Clarifications on weekday hands-on
- Commands: AND, IN, OR, NOT, DESC, ASC, ORDER BY, GROUP BY, TOP, BETWEEN, LIKE, (Aggregative functions: MIN, MAX, AVG, COUNT, SUM).

# Introduction to SQL Joins
## INNER JOIN

- The "INNER JOIN" keyword selects records that have matching values in both tables.
- "JOIN" and "INNER JOIN" will return the same result.  "INNER" is the default join type for "JOIN", so when you write "JOIN" the parser actually writes "INNER JOIN".

![SQL INNER JOIN](https://www.w3schools.com/sql/img_inner_join.png)

### ****Syntax****

****SELECT**** table1.column1,table1.column2,table2.column1,....  
****FROM**** table1   
****INNER JOIN**** table2  
****ON**** table1.matching_column = table2.matching_column;

Here,

- ****table1:**** First table.
- ****table2****: Second table
- ****matching_column****: Column common to both the tables.

### Left Outer Join
- LEFT JOIN returns all the rows of the table on the left side of the join and matches rows for the table on the right side of the join.
- For the rows for which there is no matching row on the right side, the result-set will contain __null__. 
- LEFT JOIN is also known as LEFT OUTER JOIN.

![sql left join visual representation](https://i.stack.imgur.com/VkAT5.png)

### ****Syntax****

****SELECT**** table1.column1,table1.column2,table2.column1,....  
****FROM**** table1   
****LEFT JOIN**** table2  
****ON**** table1.matching_column = table2.matching_column;

Here,

- ****table1:**** First table.
- ****table2****: Second table
- ****matching_column****: Column common to both the tables.

## ****SQL RIGHT JOIN****

- Right Join returns all the rows of the table on the right side of the join and matching rows for the table on the right side of the join.
- It is very similar to LEFT JOIN For the rows for which there is no matching row on the left side, the result-set will contain __null__. 
- RIGHT JOIN is also known as RIGHT OUTER JOIN. 

### ****Syntax:****

The syntax of RIGHT JOIN in SQL is:

****SELECT**** table1.column1,table1.column2,table2.column1,....  
****FROM**** table1   
****RIGHT JOIN**** table2  
****ON**** table1.matching_column = table2.matching_column;

![sql right join visual representation](https://media.geeksforgeeks.org/wp-content/uploads/20220515095048/join.jpg)

Here,

- ****table1****: First table.
- ****table2****: Second table
- ****matching_column****: Column common to both the tables.

****Note****: We can also use ****RIGHT OUTER JOIN**** instead of RIGHT JOIN, both are the same. 




## ****SQL FULL JOIN****

- Full Join creates the result-set by combining results of both LEFT JOIN and RIGHT JOIN. The result-set will contain all the rows from both tables. 
- For the rows for which there is no matching, the result-set will contain __NULL__ values.
- Full Join can also be called as Full Outer Join

![visual representation of sql full join](https://i.stack.imgur.com/3Ll1h.png)

### ****Syntax****

The syntax of SQL FULL JOIN is:

****SELECT**** table1.column1,table1.column2,table2.column1,....  
****FROM**** table1   
****FULL JOIN**** table2  
****ON**** table1.matching_column = table2.matching_column; 

Here,

- ****table1****: First table.
- ****table2****: Second table
- ****matching_column****: Column common to both the tables.
### Self Join
- Joins in SQL, a self join is a regular join that is used to join a table with itself. 
- It basically allows us to combine the rows from the same table based on some specific conditions.
- It is very useful and easy to work with, and it allows us to retrieve data or information which involves comparing records within the same table.

****Syntax:****

> SELECT columns
> FROM table AS alias1
> JOIN table AS alias2 ON alias1.column = alias2.column;

****Explnation:****

- SELECT columns: With the help of this we specify the columns you want to retrieve from the self-joined table.
- FROM table AS alias1: With the help of this we specify the name of the table you want to join with itself.
- JOIN table AS alias2: In this we use the JOIN keyword to show that we are performing a self join on the same table.

****Example:****

Let’s use an illustration to further understand how the self-join functions. Assume that we have a table called “GFGemployees” with the columns employee_id, employee_name, and manager_id. Each employee in the company is assigned a manager, and using the manager-ids, we can identify each employee. We need to extract the list of employees along with the names of their managers because the manager_id column contains the manager ID for each employee

****Step 1:**** First, we need to create the “GFGemployees” table with following query.

CREATE TABLE GFGemployees(employee_id   
INT PRIMAR KEY, employee_name VARCHAR(50), manager_id INT);  

****Step 2:**** Now we will add data into the ‘GFGemployees’ table using INSERT INTO statement:

INSERT INTO GFGemployees (employee_id, employee_name, manager_id)  
VALUES  (1, 'Zaid', 3),  (2, 'Rahul', 3),  (3, 'Raman', 4),    
(4, 'Kamran', NULL),  (5, 'Farhan', 4);  

****Output:****

|             |               |            |
| ----------- | ------------- | ---------- |
| employee_id | employee_name | manager_id |
| 1           | Zaid          | 3          |
| 2           | Rahul         | 3          |
| 3           | Raman         | 4          |
| 4           | Kamran        | NULL       |
| 5           | Farhan        | 4          |

****Step 3: Explanation and implementation of Self Join****

Now, we need to perform self join on the table we created i.e.”GFGemployees” in order to retrieve the list of employees and their corresponding managers name and for that we need to write a query, where we will create two different aliases for the “GFGemployees” table as “e” which will represent the GFG employee’s information and “m” will represent the manager’s information. This way by joining the table with itself using the manager_id and employee_id columns, we can generate relationship between employees and their managers.

****Step 4: Query for Self-join****

SELECT e.employee_name AS employee,  
m.employee_name AS managerFROM   
GFGemployees AS eJOIN GFGemployees   
AS m ON e.manager_id = m.employee_id;  
  
  

****Output:****

The resultant table after performing self join will be as follows:

|          |         |
| -------- | ------- |
| employee | manager |
| Zaid     | Raman   |
| Rahul    | Raman   |
| Raman    | Kamran  |
| Farhan   | Kamran  |

### Product Join/Cartesian Product Join/Cross Join
In a CARTESIAN JOIN there is a join for each row of one table to every row of another table.
This usually happens when the matching column or WHERE condition is not specified.

- In the absence of a WHERE condition the CARTESIAN JOIN will behave like a CARTESIAN PRODUCT . i.e., the number of rows in the result-set is the product of the number of rows of the two tables.
- In the presence of WHERE condition this JOIN will function like a INNER JOIN.
- Generally speaking, Cross join is similar to an inner join where the join-condition will always evaluate to True


![Sql cross join syntax](https://www.w3resource.com/w3r_images/cross-join-round.png)  

**Syntax:**

SELECT * 
FROM table1 
CROSS JOIN table2;

### SubQuery


- Defined as Query within another query. In other words we can say that a Subquery is a query that is embedded in WHERE clause of another SQL query.
- You can place the Subquery in a number of SQL clauses: [WHERE](https://www.geeksforgeeks.org/sql-where-clause/) clause, [HAVING](https://www.geeksforgeeks.org/having-vs-where-clause/) clause, FROM clause. Subqueries can be used with SELECT, UPDATE, INSERT, DELETE statements along with expression operator. It could be equality operator or comparison operator such as =, >, =, <= and Like operator.
- A subquery is a query within another query. The outer query is called as **main query** and inner query is called as **subquery**.
- The subquery generally executes first when the subquery doesn’t have any **co-relation** with the **main query**, when there is a co-relation the parser takes the decision **on the fly** on which query to execute on **precedence** and uses the output of the subquery accordingly.
- Subquery must be enclosed in parentheses.
- Subqueries are on the right side of the comparison operator.
- [ORDER BY](https://www.geeksforgeeks.org/sql-order-by/) command **cannot** be used in a Subquery. [GROUPBY](https://www.geeksforgeeks.org/sql-group-by/) command can be used to perform same function as ORDER BY command.
- Use single-row operators with singlerow Subqueries. Use multiple-row operators with multiple-row Subqueries.

**Syntax:** There is not any general syntax for Subqueries. However, Subqueries are seen to be used most frequently with SELECT statement as shown below:

SELECT column_name
FROM table_name
WHERE column_name _expression operator_ 
    ( SELECT COLUMN_NAME  from TABLE_NAME   WHERE ... );




