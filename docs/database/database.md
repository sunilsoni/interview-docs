---
title: Database
has_children: true
nav_order: 2
permalink: docs/database
resource: true
desc: "Database interview questions and answers."
categories: [Database]
---

# Database
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

## Increase SQL performance

- Every index increases the time takes to perform INSERTS, UPDATES, and DELETES, so the number of indexes should not be too much. Try to use maximum 4-5 indexes on one table, not more. If you have read-only table, then the number of indexes may be increased.

- Keep your indexes as narrow as possible. This reduces the size of the index and reduces the number of reads required to read the index.

- Try to create indexes on columns that have integer values rather than character values.

- If you create a composite (multi-column) index, the orders of the columns in the key are very important. Try to order the columns in the key as to enhance selectivity, with the most selective columns to the leftmost of the key.

- If you want to join several tables, try to create surrogate integer keys for this purpose and create indexes on their columns. Create surrogate integer primary key (identity for example) if your table will not have many insert operations.

- Clustered indexes are more preferable than nonclustered, if you need to select by a range of values or you need to sort results set with GROUP BY or ORDER BY. If your application will be performing the same query over and over on the same table, consider creating a covering index on the table.

- You can use the SQL Server Profiler Create Trace Wizard with "Identify Scans of Large Tables" trace to determine which tables in your database may need indexes. This trace will show which tables are being scanned by queries instead of using an index.


### Reasons of poor performance of query.

Following are the reasons for the poor performance of a query:

-  No indexes.
-  Excess recompilations of stored procedures.
-  Procedures and triggers without SET NOCOUNT ON.
-  Poorly written query with unnecessarily complicated joins.
-  Highly normalized database design.
-  Excess usage of cursors and temporary tables.
-  Queries with predicates that use comparison operators between different columns of the same table.
-  Queries with predicates that use operators, and any one of the following are true:
-  There are no statistics on the columns involved on either side of the operators.
-  The distribution of values in the statistics is not uniform, but the query seeks a highly selective value set. This situation can be especially true if the operator is anything other than the equality (=) operator.
-  The predicate uses the not equal to (!=) comparison operator or the NOT logical operator.
-  Queries that use any of the SQL Server built-in functions or a scalar-valued, user-defined function whose argument is not a constant value.
-  Queries that involve joining columns through arithmetic or string concatenation operators.
-  Queries that compare variables whose values are not known when the query is compiled and optimized.



---

## TRUNCATE vs DELETE, vs  DROP

|TRUNCATE       | DELETE	                                |DROP   |
|------------------|--------------------------|-------------------------------------------|
|  The TRUNCATE TABLE the command deletes the data inside a table, but not the table itself. TRUNCATE deletes all the rows of a table at once. It only logs once in the transaction log.| The DELETE query deletes all records from a table of a database without deleting the table schemas like columns, indexes, etc.  | The DROP TABLE statement is used to drop an existing table in a database. DROP TABLEquery removes the table definition and all data, indexes, triggers, constraints, and permissions for that table.      |
|  TRUNCATE TABLE table_name;| DELETE FROM table_name WHERE condition;|  DROP TABLE table_name;     |



### TRUNCATE
- TRUNCATE is a Data Definition Language(DDL) command.
- TRUNCATE is executed using a table lock and the whole table is locked to remove all records.
- TRUNCATE removes all rows from a table at once.
- WHERE clause cannot be used with TRUNCATE.
- It is faster performance-wise than DELETE as it only logs once in the transaction log.
- TRUNCATE cannot be used with indexed views.
- To use Truncate on a table, ALTER permission is required on the table.

### DELETE
- DELETE is a Data Manipulation Language(DML) command.
- DELETE is executed using a row lock mechanism, each row in the table is locked for deletion.
- WHERE clause can be used with DELETE query to filter out records and then delete them.
- DELETE maintains an entry in the transaction log for each row deleted. Hence it is slower than TRUNCATE.
- DELETE permission is required on the table to delete the records.
- The DELETE can be used with indexed views.


### DROP
- The DROP command removes a table from the database.
- All the tables’ rows, indexes, and privileges will also be removed.
- No Data Manipulation Language(DML) triggers will be fired.
- DROP is a Data Definition Language(DDL).
- DELETE operations can be rolled back (undone), while DROP and TRUNCATE operations cannot be rolled back.

