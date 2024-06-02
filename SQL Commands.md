

## SQL Queries

```SQL

/*create database*/
create database datalabs;



/* create schema */
create schema datalabs_space;

/* create employee table */

create table datalabs.datalabs_space.employee
(
 employee_id integer primary key,
 first_name varchar,
 last_name varchar,
 job_title varchar,
 department_id integer ,
 business_id integer ,
 gender varchar,
 reporting_manager_id integer,
 age integer,
 date_of_joining date,
 annual_salary decimal (10,2),
 country varchar,
 date_of_exit date
);

/* create department table */

create table datalabs.datalabs_space.department 
(
 department_id integer primary key,
 department_name varchar,
 department_location varchar 
 );
 
 
 /* create business unit */

create table datalabs.datalabs_space.business_unit 
(
 business_id integer primary key,
 business_name varchar
 );
 
  /*insert data into  emp table*/
 
insert into datalabs.datalabs_space.employee values 
('2002','kai','le','controls_engineer',101,1,'male','02008',47,'2022-03-23',92368,'united_states');

insert into datalabs.datalabs_space.employee values
('2003','robert','patel','analyst',102,2,'male','02008',58,'2013-10-23',45703,'united_states'),
('2004','cameron','lo','network_administrator',103,3,'male','02014',34,'2019-03-24',83576,'china'),
('2005','harper','castillo','it_systems_architect',103,2,'female','02014',39,'2018-04-07',98062,'united_states' ),	
('2006','harper','dominguez','director',101,2,'female','02006',42,'2005-06-18',175391,'united_states')
;

insert into datalabs.datalabs_space.employee values
('2007','ezra','vu','network_administrator',103,1,'male','02014',62,'2004-04-22',66227,'united_states','2014-02-14');

insert into datalabs.datalabs_space.employee values
('2008','jade','hu','sr_analyst',104,4,'female','02021',58,'2009-06-27',89744,'china'),
('2009','miles','chang','analyst',105,2,'male','02011',62,'1999-02-19',69674,'china'),
('2010','gianna','holmes','system_administrator',103,1,'female','02014',38,'2011-09-09',97630,'united_states'),	
('2011','jameson','thomas','manager',105,4,'male','02006',52,'2015-02-05',105879,'united_states'),
('2012','jameson','pena','systems_analyst',103,1,'male','02014',49,'2003-10-12','40499','united_states'),
('2013','bella','wu','sr_analyst',104,4,'female','02011',63,'2014-08-03',71418,'united_states'),
('2014','jose','wong','director',103,1,'male','02014',45,'2017-11-15',150558,'china'),
('2015','lucas','richardson','manager',106,2,'male','02014',36,'2018-07-22',118912,'united_states'),
('2087','xavier','patel','director',106,4,'male','02014',53,'2021-11-16',187740,'united_states'),
('2088','robert','soto','hris_analyst',107,3,'male','02091',47,'2008-09-10',72384,'brazil'),
('2089','nevaeh','jiang','sr_manager',106,2,'female','02014',45,'2016-08-05',143318,'china'),
('2090','chloe','reyes','director',107,4,'female','02091',45,'2008-06-18',191304,'united_states')
;

insert into datalabs.datalabs_space.employee values
('2091','lucy','edwards','director',107,4,'female','02091',33,'2015-03-16',175875,'united_states','2022-05-16')
;

 
 /* insert data into department table*/

insert into datalabs.datalabs_space.department values -- add dept_location(b1,b2,d5) 
(101,'engineering','B1'),
(102,'sales','B2'),
(103,'it','B3'),
(104,'accounting','B2'),
(105,'finance','B3'),
(106,'marketing','B1'),
(107,'human_resources','B1')
;


 
 /*into values to business table*/
 
 insert into datalabs.datalabs_space.business_unit values
(1,'manufacturing'),
(2,'corporate'),
(3,'research_&_development'),
(4,'specialty_products')
;


select, insert update, delete (80% ) - DML- ins,upd del, 
dql- Sel


/* selecting all the columns from the table */
select * from datalabs.datalabs_space.employee;

/* selecting specific columns from the table */
select employee_id,first_name from datalabs.datalabs_space.employee
;

/* select columns filtering some specific records */
select * from datalabs.datalabs_space.employee where employee_id=2003

/* select columns filtering some specific records - more than 1 parameter */
select * from datalabs.datalabs_space.employee where employee_id in (2003,2012);
;
/*inserting a record into the table */
insert into datalabs.datalabs_space.employee values
('2007','ezra','vu','network_administrator',103,1,'male','02014',62,'2004-04-22',66227,'united_states','2014-02-14');


/*updating a record into the table */
update datalabs.datalabs_space.employee 
set department_id=109
where department_id=105
;

/*delete a record from the table */
select *  from datalabs.datalabs_space.employee 
where employee_id=2008
;

/*delete all records from the table */
delete from datalabs.datalabs_space.employee 
;

/*sorting the data based on field  - asc by default*/
select * from datalabs.datalabs_space.employee order by employee_id 
;

/*sorting the data based on field  - asc by default*/
select * from datalabs.datalabs_space.employee order by department_id asc, business_id asc
;

/*understanding AND,OR,NOT in SQL  */
select * from datalabs.datalabs_space.employee where employee_id=2003 or 
employee_id=2012 
;

select * from datalabs.datalabs_space.employee where department_id=101 and business_id=2
;

select * from datalabs.datalabs_space.employee where department_id not in (103,102)
select * from datalabs.datalabs_space.employee where department_id !=103;
;


distinct, GROUP BY, TOP, BETWEEN, LIKE, (Aggregative functions: MIN, MAX, AVG, COUNT, SUM).


/* distinct data in SQL */
select distinct department_id from datalabs.datalabs_space.employee
;

select distinct business_id/*, department_id */  from datalabs.datalabs_space.employee order by department_id asc
;

/* Group by - grouping the data*/
select department_id,count(*) as Number_of_Employees,sum(annual_salary) as total_salary, min(age) as young_person
from datalabs.datalabs_space.employee group by department_id
;

/* between operator */
select * from datalabs.datalabs_space.employee as T1 where T1.age between 30 and 55 order by age
;

/*relational operator in SQL */
select * from datalabs.datalabs_space.employee as T1 where T1.age>=30 and T1.age<=55 order by age
;


/* TOP command Alternate commands - Limit */
select * from datalabs.datalabs_space.employee /* order by annual_salary desc */  limit 4
;

/* Like Pattern in SQL
% - it natches any position of the value
_ it matches the exact position of the value

*/
select * from datalabs.datalabs_space.employee where first_name like '%a_'
;

/************************** Joins ****  */
select * from datalabs.datalabs_space.department;

/*Joins - Joining tables based on matching conditions */

/*inner join  */
select T1.first_name,T1.last_name,T2.department_name from datalabs.datalabs_space.employee as T1 
inner join datalabs.datalabs_space.department T2
on T1.department_id = T2.department_id 


/* left join */

select T1.first_name,T1.last_name,T1.department_id,T2.department_name 
from datalabs.datalabs_space.employee as T1 
Left join datalabs.datalabs_space.department T2
on T1.department_id = T2.department_id 

/* right join */

select T1.first_name,T1.last_name,T1.department_id,T2.department_name 
from datalabs.datalabs_space.employee as T1 
right outer join datalabs.datalabs_space.department T2
on T1.department_id = T2.department_id 

/* Full outer join j */

select T1.first_name,T1.last_name,T1.department_id,T2.department_name 
from datalabs.datalabs_space.employee as T1 
full outer join datalabs.datalabs_space.department T2
on T1.department_id = T2.department_id 


/* Product Join / Cartesian join/cross join */
select T1.first_name,T1.last_name,T2.department_name from datalabs.datalabs_space.employee as T1 
inner join datalabs.datalabs_space.department T2
on T1.department_id = T2.department_id 


/* Self Join */

select t1.first_name,t1.last_name, concat(t2.first_name,' ',t2.last_name) as manager_name 
from datalabs.datalabs_space.employee T1
inner join datalabs.datalabs_space.employee T2
on T1.reporting_manager_id=T2.employee_id


/*** Handling case sensitive ****/
select * from datalabs.datalabs_space.employee where upper(first_name)='KAI';
select * from datalabs.datalabs_space.employee where lower(first_name)='kai';
```
