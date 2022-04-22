---
layout: default
title: SQL Queries
parent: Database
resource: true
desc: "  SQL Queries interview questions and answers."
categories: [SQL Queries]
---

#  SQL Queries
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

--- 

## Find the nth highest salary from employee table.

Finding 3rd highest salary from employee table
```log
select * from employee order by salary desc Limit N-1,1;
```
Example:

```sql
 select distinct salary from employee order by salary desc limit 2, 1;
```


--- 

##  find top n records?
-- Example: finding top 5 records from employee table

```sql
select * from employee order by salary desc limit 5;
```

--- 

##  find the count of employees working in department 'Admin'

```sql
select count(*) from employee where department = 'Admin';
```

--- 

##  fetch department wise count employees sorted by department count in desc order.

```sql
select * from employee;
```


```sql
select department, count(*) as employeecount
from employee
group by department
order by employeecount desc;
```

--- 

##  Write a query to fetch only the first name(string before space) from the FullName column of user_name table.

```sql
select distinct(substring_index(full_names, ' ', 1)) first_name from user_name;
```

--- 

##  find all the employees from employee table who are also managers

```sql
select e1.first_name, e2.last_name from employee e1
join employee e2
on e1.employee_id = e2.manager_id;
```

--- 

##  find all employees who have bonus record in bonus table

```sql
select * from employee;
select * from bonus;

select * from employee where employee_id in (select employee_ref_id from bonus where employee.employee_id = bonus.employee_ref_id);
-- This can also be used using left join.
select e.* from employee e join bonus b on e.employee_id = b.employee_ref_id;
```

--- 

##  find only odd rows from employee table
```sql
select * from employee where MOD(employee_id,2)<>0;
```

--- 

##  fetch first_name from employee table in upper case
```sql
select upper(first_name) as First_Name from employee;
```

--- 

## get combine name (first name and last name) of employees from employee table
```sql
select concat(first_name, ' ' ,last_name) as Name from employee;
```

--- 

##  print details of employee of employee 'Jennifer' and 'James'.
```sql
select * from employee where first_name in ('Jennifer', 'James');
```

--- 

##  fetch records of employee whose salary lies between

```sql
select first_name, last_name, salary from employee where salary between 100000 and 500000;
```

--- 

##  get records of employe who have joined in Jan 2017

```sql
select * from employee;

select first_name, last_name, joining_date from employee where year(joining_date)=2017 and month(joining_date) = 1;
-- incase you have an index on the joining_date column, it will not be used as index is not used when the indexed column is used in a function.
-- So, prefer this query instead which will use a range scan.
select first_name, last_name, joining_date from employee where joining_date between '2017-01-01' and '2017-02-01';
```

--- 

##  get the list of employees with the same salary

```sql
select e1.first_name, e2.last_name from employee e1, employee e2 where e1.salary = e2.salary and e1.employee_id != e2.employee_id;
```

--- 

##  show all departments along with the number of people working there.

```sql
select * from employee;

select department, count(*) as 'Number of employees' from employee
group by department
order by count(department);
```

--- 

##  show the last record from a table.

```sql
select * from employee where employee_id = (select max(employee_id) from employee);
```

--- 

## show the first record from a table.

```sql
select * from employee where employee_id = (select min(employee_id) from employee);
```

--- 

##  get last five records from a employee table.

```sql
(select * from employee order by employee_id desc limit 5) order by employee_id;
```

--- 

##  find employees having the highest salary in each department.

```sql
select first_name, last_name, department, max(salary) as 'Max Salary'from employee group by department order by max(salary);
```

--- 

##  fetch three max salaries from employee table.

```sql
select distinct salary from employee order by salary desc limit 3 ;
-- OR-----
select distinct Salary from employee e1 WHERE 3 >= (SELECT count(distinct Salary) from employee e2 WHERE e1.Salary <= e2.Salary) order by e1.Salary desc;

```
--- 

##  fetch departments along with the total salaries paid for each of them.

```sql
select department, sum(salary) as 'Total Salary' from employee group by department order by sum(salary);
```

--- 

##  find employee with highest salary in an organization from employee table.

```sql
select first_name, last_name from employee where salary = (select max(salary) from employee);
```

--- 

##      Write an SQL query that makes recommendations using the  pages that your friends liked.
-- Assume you have two tables: a two-column table of users and their friends, and a two-column table of
-- users and the pages they liked. It should not recommend pages you already like.

--- 

##  find employee (first name, last name, department and bonus) with highest bonus.

```sql
select first_name, last_name, department, max(bonus_amount) from employee e
join bonus b
on e.employee_id = b.employee_ref_id
group by department
order by max(bonus_amount) desc limit 1;
```

--- 

##  find employees with same salary