---

## Joins

The SQL Joins clause is used to combine records from two or more tables in a database. A JOIN is a means for combining fields from two tables by using values common to each.

- [Pictorial Reference](https://commons.wikimedia.org/wiki/File:SQL_Joins.svg)
- **Inner join**: Rows common in both T1 and T2
- **Left outer join**: All rows in T1
- **Right outer join**: All rows in T2
- **Full join**: All rows in T1 and T2
- **Cross join**: All rows in T1 * all rows in T2

### Inner join

The INNER JOIN creates a new result table by combining column values of two tables (table1 and table2) based upon the join-predicate. The query compares each row of table1 with each row of table2 to find all pairs of rows which satisfy the join-predicate. When the join-predicate is satisfied, column values for each matched pair of rows of A and B are combined into a result row.

Syntax -
```sql
SELECT table1.column1, table2.column2...
FROM table1
INNER JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
INNER JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```



### Left outer join

The SQL LEFT JOIN returns all rows from the left table, even if there are no matches in the right table. This means that if the ON clause matches 0 (zero) records in the right table; the join will still return a row in the result, but with NULL in each column from the right table.

This means that a left join returns all the values from the left table, plus matched values from the right table or NULL in case of no matching join predicate.

Syntax-
```sql
SELECT table1.column1, table2.column2...
FROM table1
LEFT JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```


### Right outer join

The SQL RIGHT JOIN returns all rows from the right table, even if there are no matches in the left table. This means that if the ON clause matches 0 (zero) records in the left table; the join will still return a row in the result, but with NULL in each column from the left table.

This means that a right join returns all the values from the right table, plus matched values from the left table or NULL in case of no matching join predicate.

Syntax-
```sql
SELECT table1.column1, table2.column2...
FROM table1
RIGHT JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```

### Full join

The SQL FULL JOIN combines the results of both left and right outer joins.

The joined table will contain all records from both the tables and fill in NULLs for missing matches on either side.

Syntax −
```sql
SELECT table1.column1, table2.column2...
FROM table1
FULL JOIN table2
ON table1.common_field = table2.common_field;
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
FULL JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID;
```


If your Database does not support FULL JOIN (MySQL does not support FULL JOIN), then you can use UNION ALL clause to combine these two JOINS as shown below.
```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
LEFT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID
UNION ALL
SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS
RIGHT JOIN ORDERS
ON CUSTOMERS.ID = ORDERS.CUSTOMER_ID

```

### Cross join

The CARTESIAN JOIN or CROSS JOIN returns the Cartesian product of the sets of records from two or more joined tables. Thus, it equates to an inner join where the join-condition always evaluates to either True or where the join-condition is absent from the statement.

Syntax  −

```sql
SELECT table1.column1, table2.column2...
FROM  table1, table2 [, table3 ]
```

```sql
SQL> SELECT  ID, NAME, AMOUNT, DATE
FROM CUSTOMERS, ORDERS;
```

### Self Join

The SQL SELF JOIN is used to join a table to itself as if the table were two tables; temporarily renaming at least one table in the SQL statement.

Syntax−

```sql
SELECT a.column_name, b.column_name...
FROM table1 a, table1 b
WHERE a.common_field = b.common_field;
```

```sql
SQL> SELECT  a.ID, b.NAME, a.SALARY
FROM CUSTOMERS a, CUSTOMERS b
WHERE a.SALARY < b.SALARY;
```


---

## For more information

- https://medium.com/javarevisited/know-the-differences-between-truncate-delete-and-drop-4ee70bb736fb
- [Cheat sheet](http://files.zeroturnaround.com/pdf/zt_sql_cheat_sheet.pdf)
- [Clustered vs Non-clustered indexes](https://docs.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described)
- [DB Index Wiki](https://en.wikipedia.org/wiki/Database_index)
- [SQL vs NoSQL: What's the Difference?](https://phoenixnap.com/kb/sql-vs-nosql)
- [SQL vs NoSQL: when to use?](https://www.imaginarycloud.com/blog/sql-vs-nosql/)