```sql
select e1.first_name, e1.last_name, e1.salary from employee e1, employee e2
where e1.salary = e2.salary
and e1.employee_id != e2.employee_id;
```

--- 

##  Write SQL to find out what percent of students attend school on their birthday from attendance_events and all_students tables?

```sql
select * from all_students;
select * from attendance_events;

select (count(attendance_events.student_id) * 100 / (select count(student_id) from attendance_events)) as Percent
from attendance_events
join all_students
on all_students.student_id = attendance_events.student_id
where month(attendance_events.date_event) = month(all_students.date_of_birth)
and day(attendance_events.date_event) = day(all_students.date_of_birth);
```

--- 

##  Given timestamps of logins, figure out how many people on Facebook were active all seven days
--  of a week on a mobile phone from login info table?


```sql
select * from login_info;

select a.login_time, count(distinct a.user_id) from
login_info a
Left join login_info b
on a.user_id = b.user_id
where a.login_time = b.login_time - interval 1 day
group by 1;
```

--- 

##  find out the overall friend acceptance rate for a given date from user_action table.

```sql
select * from user_action;

select count(a.user_id_who_sent)*100 / (select count(user_id_who_sent) from user_action) as percent
from user_action a
join user_action b
on a.user_id_who_sent = b.user_id_who_sent and a.user_id_to_whom = b.user_id_to_whom
where a.date_action = '2018-05-24' and b.action = "accepted";
```

--- 

## How many total users follow sport accounts from tables all_users, sport_accounts, follow_relation?

```sql
select * from all_users;
select * from sport_accounts;
select * from follow_relation;

select count(distinct c.follower_id) as count_all_sports_followers
from  sport_accounts a
join all_users b
on a.sport_player_id = b.user_id
join follow_relation c
on b.user_id = c.target_id;
```

--- 

## How many active users follow each type of sport?

```sql

select b.sport_category, count(a.user_id)
from all_users a
join sport_accounts b
on a.user_id = b.sport_player_id
join follow_relation c
on a.user_id = c.follower_id
where a.active_last_month =1
group by b.sport_category;
```

--- 

## What percent of active accounts are fraud from ad_accounts table?

```sql
select * from ad_accounts;

select count(distinct a.account_id)/(select count(account_id) from ad_accounts where account_status= "active") as 'percent'
from ad_accounts a
join ad_accounts b
on a.account_id = b.account_id
where a.account_status = 'fraud' and b.account_status='active';
```

--- 

##  How many accounts became fraud today for the first time from ad_accounts table?

```sql

select count(account_id) 'First time fraud accounts' from (
select distinct a.account_id, count(a.account_status)
from ad_accounts a
join ad_accounts b
on a.account_id = b.account_id
where b.date = curdate() and a.account_status = 'fraud'
group by account_id
having count(a.account_status) = 1) ad_accnt;
```

--- 

##  determine avg time spent per user per day from user_details and event_session_details

```sql
select * from event_session_details;
select * from user_details;

select date, user_id, sum(timespend_sec)/count(*) as 'avg time spent per user per day'
from event_session_details
group by 1,2
order by 1;

-- or --

select date, user_id, avg(timespend_sec)
from event_session_details
group by 1,2
order by 1;
```

--- 

##   find top 10 users that sent the most messages from messages_detail table.

```sql
select * from messages_detail;

select user_id, messages_sent
from messages_detail
order by messages_sent desc
limit 10;
```

--- 

##  find disctinct first name from full user name from usere_name table

```sql
select * from user_name;

select distinct(substring_index(full_names, ' ', 1)) first_name from user_name;
```

--- 

##  You have a table with userID, appID, type and timestamp. type is either 'click' or 'impression'.

```sql
-- Calculate the click through rate from dialoglog table. Now do it in for each app.
-- click through rate is defined as (number of clicks)/(number of impressions)
select * from dialoglog;

select app_id
, ifnull(sum(case when type = 'click' then 1 else 0 end)*1.0
/ sum(case when type = 'impression' then 1 else 0 end), 0 )AS 'CTR(click through rate)'
from dialoglog
group by app_id;
```

--- 

##  Given two tables Friend_request (requestor_id, sent_to_id, time),  
-- Request_accepted (acceptor_id, requestor_id, time). Find the overall acceptance rate of requests.
-- Overall acceptate rate of requests = total number of acceptance / total number of requests.

```sql
select * from friend_request;
select * from request_accepted;

select ifnull(round(
(select count(*) from (select distinct acceptor_id, requestor_id from request_accepted) as A)
/
(select count(*) from (select distinct requestor_id, sent_to_id from friend_request ) as B), 2),0
) as basic;
```

--- 

##  from a table of new_request_accepted, find a user with the most friends.

```sql
select * from new_request_accepted;

select id from
(
select id, count(*) as count
from (
select requestor_id as id from new_request_accepted
union all
select acceptor_id as id from new_request_accepted) as a
group by 1
order by count desc
limit 1) as table1;
```

--- 

##  from the table count_request, find total count of requests sent and total count of requests sent failed
-- per country

```sql
select * from count_request;

select country_code, Total_request_sent, Total_percent_of_request_sent_failed,
cast((Total_request_sent*Total_percent_of_request_sent_failed)/100 as decimal) as Total_request_sent_failed
from
(
select country_code, sum(count_of_requests_sent) as Total_request_sent,
cast(replace(ifnull(sum(percent_of_request_sent_failed),0), '%','') as decimal(2,1)) as Total_percent_of_request_sent_failed
from count_request
group by country_code
) as Table1;
```

--- 

##  create a histogram of duration on x axis, no of users on y axis which is populated by volume in each bucket
-- from event_session_details

```sql
select * from event_session_details;

select floor(timespend_sec/500)*500 as bucket,
count(distinct user_id) as count_of_users
from event_session_details
group by 1;
```

--- 

## Write SQL query to calculate percentage of confirmed messages from two tables :
-- confirmation_no (phone numbers that facebook sends the confirmation messages to) and
-- confirmed_no (phone numbers that confirmed the verification)


```sql
select round((count(confirmed_no.phone_number)/count(confirmation_no.phone_number))*100, 2)
from confirmation_no
left join confirmed_no
on confirmed_no.phone_number= confirmation_no.phone_number;
```

--- 

##  Write SQL query to find number of users who had 4 or more than 4 interactions on 2013-03-23 date
-- from user_interaction table (user_1, user_2, date).
-- assume there is only one unique interaction between a pair of users per day


```sql
select * from user_interaction;

select table1.user_id, sum(number_of_interactions) as Number_of_interactions
from
(
select user_1 as user_id, count(user_1) as number_of_interactions from user_interaction
group by user_1
union all
select user_2 as user_id, count(user_2) as number_of_interactions from user_interaction
group by user_2) table1
group by table1.user_id
having sum(number_of_interactions) >= 4;
```

--- 

## find the names of all salesperson that have order with samsonic from
-- the table: salesperson, customer, orders


```sql
select s.name
from salesperson s
join orders o on s.id = o.salesperson_id
join customer c on o.cust_id = c.id
where c.name = 'Samsonic';
```

--- 

##  find the names of all salesperson that do not have any order with Samsonic from the table: salesperson, customer, orders


```sql
select s.Name
from Salesperson s
where s.ID NOT IN(
select o.salesperson_id from Orders o, Customer c
where o.cust_id = c.ID
and c.Name = 'Samsonic');
```

--- 

##  Wrie a sql query to find the names of salespeople that have 2  or more orders.

```sql
select s.name as 'salesperson', count(o.number) as 'number of orders'
from salesperson s
join orders o on s.id = o.salesperson_id
group by s.name
having count(o.number)>=2;
```

--- 

##  Given two tables:  User(user_id, name, phone_num) and UserHistory(user_id, date, action),
-- write a sql query that returns the name, phone number and most recent date for any user that has logged in
-- over the last 30 days
-- (you can tell a user has logged in if action field in UserHistory is set to 'logged_on')


```sql
select user.name, user.phone_num, max(userhistory.date)
from user,userhistory
where user.user_id = userhistory.user_id
and userhistory.action = 'logged_on'
and userhistory.date >= date_sub(curdate(), interval 30 day)
group by user.name;
```

--- 

##  Given two tables:  User(user_id, name, phone_num) and UserHistory(user_id, date, action),
-- determine which user_ids in the User table are not contained in the UserHistory table
-- (assume the UserHistory table has a subset of the user_ids in User table). Do not use the SQL MINUS statement.
-- Note: the UserHistory table can have multiple entries for each user_id.

```sql
select user.user_id
from user
left join userhistory
on user.user_id = userhistory.user_id
where userhistory.user_id is null;
```

--- 

## from a given table compare(numbers int(4)), write a sql query that will return the maximum value
-- from the numbers without using
-- sql aggregate like max or min


```sql
select numbers
from compare
order by numbers desc
limit 1;
```

--- 

##  find out how many users inserted more than 1000 but less than 2000 images in their presentations from event_log table
-- There is a startup company that makes an online presentation software and they have event_log table that records every time a user inserted
-- an image into a presentation. one user can insert multiple images


```sql
select count(*) from
(select user_id, count(event_date_time) as image_per_user
from event_log
group by user_id) as image_per_user
where image_per_user <2000 and image_per_user>1000;
```

--- 

##  select the most recent login time by values from the login_info table


```sql
select * from login_info
where login_time in (select max(login_time) from login_info
group by user_id)
order by login_time desc limit 1;
```